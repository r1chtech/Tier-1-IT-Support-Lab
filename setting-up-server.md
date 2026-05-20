### Sections

- [Configuring VM settings before installation](#configuring-vm-settings-before-installation)
- [Installing Windows Server 2022](#installing-windows-server-2022)
- [Renaming the server](#renaming-the-server)
- [Setting a static IP address](#setting-a-static-ip-address)
- [Installing Active Directory Domain Services](#installing-active-directory-domain-services)
- [Promoting the server to a domain controller](#promoting-the-server-to-a-domain-controller)

### Configuring VM settings before installation

**Adding the Virtual Machine (VM)**

- Click `New` and enter the VM name, VM path, OS type, and OS version. Do not attach the ISO yet.
- Set the RAM and CPU cores based on your VM requirements and what your host machine can comfortably handle. I used `4 GB RAM` and `4 CPU cores`.
- Set the virtual disk size (I left the default `50 GB`), then click `Next` and `Finish` to create the VM.


**Configuring Network Adapter**

- Select the new VM and open `Settings > Network`.
- On `Adapter 1`, keep the adapter attached to `NAT`. This will be the internet-facing adapter used during setup.
- On `Adapter 2`, enable the network adapter, attach it to an `Internal Network`, and assign a name to the network. I used `RichTech-LAN` for the local lab network.
- Click `OK` to save the settings.

**Mounting ISO file**

- Open `Settings > Storage`.
- Under `Controller: IDE`, select the empty disc icon. On the right side, click the small disc icon next to `Optical Drive`, then select `Choose a disk file`.
- Browse to your ISO location (mine was `/mnt/storage/RichTech-Lab/ISOs/`) and select the `Windows Server 2022` ISO.

### Installing Windows Server 2022

- Start the VM.
- The Windows Server installer will guide you through several setup steps. Most are straightforward, but two choices are important: the edition and disk partitioning.
- For the edition, select `Windows Server 2022 Standard Evaluation (Desktop Experience)`. Without the Desktop Experience option, Windows Server installs as `Server Core`, which provides a command-line-only interface.
- For disk partitioning, you will see a single unallocated disk matching the size you configured earlier. Select the disk and click `Next`.
- After Windows finishes installing and the VM restarts, you will be prompted to set the Administrator password. Choose a strong password, then complete the setup.

### Renaming the server

- Log in to the server and open `Server Manager`.
- In the left panel, click `Local Server`. Near the top, you will see the current computer name. Click the name to open the `System Properties` window.
- Click `Change`, enter your preferred server name, then click `OK`. My server name is `RICHTECH-DC01`.
- Restart the server when prompted to apply the changes.

### Setting a static IP address

- Right‑click the network icon in the taskbar > Open Network & Internet settings > Change adapter options.  
- You’ll see two adapters: one for NAT and one for the Internal Network. To identify them, right‑click each > Status > Details. The NAT adapter will show an IP like 10.0.2.x.
- Right‑click the Internal Network adapter > Properties.  
- Select Internet Protocol Version 4 (TCP/IPv4) > Properties and set:
  - IP address: 192.168.10.1  
    This is the private address space defined by [RFC 1918](https://www.rfc-editor.org/rfc/rfc1918), which are, (10/8 prefix), (172.16/12 prefix), (192.168/16 prefix). I chose the 192.168.10.x/24 range because the lab is small and only needs a few hosts. You can pick a different private range if preferred.

  - Subnet mask: 255.255.255.0
    This corresponds to a /24 network.

  - Default gateway: (leave blank)  
    A gateway is only required when the machine must route traffic outside its subnet.

  - Preferred DNS server: 127.0.0.1  
    The server will host DNS locally, so DNS queries should loop back to itself.

Click OK to close the IPv4 properties, then OK/Close on the adapter properties.


### Installing Active Directory Domain Services

- In Server Manager, click Manage > Add Roles and Features.
- Click Next through the Before you begin and Installation Type screens.  
- Ensure the correct server is selected, then click Next.
- On the Server Roles screen, check Active Directory Domain Services.  
- When prompted to add required features, click Add Features.  
- Click Next through the Features and AD DS information screens.
- On the Confirmation page, click Install.
- Wait for the installation to complete (no restart is required just for the role install).

### Promoting the server to a domain controller

- After AD DS installs, click the yellow notification flag in Server Manager and choose "Promote this server to a domain controller."
- Select "Add a new forest" (we're creating a domain from scratch).  
- Enter the root domain name (e.g., richtech.local). I use `.local` for an internal-only domain.
- Leave defaults on the next screens. Set the Directory Services Restore Mode (DSRM) password when prompted.  
- If you see a yellow warning about DNS delegation, ignore it.
- Ensure there are no red errors (green and yellow are OK).  
- Click Install. The server will reboot automatically when promotion completes.
- After reboot, the sign-in should show COMPANY\Administrator (or your domain\Administrator).

