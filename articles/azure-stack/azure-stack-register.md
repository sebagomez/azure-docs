---
title: Register Azure Stack | Microsoft Docs
description: Register Azure Stack with your Azure subscription.
services: azure-stack
documentationcenter: ''
author: ErikjeMS
manager: byronr
editor: ''

ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: erikje

---
# Register Azure Stack with your Azure Subscription

For Azure Active Directory deployments, you can register Azure Stack with Azure to download marketplace items from Azure and to set up commerce data reporting back to Microsoft. 

> [!NOTE]
>Registration is recommended because it enables you to test important Azure Stack functionality, like marketplace syndication and usage reporting. After you register Azure Stack, usage is reported to Azure commerce. You can see it under the subscription you used for registration. Azure Stack Development Kit users will not be charged for any usage they report.
>


## Get Azure subscription

Before registering Azure Stack with Azure, you must have:

- The subscription ID for an Azure subscription. To get the ID, sign in to Azure, click **More services** > **Subscriptions**, click the subscription you want to use, and under **Essentials** you can find the **Subscription ID**. China, Germany, and US government cloud subscriptions are not currently supported.
- The username and password for an account that is an owner for the subscription (MSA/2FA accounts are supported)
- The AAD directory for the Azure subscription. You can find this directory in Azure by hovering over your avatar at the top right corner of the Azure portal. 
- Registered the AzureStack resource provider (see the **Register** section below for details)

If you don’t have an Azure subscription that meets these requirements, you can [create a free Azure account here](https://azure.microsoft.com/en-us/free/?b=17.06). Registering Azure Stack incurs no cost on your Azure subscription.




## Register

> [!NOTE]
>All these steps must be completed on the host computer, not the console computer.
>

1. Sign in to the Azure Stack Development Kit host administrator portal (https://adminportal.local.azurestack.external).
2. [Install PowerShell for Azure Stack](azure-stack-powershell-install.md). 
3. Copy the [RegisterWithAzure.ps1 script](https://go.microsoft.com/fwlink/?linkid=842959) to a folder (such as C:\Temp).
4. Start PowerShell ISE as an administrator.
5. Ensure the Azure Stack resource provider has been registered 

    ```powershell
    Get-AzureRmResourceProvider -ProviderNamespace 'Microsoft.AzureStack'
    ```
    
    If you have not registered with the azurestack resource provider you can do so by running the following:
    
    ```powershell
    Register-AzureRmResourceProvider -ProviderNamespace 'Microsoft.AzureStack'
    ```
    
6. Run the RegisterWithAzure.ps1 script, replacing the following placeholders:
    - *YourAccountName* is the owner of the Azure subscription
    - *YourID* is the Azure subscription ID that you want to use to register Azure Stack
    - *YourDirectory* is the name of your Azure Active Directory tenant that your Azure subscription is a part of.

    ```powershell
    RegisterWithAzure.ps1 -azureSubscriptionId YourID -azureDirectoryTenantName YourDirectory -azureAccountId YourAccountName
    ```
    
    For example:
    
    ```powershell
    C:\temp\RegisterWithAzure.ps1 -azureSubscriptionId "5e0ae55d-0b7a-47a3-afbc-8b372650abd3" `
    -azureDirectoryTenantName "contoso.onmicrosoft.com" `
    -azureAccountId serviceadmin@contoso.onmicrosoft.com
    ```
    
7. At the two prompts, press Enter.
8. In the pop-up login window, enter your Azure subscription credentials

## Verify the registration

1. Sign in to the administrator portal (https://adminportal.local.azurestack.external).
2. Click **More Services** > **Marketplace Management** > **Add from Azure**.
3. If you see a list of items available from Azure (such as WordPress), your activation was successful.

## Next steps

[Connect to Azure Stack](azure-stack-connect-azure-stack.md)

