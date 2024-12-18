# Release highlights

This new version of DISMTools comes with new features that enhance image management and servicing tasks. Here are some of its key changes.

If you want to take a look at everything that has changed though, check out the [release notes page](https://github.com/CodingWonders/DISMTools/releases/latest) for more information.

## See image information reports in a prettier way

When saving the information of a Windows image, you will now see prettier results due to the reports now being saved as Markdown files and, with the inclusion of [Markdig](https://www.github.com/xoofx/Markdig), results can be shown in Web view.

**See more with less scrolling**, with the use of tables for the properties of any elements you may be interested in getting information about.

<p align="center">
	<img src="../../res/whats_new/WhatsNew_1.png" />
</p>

**Print beautiful information and read more at once**. The printing functionalities now print the contents of the Web view, allowing you to have the same output as the HTML page:

<p align="center">
	<img src="../../res/whats_new/WhatsNew_2.png" />
</p>

**View the Markdown source**. If you prefer to look at what forms the Markdown report, you can switch to the source view by clicking "Display content in Web view"

[Learn how to make the most of image information reports](../../img_tasks/info/infodlgs/#saving-image-information)

## Get information about the features and capabilities you want

DISMTools 0.6 lets you get information about a set of features and capabilities filtered by their state. For example, to get Client features that are enabled, type `Client state:enabled`. To get the features that are disabled, type `state:disabled` in your search query.

<p align="center">
	<img src="../../../res/img_tasks/info/feat_info_state_filter.gif" />
</p>

[Learn more](../../img_tasks/info/infodlgs/#searching-through-this-information)

## Manage image registry hives more easily

DISMTools 0.6 introduces an easy-to-use control panel for the registry hives of the image or offline installation you are managing. You can use this control panel to load one or more hives from our default set (`SOFTWARE`, `SYSTEM`, `DEFAULT` and `NTUSER.DAT`), or any other hive in the image. When you close this control panel, all loaded hives will be automatically unloaded for you, so you don't have to unload them manually.

<p align="center">
	<img src="../../res/whats_new/WhatsNew_3.png" />
</p>

[Learn more](../../img_tasks/tools/regcpl)

## Improved unattended answer file features

The unattended answer file features have seen slight improvements as well. Now, you can configure placeholders for additional components automatically, without having to resort to manual additions of such components to the passes of your unattended answer files. And, after creating the answer file, you can quickly begin editing it further on both the Editor mode and the Windows System Image Manager (SIM), which is part of the Assessment and Deployment Kit.

There are some minor improvements to the overall features too.

## Overall refinements

This release also focuses on refining existing tasks and functionality to improve the user experience. For example, more items have received translations, the program is more reliable, and components have been updated to their latest versions.

<!-- Room for more features -->

# Thanks to the contributors

The following people have helped shape this version of DISMTools by reporting issues or suggesting new features or changes:

- [David Retzloff](https://forums.mydigitallife.net/members/david-retzloff.1567430/) for spotting issues with the unattended answer file features,
- [Procstas](https://github.com/Procstas) for spotting issues with some actions of the project tree view,
- [l33m4n](https://github.com/l33m4n) for spotting issues with the configuration of some settings, and
- [bovirus](https://github.com/bovirus) for spotting and fixing issues with the installer

<!-- The third one is temporary depending on whether or not the issues had been fixed by the time of the release of 0.6 -->

If you want to appear in this list, you can report issues or suggestions in any channel you prefer (via the [MDL forum thread](https://forums.mydigitallife.net/threads/dismtools.87263/), via the [GitHub repository](https://github.com/CodingWonders/DISMTools), or via any announcements on the [DISMTools subreddit](https://reddit.com/r/DISMTools) or on the [Windows](https://reddit.com/r/Windows), [Windows11](https://reddit.com/r/Windows11) and [Windows10](https://reddit.com/r/Windows10) subreddits (as comments)) or submit new code changes (read the [contribution guidelines](https://github.com/CodingWonders/DISMTools/blob/stable/CONTRIBUTING.md) for more information).