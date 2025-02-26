---
title: Import or export installation configurations
titleSuffix: ''
description: Learn how to export your installation configuration to a .vsconfig file to share with others, and how to import it to clone.
ms.date: 11/28/2023
ms.topic: how-to
helpviewer_keywords:
- import installation configuration
- export installation configuration
- install Visual Studio
- Visual Studio installer
author: anandmeg
ms.author: meghaanand
manager: jmartens

ms.subservice: installation
---
# Import or export installation configurations

You can use installation configuration files to configure Visual Studio. To do so, export the workloads and components information to a [.vsconfig file](#vsconfig-file-format) by using the Visual Studio Installer. You can then import the configuration into new or existing installations, use them to create or modify a layout or an offline installation, and share them with others.

> Starting with Visual Studio 2022 version 17.9 Preview 1, you can now include some extensions in a *.vsconfig file, and then use the Visual Studio Installer to import them into Visual Studio. Further details about this functionality are described in the [Extensions Preview](#extensions) section below.

## Export a configuration

You can export an installation configuration file from a previously installed instance of Visual Studio. 

### Use the Visual Studio Installer UI

1. Open the Visual Studio Installer.

1. On the product card, choose the **More** button, and then select **Export configuration**.

   ![Export configuration from the product card in the Visual Studio installer](../install/media/vs-2022/export-config.png)

1. Browse to or type the location where you want to save your .vsconfig file, and then choose **Review details**.

   ![Export configuration from the Visual Studio installer](../install/media/vs-2022/review-details-1.png)

1. Make sure you've got the workloads and components that you want, and then choose **Export**.

   ::: moniker range="vs-2022"

      :::image type="content" source="../install/media/vs-2022/export-configuration-confirmation-1.png" alt-text="Screenshot of the Export Window.":::

   ::: moniker-end

### Export a configuration file programmatically

You can export a configuration programmatically by using the `export` verb as described in the [Install Visual Studio from the command line](use-command-line-parameters-to-install-visual-studio.md) documentation.

## Import a configuration

Similar to exporting a configuration, you can also import an installation configuration file into either a previously installed instance of Visual Studio, or use it to initialize a new installation of Visual Studio.  

### Use the Visual Studio Installer UI

When you're ready to import an installation configuration file, follow these steps.

1. Open the Visual Studio Installer.

1.  On either the **Installed** tab or the **Available** tab, select **More** > **Import configuration** on the product card.

1. Locate the .vsconfig file that you want to import, and then choose **Review details**.

1. Make sure you've got the workloads and components that you want, and then choose **Close**.

### Programmatically use a configuration file to add components to an existing installation
 
Use `--config` to either initialize or modify an existing installation to add or remove components. The example below uses the installer already on the client machine to modify an existing installation.

```shell
"C:\Program Files (x86)\Microsoft Visual Studio\Installer\setup.exe" modify --installPath "C:\VS" --config "C:\myconfig.vsconfig"
```

> [!NOTE]
> To add or remove components to an existing installation by using a config file (_*.vsconfig_), you'll need to **modify** your installed product and not update. **Update** just updates the components to the latest version; it doesn't add or remove new ones. To learn more, see [Install Visual Studio from the command line](use-command-line-parameters-to-install-visual-studio.md).

## Use a configuration file to initialize the contents of a layout

Using the correct bootstrapper that corresponds to the version and edition of Visual Studio that you want, open an administrator command prompt and run the following command to use `--config` to configure the contents of a layout:

```shell
vs_enterprise.exe --layout c:\localVSlayout --config c:\myconfig.vsconfig --lang en-US 
```

## Automatically install missing components

Save a .vsconfig file to your solution root directory and then open a solution. Visual Studio automatically detects the missing components and prompts you to install them.

![Solution Explorer suggests additional components](../install/media/vs-2019/solution-explorer-config-file.png)

You can also generate a .vsconfig file right from Solution Explorer.

1. Right-click on your solution file.

1. Choose **Add** > **Installation Configuration File**.

1. Confirm the location where you want to save the .vsconfig file, and then choose **Review details**.

1. Make sure you've got the workloads and components that you want, and then choose **Export**.

We also created an open source utility that locates Visual Studio installation *.vsconfig files downstream recursively and merges them all together. You can find [more information about the VSConfigFinder tool here](https://github.com/microsoft/VSConfigFinder).

## vsconfig file format

The .vsconfig file is a json file format that contains a components section that contains [workloads and components](workload-and-component-ids.md).

```shell
{
  "version": "1.0", 
  "components": [ 
    "Microsoft.VisualStudio.Component.CoreEditor", 
    "Microsoft.VisualStudio.Workload.CoreEditor", 
    "Microsoft.VisualStudio.Component.NuGet" 
    ] 
}
```

### Extensions
[!INCLUDE [Preview](~/includes/preview.md)]

Starting in [November 2023 with the previews, Visual Studio 2022 version 17.9](https://devblogs.microsoft.com/visualstudio/introducing-visual-studio-17-9-preview-1-is-here/#extensibility) now allows you to specify public marketplace or local private extensions in the *.vsconfig file and use the Visual Studio Installer to load them machine wide, meaning that they are available for all users. Because these extensions are installed machine wide, whoever installs them must have admin privileges directly, or they must have been granted control via the [AllowStandardUserControl](https://aka.ms/vs/setup/policies) policy. Note that any extensions previously installed by the Visual Studio Extension Manager had the capability of being (and were typically) installed per user, not machine wide, and the user didn't need to have admin perms. 

_**For now**_, the Visual Studio Installer only supports importing certain types of extensions. As such, the following behaviors are not currently supported and are on our backlog product roadmap; your [feedback](https://developercommunity.visualstudio.com) will help us prioritize properly.  
 * The ability to use the Visual Studio Installer to export extensions is not currently available.    
 * Updating extensions will, for the time being, continue to be handled via the [legacy method](/visualstudio/ide/finding-and-using-visual-studio-extensions#automatic-extension-updates), not via the Visual Studio Installer.
 * The ability to load extensions via the *.vsconfig file currently only applies to Visual Studio 2022.
 * Only extensions contained in a *.vsix package and that don't contain any embedded extensions or other complicating factors can be installed via the *.vsconfig file.
 * You can only load public marketplace extensions, not local private extensions, via automatic detection and parsing of the *.vsconfig file in the solution directory.
 * You can use the new `--allowUnsignedExtensions` parameter to programmatically allow unsigned extensions to be loaded. This can also be included in the *response.json* if installing from a layout. Use the "allowUnsignedExtensions" : true syntax as described in the [Example customized layout response file content](/visualstudio/install/automated-installation-with-response-file#example-customized-layout-response-file-content) documentation

The .vsconfig file format that includes extensions should look like this.

```shell
{
  "version": "1.0", 
  "components": [ 
    // Whatever components you want to install come here, in quotes, separated by commas.
    // You can use the installer to select the components you want to install and then export them,
    // Or you can specify the ones you want according to the [component-id's](https://learn.microsoft.com/en-us/visualstudio/install/workload-and-component-ids).
    // This array should not be null! If you don't want to install any component, just leave the array empty.
  ],
  "extensions": [
    // The extensions you want to install are specified in this section, in quotes, separated by commas.
    // Extensions are optional in .vsconfig, so if you don't want any, you can delete the entire extensions section.
    // The extensions must be in a *.vsix package
    // Make sure that the extensions you specify are designed to work with that version of Visual Studio.
    // example syntax:
    "https://marketplace.visualstudio.com/items?itemName=MadsKristensen.ImageOptimizer64bit",
    "c:\\mylocaldrive\\someextension.vsix",
    "\\\\server\\share\\myextension.vsix",
    "https://myweb/anotherextension.vsix"
  ]
}
```

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## Related content

* [Configure Visual Studio across your organization with .vsconfig April 2019 blog post](https://devblogs.microsoft.com/setup/configure-visual-studio-across-your-organization-with-vsconfig/)
* [Create a network installation of Visual Studio](create-a-network-installation-of-visual-studio.md)
* [Update a networked-based installation of Visual Studio](update-a-network-installation-of-visual-studio.md)
* [Control updates to Visual Studio deployments](controlling-updates-to-visual-studio-deployments.md)
* [Configure policies for enterprise deployments](configure-policies-for-enterprise-deployments.md)
