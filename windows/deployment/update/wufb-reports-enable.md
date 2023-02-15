---
title: Enable Windows Update for Business reports
manager: aaroncz
description: How to enable Windows Update for Business reports through the Azure portal
ms.prod: windows-client
author: mestew
ms.author: mstewart
ms.topic: article
ms.date: 11/15/2022
ms.technology: itpro-updates
---

# Enable Windows Update for Business reports
<!--37063317, 30141258, 37063041-->
***(Applies to: Windows 11 & Windows 10)***

After verifying the [prerequisites](wufb-reports-prerequisites.md) are met, you can start to set up Windows Update for Business reports. The two main steps for setting up  Windows Update for Business reports are:

1. [Add Windows Update for Business reports](#bkmk_add) to your Azure subscription. This step has the following phases:
   1. [Select or create a new Log Analytics workspace](#bkmk_workspace) for use with Windows Update for Business reports.
   1. Enroll into Windows Update for Business reports using one of the following methods:
      - Enroll through the [Azure Workbook](#bkmk_enroll) (preferred method)
      - Enroll from the [Microsoft 365 admin center](#bkmk_admin-center).

1. Configure the clients to send data to Windows Update for Business reports. You can configure clients in the following three ways:
    - Use a [script](wufb-reports-configuration-script.md)
    - Use [Microsoft Intune](wufb-reports-configuration-intune.md)
    - Configure [manually](wufb-reports-configuration-manual.md)

> [!IMPORTANT]
> Windows Update for Business reports is a Windows service hosted in Azure that uses Windows diagnostic data. You should be aware that Windows Update for Business reports doesn't meet [US Government community compliance (GCC)](/office365/servicedescriptions/office-365-platform-service-description/office-365-us-government/gcc#us-government-community-compliance) requirements. For a list of GCC offerings for Microsoft products and services, see the [Microsoft Trust Center](/compliance/regulatory/offering-home). Windows Update for Business reports is available in the Azure Commercial cloud, but not available for GCC High or United States Department of Defense customers.

## <a name="bkmk_add"></a> Add Windows Update for Business reports to your Azure subscription

Before you configure clients to send data, you'll need to add Windows Update for Business reports to your Azure subscription so the data can be received. First, you'll select or create a new Log Analytics workspace to use. Second, you'll enroll Windows Update for Business reports to the workspace.

## <a name="bkmk_workspace"></a> Select or create a new Log Analytics workspace for Windows Update for Business reports

Windows Update for Business reports uses an [Azure Log Analytics workspaces](/azure/azure-monitor/logs/log-analytics-overview) that you own for storing the client diagnostic data. Identify an existing workspace or create a new one using the following steps:

1. Sign in to the Azure portal at [https://portal.azure.com](https://portal.azure.com).
   - Although an Azure subscription is required, you won't be charged for ingestion of Windows Update for Business reports data.
1. In the Azure portal, type **Log Analytics** in the search bar. As you begin typing, the list filters based on your input.
1. Select **Log Analytics workspaces**.
1. If you already have a Log Analytics workspace, determine which Log Analytics workspace you'd like to use for Windows Update for Business reports. Ensure the workspace is in a **Compatible Log Analytics region** from the table listed in the [prerequisites](wufb-reports-prerequisites.md#log-analytics-regions).
   - [Azure Update Management](/azure/automation/automation-intro#update-management) users should use the same workspace for Windows Update for Business reports.
1. If you don't have an existing Log Analytics workspace or you don't want to use a current workspace, [create a new workspace](/azure/azure-monitor/logs/quick-create-workspace) in a [compatible region](wufb-reports-prerequisites.md#log-analytics-regions).

> [!Note]
> - You can only map one tenant to one Log Analytics workspace. Mapping one tenant to multiple workspaces isn't supported.
> - If you change the Log Analytics workspace for Windows Update for Business reports, stale data will be displayed for about 24 hours until the new workspace is fully onboarded. You will also need to reconfigure the Windows Update for Business reports settings to enroll again.

## <a name="bkmk_enroll"></a> Enroll into Windows Update for Business reports

Enroll into Windows Update for Business reports by configuring its settings through either the Azure Workbook or from the Microsoft 365 admin center. Completing the Windows Update for Business reports configuration removes needing to specify [`CommercialID`](update-compliance-get-started.md#get-your-commercialid), which was needed by Update Compliance, the predecessor of Windows Update for Business reports.

Use one of the following methods to enroll into Windows Update for Business reports:

##### <a name="bkmk_enroll-workbook"></a> Enroll through the Azure Workbook (recommended method)

1. In the [Azure portal](https://portal.azure.com), select **Monitor** > **Workbooks** from the menu bar.
   - You can also type **Monitor** in the search bar. As you begin typing, the list filters based on your input.

1. When the gallery opens, select the **Windows Update for Business reports** workbook. If needed, you can filter workbooks by name in the gallery.
1. Select the **Get started** button when prompted by the workbook to open the **Windows Update for Business reports enrollment** flyout.
1. In the flyout, specify which **Subscription** and **Azure Log Analytics Workspace** you want to use for Windows Update for Business reports.
   - If you need to create a new Log Analytics workspace, select **Create new workspace** and follow the prompts to [create a new workspace](#bkmk_workspace).
1. Select **Save settings** to save the settings and enroll into Windows Update for Business reports.
   > [!Tip]
   > If a `403 Forbidden` error occurs, verify the account you're using has [permissions](wufb-reports-prerequisites.md#permissions) to enroll into Windows Update for Business reports.
1. The initial setup can take up to 24 hours. During this time, the workbook will display that it's **Waiting for Windows Update for Business reports data**.

##### <a name="bkmk_admin-center"></a> Enroll through the Microsoft 365 admin center
<!--Using include for onboarding Windows Update for Business reports through the Microsoft 365 admin center-->
[!INCLUDE [Onboarding Windows Update for Business reports through the Microsoft 365 admin center](./includes/wufb-reports-onboard-admin-center.md)]

## Next steps

Once you've added Windows Update for Business reports to a workspace in your Azure subscription and configured the settings through the Microsoft 365 admin center, you'll need to configure any devices you want to monitor. Enroll devices into Windows Update for Business reports using any of the following methods:

- [Configure clients with a script](wufb-reports-configuration-script.md)
- [Configure clients manually](wufb-reports-configuration-manual.md)
- [Configure clients with Microsoft Intune](wufb-reports-configuration-intune.md)