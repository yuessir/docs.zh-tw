---
title: 在 Alpine 上安裝 .NET Core-.NET Core
description: 示範在 Alpine 上安裝 .NET Core SDK 和 .NET Core 執行時間的各種方式。
author: adegeo
ms.author: adegeo
ms.date: 06/04/2020
ms.openlocfilehash: 92753933cbcedae28867b66293d1044f700d7baa
ms.sourcegitcommit: dc2feef0794cf41dbac1451a13b8183258566c0e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/24/2020
ms.locfileid: "85324827"
---
# <a name="install-net-core-sdk-or-net-core-runtime-on-alpine"></a><span data-ttu-id="88710-103">在 Alpine 上安裝 .NET Core SDK 或 .NET Core 執行時間</span><span class="sxs-lookup"><span data-stu-id="88710-103">Install .NET Core SDK or .NET Core Runtime on Alpine</span></span>

<span data-ttu-id="88710-104">本文說明如何在 Alpine 上安裝 .NET Core。</span><span class="sxs-lookup"><span data-stu-id="88710-104">This article describes how to install .NET Core on Alpine.</span></span> <span data-ttu-id="88710-105">當 Alpine 版本不支援時，該版本就不再支援 .NET Core。</span><span class="sxs-lookup"><span data-stu-id="88710-105">When a Alpine version falls out of support, .NET Core is no longer supported with that version.</span></span> <span data-ttu-id="88710-106">不過，這些指示可以協助您取得在這些版本上執行的 .NET Core，即使它不受支援也一樣。</span><span class="sxs-lookup"><span data-stu-id="88710-106">However, these instructions may help you to get .NET Core running on those versions, even though it isn't supported.</span></span>

[!INCLUDE [linux-intro-sdk-vs-runtime](includes/linux-intro-sdk-vs-runtime.md)]

