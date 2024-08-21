# Release highlights

This new version of DISMTools comes with new features that enhance image management and servicing tasks. Here are some of its key changes.

If you want to take a look at everything that has changed though, check out the [release notes page](https://github.com/CodingWonders/DISMTools/releases/latest) for more information.

## Test your Windows images with more confidence

The ISO creation tools have seen several improvements with the addition of 2 new features. The **Driver Installation Module** lets you add drivers to Windows Preinstallation Environments to add support for devices that are not compatible by default, and the **Extensibility Suite** lets you perform further customizations to the DISMTools Preinstallation Environment to include your applications (either the ones that you have made or the ones that you find useful to include).

<p align="center">
	<img src="../../res/whats_new/WhatsNew_1.png" />
</p>

[Check out the new features](../../img_tasks/tools/isocreator#driver-installation-module)

## Task additions and improvements

DISMTools 0.5.1 comes with improvements to existing tasks and some newcomers. For example, you can now configure stub package preferences for AppX packages, so that you can either explicitly install the full version of an application, its stub version (meaning that the full application will be downloaded on first launch), or go with the defaults for the application package.

Also, you can now list the contents of Windows images (even the ones that haven't been mounted) with the **Windows Image Explorer**, which is also available as a standalone download.

Next, package addition has received the ability to add Microsoft Update Manifest (MUM) files. And, finally, you can now configure keyboard layered drivers for Japanese and Korean keyboards.

<p align="center">
	<img src="../../res/whats_new/WhatsNew_2.png" />
</p>

Learn more about:

- [Stub package preferences](../../img_tasks/appx/add_provisionedappxpackage/#options)
- [Listing files of Windows images](../../img_tasks/mgmt/list_image)
- [Microsoft Update Manifest files](../../img_tasks/packages/add_package/#microsoft-update-manifest-files)
- [Setting keyboard layered drivers](../../img_tasks/langs/set_layereddriver)

## Revamped unattended answer file features

The unattended answer file features have been significantly revamped, thanks to a new base powered by the [unattended answer file generator from Christoph Schneegans](https://schneegans.de/windows/unattend-generator/). This includes a revamped creation wizard, a new manager, and a new task that lets you apply such files.

When creating your ISO files, you can also use your unattended answer file to test it. The Operating System installer will apply it for you.

<p align="center">
	<img src="../../res/whats_new/WhatsNew_3.png" />
</p>

[Explore the new unattended answer file features](../../img_tasks/unattend/unattend)

## New translations

*Ciao!* We have travelled to a country with amazing places like Rome or Venice, with amazing food like spaghetti or *ravioli*, and with tourist attractions like the Colosseum or the leaning tower of Pisa.

Jokes aside, we have added Italian translations to this version, making it the fifth supported language.

<p align="center">
	<img src="../../res/whats_new/WhatsNew_4.jpg" />
</p>

## Overall refinements

This release also focuses on refining existing tasks and functionality to improve the user experience. For example, you can now get a description of operation errors instead of generic instructions telling you to look at the error codes online. We have updated the dependencies of the program, simplified the logic of some tasks, and improved detection of Assessment and Deployment Kits as well.

<!-- Room for more features -->

# Thanks to the contributors

The following people have helped shape this version of DISMTools by reporting issues or suggesting new features or changes:

- [AnubyteCode](https://github.com/AnubyteCode) for suggesting MUM package addition,
- [drew84](https://forums.mydigitallife.net/members/drew84.422144/) for suggesting Christoph Schneegans' library for the unattended answer file features, and
- [vadimlitvinenko87](https://github.com/vadimlitvinenko87) for spotting video feed detector issues

If you want to appear in this list, you can report issues or suggestions in any channel you prefer (via the [MDL forum thread](https://forums.mydigitallife.net/threads/dismtools.87263/), via the [GitHub repository](https://github.com/CodingWonders/DISMTools), or via any announcements on the [DISMTools subreddit](https://reddit.com/r/DISMTools) or on the [Windows](https://reddit.com/r/Windows), [Windows11](https://reddit.com/r/Windows11) and [Windows10](https://reddit.com/r/Windows10) subreddits (as comments)) or submit new code changes (read the [contribution guidelines](https://github.com/CodingWonders/DISMTools/blob/stable/CONTRIBUTING.md) for more information).