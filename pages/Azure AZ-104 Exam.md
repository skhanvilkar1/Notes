- Managing Azure Active Directory
  collapsed:: true
	- How to use Azure to secure your identities and understand how users and groups are implemented in Azure AD.
	- Azure Active Directory
		- Cloud based identity and directory management service enabling access to Azure services and other SaaS solutions like Microsoft 365, DropBox, Salesforce etc.
		- Self service options like password reset, authentication, SSO, device management, hybrid identities etc. On-prem applications etc.
		- AD concepts 
		  collapsed:: true
			- Identity  - Object that can be authenticated. User, group or service principals (service accounts)
			- Account - Associate data attributes to an identity we call it account. Example location, department and phone number of user makes that identity an Account.
			- Azure AD Account  - Accounts created in Azure AD is called Azure AD account
			- Azure AD Tenant or directory - Dedicated instance of Azure AD that is created during sign up of any Microsoft cloud service subscription. Tenant and Directory means same. We can have one or multiple directories based on requirement.
		- Azure AD vs Active Directory Domain Services (ADDS)
		  collapsed:: true
			- Two different services. Installing ADDS in Azure is not Azure AD
			- Azure AD is cloud based or web based , so its queried using HTTP or HTTPS. ADDS using LDAP protocol for querying
			- AZ AD uses SAML, WS-Federation, Open ID and OAuth for authorization. ADDS uses KERBEROS for authentication
			- AZ AD Federation can be set up with 3rd party providers like Facebook v/s ADDS , Federation is only to other domains, 3rd party not supported.
			- Azure AD is managed service offering v/s ADDS will run on VMs or Physical Windows Servers.
		- Azure AD Editions
			- Premium P2 - No directory object limit, Single Sign on, B2B collab, O365 access, Hybrid identities, Conditional access, identity Protection, Identity Governance.
			- Premium P1 -No directory object limit, Single Sign on, B2B collab, O365 access, Hybrid identities, Conditional access
			- M365 Apps - No directory object limit, Single Sign on, B2B collaboration, O365 access
			- FREE - included with Azure Subscription - No directory object limit, Single Sign on, B2B collaboration.
		- User Accounts
		  collapsed:: true
			- User accounts are used for authentication and authorization.  All users must have an account
			- Each user can have optional properties.
			- All users can be accessed from Azure Active Directory > USERS > All users
			- We can perform bulk operations like bulk create, bulk invite and bulk delete.
			-
			- Types of Identities -
			- Cloud Identities - Users exist only in  internal Azure AD or external Azure AD
			- Guest Users - Exist outside of Azure , Microsoft accounts, Live Accounts etc.
			- Directory synchronized users - These users are synchronized from your on-prem Windows AD. We cannot create directory synchronized users (obvious)
			- REFER USER CREATION LAB HERE IN AZURE AD.
			-
		- User Accounts - Bulk Operations 
		  collapsed:: true
			- Bulk operations will let you download a CSV template where you add users you want to create, delete or invite.
			  BULK CREATE
			  BULK INVITE
			  BULK DELETE
			  BULK DOWNLOAD
			- Azure Active Directory > Users - you will see Bulk Operations option, download CSV Template
			- You can restore DELETED users by going to Users > Deleted users option
	- Azure AD Join
	  collapsed:: true
		- We can uses Azure AD join to manage our corporate assets (similar to domain join in ADDS)
		- IT admins make sure devices are secure and follow security standards
		- Azure AD join offers SINGLE SIGN ON - app services and SAAS solutions
		- Provides Access to Microsoft Store for Business
		- Enterprise state Roaming - sync all your config across devices
		- Windows Hello - Sign in using biometric or facial sign in
		- Device Management - Admins can check complaince and restric
		- On-prem Access - Seamless access to on-prem apps and leverage single sign on
	- Self-Service Password Reset (SSPR)
	  collapsed:: true
		- Enables users to reset password without need to call IT helpdesk
		- Setup Multiple methods to reset
		- Premium P2 license
		- Enable for all users or targeted users
		- Admin accounts - enabled by default. 
		  
		  STEP 1 - Enable SSPR for all or targeted users
		  STEP 2 - Set up number of authentication methods required for reset of password
		  STEP 3 - Users will be requested to register for SSPR next time login and enable reset method
		-
		- REFER SSPR LAB Azure Active Directory > Password Reset > go to properties , options available none, selected, all
		- If a user wants to setup up his/her profile , they can go to aka.ms/ssprsetup and they will be able to setup their SSPR reset options. Methods available are Authenticator app / phone etc.
		- If user wants to reset password they can go to --> aka.ms/sspr > redirects to passwordreset.microsoftonline.com
		-
		-
	- Group Accounts
	  collapsed:: true
		- Security groups -> assign a role, inherited by all users of group
		- MS 365 groups -> offers collab. opportunities
		  
		  Membership Assignment Types
		- Assigned - default
		- Dynamic users - attribute of users changed, AZ will check and modify/remove
		  --> Check Dynamic Membership rules under group. specify your query/expression here
		- Dynamic device - will dynamically check device properties and will remove if attributes match remove rule. Not available for MS 365 groups
		-
	- Multi-Tenant Environments
	  collapsed:: true
		- Each Tenant or directory represents an organization. An org can have one or more tenants.
		- Azure AD there is no parent child relationship
		- Each Azure AD org is fully independent. Each tenant is considered separate
		- Resource Independence - Creation and deletion of resource in one Tenant does not have any impact on another tenant.
		- Administration independence - Level of permission of user account is only valid within the tenant
		- Synchronization independence - Each Azure AD Tenant's synchronization of accounts can be independently set up for each tenant.
		- Default domain provided yourorg.onmicrosoft.com , you can bring your custom domain names need to set up DNS
		- You can switch between directories (tenants)
		- You need an invite from Tenant admin to join another Tenants.
	-
- Azure Subscriptions
	- Need subscription to create resources. All charges of all resources made are charged to subscription.
	  Hence Azure subscription acts like a billing boundary for usage.
	- Resources deployed are mapped to Azure Subscription
	- Help us set up environmental boundaries - Dev, TEST , QA etc
	- Every subscription has unique subscription ID.
	- An account can have multiple subscriptions
	- Any identity part of Azure AD or trusted MS Cloud service can sign up for a subscription.
	- Different types
	  collapsed:: true
		- Enterprise Agreements - 500 or more users and devices. Offers services and licensing at discounted rates. Pre payment required
		- Pay-as-you-go subscription - Ideal for small size org. Monthly billing
		- CSP - Cloud Solution Provider - Licensed by microsoft partner. managed by Microsoft partners
		- Free Trial - $200 credit for 30 days and free limited access for 12 months
		- Azure for Students
		- Visual Studio subscription
	- Subscription can act as scope of access management and policy governance.
	-
	-
	- Understanding Hierarchy
		- Management Groups -> offers a scope above subscriptions by which you will be able to group subscriptions together
		- Root Management group is created by default and you have upto 6 levels of nested groups excluding the root group.
		- Each subscription can contain one or more resources.
		- Hierarchy helps in implementing polices 
		  Management Groups > Subscriptions > Resource Groups > Resources
	-