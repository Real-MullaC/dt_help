# Unattended answer file creator

<p align="center">
    <img src="../../../res/img_tasks/unattend/unatt_creator/unatt_creator_express.png" />
</p>

The unattended answer file creator lets you create unattended answer files compatible with Windows 10 and 11 in 2 ways: an easy-to-use wizard, or a text editor

*This tool is available in DISMTools 0.5.1 and later*

## Creator modes

The creator contains 2 modes: an Express mode and an Editor mode. You can easily switch to either mode by clicking the buttons at the left corners of the window.

### Express mode

The express mode is useful for those who have never created answer files before or don't want to use text editors. Simply follow the steps of the wizard, and you will have your file in no time.

If you have a project loaded, DISMTools will let you save your unattended answer files to the unattended answer file folder of your project without you having to change directories. You can obviously save these files anywhere.

If you would like to learn more about the steps in this wizard, keep reading.

#### Wizard Steps

In the **Regional Configuration** page, you can set the language, system locale, keyboard layout and home location of the target system. Set these to values that suit your needs. Or, you can set them during the configuration of the applied operating system:

<p align="center">
    <img src="../../../res/img_tasks/unattend/unatt_creator/steps/unatt_creator_regional_settings.png" />
</p>

In the **System Configuration** page, you can set the computer name, the architectures that you wish to target with your answer file, and other settings:

<p align="center">
    <img src="../../../res/img_tasks/unattend/unatt_creator/steps/unatt_creator_system_configuration.png" />
</p>

Additional options include:

- **Using a configuration set or distribution share**: a configuration set can be used to preload applications and drivers into the target image. You can create these sets with the Windows System Image Manager. Make sure that there is a configuration set on the ISO file to which you are copying the answer file
- **Windows 11 settings**: these help you bypass the system requirements and network connection setup. Configure the latter if the target system does not have network capabilities. If you are looking to bypass this to be able to create local accounts, you can create the user accounts from this wizard as well

In the **Time Zone** page, you can set the time zone of the target system:

<p align="center">
    <img src="../../../res/img_tasks/unattend/unatt_creator/steps/unatt_creator_timezone.png" />
</p>

In the **Disk Configuration** page, you can set the disk configuration of the target system. You can let Setup give you the control over the disk configuration, or you can partition the first disk. You can also automate the entire disk configuration process by specifying DiskPart scripts:

<p align="center">
    <img src="../../../res/img_tasks/unattend/unatt_creator/steps/unatt_creator_disk_config.png" />
</p>

In the **Product Key** page, you can set the product key of the target system. You can choose from a generic product key tailored to the image edition, or you can type a custom product key:

<p align="center">
    <img src="../../../res/img_tasks/unattend/unatt_creator/steps/unatt_creator_product_key.png" />
</p>

Notes:

- If you want to use a generic product key, choose the one tailored to your edition. Generic product keys are only meant for operating system installation, and will not activate the system
- If you want to use a custom product key, make sure that it is valid and that it is for the edition of the image. DISMTools will only check if the syntax of the product key is correct, but will not check if the product key is valid for installation or activation

In the **User Accounts** page, you can create the local user accounts of the target system. You can create up to 5 accounts, and you can set the password of each account:

<p align="center">
    <img src="../../../res/img_tasks/unattend/unatt_creator/steps/unatt_creator_user_accounts.png" />
</p>

From here, you can also enable auto-logon settings for the target system. But, if you don't want to use local accounts, or want the operating system to ask you, you can skip this step.

