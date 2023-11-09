## Integrate Azure AD with Multiple AWS Accounts
### Adding AWS Application from Gallery

To configure the integration of AWS into Azure AD, you will need to add the AWS application from application gallery on Azure to your list of manage SaaS applications.
#### Steps

- In the Azure portal, on the left navigation panel, click Azure Active Directory
- Navigate to Enterprise Applications and then select the All Applications
- To add new application, click New applicationbutton on the top of dialog.
- In the search box, type Amazon Web Services (AWS), select Amazon Web Services (AWS) from result panel then click Add button to add the application.

####Configure AWS app & Azure AD single sign-on

For single sign-on to work, a link relationship between an Azure AD user and the related user in Amazon Web Services (AWS) needs to be established.

In Amazon Web Services (AWS), assign the value of the user name in Azure AD as the value of the Username to establish the link relationship.

To configure and test Azure AD single sign-on with Amazon Web Services (AWS), you need to complete the following below

####Configure Azure single sign-on
To configure Azure AD single sign-on with Amazon Web Services (AWS), perform the following steps:
- In the Azure portal, on the Amazon Web Services (AWS)application integration page, select Single sign-on.
- On the Select a Single sign-on method dialog, select SAML mode to enable single sign-on.
- On the Set up Single Sign-On with SAMLpage, click Edit icon to open Basic SAML Configuration
- On the Basic SAML Configuration section, the user does not have to perform any step as the app is already pre-integrated with Azure.
- Amazon Web Services (AWS) application expects the SAML assertions in a specific format. Configure the following claims for this application. You can manage the values of these attributes from the User Attributes & Claims section on application integration page. On the Set up Single Sign-On with SAML page, click Edit button to open User Attributes & Claims
- In the User Claimssection on the User Attributes dialog, configure SAML token attribute as shown in the image above and perform the following steps:

| Name | Source Attribute | Namespace |
|----------|-------------------------|------------------|
|RoleSessionName | user.userprincipalname | https://aws.amazon.com/SAML/Attributes |
| Role | user.assignedroles | https://aws.amazon.com/SAML/Attributes |
| SessionDuration | "provide a value between 900 seconds (15 minutes) to 43200 seconds (12 hours)" | https://aws.amazon.com/SAML/Attributes |

#### Adding Claims
- Click Add New Claim to open the Manage User claims
- In the Name textbox, type the attribute name shown for that row.
- In the Namespace textbox, type the Namespace value shown for that row.
- Select Source as Attribute.
- From the Source attribute list, type the attribute value shown for that row.
- Click Ok
- Click Save.
- On the Set up Single Sign-On with SAML page, in the SAML Signing Certificate section, click Download to download the Federation Metadata XML and save it on your computer.

####Configure Amazon Web Services (AWS) Single Sign-On
- In a different browser window, sign-on to your Amazon Web Services (AWS).
- Click AWS Home.
- Click Identity and Access Management.
- Click Identity Providers, and then click Create Provider.
- On the Configure Provider dialog page, perform the following steps:
- As Provider Type, select SAML.
- In the Provider Name textbox, type a provider name.
- To upload your downloaded metadata file from Azure portal, click Choose File.
- Click Next Step.
- On the Verify Provider Information dialog page, click Create.
- Click Roles, and then click Create role.
- On the Create role page, perform the following steps:
- Select SAML 2.0 federation under Select type of trusted entity.
- Under Choose a SAML 2.0 Provider section, select the SAML provider you have created previously.
- Select Allow programmatic and AWS Management Console access.
- Click Next: Permissions.
- On the Attach Permissions Policiesdialog, please attach the appropriate policy as per your organization. Click Next: Review.
- On the Review dialog, perform the following steps:
- In the Role name textbox, enter your Role name.
- In the Role description textbox, enter the description.
- Click Create Role.
- Create as many roles as needed and map them to the Identity Provider.
- Sign out from your current AWS account and login with other account where you want to configure single sign on with Azure AD.
- Perform step-2 to step-10 to create multiple roles that you want to setup for this account. If you have more than two accounts, please perform the same steps for all the accounts to create roles for them.
- Once all the roles are created in the accounts, they show up in the Roles list for those accounts.
- We need to capture all the Role ARN and Trusted Entities for all the roles across all the accounts, which we need to map manually with Azure AD application.
- Click on the roles to copy Role ARNand Trusted Entities You need these values for all the roles that you need to create in Azure AD.
- Perform the above step for all the roles in all the accounts and store all of them in format Role ARN, Trusted entities in a notepad.

#### Application Registration
- In the Azure Portal, navigate to App Registration
- Click on your AWS application
- Open Manifest Tab, this will bring up the edit manifest page, where you have to add pair values (add pair values for each role that you created in AWS. e.g. if you have created 6 roles on AWS you will need to create 6 pair values)

Sample pair values are below


     {
      "allowedMemberTypes": [
        "User"
      ],
      "displayName": "AWS-Prod-Admins,AzureAD",
      "id": "f0b999cd-0e5d-4faa-8c7b-d9224c4b27a5",
      "isEnabled": true,
      "description": "To grant Full Admin (AWS) Access to users for Prod Account,AzureAD",
      "value": "arn:aws:iam::xxxxxxxx:role/AWS-Prod-Admins,arn:aws:iam::xxxxxxxx:saml-provider/AzureAD"
     }
Remember that you have to add one of these sections for each pair Group-Role, as mentioned above.

#### User/Group Assignment
- In the Azure Portal, navigate to Enterprise applications.
- Select your Amazon Web Services Application
- Navigate to Users and groups
- Click on Add user
- Click on users and groups and search for the security group that you created on your AD on premise
- Click on the security group / user and click select
- Click on select role and search for the role that you want to bind the security group/user with this role.

e.g. AWS-30000000-Admin (security group) – AWS-xxxxxx-Admins (role)

#### MFA
- Select Conditional Access
- You will see list of Policies (or just one policy) for your AWS application
- Click the Policy and click on users and groups
- Search for the same security groups that you linked against roles
- Once all the users/groups are selected, click on Done button and click Save

#### Testing
- Navigate to portal.office365.com and login with your credentials
- Click on all applications and select your AWS application.
- You should be prompted for MFA
- Once MFA is approved, you should be able to sign in to AWS.

#### Multiple AWS account

For Multiple AWS accounts, you will need to do below

##### AWS
- Create Identity provide using same Meta Data Federation File (Step 1 .1 / 8)
- Create roles (Step 2 /7)

###### Office365
- Navigate to app registration (Step 3)
- Add the pair values
- User/Group assignment
##### MFA
Testing
- Test by navigating to portal.office365.com
