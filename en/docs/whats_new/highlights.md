# Release highlights

This new version of DISMTools comes with new features that enhance image management and servicing tasks. Here are some of its key changes.

If you want to take a look at everything that has changed though, check out the [release notes page](https://github.com/CodingWonders/DISMTools/releases/latest) for more information.

## Start installations from full operating environments, and more Preinstallation Environment goodies

DISMTools 0.6.1 features a new way to start the installation of your customized image with a technology called *HotInstall*. This installer configures the boot entries of your computer to automatically boot to the DISMTools Preinstallation Environment, from which you can perform image application and disk configuration.

<p align="center">
	<img src="../../res/img_tasks/tools/isocreator/hotinstall/hotinstall_progress.png" />
</p>

The Preinstallation Environment Helper has also been improved, adding support for the latest Windows ADKs, the ability to create disc images with [boot binaries signed with new certificates](https://techcommunity.microsoft.com/blog/windows-itpro-blog/revoking-vulnerable-windows-boot-managers/4121735), and the ability to get more information about your Windows image:

<p align="center">
	<img src="../../res/img_tasks/tools/isocreator/DT_PE_ImageInfo.png" />
</p>

The ISO creator lets you copy your disc images to Ventoy drives as well:

<p align="center">
	<img src="../../res/img_tasks/tools/isocreator/isocreator_vtoy.png" />
</p>

[Learn more about the new ISO creation features](../../img_tasks/tools/isocreator)

## New features for your unattended answer files

The unattended answer file features now let you configure post-installation scripts in PowerShell. You can write your own code, or you can open an existing script.

<p align="center">
	<img src="../../res/whats_new/WhatsNew_2.png" />
</p>

You can also **normalize the spacing** of unattended answer files to make it consistent:

<p align="center">
	<img src="../../res/img_tasks/unattend/unatt_creator/unatt_creator_editor_normalize.gif" />
</p>

Your unattended answer files can also target multiple processor architectures. For example, you can create an answer file that works on regular computers and ARM-based Copilot+ PCs:

<p align="center">
	<img src="../../res/whats_new/WhatsNew_4.png" />
</p>

[Learn more about the new unattended answer file features](../../img_tasks/unattend/unatt_create)

## Overall refinements

This release also focuses on refining existing tasks and functionality to improve the user experience. For example, more items have received translations, the program is more reliable, and components have been updated to their latest versions.

<!-- Room for more features -->

# Thanks to the contributors

The following people have helped shape this version of DISMTools by reporting issues or suggesting new features or changes:

- [Dretreyt](https://github.com/Dretreyt) for spotting issues with setting save functionality,
- [arielsil](https://github.com/arielsil) for spotting issues with some background processes functions and some tasks,
- [novice55](https://github.com/novice55) for spotting issues with background processes,
- [webber3242](https://github.com/webber3242) for spotting issues with project creation,
- [Dede333](https://github.com/Dede333) for helping spot WIMBoot issues with non-Windows 8.1 images, and
- [InnerBrat](https://github.com/InnerBrat) for spotting folder attribute detection issues

If you want to appear in this list, you can report issues or suggestions in any channel you prefer (via the [MDL forum thread](https://forums.mydigitallife.net/threads/dismtools.87263/), via the [GitHub repository](https://github.com/CodingWonders/DISMTools), or via any announcements on the [DISMTools subreddit](https://reddit.com/r/DISMTools) or on the [Windows](https://reddit.com/r/Windows), [Windows11](https://reddit.com/r/Windows11) and [Windows10](https://reddit.com/r/Windows10) subreddits (as comments)) or submit new code changes (read the [contribution guidelines](https://github.com/CodingWonders/DISMTools/blob/stable/CONTRIBUTING.md) for more information).