<span data-ttu-id="88710-107">沒有安裝程式可供 Alpine。</span><span class="sxs-lookup"><span data-stu-id="88710-107">There are no installers for Alpine.</span></span> <span data-ttu-id="88710-108">您必須使用[安裝腳本](#scripted-install)或遵循[手動安裝](#manual-install)指示。</span><span class="sxs-lookup"><span data-stu-id="88710-108">You must either use the [install script](#scripted-install) or follow the [manual install](#manual-install) instructions.</span></span>

## <a name="supported-distributions"></a><span data-ttu-id="88710-109">支援的發行版本</span><span class="sxs-lookup"><span data-stu-id="88710-109">Supported distributions</span></span>

<span data-ttu-id="88710-110">下表列出目前支援的 .NET Core 版本，以及支援的 Alpine 版本。</span><span class="sxs-lookup"><span data-stu-id="88710-110">The following table is a list of currently supported .NET Core releases and the versions of Alpine they're supported on.</span></span> <span data-ttu-id="88710-111">在[.Net Core 版本達到支援終止](https://dotnet.microsoft.com/platform/support/policy/dotnet-core)，或[Alpine 版本達到生命週期結束](https://wiki.alpinelinux.org/wiki/Alpine_Linux:Releases)之前，這些版本仍受到支援。</span><span class="sxs-lookup"><span data-stu-id="88710-111">These versions remain supported until either the version of [.NET Core reaches end-of-support](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) or the version of [Alpine reaches end-of-life](https://wiki.alpinelinux.org/wiki/Alpine_Linux:Releases).</span></span>

- <span data-ttu-id="88710-112">✔️表示仍然支援 Alpine 或 .NET Core 的版本。</span><span class="sxs-lookup"><span data-stu-id="88710-112">A ✔️ indicates that the version of Alpine or .NET Core is still supported.</span></span>
- <span data-ttu-id="88710-113">A ❌ 表示該 Alpine 版本不支援 Alpine 或 .Net Core 的版本。</span><span class="sxs-lookup"><span data-stu-id="88710-113">A ❌ indicates that the version of Alpine or .NET Core isn't supported on that Alpine release.</span></span>
- <span data-ttu-id="88710-114">當 Alpine 版本和 .NET Core 版本都✔️時，就會支援該作業系統和 .NET 組合。</span><span class="sxs-lookup"><span data-stu-id="88710-114">When both a version of Alpine and a version of .NET Core have ✔️, that OS and .NET combination are supported.</span></span>

| <span data-ttu-id="88710-115">Alpine</span><span class="sxs-lookup"><span data-stu-id="88710-115">Alpine</span></span>                   | <span data-ttu-id="88710-116">.NET Core 2.1</span><span class="sxs-lookup"><span data-stu-id="88710-116">.NET Core 2.1</span></span> | <span data-ttu-id="88710-117">.NET Core 3.1</span><span class="sxs-lookup"><span data-stu-id="88710-117">.NET Core 3.1</span></span> | <span data-ttu-id="88710-118">.NET 5 Preview</span><span class="sxs-lookup"><span data-stu-id="88710-118">.NET 5 Preview</span></span> |
|--------------------------|---------------|---------------|----------------|
| <span data-ttu-id="88710-119">✔️3.12</span><span class="sxs-lookup"><span data-stu-id="88710-119">✔️ 3.12</span></span>  | <span data-ttu-id="88710-120">✔️2。1</span><span class="sxs-lookup"><span data-stu-id="88710-120">✔️ 2.1</span></span>        | <span data-ttu-id="88710-121">✔️3。1</span><span class="sxs-lookup"><span data-stu-id="88710-121">✔️ 3.1</span></span>        | <span data-ttu-id="88710-122">✔️ 5.0 Preview</span><span class="sxs-lookup"><span data-stu-id="88710-122">✔️ 5.0 Preview</span></span> |
| <span data-ttu-id="88710-123">✔️3.11</span><span class="sxs-lookup"><span data-stu-id="88710-123">✔️ 3.11</span></span>  | <span data-ttu-id="88710-124">✔️2。1</span><span class="sxs-lookup"><span data-stu-id="88710-124">✔️ 2.1</span></span>        | <span data-ttu-id="88710-125">✔️3。1</span><span class="sxs-lookup"><span data-stu-id="88710-125">✔️ 3.1</span></span>        | <span data-ttu-id="88710-126">✔️ 5.0 Preview</span><span class="sxs-lookup"><span data-stu-id="88710-126">✔️ 5.0 Preview</span></span> |
| <span data-ttu-id="88710-127">✔️3.10</span><span class="sxs-lookup"><span data-stu-id="88710-127">✔️ 3.10</span></span>  | <span data-ttu-id="88710-128">✔️2。1</span><span class="sxs-lookup"><span data-stu-id="88710-128">✔️ 2.1</span></span>        | <span data-ttu-id="88710-129">✔️3。1</span><span class="sxs-lookup"><span data-stu-id="88710-129">✔️ 3.1</span></span>        | <span data-ttu-id="88710-130">✔️ 5.0 Preview</span><span class="sxs-lookup"><span data-stu-id="88710-130">✔️ 5.0 Preview</span></span> |
| <span data-ttu-id="88710-131">✔️3。9</span><span class="sxs-lookup"><span data-stu-id="88710-131">✔️ 3.9</span></span>   | <span data-ttu-id="88710-132">✔️2。1</span><span class="sxs-lookup"><span data-stu-id="88710-132">✔️ 2.1</span></span>        | <span data-ttu-id="88710-133">✔️3。1</span><span class="sxs-lookup"><span data-stu-id="88710-133">✔️ 3.1</span></span>        | <span data-ttu-id="88710-134">✔️ 5.0 Preview</span><span class="sxs-lookup"><span data-stu-id="88710-134">✔️ 5.0 Preview</span></span> |
| <span data-ttu-id="88710-135">❌3.8</span><span class="sxs-lookup"><span data-stu-id="88710-135">❌ 3.8</span></span>   | <span data-ttu-id="88710-136">✔️2。1</span><span class="sxs-lookup"><span data-stu-id="88710-136">✔️ 2.1</span></span>        | <span data-ttu-id="88710-137">❌3.1</span><span class="sxs-lookup"><span data-stu-id="88710-137">❌ 3.1</span></span>        | <span data-ttu-id="88710-138">❌5.0 預覽</span><span class="sxs-lookup"><span data-stu-id="88710-138">❌ 5.0 Preview</span></span> |

<span data-ttu-id="88710-139">已不再支援下列 .NET Core 版本。</span><span class="sxs-lookup"><span data-stu-id="88710-139">The following versions of .NET Core are no longer supported.</span></span> <span data-ttu-id="88710-140">這些下載仍會保持發佈：</span><span class="sxs-lookup"><span data-stu-id="88710-140">The downloads for these still remain published:</span></span>

- <span data-ttu-id="88710-141">3.0</span><span class="sxs-lookup"><span data-stu-id="88710-141">3.0</span></span>
- <span data-ttu-id="88710-142">2.2</span><span class="sxs-lookup"><span data-stu-id="88710-142">2.2</span></span>
- <span data-ttu-id="88710-143">2.0</span><span class="sxs-lookup"><span data-stu-id="88710-143">2.0</span></span>

## <a name="dependencies"></a><span data-ttu-id="88710-144">相依性</span><span class="sxs-lookup"><span data-stu-id="88710-144">Dependencies</span></span>

<span data-ttu-id="88710-145">Alpine Linux 上的 .NET Core 需要安裝下列相依性：</span><span class="sxs-lookup"><span data-stu-id="88710-145">.NET Core on Alpine Linux requires the following dependencies installed:</span></span>

- <span data-ttu-id="88710-146">icu-程式庫</span><span class="sxs-lookup"><span data-stu-id="88710-146">icu-libs</span></span>
- <span data-ttu-id="88710-147">krb5-libs</span><span class="sxs-lookup"><span data-stu-id="88710-147">krb5-libs</span></span>
- <span data-ttu-id="88710-148">libintl</span><span class="sxs-lookup"><span data-stu-id="88710-148">libintl</span></span>
- <span data-ttu-id="88710-149">libssl1.0.0 1.1 （Alpine v 3.9 或更新版本）</span><span class="sxs-lookup"><span data-stu-id="88710-149">libssl1.1 (Alpine v3.9 or greater)</span></span>
- <span data-ttu-id="88710-150">libssl1.0.0 1.0 （Alpine 3.8）</span><span class="sxs-lookup"><span data-stu-id="88710-150">libssl1.0 (Alpine v3.8)</span></span>
- <span data-ttu-id="88710-151">libstdc++</span><span class="sxs-lookup"><span data-stu-id="88710-151">libstdc++</span></span>
- <span data-ttu-id="88710-152">lttng-ust</span><span class="sxs-lookup"><span data-stu-id="88710-152">lttng-ust</span></span>
- <span data-ttu-id="88710-153">numactl （選擇性）</span><span class="sxs-lookup"><span data-stu-id="88710-153">numactl (optional)</span></span>
- <span data-ttu-id="88710-154">zlib</span><span class="sxs-lookup"><span data-stu-id="88710-154">zlib</span></span>

## <a name="scripted-install"></a><span data-ttu-id="88710-155">腳本式安裝</span><span class="sxs-lookup"><span data-stu-id="88710-155">Scripted install</span></span>

[!INCLUDE [linux-install-scripted](includes/linux-install-scripted.md)]

## <a name="manual-install"></a><span data-ttu-id="88710-156">手動安裝</span><span class="sxs-lookup"><span data-stu-id="88710-156">Manual install</span></span>

[!INCLUDE [linux-install-manual](includes/linux-install-manual.md)]

## <a name="next-steps"></a><span data-ttu-id="88710-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="88710-157">Next steps</span></span>

- [<span data-ttu-id="88710-158">教學課程：使用 Visual Studio Code 建立具有 .NET Core SDK 的主控台應用程式</span><span class="sxs-lookup"><span data-stu-id="88710-158">Tutorial: Create a console application with .NET Core SDK using Visual Studio Code</span></span>](../tutorials/with-visual-studio-code.md)