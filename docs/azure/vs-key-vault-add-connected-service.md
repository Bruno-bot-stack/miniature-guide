---
title: Add Key Vault support to your ASP.NET project using Visual Studio
titleSuffix: ""
description: Use this tutorial to help you learn how to add Key Vault support to an ASP.NET or ASP.NET Core web application.
author: ghogen
manager: mijacobs
ms.custom: devx-track-csharp
ms.topic: how-to
ms.date: 04/10/2024
ms.author: ghogen
---

# Add Key Vault to your web application by using Visual Studio Connected Services

In this tutorial, you will learn how to easily add everything you need to start using Azure Key Vault to manage your secrets for web projects in Visual Studio, whether you are using ASP.NET Core or any type of ASP.NET project. By using the Connected Services feature in Visual Studio, you can have Visual Studio automatically add all the NuGet packages and configuration settings you need to connect to Key Vault in Azure.

For details on the changes that Connected Services makes in your project to enable Key Vault, see [Key Vault Connected Service - What happened to my ASP.NET project](#how-your-aspnet-framework-project-is-modified) or [Key Vault Connected Service - What happened to my ASP.NET Core project](#how-your-aspnet-core-project-is-modified).

## Prerequisites

- [!INCLUDE [prerequisites-azure-subscription](includes/prerequisites-azure-subscription.md)]
- **Visual Studio 2019 version 16.3** or later [Download it now](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs).

## Add Key Vault support to your project

Before you begin, make sure that you're signed in to Visual Studio. Sign in with the same account that you use for your Azure subscription. Then open an ASP.NET 4.7.1 or later, or ASP.NET Core web project, and do the following steps. The steps shown are for Visual Studio 2022 version 17.4. The flow might be slightly different for other versions of Visual Studio.

1. In **Solution Explorer**, right-click the project that you want to add the Key Vault support to, and choose **Add** > **Connected Service**. Under **Service Dependencies**, choose the **+** icon.
   The Connected Service page appears with services you can add to your project.
1. In the menu of available services, choose **Azure Key Vault** and click **Next**.

   ![Choose "Azure Key Vault"](./media/vs-key-vault-add-connected-service/key-vault-connected-service.png)

1. Select the subscription you want to use, and then if you already have a key vault you want to use, select it and click **Next**.

   ![Screenshot Select your subscription](./media/vs-key-vault-add-connected-service/key-vault-connected-service-select-vault.png)

1. If you don't have an existing Key Vault, click on **Create new Key Vault**. You'll be asked to provide the resource group, location, and SKU.

   ![Screenshot of "Create Azure Key Vault" screen](./media/vs-key-vault-add-connected-service/create-new-key-vault.png)

1. In the **Configure Key Vault** screen, you can change the name of the environment variable that references the key vault URI. The connection string is not stored here; it's stored in the key vault.

   ![Screenshot of Connect to Azure Key Vault screen.](./media/vs-key-vault-add-connected-service/connect-to-azure-key-vault.png)

1. Click **Next** to review a summary of the changes and then **Finish**.

Now, connection to Key Vault is established and you can access your secrets in code. If you just created a new key vault, test it by creating a secret that you can reference in code. You can create a secret by using the [Azure portal](/azure/key-vault/secrets/quick-create-portal), [PowerShell](/azure/key-vault/secrets/quick-create-powershell), or the [Azure CLI](/azure/key-vault/secrets/quick-create-cli).

See code examples of working with secrets at [Azure Key Vault Secrets client library for .NET - Code examples](/azure/key-vault/secrets/quick-create-net?tabs=azure-cli#code-examples).

## Configure access to the key vault

If your key vault is running on a different Microsoft account than the one you're signed in to Visual Studio (for example, the key vault is running on your work account, but Visual Studio is using your private account) you get an error in your Program.cs file, that Visual Studio can't get access to the key vault. To fix this issue, go to the [Azure portal](https://portal.azure.com), open your key vault, and choose **Access control (IAM)** to set permissions. See [Provide access to Key Vault keys, certificates, and secrets with an Azure role-based access control](/azure/key-vault/general/rbac-guide?tabs=azure-cli).

> [!NOTE]
> Older key vaults might use a legacy access policy model. It is recommended to migrate older key vaults to use Azure RBAC. See [Azure role-based access control (RBAC) vs. access policies](/azure/key-vault/general/rbac-access-policy).

## How your ASP.NET Core project is modified

This section identifies the exact changes made to an ASP.NET project when adding the key vault connected service using Visual Studio.

### Added references for ASP.NET Core

Affects the project file .NET references and NuGet package references.

| Type | Reference |
| --- | --- |
| NuGet | Microsoft.AspNetCore.AzureKeyVault.HostingStartup |

### Added files for ASP.NET Core

- `ConnectedService.json` added, which records some information about the Connected Service provider, version, and a link the documentation.

### Project file changes for ASP.NET Core

- Added the Connected Services ItemGroup and `ConnectedServices.json` file.

### launchsettings.json changes for ASP.NET Core

- Added the following environment variable entries to both the IIS Express profile and the profile that matches your web project name:

    ```json
      "environmentVariables": {
        "ASPNETCORE_HOSTINGSTARTUP__KEYVAULT__CONFIGURATIONENABLED": "true",
        "ASPNETCORE_HOSTINGSTARTUP__KEYVAULT__CONFIGURATIONVAULT": "<your keyvault URL>"
      }
    ```

### Changes on Azure for ASP.NET Core

- Created a resource group (or used an existing one).
- Created a key vault in the specified resource group.

## How your ASP.NET Framework project is modified

This section identifies the exact changes made to an ASP.NET project when adding the key vault connected service using Visual Studio.

### Added references for ASP.NET Framework

Affects the project file .NET references and `packages.config` (NuGet references).

| Type | Reference |
| --- | --- |
| .NET; NuGet | Azure.Identity |
| .NET; NuGet | Azure.Security.KeyVault.Keys |
| .NET; NuGet | Azure.Security.key vault.Secrets |

> [!IMPORTANT]
> By default Azure.Identity 1.1.1 is installed, which does not support Visual Studio Credential. You can update package reference manually to 1.2+ use Visual Studio Credential.

### Added files for ASP.NET Framework

- `ConnectedService.json` added, which records some information about the Connected Service provider, version, and a link to the documentation.

### Project file changes for ASP.NET Framework

- Added the Connected Services ItemGroup and ConnectedServices.json file.
- References to the .NET assemblies described in the [Added references](#added-references-for-aspnet-framework) section.

## Next steps

If you followed this tutorial, your Key Vault permissions are set up to run with your own Azure subscription, but that might not be desirable for a production scenario. You can create a managed identity to manage Key Vault access for your app. See [How to Authenticate to Key Vault](/azure/key-vault/general/authentication) and [Assign a Key Vault access policy](/azure/key-vault/general/assign-access-policy-portal).

Learn more about Key Vault development by reading the [Key Vault Developer's Guide](/azure/key-vault/general/developers-guide).

If your goal is to store configuration for an ASP.NET Core app in an Azure key vault, see [Azure Key Vault configuration provider in ASP.NET Core](/aspnet/core/security/key-vault-configuration).
