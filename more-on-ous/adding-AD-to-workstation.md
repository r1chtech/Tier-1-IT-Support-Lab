### Adding Active Directory Tools to a Workstation

- Assume John Doe works in IT, specifically on the helpdesk. John Doe will have two accounts: one standard user account and one administrative account.

- John Doe logs into a workstation for the first time using his standard account. He searches for Active Directory, but it does not exist.

- We need to install the Active Directory component from RSAT (Remote Server Administration Tools). Only the Active Directory module should be installed because the helpdesk technician will need only that.

- Open PowerShell as an administrator (the same way you would log in to a server).

- Run the following command

```ps1
Get-WindowsCapability -Online -Name RSAT*
```

This will display all available RSAT components and features, and also indicate which features are already installed.

Since we are only interested in Active Directory, run the command below and wait for it to complete.

```ps1
Add-WindowsCapability -Online -Name Rsat.ActiveDirectory.DS-LDS.Tools~~~~0.0.1.0
```

- After installation, press `Win + R` to open the Run dialog, then type dsa.msc to open Active Directory Users and Computers.

- Pin Active Directory Users and Computers to the taskbar and close it at this point because John Doe has no elevated privileges, and therefore cannot perform any administrative actions.

- Hold shift key and right click on Active Directory Users and Computers on the taskbar and select `run as different user`.

  > Note: Delegated AD permissions do not equal local administrator rights that is why you choose 'run as different account' instead of 'run as administrator'. Delegation does not add users to the local administrators group.

- When prompted, enter the administrative credentials. for example: username `RICHTECH\adm-j.doe`.

> Note: For GUI installation instructions, refer to [this site](https://activedirectorypro.com/install-rsat-remote-server-administration-tools-windows-10/).
