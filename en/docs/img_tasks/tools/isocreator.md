# Testing your Windows images with the ISO creation tools

<p align="center">
	<img src="../../../res/img_tasks/tools/isocreator/isocreator.png" />
</p>

If you want to test the changes made to a Windows image, you can easily do so with the ISO creation tools, which include the **ISO creator** and the **Preinstallation Environment (PE) Helper**.

You will need the Windows Assessment and Deployment Kit (ADK), which you can download using the convenient link on the bottom left.

*This tool is available in DISMTools 0.5 and later.*

## Usage

To create a new ISO file, do the following:

1. **Pick your Windows image.** You can either browse through your computer for a Windows image to copy, pick an image from the pop-up mounted image picker, or pick the currently loaded one. Once you pick a Windows image, you will see information about each index in the image
2. **Choose the architecture for the Preinstallation Environment** by using the architecture list. It is recommended to pick the one that the image supports
3. (Optional, new in DISMTools 0.5.1) **Choose an unattended answer file to apply**
4. **Choose the target location of the ISO file.** If the target image exists, you will be asked if you want to replace it when clicking Create

With DISMTools 0.6.1 and later, you can also specify 2 options:

- **Copy to Ventoy drives** lets you take advantage of your [Ventoy](https://ventoy.net/en) drives for operating system installation. After the ISO is generated, it will be copied automatically to all Ventoy drives you have plugged into your computer
- **Use newly-signed boot binaries** will make the ISO files that you create ship with EFI boot binaries signed with the *Windows UEFI CA 2023* code-signing certificate. This is not checked by default because of reasons that are mentioned later in this document

This process can take between 5 to 10 minutes, depending on the size of the Windows image and the speed of your computer's disk drive.

## Starting installation (local-only)

You can start the installation of your operating system in 2 ways:

- By booting to installation media,
- By starting the installation from within a full Windows environment (DISMTools 0.6.1 and later), or
- By booting to the boot image of the installation disc file via the **Preboot eXecution Environment** (PXE) (DISMTools 0.7 and later)

### Starting from a full Windows environment

DISMTools 0.6.1 and later come with a program that prepares your computer for OS installation. This is called *HotInstall*, and the process of computer preparation is as follows:

**NOTE:** HotInstall does not support Ventoy drives, due to the way they work

1. Start `setup.exe` in the root of the DVD or USB drive. If you see a notification when inserting the installation media, you can also click on it to start the installer, effectively taking advantage of AutoRun:

	![HotInstall start](../../../res/img_tasks/tools/isocreator/hotinstall/hotinstall_dvdstart.png)

2. Accept the disclaimers and click Next:

	![HotInstall disclaimer](../../../res/img_tasks/tools/isocreator/hotinstall/hotinstall_disclaimers.png)

3. Review that the ISO file contains the installation image you want to test, and click Next. On this screen, you can also export all your third-party drivers to a folder, in case you need them later:

	![HotInstall image review](../../../res/img_tasks/tools/isocreator/hotinstall/hotinstall_review_image_info.png)
	
4. Wait for your computer to be prepared for installation. This process will take some time, depending on your computer's performance:

	![HotInstall progress](../../../res/img_tasks/tools/isocreator/hotinstall/hotinstall_progress.png)

After restarting your computer, choose "DISMTools Operating System Installation" (if it is not selected by default) and press Enter. The first stage of the installation will start:

<p align="center">
	<img src="../../../res/img_tasks/tools/isocreator/hotinstall/hotinstall_bootmgr.png" />
</p>

### Continuing the installation

Whether you've started the installation with HotInstall or by booting to installation media, the installation process will be the same. The Preinstallation Environment Helper will guide you through the installation process, which includes:

1. Selecting the disk and partition where the operating system will be installed
2. Choosing the index of the Windows image to apply
3. Applying the Windows image
4. Running serviceability tests
5. Creating boot files
6. Rebooting your system

Let's go over these steps in more detail:

**NOTE:** if you started installation of the Windows image from USB by booting to it, choose option 1 for a local installation

#### Selecting the disk and partition

The PE Helper will get the disks that are available on your computer:

<p align="center">
	<img src="../../../res/img_tasks/tools/isocreator/dt_pe/dt_pe_disk_chooser.png" />
</p>

On this screen, you can also stop for a moment to take actions if something does not look right with the disk listing, or if you want to see what disks have enough free space for the installation of your Windows image:

- If you don't see the disk you want to use, it could be because your computer uses a third-party disk controller. If that is the case, type `DIM` and press Enter to open the Driver Installation Module. More information on how to use this tool can be found later in this document
- (**Only for installations started with HotInstall**) If you want to see the free space on your disks, type `DSCR` and press Enter. This will show you the Disk Space Checker report generated by HotInstall:

<p align="center">
	<img src="../../../res/img_tasks/tools/isocreator/hotinstall/hotinstall_dscr.png" />
</p>

After selecting the disk, you will be asked to select the partition where the operating system will be installed. You can choose to clean all the partitions of your disk, or you can choose to format a specific partition:

<p align="center">
	<img src="../../../res/img_tasks/tools/isocreator/dt_pe/dt_pe_part_chooser.png" />
</p>

**IMPORTANT:** all actions past this point are irreversible. Make sure that you have backed up your data, and that you have selected the correct disk, before proceeding.

#### Choosing the index of the Windows image

After selecting the disk and partition, you will be asked to choose the index of the Windows image that you want to apply. The PE Helper will show you basic index information, including the name you have given to the image:

<p align="center">
	<img src="../../../res/img_tasks/tools/isocreator/dt_pe/dt_pe_image_chooser.png" />
</p>

You can also see more information about the image by typing `INFO` and pressing Enter:

<p align="center">
	<img src="../../../res/img_tasks/tools/isocreator/DT_PE_ImageInfo.png" />
</p>

After choosing the index, the PE Helper will apply the image to the selected disk or partition, will run serviceability tests, and will create boot files.

After everything is done, your computer will restart automatically in 10 seconds:

<p align="center">
	<img src="../../../res/img_tasks/tools/isocreator/dt_pe/dt_pe_comp_restart.png" />
</p>

From this point, you can remove the installation media and let your computer finish operating system configuration.

#### Windows UEFI CA 2023 information

The Windows UEFI CA 2023 certificate is now used to sign new EFI boot binaries. This is present in versions 10.1.26100.2454 and later of the Windows ADK as an option for ISO file creation.

Some computers may not boot correctly using these new EFI boot binaries, and compatibility may depend on whether or not a device that uses UEFI contains this certificate. You can check if your computer contains this certificate by running the following PowerShell command as an administrator:

```powershell
[System.Text.Encoding]::ASCII.GetString((Get-SecureBootUEFI db).bytes) -match 'Windows UEFI CA 2023'
```

If the command returns `True`, your computer has this certificate. Otherwise, you may need updates to add support for this certificate. If you have doubts regarding the compatibility of your computer with this certificate, it is recommended to leave the option unchecked.

MBR systems are not affected by this change.

You can learn more here: [Revoking vulnerable Windows boot managers](https://techcommunity.microsoft.com/blog/windows-itpro-blog/revoking-vulnerable-windows-boot-managers/4121735)

### Driver Installation Module

The **Driver Installation Module** (DIM) is a quick and easy way of adding device drivers to booted Windows Preinstallation Environments:

<p align="center">
	<img src="../../../res/img_tasks/tools/isocreator/dim/DIM_MainScreen.png" />
</p>

While full functionality is achieved with the DISMTools Preinstallation Environment, you can still use the DIM in every Preinstallation Environment. This is compatible with the x86, amd64, and arm64 architectures.

*NOTE: arm64 support for the DIM arrived in version 0.6.2.*

#### Usage

1. Click the "Add" button and choose between a single driver file or an entire folder

	- If you choose a folder, the Driver Installation Module will perform a recursive scan for INF files. This may pick up invalid INF files you may have

2. Perform any changes with the "Edit" and "Remove" buttons
3. Click the "Install" button and let the program add the drivers

After driver installation, you will see an installation summary:

<p align="center">
	<img src="../../../res/img_tasks/tools/isocreator/dim/DIM_Summary.png" />
</p>

Later, after applying your Windows image, the Preinstallation Environment Helper will add those drivers to the target image.

#### Practical use: computers with third-party disk controllers

A practical use of the Driver Installation Module is to add compatibility for disk controllers that are not shipped with Windows PEs by default. This is the case if the test system is relatively new.

<p align="center">
	<img src="../../../res/img_tasks/tools/isocreator/dim/practical_use/disk_before.jpg" />
</p>

Here's how you can proceed:

1. Boot to a live Linux environment and use the partition manager that may come with it to grab the model of the desired drive. If you don't have a Linux ISO available, we recommend [GParted Live](https://gparted.org/livecd.php) for its simplicity and its small size

	![GParted](../../../res/img_tasks/tools/isocreator/dim/practical_use/diskinfo.jpg)
	
2. Additionally, you may want to get information about the model of the computer. In most Linux systems, you can run `sudo lshw` in the terminal

	![Computer info](../../../res/img_tasks/tools/isocreator/dim/practical_use/compinfo.jpg)
	
	After getting the model of the computer, go to the computer manufacturer's website to download compatible drivers. **Make sure that you extract them and that you DON'T install them to your system by accident**. After that, copy the drivers to wherever you want
	
3. Open the Driver Installation Module, add the folder containing the drivers and click Install

	![DIM Installation](../../../res/img_tasks/tools/isocreator/dim/practical_use/dim_install.jpg)
	
4. Check disks once again

	![Disk Listing](../../../res/img_tasks/tools/isocreator/dim/practical_use/disk_after.jpg)
	
<!-- And, yes, I know how to make screenshots -->

#### Serviceability tests

Serviceability tests are performed during OS installation to make sure that the image that has been applied is valid. They are only run if the architectures of the PE and the image are the same, and must pass in order to successfully complete the installation of the operating system.

If these tests fail, you may need to repair the component store of your Windows image.

## Network-based installations

If you want to deploy your installation image to several computers at once with a deployment server, you can follow this guide.

**NOTE:** the only supported platform is Windows Deployment Services (WDS). Additional platforms might be supported in the future.

### Preparing your server

The first step is to prepare your server for Windows Deployment Services and, if not set up, your network infrastructure. This section will cover both tasks.

#### Checking Server Roles

To successfully deploy operating systems via the network, you will need the following server roles:

- DHCP (Dynamic Host Configuration Protocol)
- Windows Deployment Services

**NOTE:** you can have a different server that acts as the DHCP server. In that case, you only need the WDS role

You should be able to determine whether they are installed by simply searching for the management tools:

![DHCP Requirement](../../../res/img_tasks/tools/isocreator/netinstall/wds/dhcp_req.png)

![WDS Requirement](../../../res/img_tasks/tools/isocreator/netinstall/wds/wds_req.png)

If not present, it's time to assess the current situation of the server. To do this:

1. Go to Server Manager
2. Click "Add roles and features", and perform a role-based or feature-based installation
3. Select your server, and check which roles are present. Both must be installed:

	![Server Roles](../../../res/img_tasks/tools/isocreator/netinstall/wds/roles.png)
	
Based on this:

- *If they are not installed:*

	1. Check both DHCP and WDS and continue installation, whilst including management tools
	2. Continue without modifying any features, unless you want to enable or disable some of them
	3. Read the instructions for DHCP carefully
	4. In the configuration of the WDS role, leave both servers (deployment and transport) checked
	5. Proceed with the installation. After installing the roles, you will see that a role needs configuration. That is the DHCP role.
	6. As stated earlier, perform the configuration of the DHCP server
	
		![DHCP Configuration](../../../res/img_tasks/tools/isocreator/netinstall/wds/dhcp_config.png)
	
	7. Click "Commit" and "Close":
	
		![DHCP Configuration 2](../../../res/img_tasks/tools/isocreator/netinstall/wds/dhcp_postconfig_commit.png)
	
- *If they are installed, but the management tools are not present:*

	You will have to enable the `DHCPServer-Tools` and `Microsoft-Windows-Deployment-Services-Admin-Pack` features. You can do this by [enabling the features](../../features/enable_feature) from within the [online installation management mode](../../online_inst_mgmt).
	
	You may have to restart the server after enabling the features.

#### Preparing the network infrastructure

If you already have a network infrastructure set up for remote deployment, feel free to skip this step. However, if you just want to tinker with remote installations at home with a wireless connection, you can do the following steps to create a virtual switch (*vSwitch*).

**Notes:** 

- These steps only work with Hyper-V
- After rebooting your host computer, your virtual machines connected to your switch may lose connection to the Internet. However, the switch will still function for remote OS installation
- Additional data consumption may occur

To set up the virtual switch:

1. In Hyper-V Manager, open the virtual switch manager and set up a new **Internal** switch. Give it the name you want, and click OK. You should have the following settings:

	![vSwitch](../../../res/img_tasks/tools/isocreator/netinstall/wds/viridian_new_vswitch.png)

2. After creating the switch, press <kbd>Win</kbd> + <kbd>R</kbd> and run `ncpa.cpl`. Then, double-click your wireless NIC (*Network Interface Card*) and go to the adapter settings
3. Set up Internet Connection Sharing using the newly created switch. The resulting IP address from ICS is usually `192.168.137.1`

Finally, configure the server to use the new switch:

![Connect To Switch](../../../res/img_tasks/tools/isocreator/netinstall/wds/viridian_connect_to_switch.png)

Turn on the server VM and run `ipconfig /all` to make sure the virtual network adapter is detecting the address used by Internet Connection Sharing as the default gateway. If so, then try pinging it:

![Connect To Switch](../../../res/img_tasks/tools/isocreator/netinstall/wds/viridian_server_ipconfig.png)

**Tip:** if you want to make sure the IP address of the server doesn't change (remains static), or if it can't pick up the default gateway address, go to the network adapter properties of the virtual network adapter, and configure IPv4 to use the following values:

![Static IP](../../../res/img_tasks/tools/isocreator/netinstall/wds/viridian_server_static_ip.png)

If the server can ping your computer, then you have a working vSwitch. You can now hook up the rest of the virtual machines you would like to use to that vSwitch.

#### Configuring the WDS server and DHCP Scopes

Now that the server can use your switch, we'll need to configure it so that it can work with WDS. To do this, open the WDS management tool, and select your server. Then, right-click it and select "Configure Server":

![Configure Server](../../../res/img_tasks/tools/isocreator/netinstall/wds/wds_configure_server.png)

Next, select the mode in which the server will operate. This cannot be changed afterwards without removing the server and reconfiguring it, so make sure that you select the correct mode.

If you have a different server that acts as a Domain Controller (DC) using Active Directory, or if the current server already acts as the DC, leave the first option checked. Otherwise, if you don't have a Domain Controller, or if you just want to tinker with network-based deployment, choose Standalone mode:

![Server Modes](../../../res/img_tasks/tools/isocreator/netinstall/wds/wds_server_modes.png)

*For this guide, we'll go with the Standalone mode, since we don't have a domain controller*

Afterwards, select the path in which the remote installation files will be stored. By default, the `RemoteInstall` folder will be stored on the root of the system drive. Change it if it's necessary, but for our case it's fine:

![Remote Install Location](../../../res/img_tasks/tools/isocreator/netinstall/wds/wds_server_remoteinstall.png)

The following step is very important, and depends on where you configured the DHCP server. If the WDS server is also the DHCP server, then leave both options checked. Otherwise, only leave the first option checked, and configure DHCP option 60 on the DHCP server. More on these options later in the guide:

![Proxy DHCP](../../../res/img_tasks/tools/isocreator/netinstall/wds/wds_server_proxy_dhcp.png)

Finally, you need to configure initial PXE settings to respond to both known and unknown client computers. Additionally, you can choose to require administrator approval for unknown clients. This gives you greater control over which devices can connect and which ones can't. You can modify the initial PXE settings later if you wish:

![Initial PXE Settings](../../../res/img_tasks/tools/isocreator/netinstall/wds/wds_server_pxe_initial_settings.png)

After clicking Next, the server will be configured and the WDS service will start. However, you may encounter this problem when trying to start the service:

![WDS Service Startup Error](../../../res/img_tasks/tools/isocreator/netinstall/wds/wds_server_startup_error.png)

If this happens, you can try starting the service manually by going here:

![Service Manual Startup](../../../res/img_tasks/tools/isocreator/netinstall/wds/wds_manual_start.png)

Now that you have WDS set up, we'll talk about the other half of the server.

A DHCP server, in order to automatically assign IP addresses to clients, needs to have scopes with lengths that can contain the maximum amount of clients to use. If you already configured scopes, you can skip this step. Otherwise, keep reading.

Open the DHCP management tool, select your server, then go to IPv4. We'll create a basic IPv4 scope using a unicast transmission (more common).

![DHCPv4 panel](../../../res/img_tasks/tools/isocreator/netinstall/wds/dhcp_ipv4_scope_panel.png)

Right-click IPv4 and select New scope. In the wizard, follow these steps:

1. Give your scope a name and an optional description to better identify it:

	![Scope Identification](../../../res/img_tasks/tools/isocreator/netinstall/wds/dhcp_ipv4_scope_name.png)

2. Next, provide an IP address range that will be used to provide addresses to clients (this is known as the **address pool**). It should have the same subnet mask you have configured in your server. For this guide, we'll create a scope that can host addresses to 51 clients:

	![Address Pool](../../../res/img_tasks/tools/isocreator/netinstall/wds/dhcp_ipv4_scope_addressrange.png)
	
3. If you don't want to assign addresses within a certain range, you can add exclusions to the scope. For this guide, we won't exclude addresses:

	![Address Pool Exclusions](../../../res/img_tasks/tools/isocreator/netinstall/wds/dhcp_ipv4_scope_excludedrange.png)
	
4. Configure the scope lease duration. A DHCP lease to a client can last for a given time before the server gives a different IP address to said client. The default of 8 days is usually fine, unless it is meant to be something else in your environment:

	![Address Lease Duration](../../../res/img_tasks/tools/isocreator/netinstall/wds/dhcp_ipv4_scope_leases.png)

5. When asked to configure more details about the scope, select Yes and click Next. Then, specify the default gateway address for the scope. If you followed the guide on setting up the vSwitch, the gateway address you need to enter is the IP address offered by your host as part of Internet Connection Sharing. This is also the DNS address to add in the next screen if you set it up earlier:

	![Gateway](../../../res/img_tasks/tools/isocreator/netinstall/wds/dhcp_ipv4_scope_gateway.png)

6. After configuring the gateway address and the DNS server address, leave the WINS server section as is and click Next. When you're asked to activate the scope, select No and click Next:

	![Activation](../../../res/img_tasks/tools/isocreator/netinstall/wds/dhcp_ipv4_scope_activate.png)

7. In the newly created scope, right-click Scope Options, and select "Configure Options...":

	![Configure Options](../../../res/img_tasks/tools/isocreator/netinstall/wds/dhcp_scope_options_menu_item.png)
	
8. Then, configure the following options as follows:

	- DHCP Option 66 (*Boot Server Host Name*): the IP address of the WDS server
	- DHCP Option 67 (*Bootfile Name*): `boot\x64\wdsnbp.com` (do this if all your machines use the amd64 architecture)
	
	For example:
	
	![Required scopes](../../../res/img_tasks/tools/isocreator/netinstall/wds/dhcp_scope_options_required.png)

9. Finally, right-click the scope and click "Activate"

### Adding the Windows images

Before booting the clients to perform network-based deployments, we'll first need to add the Windows images. Here's how you can do it:

1. Insert or mount the ISO file that was just created, and copy all the WIM files to any folder on your server:

	![Copy Files](../../../res/img_tasks/tools/isocreator/netinstall/wds/wds_copy_images.png)

2. Then, in WDS, go to "(Your Server) -> Boot images", right-click the empty area and select "Add boot image..."

	![Add Boot Image](../../../res/img_tasks/tools/isocreator/netinstall/wds/wds_add_boot_image.png)

3. Next, select the boot image (`boot.wim`) and finish the wizard:

	![Boot Image Location](../../../res/img_tasks/tools/isocreator/netinstall/wds/wds_boot_image_location.png)

4. Afterwards, go to "(Your Server) -> Install Images", right-click the empty area and select "Add install image..."

	![Add Install Image](../../../res/img_tasks/tools/isocreator/netinstall/wds/wds_add_install_image.png)

5. This will require the creation of an image group. Name it however you want, and then specify the install image to add (`install.wim`):

	![Image Group](../../../res/img_tasks/tools/isocreator/netinstall/wds/wds_add_image_group.png)
	
	![Install Image Location](../../../res/img_tasks/tools/isocreator/netinstall/wds/wds_install_image_location.png)

6. The install image may contain more than 1 index. Check the ones that you want to deploy using WDS and finish the wizard. You can also provide custom names and descriptions for each of the indexes when deploying them through the network:

	![Indexes](../../../res/img_tasks/tools/isocreator/netinstall/wds/wds_install_image_indexes.png)
	
Finally, you should have this setup:

![Image Setup](../../../res/img_tasks/tools/isocreator/netinstall/wds/wds_final_image_config.png)

You can now start the PXE clients. In the server, you also need to start the server component of the WDS Helper. To do this, right-click `wdshelper_server.ps1` in `<Drive Root>\pxehelpers\wds`, and select "Run with PowerShell"

![WDSH Server Startup](../../../res/img_tasks/tools/isocreator/netinstall/wds/wdsh_server_startup.png)

### Beginning installation via PXE

If you followed each step right, you should now see a screen like the following one:

![WDS Startup](../../../res/img_tasks/tools/isocreator/netinstall/wds/wds_startup.png)

If so, press <kbd>ENTER</kbd> now and wait for the DISMTools PE to start up. Once it starts up, select option 2 for network installation:

![DT PE Network](../../../res/img_tasks/tools/isocreator/netinstall/wds/dt_pe_netinstall.png)

Eventually, you'll arrive at this screen. Provide the server IP address, the port to which the server is listening (usually port 8080), the name of the user that's hosting the images (in most cases, `Administrator`), and the password:

![WDSHC AuthInfo](../../../res/img_tasks/tools/isocreator/netinstall/wds/wdsh_client_authinfo.png)

Choose your image from the list that will then appear, and the group it's in; and press ENTER:

![WDSHC Install Images](../../../res/img_tasks/tools/isocreator/netinstall/wds/wdsh_client_install_images.png)

After preparing the deployment of the image file, configure your disks accordingly:

![WDSHC Disk Configuration](../../../res/img_tasks/tools/isocreator/netinstall/wds/wdsh_client_diskconfig.png)

Then, select the index:

![WDSHC Install Image Index](../../../res/img_tasks/tools/isocreator/netinstall/wds/wdsh_client_select_image_index.png)

And, finally, wait for the image to be applied:

![WDSHC Applying Image](../../../res/img_tasks/tools/isocreator/netinstall/wds/wdsh_client_apply_image.png)

## Extensibility Suite

The Extensibility Suite lets you expand the DISMTools Preinstallation Environment even further by letting you modify its functionality and add applications. You can add to the Preinstallation Environment applications that you may find useful, or applications that you have worked on.

*This task is available in DISMTools 0.5.1 and later.*

### Usage

1. Go to Tools > Create a testing environment...
2. Specify the architecture and target location
3. Click Create

Then, you can look at the README file in the target directory to learn more.

## Remarks

- **Please make sure to commit your unsaved changes to your image before creating the ISO file**