You can also configure password expiration settings for the target system, but it is not recommended to do so, according to the [National Institute of Standards and Technology (NIST)](https://pages.nist.gov/800-63-FAQ/#q-b05):

<p align="center">
    <img src="../../../res/img_tasks/unattend/unatt_creator/steps/unatt_creator_user_accounts_pw_expiry.png" />
</p>

Finally, you can configure Account Lockout policies for the target system, or disable them. The latter is not recommended, as it can make the system more vulnerable to brute-force attacks:

<p align="center">
    <img src="../../../res/img_tasks/unattend/unatt_creator/steps/unatt_creator_user_accounts_lockout.png" />
</p>

Notes:

- At least one account must be part of the Administrators group

In the **Virtual Machine Support** page, you can specify whether or not you want to install the integration features of your virtual machine provider (eg. VirtualBox Guest Additions or VMware Tools):

<p align="center">
    <img src="../../../res/img_tasks/unattend/unatt_creator/steps/unatt_creator_vm_support.png" />
</p>

In the **Network Configuration** page, you can specify whether the target system will connect to a wireless network:

<p align="center">
    <img src="../../../res/img_tasks/unattend/unatt_creator/steps/unatt_creator_network_config.png" />
</p>

Notes:

- The authentication technology must be supported by both the wireless router and the network adapter of the target system. Make sure that the system contains a wireless adapter first
- If you don't want to set up a wireless network connection, or if the target system does not contain a wireless adapter, choose *Skip configuration*

In the **System Telemetry** page, you can specify whether or not you want to send information to Microsoft and third-parties:

<p align="center">
    <img src="../../../res/img_tasks/unattend/unatt_creator/steps/unatt_creator_telemetry.png" />
</p>

Notes:

- Choosing *Disable telemetry* will **not** disable all sources of data collection. You will have to perform additional modifications to your Windows image in order to further reduce data collection

In the **Post-Installation Scripts** page, you can configure additional scripts in PowerShell that will be run during Windows installation, or when accounts log on for the first time:

<p align="center">
    <img src="../../../res/img_tasks/unattend/unatt_creator/steps/unatt_creator_postinst_scripts.png" />
</p>

You can either write the post-installation scripts from scratch, or import existing ones.

Notes:

- Support for Batch scripts will be added in a future update
- After scripts are done, you can restart Windows Explorer in case you have applied personalization changes, for example, via the Registry

In the **Component Settings** page, you can specify placeholders for additional components that you want to add to your answer file for specific passes. You will have to fill them in manually after the answer file is generated:

<p align="center">
    <img src="../../../res/img_tasks/unattend/unatt_creator/steps/unatt_creator_components.png" />
</p>

Notes:

- You can learn more about the components [here](https://learn.microsoft.com/en-us/windows-hardware/customize/desktop/unattend/components-b-unattend)
- You can fill in the placeholders in the Editor mode, or in the Windows System Image Manager
- If you don't want to configure components, simply skip this step

Finally, before creating the answer file, you can review the settings that you have configured in the wizard. If you want to change any settings, you can go back to the respective pages:

<p align="center">
    <img src="../../../res/img_tasks/unattend/unatt_creator/steps/unatt_creator_review.png" />
</p>

After creating the answer file, you can create another one, open the file location, apply it, or edit it with the Editor mode or the Windows System Image Manager.

### Editor mode

The editor mode lets you perform advanced customizations to your unattended answer file to add more things, like additional components or rules. You can operate the editor mode using the buttons in the toolbar.

<p align="center">
    <img src="../../../res/img_tasks/unattend/unatt_creator/unatt_creator_editor.png" />
</p>

DISMTools 0.6.1 adds the ability to normalize the spacing of the answer file to make it consistent:

<p align="center">
    <img src="../../../res/img_tasks/unattend/unatt_creator/unatt_creator_editor_normalize.gif" />
</p>

## Requirements

The unattended answer file creator requires the .NET 9 Runtime for the generator program to function. If DISMTools detects that the runtime hasn't been installed, you will be offered the ability to use the self-contained version, which contains the runtime:

<p align="center">
    <img src="../../../res/img_tasks/unattend/unatt_creator/unattendgen_selfcontained.png" />
</p>

If you decide to use this version, DISMTools will save this preference until the self-contained version is removed, either manually, or due to a program update.

Downloading this version will take some time, depending on your network connection speed and computer performance. After the download is complete, you will see a notification in your system tray, depending on what icons are allowed to appear in the tray:

<p align="center">
    <img src="../../../res/img_tasks/unattend/unatt_creator/unattendgen_notify.png" />
</p>

Finally, like with the **Windows Image Explorer**, you can use the generator program separately. You can check out its repository [here](https://github.com/CodingWonders/UnattendGen)

## Acknowledgements

Special thanks to Christoph Schneegans for creating the library that makes this creator possible.