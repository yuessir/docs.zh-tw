---
title: 使用 ASP.NET Core 和 Azure 架構現代化 Web 應用程式
description: 本指南會提供使用 ASP.NET Core 和 Azure 建置整合型 Web 應用程式的端對端指引。
author: ardalis
ms.author: wiwagn
ms.date: 01/30/2019
ms.openlocfilehash: 739dd607aaa45f73e777a30c6495e329236fee17
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/30/2019
ms.locfileid: "70296289"
---
# <a name="architect-modern-web-applications-with-aspnet-core-and-azure"></a><span data-ttu-id="5afe5-103">使用 ASP.NET Core 和 Azure 架構現代化 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="5afe5-103">Architect Modern Web Applications with ASP.NET Core and Azure</span></span>

![《Architect Modern Web Applications》(設計現代化 Web 應用程式架構) 指南的封面影像。](./media/index/web-application-guide-cover-image.png)

<span data-ttu-id="5afe5-105">發行者</span><span class="sxs-lookup"><span data-stu-id="5afe5-105">PUBLISHED BY</span></span>

<span data-ttu-id="5afe5-106">Microsoft 開發人員部門 .NET 和 Visual Studio 產品小組</span><span class="sxs-lookup"><span data-stu-id="5afe5-106">Microsoft Developer Division, .NET, and Visual Studio product teams</span></span>

<span data-ttu-id="5afe5-107">Microsoft Corporation 部門</span><span class="sxs-lookup"><span data-stu-id="5afe5-107">A division of Microsoft Corporation</span></span>

<span data-ttu-id="5afe5-108">One Microsoft Way</span><span class="sxs-lookup"><span data-stu-id="5afe5-108">One Microsoft Way</span></span>

<span data-ttu-id="5afe5-109">Redmond, Washington 98052-6399</span><span class="sxs-lookup"><span data-stu-id="5afe5-109">Redmond, Washington 98052-6399</span></span>

<span data-ttu-id="5afe5-110">Copyright © 2019 by Microsoft Corporation</span><span class="sxs-lookup"><span data-stu-id="5afe5-110">Copyright © 2019 by Microsoft Corporation</span></span>

<span data-ttu-id="5afe5-111">著作權所有，並保留一切權利。</span><span class="sxs-lookup"><span data-stu-id="5afe5-111">All rights reserved.</span></span> <span data-ttu-id="5afe5-112">本書內容的任何部分在未經過發行者書面許可下，不得以任何形式或透過任何方式進行重製或傳送。</span><span class="sxs-lookup"><span data-stu-id="5afe5-112">No part of the contents of this book may be reproduced or transmitted in any form or by any means without the written permission of the publisher.</span></span>

<span data-ttu-id="5afe5-113">本書是以「現況」提供，代表作者的觀點和意見。</span><span class="sxs-lookup"><span data-stu-id="5afe5-113">This book is provided “as-is” and expresses the author’s views and opinions.</span></span> <span data-ttu-id="5afe5-114">本書中所述之觀點、意見與資訊 (包括 URL 及其他網際網路網站參考) 可能會隨時變更，恕不另行通知。</span><span class="sxs-lookup"><span data-stu-id="5afe5-114">The views, opinions and information expressed in this book, including URL and other Internet website references, may change without notice.</span></span>

<span data-ttu-id="5afe5-115">此處所描述的一些範例僅供說明，純屬虛構。</span><span class="sxs-lookup"><span data-stu-id="5afe5-115">Some examples depicted herein are provided for illustration only and are fictitious.</span></span> <span data-ttu-id="5afe5-116">任何實際關聯或連結純屬巧合。</span><span class="sxs-lookup"><span data-stu-id="5afe5-116">No real association or connection is intended or should be inferred.</span></span>

<span data-ttu-id="5afe5-117">Microsoft 與列於 https://www.microsoft.com 「商標」網頁的商標是 Microsoft 集團的商標。</span><span class="sxs-lookup"><span data-stu-id="5afe5-117">Microsoft and the trademarks listed at https://www.microsoft.com on the “Trademarks” webpage are trademarks of the Microsoft group of companies.</span></span>

<span data-ttu-id="5afe5-118">Mac 與 macOS 是 Apple Inc. 的商標。</span><span class="sxs-lookup"><span data-stu-id="5afe5-118">Mac and macOS are trademarks of Apple Inc.</span></span>

