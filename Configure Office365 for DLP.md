**To configure Data Loss Prevention (DLP), perform the following steps:**

1.  Login as tenant admin to the Office 365 Admin center from or by clicking Admin from the App Launcher
![image](https://user-images.githubusercontent.com/67142634/111323692-055f9800-8662-11eb-83f1-945d8580491e.png)

2.  Click on the Security & Compliance Admin Center from the Office 365 Admin center left navigation (You can also get there from https://protection.office.com using tenant admin) 
![image](https://user-images.githubusercontent.com/67142634/111323738-101a2d00-8662-11eb-9f1a-191de171887a.png)

3.  Click on Policy  Create a policy under Data loss prevention in the left navigation in the Security & Compliance admin center
![image](https://user-images.githubusercontent.com/67142634/111323768-15777780-8662-11eb-8753-c7a9a6dd5df2.png)

4.  Find the policy or create a custom policy you need to enforce using the New DLP policy wizard (i.e. I am selecting UK Financial Data template to protect against Credit Card Numbers, EU Debit Card Numbers and SWIFT Code)
![image](https://user-images.githubusercontent.com/67142634/111323790-190afe80-8662-11eb-97ae-beef81078c78.png)

5.  Provide a name for the policy
![image](https://user-images.githubusercontent.com/67142634/111323836-21fbd000-8662-11eb-8e72-b95b7b3d713c.png)

6.  Select the locations – Either all locations or specific locations (Exchange, SharePoint or OneDrive) on where to protect (this is where the tips will show up as well)
![image](https://user-images.githubusercontent.com/67142634/111323860-2627ed80-8662-11eb-834c-048d9af408e0.png)

7.  If you choose specific locations, you get additional capabilities for Inclusions and Exclusion rules.
    - For Exchange, you can include or exclude specific distribution groups.
    - For SharePoint, you can include or exclude specific SharePoint sites.
    - For OneDrive, you can include or exclude specific OneDrive accounts. d. For Teams, you can include or exclude specific Teams accounts.
![image](https://user-images.githubusercontent.com/67142634/111324039-5079ab00-8662-11eb-8bd6-51548a0580ae.png)

8. Select the type of content you want to protect (with people inside or outside your organization) or create more advanced rules
![image](https://user-images.githubusercontent.com/67142634/111324086-5cfe0380-8662-11eb-8d1f-76ec4b8e2838.png)

9. Indicate what you want to do if the rule is detected
![image](https://user-images.githubusercontent.com/67142634/111324102-61c2b780-8662-11eb-9204-21ed834833d3.png)

10. Turn the rule on or test it out (it will take a little bit of time before it takes effect)
![image](https://user-images.githubusercontent.com/67142634/111324121-65eed500-8662-11eb-8beb-c4a7d42fc74f.png)

11. Review the settings and Create the rule
![image](https://user-images.githubusercontent.com/67142634/111324137-68e9c580-8662-11eb-8dc7-789b38c31dce.png)

View the [Microsoft support article](https://support.office.com/en-us/article/Send-email-notifications-and-show-policy-tips-for-DLP-policies-87496bc5-9601-4473-8021-cb05c71369c1) for more details on sending email notifications and show policy tips for DLP policies.
