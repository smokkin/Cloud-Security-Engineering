You have been asked to create a proof of concept showing how Azure users and groups are created. Also, how role-based access control is used to assign roles to groups. Specifically, you need to:

Create a Senior Admins group containing the user account of Joseph Price as its member.
Create a Junior Admins group containing the user account of Isabel Garcia as its member.
Create a Service Desk group containing the user account of Dylan Williams as its member.
Assign the Virtual Machine Contributor role to the Service Desk group.
For all the resources in this lab, we are using the East US region. Verify with your instructor this is the region to use for class.

Lab objectives
In this lab, you will complete the following exercises:

Exercise 1: Create the Senior Admins group with the user account Joseph Price as its member (the Azure portal).
Exercise 2: Create the Junior Admins group with the user account Isabel Garcia as its member (PowerShell).
Exercise 3: Create the Service Desk group with the user Dylan Williams as its member (Azure CLI).
Exercise 4: Assign the Virtual Machine Contributor role to the Service Desk group.
Role-Based Access Control architecture diagram

<img width="2000" height="1071" alt="image" src="https://github.com/user-attachments/assets/e6208b9f-6c4b-4d99-a633-ce6ea3aa60ed" />

Exercise 1: Create the Senior Admins group with the user account Joseph Price as its member.

In this exercise, you will complete the following tasks:

Task 1: Use the Azure portal to create a user account for Joseph Price.
Task 2: Use the Azure portal to create a Senior Admins group and add the user account of Joseph Price to the group.

Task 1: Use the Azure portal to create a user account for Joseph Price
In this task, you will create a user account for Joseph Price.

Start a browser session and sign-in to the Azure portal https://portal.azure.com/.

Sign in to the Azure portal using an account that has the Owner or Contributor role in the Azure subscription you are using for this lab and the Global Administrator role in the Microsoft Entra tenant associated with that subscription.

In the Search resources, services, and docs text box at the top of the Azure portal page, type Microsoft Entra ID and press the Enter key.

On the Overview blade of the Microsoft Entra ID tenant, in the Manage section, select Users, and then select + New user.

On the New User blade, ensure that the Create user option is selected, and specify the following settings:

Setting	Value
User name	Joseph
Name	Joseph Price
Click on the copy icon next to the User name to copy the full user.

Ensure that the Auto-generate password is selected, select the Show password checkbox to identify the automatically generated password. You would need to provide this password, along with the user name to Joseph.

Click Create.

Refresh the Users | All users blade to verify the new user was created in your Microsoft Entra tenant.
<img width="1431" height="772" alt="image" src="https://github.com/user-attachments/assets/a722fe3d-4e4b-4b69-bf9f-3a52a5fbfe64" />
<img width="1429" height="770" alt="image" src="https://github.com/user-attachments/assets/90011653-00bb-4670-8b7a-1cc5746996b5" />
<img width="1431" height="770" alt="image" src="https://github.com/user-attachments/assets/8bb54795-6e88-4b75-922b-faab5c1d8336" />

Task2: Use the Azure portal to create a Senior Admins group and add the user account of Joseph Price to the group.
In this task, you will create the Senior Admins group, add the user account of Joseph Price to the group, and configure it as the group owner.

In the Azure portal, navigate back to the blade displaying your Microsoft Entra ID tenant.

In the Manage section, click Groups, and then select + New group.

On the New Group blade, specify the following settings (leave others with their default values):

Setting	Value
Group type	Security
Group name	Senior Admins59599230
Membership type	Assigned
Click the No owners selected link, on the Add owners blade, select Joseph Price, Joseph-59599230@LODSPRODMCA.onmicrosoft.com and click Select.

Click the No members selected link, on the Add members blade, select Joseph Price, Joseph-59599230@LODSPRODMCA.onmicrosoft.com and click Select.

Back on the New Group blade, click Create.

Result: You used the Azure Portal to create a user and a group, and assigned the user to the group.
<img width="1429" height="771" alt="image" src="https://github.com/user-attachments/assets/de1a549b-e43d-4d73-9fa6-47429b5e4680" />
<img width="1429" height="770" alt="image" src="https://github.com/user-attachments/assets/fce69b83-f9cd-451d-92ab-5a419c9ccc8b" />
<img width="1428" height="766" alt="image" src="https://github.com/user-attachments/assets/fc353df6-d8e9-4a07-8fec-5ad8c757df47" />
<img width="1428" height="779" alt="image" src="https://github.com/user-attachments/assets/34eb0388-999f-4a0f-a30e-c23e052f0cbd" />
<img width="1426" height="764" alt="image" src="https://github.com/user-attachments/assets/d1b1cff8-7564-4cb2-9f07-446465e83c8c" />

