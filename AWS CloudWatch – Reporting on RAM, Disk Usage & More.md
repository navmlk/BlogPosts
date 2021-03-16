Amazon Web Services reports some good metrics on the console by default, like CPU, but it’s missing some key metrics like memory usage or disk space; these are important to monitor to ensure instance uptime and health.It’s a good idea keeping everything in the same place, so we can leave CPU and all the other default metrics as they are, but in addition append the extra ones we want, like how much disk space we have, or how much memory is being used.

> The monitoring scripts are authored by Amazon themselves, but aren’t included unless you set them up yourself, which isn’t always obvious. The scripts are available for a variety of different operating systems that could be running on your instances, however we will focus on Windows-based systems in this post. Amazon’s own documentation on this topic, while comprehensive, is hard to find; hopefully this post will help you with your own instance monitoring.

We will be leveraging AWS Systems Manager, IAM, CloudWatch and EC2 services on AWS cloud to get logs and Metrics on CloudWatch.

1.  Navigate to AWS IAM Service (Global Service) to create relevant roles and policies

Follow [this](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-sharing-logs-create-role.html) post on how to create roles and assign policies

-   CloudWatchAdmin (with below policies)
    -   AmazonEC2RoleforSSM
    -   CloudWatchAgentAdminPolicy (This will allow store the config file to Parameter Store on Systems Manager – that will be used to start cloudwatch service on EC2 instances)

You will need to assign this role to EC2 instance where you will be creating the config file so once generated the file can be pushed to Parameter Store. If this role isn’t assigned to EC2 instance the config file won’t be stored in Parameter Store.

-   CloudWatchServer
    -   AmazonEC2RoleforSSM
    -   CloudWatchAgentServerPolicy (The only difference from CloudWatchAgentAdminPolicy is that it can’t store config file to parameter store).
    
You will need to assign this role to EC2 instance to capture logs and Metrics in cloudwatch.

2.  Navigate to EC2 service and assign CloudWatchAdmin role to the EC2 instance where you will be generating the CloudWatch Config file and then storing it to parameter store.