<span data-ttu-id="5afe5-119">Docker 鯨魚標誌是 Docker, Inc. 的註冊商標。使用需要許可。</span><span class="sxs-lookup"><span data-stu-id="5afe5-119">The Docker whale logo is a registered trademark of Docker, Inc. Used by permission.</span></span>

<span data-ttu-id="5afe5-120">所有其他商標和標誌屬於其各自擁有者的財產。</span><span class="sxs-lookup"><span data-stu-id="5afe5-120">All other marks and logos are property of their respective owners.</span></span>

<span data-ttu-id="5afe5-121">作者:</span><span class="sxs-lookup"><span data-stu-id="5afe5-121">Author:</span></span>

> <span data-ttu-id="5afe5-122">**Steve "ardalis" Smith** - 軟體架構設計人員和講師 - [Ardalis.com](https://ardalis.com)</span><span class="sxs-lookup"><span data-stu-id="5afe5-122">**Steve "ardalis" Smith** - Software Architect and Trainer - [Ardalis.com](https://ardalis.com)</span></span>

<span data-ttu-id="5afe5-123">編輯者：</span><span class="sxs-lookup"><span data-stu-id="5afe5-123">Editors:</span></span>

> <span data-ttu-id="5afe5-124">**Maira Wenzel**</span><span class="sxs-lookup"><span data-stu-id="5afe5-124">**Maira Wenzel**</span></span>

## <a name="introduction"></a><span data-ttu-id="5afe5-125">簡介</span><span class="sxs-lookup"><span data-stu-id="5afe5-125">Introduction</span></span>

<span data-ttu-id="5afe5-126">.NET Core 和 ASP.NET Core 提供許多優於傳統.NET 開發的優點。</span><span class="sxs-lookup"><span data-stu-id="5afe5-126">.NET Core and ASP.NET Core offer several advantages over traditional .NET development.</span></span> <span data-ttu-id="5afe5-127">如果下列部分或所有項目對應用程式成功而言十分重要，則您應該將 .NET Core 用於伺服器應用程式：</span><span class="sxs-lookup"><span data-stu-id="5afe5-127">You should use .NET Core for your server applications if some or all of the following are important to your application's success:</span></span>

- <span data-ttu-id="5afe5-128">跨平台支援。</span><span class="sxs-lookup"><span data-stu-id="5afe5-128">Cross-platform support.</span></span>

- <span data-ttu-id="5afe5-129">使用微服務。</span><span class="sxs-lookup"><span data-stu-id="5afe5-129">Use of microservices.</span></span>

- <span data-ttu-id="5afe5-130">使用 Docker 容器。</span><span class="sxs-lookup"><span data-stu-id="5afe5-130">Use of Docker containers.</span></span>

- <span data-ttu-id="5afe5-131">高效能和延展性需求。</span><span class="sxs-lookup"><span data-stu-id="5afe5-131">High performance and scalability requirements.</span></span>

- <span data-ttu-id="5afe5-132">相同伺服器上應用程式之 .NET 版本的並存版本控制。</span><span class="sxs-lookup"><span data-stu-id="5afe5-132">Side-by-side versioning of .NET versions by application on the same server.</span></span>

<span data-ttu-id="5afe5-133">傳統 .NET 應用程式可以並確實支援這些需求，但 ASP.NET Core 和 .NET Core 已最佳化可提供針對上述案例的改善支援。</span><span class="sxs-lookup"><span data-stu-id="5afe5-133">Traditional .NET applications can and do support many of these requirements, but ASP.NET Core and .NET Core have been optimized to offer improved support for the above scenarios.</span></span>

<span data-ttu-id="5afe5-134">越來越多的組織會選擇使用 Microsoft Azure 這類服務，以在雲端中裝載其 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5afe5-134">More and more organizations are choosing to host their web applications in the cloud using services like Microsoft Azure.</span></span> <span data-ttu-id="5afe5-135">如果下列對您的應用程式或組織十分重要，則您應該考慮將應用程式裝載在雲端中：</span><span class="sxs-lookup"><span data-stu-id="5afe5-135">You should consider hosting your application in the cloud if the following are important to your application or organization:</span></span>

- <span data-ttu-id="5afe5-136">降低對資料中心成本的投資 (硬體、軟體、空間、公用程式、伺服器管理等等)</span><span class="sxs-lookup"><span data-stu-id="5afe5-136">Reduced investment in data center costs (hardware, software, space, utilities, server management, etc.)</span></span>

- <span data-ttu-id="5afe5-137">彈性定價 (根據使用量付費，而閒置容量不需付費)。</span><span class="sxs-lookup"><span data-stu-id="5afe5-137">Flexible pricing (pay based on usage, not for idle capacity).</span></span>

- <span data-ttu-id="5afe5-138">可靠性極高。</span><span class="sxs-lookup"><span data-stu-id="5afe5-138">Extreme reliability.</span></span>

- <span data-ttu-id="5afe5-139">改善的應用程式行動性；輕鬆地變更您應用程式的部署位置和方式。</span><span class="sxs-lookup"><span data-stu-id="5afe5-139">Improved app mobility; easily change where and how your app is deployed.</span></span>

- <span data-ttu-id="5afe5-140">彈性容量；根據實際需求相應增加或減少。</span><span class="sxs-lookup"><span data-stu-id="5afe5-140">Flexible capacity; scale up or down based on actual needs.</span></span>

<span data-ttu-id="5afe5-141">使用 ASP.NET Core 建置 Web 應用程式 (且其裝載於 Azure) 提供許多比傳統替代項目更具競爭性的優點。</span><span class="sxs-lookup"><span data-stu-id="5afe5-141">Building web applications with ASP.NET Core, hosted in Azure, offers many competitive advantages over traditional alternatives.</span></span> <span data-ttu-id="5afe5-142">ASP.NET Core 已針對現代化 Web 應用程式開發做法和雲端裝載案例最佳化。</span><span class="sxs-lookup"><span data-stu-id="5afe5-142">ASP.NET Core is optimized for modern web application development practices and cloud hosting scenarios.</span></span> <span data-ttu-id="5afe5-143">在本指南中，您將學習如何架構 ASP.NET Core 應用程式，以善加利用這些功能。</span><span class="sxs-lookup"><span data-stu-id="5afe5-143">In this guide, you'll learn how to architect your ASP.NET Core applications to best take advantage of these capabilities.</span></span>

## <a name="purpose"></a><span data-ttu-id="5afe5-144">用途</span><span class="sxs-lookup"><span data-stu-id="5afe5-144">Purpose</span></span>

<span data-ttu-id="5afe5-145">本指南會提供使用 ASP.NET Core 和 Azure 建置整合型  Web 應用程式的端對端指引。</span><span class="sxs-lookup"><span data-stu-id="5afe5-145">This guide provides end-to-end guidance on building *monolithic* web applications using ASP.NET Core and Azure.</span></span> <span data-ttu-id="5afe5-146">此處的「整合型」是指這些應用程式會部署為單一單位，而不是互動服務和應用程式的集合。</span><span class="sxs-lookup"><span data-stu-id="5afe5-146">In this context, "monolithic" refers to the fact that these applications are deployed as a single unit, not as a collection of interacting services and applications.</span></span>

<span data-ttu-id="5afe5-147">本指南是 [" _.NET Microservices.Architecture for Containerized .NET Applications_"](../microservices/index.md) 的補充說明，該書籍著重在 Docker、微服務及部署容器以裝載企業應用程式的部分。</span><span class="sxs-lookup"><span data-stu-id="5afe5-147">This guide is complementary to the ["_.NET Microservices. Architecture for Containerized .NET Applications_"](../microservices/index.md) which focuses more on Docker, Microservices, and Deployment of Containers to host enterprise applications.</span></span>

### <a name="net-microservices-architecture-for-containerized-net-applications"></a><span data-ttu-id="5afe5-148">.NET 微服務。</span><span class="sxs-lookup"><span data-stu-id="5afe5-148">.NET Microservices.</span></span> <span data-ttu-id="5afe5-149">容器化 .NET 應用程式的架構</span><span class="sxs-lookup"><span data-stu-id="5afe5-149">Architecture for Containerized .NET Applications</span></span>

- <span data-ttu-id="5afe5-150">**電子書**</span><span class="sxs-lookup"><span data-stu-id="5afe5-150">**e-book**</span></span>  
  <https://aka.ms/MicroservicesEbook>
- <span data-ttu-id="5afe5-151">**範例應用程式**</span><span class="sxs-lookup"><span data-stu-id="5afe5-151">**Sample Application**</span></span>  
  <https://aka.ms/microservicesarchitecture>

## <a name="who-should-use-this-guide"></a><span data-ttu-id="5afe5-152">誰應該使用本指南</span><span class="sxs-lookup"><span data-stu-id="5afe5-152">Who should use this guide</span></span>

<span data-ttu-id="5afe5-153">本指南的對象主要是開發人員、開發負責人和架構設計人員，而他們對使用 Microsoft 技術和服務在雲端中建置現代化 Web 應用程式感興趣。</span><span class="sxs-lookup"><span data-stu-id="5afe5-153">The audience for this guide is mainly developers, development leads, and architects who are interested in building modern web applications using Microsoft technologies and services in the cloud.</span></span>

<span data-ttu-id="5afe5-154">次要對象是技術決策者，其已熟悉 ASP.NET 或 Azure，並尋找是否可以升級為新專案或現有專案之 ASP.NET Core 的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="5afe5-154">A secondary audience is technical decision makers who are already familiar ASP.NET or Azure and are looking for information on whether it makes sense to upgrade to ASP.NET Core for new or existing projects.</span></span>

## <a name="how-you-can-use-this-guide"></a><span data-ttu-id="5afe5-155">此指南的使用方式</span><span class="sxs-lookup"><span data-stu-id="5afe5-155">How you can use this guide</span></span>

<span data-ttu-id="5afe5-156">本指南已壓縮成相當小的文件，著重於使用現代化 .NET 技術和 Windows Azure 來建置 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5afe5-156">This guide has been condensed into a relatively small document that focuses on building web applications with modern .NET technologies and Windows Azure.</span></span> <span data-ttu-id="5afe5-157">因此，可以完整讀取它，以提供對這類應用程式和其技術考量的基礎了解。</span><span class="sxs-lookup"><span data-stu-id="5afe5-157">As such, it can be read in its entirety to provide a foundation of understanding such applications and their technical considerations.</span></span> <span data-ttu-id="5afe5-158">本指南與其範例應用程式也可以作為起點或參考。</span><span class="sxs-lookup"><span data-stu-id="5afe5-158">The guide, along with its sample application, can also serve as a starting point or reference.</span></span> <span data-ttu-id="5afe5-159">使用相關聯的範例應用程式作為您專屬應用程式的範本，或查看如何組織應用程式的元件組件。</span><span class="sxs-lookup"><span data-stu-id="5afe5-159">Use the associated sample application as a template for your own applications, or to see how you might organize your application's component parts.</span></span> <span data-ttu-id="5afe5-160">當您要為專屬應用程式權衡這些選擇時，請回頭參考指南內架構和技術選項的原則與說明還有決策考量。</span><span class="sxs-lookup"><span data-stu-id="5afe5-160">Refer back to the guide's principles and coverage of architecture and technology options and decision considerations when you're weighing these choices for your own application.</span></span>

<span data-ttu-id="5afe5-161">請隨意將本指南轉寄給您的小組，協助確保對這些考量和機會有共同的了解。</span><span class="sxs-lookup"><span data-stu-id="5afe5-161">Feel free to forward this guide to your team to help ensure a common understanding of these considerations and opportunities.</span></span> <span data-ttu-id="5afe5-162">讓所有人都使用一組共用術語和基礎原則，有助確保套用一致的架構模式和做法。</span><span class="sxs-lookup"><span data-stu-id="5afe5-162">Having everybody working from a common set of terminology and underlying principles helps ensure consistent application of architectural patterns and practices.</span></span>

## <a name="references"></a><span data-ttu-id="5afe5-163">參考</span><span class="sxs-lookup"><span data-stu-id="5afe5-163">References</span></span>

- <span data-ttu-id="5afe5-164">**針對伺服器應用程式在 .NET Core 和 .NET Framework 之間進行選擇**</span><span class="sxs-lookup"><span data-stu-id="5afe5-164">**Choosing between .NET Core and .NET Framework for server apps**</span></span>  
  [https://docs.microsoft.com/dotnet/standard/choosing-core-framework-server](../../standard/choosing-core-framework-server.md)

>[!div class="step-by-step"]
>[<span data-ttu-id="5afe5-165">下一步</span><span class="sxs-lookup"><span data-stu-id="5afe5-165">Next</span></span>](modern-web-applications-characteristics.md)