Exercise 2: Create a Junior Admins group containing the user account of Isabel Garcia as its member.

In this exercise, you will complete the following tasks:

Task 1: Use PowerShell to create a user account for Isabel Garcia.
Task 2: Use PowerShell to create the Junior Admins group and add the user account of Isabel Garcia to the group.

Task 1: Use PowerShell to create a user account for Isabel Garcia.

In this task, you will create a user account for Isabel Garcia by using PowerShell.

Open the Cloud Shell by clicking the Cloud Shell icon in the top-right corner of the Azure portal.

If prompted, select No storage account required, select the name of your subscription, and then select Apply. This is required only the first time you launch the Cloud Shell.

In the Cloud Shell pane, ensure PowerShell is selected from the drop-down menu in the upper-left corner. (Note: In the new Cloud Shell, this will say: -->Switch to Bash)

In the PowerShell session within the Cloud Shell pane, run the following to create a password profile object:

powershell
TypeCopy
$passwordProfile = New-Object -TypeName Microsoft.Open.AzureAD.Model.PasswordProfile
In the PowerShell session within the Cloud Shell pane, run the following to set the value of the password within the profile object:

powershell
TypeCopy
$passwordProfile.Password = "Pa55w.rd1234"
In the PowerShell session within the Cloud Shell pane, run the following to connect to Microsoft Entra ID:

powershell
TypeCopy
Connect-AzureAD
In the PowerShell session within the Cloud Shell pane, run the following to identify the name of your Microsoft Entra tenant:

powershell
TypeCopy
$domainName = ((Get-AzureAdTenantDetail).VerifiedDomains)[0].Name
In the PowerShell session within the Cloud Shell pane, run the following to create a user account for Isabel Garcia:
powershell
TypeCopy
New-AzureADUser -DisplayName 'Isabel Garcia' -PasswordProfile $passwordProfile -UserPrincipalName "Isabel@$domainName" -AccountEnabled $true -MailNickName 'Isabel'
In the PowerShell session within the Cloud Shell pane, run the following to list Microsoft Entra ID users (the accounts of Joseph and Isabel should appear on the listed):

powershell
TypeCopy
Get-AzureADUser -All $true | Where-Object {$_.UserPrincipalName -like "Isabel-59599230*"} 
<img width="1428" height="765" alt="image" src="https://github.com/user-attachments/assets/ebd51282-cc65-410c-a9d9-3cfc86c23159" />
<img width="1425" height="763" alt="image" src="https://github.com/user-attachments/assets/5d26401f-fd7d-40a4-b9ef-afb25718dd46" />

Task2: Use PowerShell to create the Junior Admins group and add the user account of Isabel Garcia to the group.
In this task, you will create the Junior Admins group and add the user account of Isabel Garcia to the group by using PowerShell.

In the same PowerShell session within the Cloud Shell pane, run the following to create a new security group named Junior Admins:

powershell
TypeCopy
New-AzureADGroup -DisplayName 'Junior Admins5959923059599230' -MailEnabled $false -SecurityEnabled $true -MailNickName JuniorAdmins
In the PowerShell session within the Cloud Shell pane, run the following to list groups in your Microsoft Entra tenant (the list should include the Senior Admins59599230 and Junior Admins59599230 groups)

powershell
TypeCopy
Get-AzureADGroup
In the PowerShell session within the Cloud Shell pane, run the following to obtain a reference to the user account of Isabel Garcia:

powershell
TypeCopy
$user = Get-AzureADUser -Filter "UserPrincipalName eq 'Isabel-59599230@LODSPRODMCA.onmicrosoft.com'"
In the PowerShell session within the Cloud Shell pane, run the following to add the user account of Isabel to the Junior Admins5959923059599230 group:

powershell
TypeCopy
Add-AzADGroupMember -MemberUserPrincipalName $user.userPrincipalName -TargetGroupDisplayName "Junior Admins5959923059599230"
In the PowerShell session within the Cloud Shell pane, run the following to verify that the Junior Admins5959923059599230 group contains the user account of Isabel:

powershell
TypeCopy
Get-AzADGroupMember -GroupDisplayName "Junior Admins5959923059599230"
Result: You used PowerShell to create a user and a group account, and added the user account to the group account.
<img width="1425" height="764" alt="image" src="https://github.com/user-attachments/assets/0e4cb64f-ca4c-4aef-bdad-12ff31aa4643" />