![alt text](https://sysadmindiary.co.uk/wp-content/uploads/2019/10/006.png)

-   Select the EC2 instance which you want to monitor using cloudwatch agnet and assign CloudWatchServer role to this instance.

![alt text](https://sysadmindiary.co.uk/wp-content/uploads/2019/10/007.png)
3. Navigate to AWS Systems Manager to push CloudWatch Agent to EC2 instances.

-   Click on Managed instances and verify that both instances are visible, (which were assigned CloudWatchAdmin & CloudWatchServer roles).
-   Navigate to Run Command and click on Run Command

![alt text](https://sysadmindiary.co.uk/wp-content/uploads/2019/10/008-1024x432.png)
-   Select AWS-ConfigureAWSPackage

![alt text](https://sysadmindiary.co.uk/wp-content/uploads/2019/10/009-1024x513.png)
-   Specify below values to Command parameters

![alt text](https://sysadmindiary.co.uk/wp-content/uploads/2019/10/010-1024x238.png)
-   Click on choose Targets manually and click on Run

(This will install CloudWatch Agent on target EC2 instances)
![alt text](https://sysadmindiary.co.uk/wp-content/uploads/2019/10/011-1024x390.png)

4. Now RDP on to EC2 instance which has CloudWatchAdmin role assigned to it.

-   Launch CMD as admin and navigate to `C:\Program Files\Amazon\CloudWatchAgent`
-   Execute amazon-cloudwatch-agent-config-wizard.exe
-   Go through the wizard as below, this will generate the config file that will be stored in parameter store.
```aws
On which OS are you planning to use the agent?
1. linux
2. windows
default choice: [2]:
Choose 2

Are you using EC2 or On-Premises hosts?
1. EC2
2. On-Premises
default choice: [1]:
Choose 1

Do you want to turn on StatsD daemon?
1. yes
2. no
default choice: [1]:
Choose 2

Do you have any existing CloudWatch Log Agent configuration file to import for migration?
1. yes
2. no
default choice: [2]:
Choose 2

Do you want to monitor any host metrics? e.g. CPU, memory, etc.
1. yes
2. no
default choice: [1]:
Choose 1
Do you want to monitor cpu metrics per core? Additional CloudWatch charges may apply.
1. yes
2. no
default choice: [1]:
Choose 1

Do you want to add ec2 dimensions (ImageId, InstanceId, InstanceType, AutoScalingGroupName)into all of your metrics if the info is available?
1. yes
2. no
default choice: [1]:
Choose 1
Would you like to collect your metrics at high resolution (sub-minute resolution)? This enables sub-minute resolution for all metrics, but you can customize for specific metrics in the output json file.
1. 1s
2. 10s
3. 30s
4. 60s
default choice: [4]:
Choose 4

Which default metrics config do you want?
1. Basic
2. Standard
3. Advanced
4. None
default choice: [1]:            
Choose 1

Are you satisfied with the above config? Note: it can be manually customized after the wizard completes to add additional items.
1. yes
2. no
default choice: [1]:
Choose 1 (if you are satisfied with the config so far)

Do you want to monitor any customized log files?
1. yes
2. no
default choice: [1]:
(If you want to monitor any customized log files choose 1 otherwise 2)

Do you want to monitor any Windows event log?
1. yes
2. no
default choice: [1]:
(If you want to monitor any Windows Event logs choose 1 otherwise 2)

Do you want to store the config in the SSM parameter store?
1. yes
2. no
default choice: [1]:
Choose 1

What parameter store name do you want to use to store your config? (Use 'AmazonCloudWatch-' prefix if you use our managed AWS policy)
default choice: [AmazonCloudWatch-windows]
Choose default

Trying to fetch the default region based on ec2 metadata...Which region do you want to store the config in the parameter store?
default choice: [eu-west-1]
Choose Default

Which AWScredential should be used to send json config to parameter store?1. *****************************(From SDK)
2. Other
default choice: [1]:
Choose default
(This value is auto generated from the role that is assigned to
this EC2 instance)
```
Now Cloudwatch config file is generated and pushed in to parameter store in Systems Manager service.

5.  Navigate to Systems Manager Service on AWS Management console.

-   Verify that AmazonCloudWatch-Windows File exists in parameter store by selecting Parameter Store
![alt text](https://sysadmindiary.co.uk/wp-content/uploads/2019/10/012-1024x541.png)
-   Now we need to push this config file to EC2 instances to start Cloudwatch Agent Service.
-   Click on Run Command on AWS System Manager Service.
-   Select Document name prefix Equal AmazonCloudWatch
![alt text](https://sysadmindiary.co.uk/wp-content/uploads/2019/10/013-1024x300.png)

Specify Command Parameters as below
![image](https://user-images.githubusercontent.com/67142634/111317353-fece2200-865b-11eb-848a-481611b95259.png)

Choose targets manually
![image](https://user-images.githubusercontent.com/67142634/111317417-10afc500-865c-11eb-938c-e7f379ebe8fe.png)

Hit Run
This will push the config file from parameter store to EC2 instances
7. Verify Logs & Metrics are being captured in CloudWatch

Navigate to CloudWatch services
Select Metrics, you should see CWAgent under Custom Namespaces
![image](https://user-images.githubusercontent.com/67142634/111317491-1f967780-865c-11eb-9ff6-d791ababf84c.png)

**References:**

https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/create-cloudwatch-agent-configuration-file-wizard.html

https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/CloudWatch-Agent-Configuration-File-Details.html

https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/troubleshooting-CloudWatch-Agent.html

https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/CloudWatch-Agent-custom-metrics-statsd.html

https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/create-cloudwatch-agent-configuration-file-wizard.html
