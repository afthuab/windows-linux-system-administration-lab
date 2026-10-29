
## 1. Windows User and Group Administration

### Objective
Create a local Windows user and a local security group,
add the user to the group, and verify the configuration.

### Environment
- Virtual machine: VirtualBox (WIN-LAB01)
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
The local user 'labuser1' was created successfully. The 'LabOps' group was created successfully, and 'labuser1' was added to the group. The account and group membership were verified using PowerShell.

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
1. Windows users and group
![windows user and group](../screenshots/windows-users-group.png)


## 2. Windows File Permissions

### Objective
Configure Windows folder permissions by granting the
LabOps group Modify access to a shared directory and
verify that a member of the group can create and save files.

### Environment
- Virtual machine: VirtualBox (WIN-LAB01)
- Operating system: Windows 11
- Test user: labuser1
- Security group: LabOps
- Test directory: C:\LabData\TeamShare
- Tool: Windows PowerShell and File Explorer

### Procedure
1. Opened PowerShell with administrator privileges.
2. Created the directory C:\LabData\TeamShare.
3. Granted Modify permission to the LabOps group.
4. Verified the folder permissions using icacls command.
5. Signed in using the labuser1 account.
6. Opened the TeamShare directory.
7. Created permission-test.txt.
8. Entered test content and saved the file successfully.

### Commands Used

```powershell
New-Item -ItemType Directory -Path "C:\LabData\TeamShare" -Force

icacls "C:\LabData\TeamShare" /grant "$($env:COMPUTERNAME)\LabOps:(OI)(CI)M"

icacls "C:\LabData\TeamShare"
```

### Result
The folder permissions were configured successfully and granted Modify permission on the TeamShare directory.
The icacls output confirmed the LabOps group's Modify
permission. The labuser1 account successfully created
and saved permission-test.txt in the TeamShare directory.

### Analysis
Windows NTFS permissions control which users and groups
can access files and folders and what actions they can
perform. Assigning permissions to a group simplifies
administration because access can be managed through
group membership rather than by configuring each user
individually.

### Conclusion
This exercise demonstrated how to configure and verify
Windows folder permissions using PowerShell. I granted
the LabOps group Modify access to the TeamShare directory
and verified that labuser1 could create and save a test
file. This confirmed that the configured permissions
worked for the intended user. The exercise also showed
how group based permissions support consistent and
manageable access control.

### ScreenshotsS
1. Windows permission & icacls command
![Windows Permission icacls Command](../screenshots/windows-icacls-command.png)
2. Permission test with file content
![Permission test with file content](../screenshots/permission-test-content.png)
