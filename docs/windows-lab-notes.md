
## 1. Windows User and Group Administration

### Objective
Create a local Windows user and a local security group,
add the user to the group, and verify the configuration.

### Environment
- Virtual machine: WIN-LAB01
- Operating system: Windows 11
- User created: labuser1
- Group created: LabOps
- Tools used: Windows PowerShell

### Procedure
1. Opened PowerShell with administrator privileges.
2. Created the local group named LabOps.
3. Created the local user named labuser1.
4. Added labuser1 to the LabOps group.
5. Verified the user account and group membership
   using PowerShell commands.

### Commands Used

```powershell
New-LocalGroup -Name "LabOps" `
  -Description "Lab permissions testing group"

$Password = Read-Host "Enter a temporary lab password" -AsSecureString

New-LocalUser -Name "labuser1" `
  -Password $Password `
  -Description "Test account for administration lab"

Add-LocalGroupMember -Group "LabOps" -Member "labuser1"

Get-LocalUser -Name "labuser1"

Get-LocalGroup -Name "LabOps"

Get-LocalGroupMember -Group "LabOps"
```

### Result
1. The local user 'labuser1' was created successfully.
2. The 'LabOps' group was created successfully, and
3. 'labuser1' was added to the group.
4. The account and group membership were verified using PowerShell.

### Analysis
Local user accounts provide individual identities
for accessing a Windows system. Groups simplify
permission management by allowing permissions to
be assigned to a collection of users rather than
configured separately for every account.

### Conclusion
This exercise demonstrated how to create and manage
local Windows user accounts and security groups
using PowerShell. I verified that the labuser1
account existed and was a member of LabOps.
This group was subsequently used in the file
permission exercise to grant access to the
TeamShare directory.

### Screenshots
1. **Windows Users and Group**
![windows user and group](../screenshots/windows-users-group.png)
