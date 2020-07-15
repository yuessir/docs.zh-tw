---
title: Azure Tools For Visual Studio 2015
description: 取得工具，開始從 Visual Studio 2015 使用 Azure .NET 程式庫。
ms.date: 06/19/2020
ms.custom: azure-sdk-dotnet
ms.openlocfilehash: 72229ce0c0276912ddc5658e34f4572a7948a4e6
ms.sourcegitcommit: cb27c01a8b0b4630148374638aff4e2221f90b22
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/09/2020
ms.locfileid: "86174905"
---
# <a name="azure-tools-for-visual-studio-2015"></a><span data-ttu-id="dc114-103">Azure Tools For Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="dc114-103">Azure tools for Visual Studio 2015</span></span>

<span data-ttu-id="dc114-104">要安裝 **Azure SDK for Visual Studio 2015** 和 **Service Fabric SDK and Tools for Visual Studio 2015** 最快速且輕鬆的方式，是使用 [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)。</span><span class="sxs-lookup"><span data-stu-id="dc114-104">The quickest and easiest way to install the **Azure SDK for Visual Studio 2015** and **Service Fabric SDK and Tools for Visual Studio 2015** is using the [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).</span></span> <span data-ttu-id="dc114-105">Microsoft Web Platform Installer 是免費的工具，可簡化下載、安裝和更新一些 Microsoft Web Platform 的元件，包括 Azure tools for Visual Studio 2015。</span><span class="sxs-lookup"><span data-stu-id="dc114-105">The Microsoft Web Platform Installer is a free tool that streamlines downloading, installing, and updating some of the components of the Microsoft Web Platform, including Azure tools for Visual Studio 2015.</span></span> <span data-ttu-id="dc114-106">也可從 [Azure 下載頁面](https://azure.microsoft.com/downloads/)下載這些 SDK，並安裝作為個別的元件。</span><span class="sxs-lookup"><span data-stu-id="dc114-106">These SDKs can also be downloaded and installed as individual components from the [Azure Downloads page](https://azure.microsoft.com/downloads/).</span></span>

## <a name="using-the-web-platform-installer"></a><span data-ttu-id="dc114-107">使用 Web Platform Installer</span><span class="sxs-lookup"><span data-stu-id="dc114-107">Using the Web Platform Installer</span></span>

1. <span data-ttu-id="dc114-108">下載及執行此 [Web Platform Installer 啟動載入器](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=VWDOrVs2015AzurePack;MicrosoftAzure-ServiceFabric-VS2015)。</span><span class="sxs-lookup"><span data-stu-id="dc114-108">Download and run this [Web Platform Installer bootstrapper](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=VWDOrVs2015AzurePack;MicrosoftAzure-ServiceFabric-VS2015).</span></span>

2. <span data-ttu-id="dc114-109">啟動載入器將會安裝 Web Platform Installer (如有需要)，並自動將最新版的 **Azure SDK for Visual Studio 2015** 和 **Service Fabric SDK and Tools for Visual Studio 2015** 項目放入 [要安裝的項目]\*\* 清單。</span><span class="sxs-lookup"><span data-stu-id="dc114-109">The bootstrapper will install Web Platform Installer (if needed) and automatically put the latest versions of the  **Azure SDK for Visual Studio 2015** and **Service Fabric SDK and Tools for Visual Studio 2015** items in your *Items to be installed* list.</span></span> <span data-ttu-id="dc114-110">按一下 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="dc114-110">Click **Install**.</span></span>

    ![Web Platform Installer](media/vs2015-install/webpi.png)

3. <span data-ttu-id="dc114-112">在下一個畫面上，按一下 [我接受]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="dc114-112">On the next screen, click **I Accept**.</span></span> <span data-ttu-id="dc114-113">Web PI 就會開始下載及安裝您選取的元件。</span><span class="sxs-lookup"><span data-stu-id="dc114-113">Web PI will begin downloading and installing the components you selected.</span></span>

4. <span data-ttu-id="dc114-114">安裝完成之後，會顯示確認畫面。</span><span class="sxs-lookup"><span data-stu-id="dc114-114">After the installation is finished, it will display a confirmation screen.</span></span> <span data-ttu-id="dc114-115">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="dc114-115">Click **Finish**.</span></span> <span data-ttu-id="dc114-116">您現在可以關閉 Web Platform Installer。</span><span class="sxs-lookup"><span data-stu-id="dc114-116">You can now close Web Platform Installer.</span></span>

## <a name="verifying-the-installation"></a><span data-ttu-id="dc114-117">驗證安裝</span><span class="sxs-lookup"><span data-stu-id="dc114-117">Verifying the installation</span></span>

1. <span data-ttu-id="dc114-118">在 Visual Studio 2015 中，按一下 [工具]\*\*\*\* 功能表，然後按一下 [擴充功能和更新...]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="dc114-118">In Visual Studio 2015, click the **Tools** menu, and then click **Extensions and Updates...**.</span></span>

2. <span data-ttu-id="dc114-119">顯示的清單會包含數個 Azure 工具，例如 **Microsoft Azure App Service 工具**、**已連線 Microsoft Azure 儲存體的服務**，和 **Service Fabric 工具**。</span><span class="sxs-lookup"><span data-stu-id="dc114-119">The displayed list will contain several Azure tools, such as **Microsoft Azure App Service Tools**, **Microsoft Azure Storage Connected Service**, and **Service Fabric Tools**.</span></span>

    ![擴充功能和更新](media/vs2015-install/ext-tools.png)