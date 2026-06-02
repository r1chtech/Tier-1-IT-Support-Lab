### Sections

- [Overview](#overview)
- [Creating and Removing Organisational Units (OUs) in AD](#creating-and-removing-organisational-units-ous)
- [Managing users in AD](#managing-users)
- [Managing security groups in AD](#managing-users-in-ad)
- [Creating shared folders](#creating-shared-folders)
- [Configuring network share permissions](#configuring-network-share-permissions)
- [Configuring NTFS permissions](#configuring-ntfs-permissions)

### Overview

PowerShell uses the Active Directory (AD) module to manage AD objects. In summary, the main cmdlet verbs used here are New, Get, Set, Add, and Remove. These follow the syntax `Get-AD<object>`. For example, Get-ADOrganizationalUnit, Get-ADUser, Get-ADForest, and so on.

> Note: The 'New' verb is used with the `-Path` parameter, while 'Get', 'Set', and 'Remove' use the `-Identity` parameter to locate the target OU.

[Read more here](https://learn.microsoft.com/en-us/powershell/module/activedirectory/?view=windowsserver2025-ps)

### Creating And Removing Organisational Units (OUs) in AD

Log into RICHTECH-DC01 and open PowerShell. By default, it should open as administrator. If not, right click and select 'Run as Administrator'.

**Creating OU**

- To create a single OU, use the following command.

  ```ps1
  New-ADOrganizationalUnit -Path "OU=RichTech-Staff,DC=richtech,DC=local" -Name "TestOU"
  ```

  - New-ADOrganizationalUnit: cmdlet used to create the OU.
  - Path: specifies where the OU should be created. Note that the AD distinguished name path is written from bottom to top (the opposite of a typical file system path)
    eg:

    ```
    /
    └── RichTech-Staff
      ├── Finance
      ├── IT
      ├── ...
    ```

    If you wanted to create a file or folder inside IT, you would use a path like RichTech-Staff/IT (top to bottom).

    In Active Directory, however, you write the path from the most specific (child) OU to the most general (parent) OU, then the domain components. For example:

    `OU=IT,OU=RichTech-Staff,DC=richtech,DC=local`

    This is equivalent to thinking IT inside RichTech-Staff (child before parent ie. bottom to top)

  - Name: specifies the name of the new OU.

- Verify that OU has has been created using

  ```ps1
  Get-ADOrganizationalUnit -Filter 'Name -like "TestOU"'
  ```

  You should see the details of the OU displayed.

  ![](../images/more-on-ous-images/ou-cli-1.png)

**Removing OU**

- Before deleting an OU, you must first disable accidental deletion protection, as this setting is enabled ($true) by default.
- Use the following command to set accidental deletion protection to $false

  ```ps1
  Set-ADOrganizationalUnit -Identity "OU=TestOU,OU=RichTech-Staff,DC=richtech,DC=local" -ProtectedFromAccidentalDeletion $false
  ```

- Then use the `Remove-ADOrganizationalUnit` cmdlet to delete the OU

  ```ps1
  Remove-ADOrganizationalUnit -Identity "OU=TestOU,OU=RichTech-Staff,DC=richtech,DC=local"
  ```

  Input `Y` to confirm deletion when prompted.

- Verify that the OU has been removed by running

  ```ps1
  Get-ADOrganizationalUnit -Filter 'Name -like "TestOU"'
  ```

  No output should be returned because the OU no longer exists.

  ![](../images/more-on-ous-images/ou-cli-2.png)

### Managing Users in AD

**Creating a User**

- To create a user, use the following command
  ```ps1
  New-ADUser
  ```
- You will be prompted to enter the Name of the user. Type their full name and press Enter. For example: 'Kofi Annan'

  > Note: The Name attribute is the display name

- Verify that the user has been created using the command below

  ```ps1
  Get-ADUser -Identity "Kofi Annan"
  ```

  By default, the account is disabled, some attribute fields are blank, and the account resides in the default Users container

- Move the account into the preferred OU using the 'Move-ADObject' cmdlet.

  ```ps1
  Move-ADObject -Identity "CN=Kofi Annan,CN=Users,DC=richtech,DC=local" -TargetPath "OU=Finance,OU=RichTech-Staff,DC=richtech,DC=local"
  ```

  The -Identity value (`"CN=Kofi Annan,CN=Users,DC=richtech,DC=local"`) is the Distinguished Name (DN) of the user, which you can retrieve from the Get-ADUser output.

- Verify the move using the command below

  ```ps1
  Get-ADUser -SearchBase "OU=Finance,OU=RichTech-Staff,DC=richtech,DC=local" -Filter "Name -like 'Kofi Annan'"
  ```

- After moving the account, set the missing attributes. But before that, it is recommended not to use a plaintext password directly. Instead, create a secure string variable.

  First, create a variable named `$passwd` that holds a secure string:

  ```ps1
  $passwd = ConvertTo-SecureString "changeme123!" -AsPlainText -Force
  ```

  The password is now stored securely in `$passwd` and can be referenced by passing `$passwd` to relevant cmdlets.

  Set the password separately.

  ```ps1
  Set-ADAccountPassword -Identity "Kofi Annan" -Reset -NewPassword $passwd
  ```

  Then set the remaining attributes.

  ```ps1
  Set-ADUser -Identity "Kofi Annan" `
  -GivenName "Kofi" `
  -Surname "Annan" `
  -SamAccountName "k.annan" `
  -UserPrincipalName "k.annan@richtech.local" `
  -ChangePasswordAtLogon $true `
  -Enabled $true
  ```

- Verify the changes using the 'Get-ADUser' command mentioned earlier
- Alternatively, you can create the user and set all attributes in one command. This assumes you have already stored the password in the `$passwd` variable.
  ```ps1
  New-ADUser `
  -Path "OU=Finance,OU=RichTech-Staff,DC=richtech,DC=local" `
  -Name "Kofi Annan" `
  -GivenName "Kofi" `
  -Surname "Annan" `
  -SamAccountName "k.annan" `
  -UserPrincipalName "k.annan@richtech.local" `
  -AccountPassword $passwd `
  -ChangePasswordAtLogon $true `
  -Enabled $true
  ```

**Removing User**

- To remove a user from Active Directory, use the Remove-ADUser cmdlet as shown below:

  ```ps1
  Remove-ADUser -Identity "k.annan"
  ```

  When prompted to confirm, type `Y` (for Yes) and press Enter.

  > Note: This action is irreversible. Deleted users are not moved to a Recycle Bin by default unless the Active Directory Recycle Bin has been enabled. [Read more](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/get-started/adac/active-directory-recycle-bin?tabs=adac)

### Managing Security Groups in AD

### Creating Shared Folders

### Configuring Network Share Permissions

### Configuring NTFS permissions
