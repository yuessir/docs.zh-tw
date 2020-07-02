---
title: 在 Fedora 上安裝 .NET Core-.NET Core
description: 示範在 Fedora 上安裝 .NET Core SDK 和 .NET Core 執行時間的各種方式。
author: adegeo
ms.author: adegeo
ms.date: 06/04/2020
ms.openlocfilehash: c9774ff347382a6fe0be1ac1dcb78a74242ec999
ms.sourcegitcommit: dc2feef0794cf41dbac1451a13b8183258566c0e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/24/2020
ms.locfileid: "85324793"
---
# <a name="install-net-core-sdk-or-net-core-runtime-on-fedora"></a><span data-ttu-id="e09e3-103">在 Fedora 上安裝 .NET Core SDK 或 .NET Core 執行時間</span><span class="sxs-lookup"><span data-stu-id="e09e3-103">Install .NET Core SDK or .NET Core Runtime on Fedora</span></span>

<span data-ttu-id="e09e3-104">Fedora 上支援 .NET Core。</span><span class="sxs-lookup"><span data-stu-id="e09e3-104">.NET Core is supported on Fedora.</span></span> <span data-ttu-id="e09e3-105">本文說明如何在 Fedora 上安裝 .NET Core。</span><span class="sxs-lookup"><span data-stu-id="e09e3-105">This article describes how to install .NET Core on Fedora.</span></span> <span data-ttu-id="e09e3-106">當 Fedora 版本不支援時，該版本就不再支援 .NET Core。</span><span class="sxs-lookup"><span data-stu-id="e09e3-106">When a Fedora version falls out of support, .NET Core is no longer supported with that version.</span></span> <span data-ttu-id="e09e3-107">不過，這些指示可以協助您取得在這些版本上執行的 .NET Core，即使它不受支援也一樣。</span><span class="sxs-lookup"><span data-stu-id="e09e3-107">However, these instructions may help you to get .NET Core running on those versions, even though it isn't supported.</span></span>

[!INCLUDE [linux-intro-sdk-vs-runtime](includes/linux-intro-sdk-vs-runtime.md)]

[!INCLUDE [linux-install-package-manager-x64-vs-arm](includes/linux-install-package-manager-x64-vs-arm.md)]

## <a name="supported-distributions"></a><span data-ttu-id="e09e3-108">支援的發行版本</span><span class="sxs-lookup"><span data-stu-id="e09e3-108">Supported distributions</span></span>

<span data-ttu-id="e09e3-109">下表列出目前支援的 .NET Core 版本，以及支援的 Fedora 版本。</span><span class="sxs-lookup"><span data-stu-id="e09e3-109">The following table is a list of currently supported .NET Core releases and the versions of Fedora they're supported on.</span></span> <span data-ttu-id="e09e3-110">在[.Net Core 版本達到支援終止](https://dotnet.microsoft.com/platform/support/policy/dotnet-core)，或[Fedora 版本達到生命週期結束](https://fedoraproject.org/wiki/End_of_life)之前，這些版本仍受到支援。</span><span class="sxs-lookup"><span data-stu-id="e09e3-110">These versions remain supported until either the version of [.NET Core reaches end-of-support](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) or the version of [Fedora reaches end-of-life](https://fedoraproject.org/wiki/End_of_life).</span></span>

- <span data-ttu-id="e09e3-111">✔️表示仍然支援 Fedora 或 .NET Core 的版本。</span><span class="sxs-lookup"><span data-stu-id="e09e3-111">A ✔️ indicates that the version of Fedora or .NET Core is still supported.</span></span>
- <span data-ttu-id="e09e3-112">A ❌ 表示該 Fedora 版本不支援 Fedora 或 .Net Core 的版本。</span><span class="sxs-lookup"><span data-stu-id="e09e3-112">A ❌ indicates that the version of Fedora or .NET Core isn't supported on that Fedora release.</span></span>
- <span data-ttu-id="e09e3-113">當 Fedora 版本和 .NET Core 版本都✔️時，就會支援該作業系統和 .NET 組合。</span><span class="sxs-lookup"><span data-stu-id="e09e3-113">When both a version of Fedora and a version of .NET Core have ✔️, that OS and .NET combination are supported.</span></span>

| <span data-ttu-id="e09e3-114">Fedora</span><span class="sxs-lookup"><span data-stu-id="e09e3-114">Fedora</span></span>                   | <span data-ttu-id="e09e3-115">.NET Core 2.1</span><span class="sxs-lookup"><span data-stu-id="e09e3-115">.NET Core 2.1</span></span> | <span data-ttu-id="e09e3-116">.NET Core 3.1</span><span class="sxs-lookup"><span data-stu-id="e09e3-116">.NET Core 3.1</span></span> | <span data-ttu-id="e09e3-117">.NET 5 Preview （僅限手動安裝）</span><span class="sxs-lookup"><span data-stu-id="e09e3-117">.NET 5 Preview (manual install only)</span></span> |
|--------------------------|---------------|---------------|----------------|
| <span data-ttu-id="e09e3-118">✔️ [32](linux-fedora.md#fedora-32-)</span><span class="sxs-lookup"><span data-stu-id="e09e3-118">✔️ [32](linux-fedora.md#fedora-32-)</span></span> | <span data-ttu-id="e09e3-119">✔️2。1</span><span class="sxs-lookup"><span data-stu-id="e09e3-119">✔️ 2.1</span></span>        | <span data-ttu-id="e09e3-120">✔️3。1</span><span class="sxs-lookup"><span data-stu-id="e09e3-120">✔️ 3.1</span></span>        | <span data-ttu-id="e09e3-121">✔️ 5.0 Preview</span><span class="sxs-lookup"><span data-stu-id="e09e3-121">✔️ 5.0 Preview</span></span> |
| <span data-ttu-id="e09e3-122">✔️ [31](linux-fedora.md#fedora-31-)</span><span class="sxs-lookup"><span data-stu-id="e09e3-122">✔️ [31](linux-fedora.md#fedora-31-)</span></span> | <span data-ttu-id="e09e3-123">✔️2。1</span><span class="sxs-lookup"><span data-stu-id="e09e3-123">✔️ 2.1</span></span>        | <span data-ttu-id="e09e3-124">✔️3。1</span><span class="sxs-lookup"><span data-stu-id="e09e3-124">✔️ 3.1</span></span>        | <span data-ttu-id="e09e3-125">✔️ 5.0 Preview</span><span class="sxs-lookup"><span data-stu-id="e09e3-125">✔️ 5.0 Preview</span></span> |
| <span data-ttu-id="e09e3-126">❌ [30](linux-fedora.md#fedora-30-)</span><span class="sxs-lookup"><span data-stu-id="e09e3-126">❌ [30](linux-fedora.md#fedora-30-)</span></span> | <span data-ttu-id="e09e3-127">✔️2。1</span><span class="sxs-lookup"><span data-stu-id="e09e3-127">✔️ 2.1</span></span>        | <span data-ttu-id="e09e3-128">✔️3。1</span><span class="sxs-lookup"><span data-stu-id="e09e3-128">✔️ 3.1</span></span>        | <span data-ttu-id="e09e3-129">❌5.0 預覽</span><span class="sxs-lookup"><span data-stu-id="e09e3-129">❌ 5.0 Preview</span></span> |
| <span data-ttu-id="e09e3-130">❌[29](linux-fedora.md#fedora-29-)</span><span class="sxs-lookup"><span data-stu-id="e09e3-130">❌ [29](linux-fedora.md#fedora-29-)</span></span> | <span data-ttu-id="e09e3-131">✔️2。1</span><span class="sxs-lookup"><span data-stu-id="e09e3-131">✔️ 2.1</span></span>        | <span data-ttu-id="e09e3-132">✔️3。1</span><span class="sxs-lookup"><span data-stu-id="e09e3-132">✔️ 3.1</span></span>        | <span data-ttu-id="e09e3-133">❌5.0 預覽</span><span class="sxs-lookup"><span data-stu-id="e09e3-133">❌ 5.0 Preview</span></span> |
| <span data-ttu-id="e09e3-134">❌[28](linux-fedora.md#fedora-28-)</span><span class="sxs-lookup"><span data-stu-id="e09e3-134">❌ [28](linux-fedora.md#fedora-28-)</span></span> | <span data-ttu-id="e09e3-135">✔️2。1</span><span class="sxs-lookup"><span data-stu-id="e09e3-135">✔️ 2.1</span></span>        | <span data-ttu-id="e09e3-136">❌3.1</span><span class="sxs-lookup"><span data-stu-id="e09e3-136">❌ 3.1</span></span>        | <span data-ttu-id="e09e3-137">❌5.0 預覽</span><span class="sxs-lookup"><span data-stu-id="e09e3-137">❌ 5.0 Preview</span></span> |
| <span data-ttu-id="e09e3-138">❌[27](linux-fedora.md#fedora-27-)</span><span class="sxs-lookup"><span data-stu-id="e09e3-138">❌ [27](linux-fedora.md#fedora-27-)</span></span> | <span data-ttu-id="e09e3-139">✔️2。1</span><span class="sxs-lookup"><span data-stu-id="e09e3-139">✔️ 2.1</span></span>        | <span data-ttu-id="e09e3-140">❌3.1</span><span class="sxs-lookup"><span data-stu-id="e09e3-140">❌ 3.1</span></span>        | <span data-ttu-id="e09e3-141">❌5.0 預覽</span><span class="sxs-lookup"><span data-stu-id="e09e3-141">❌ 5.0 Preview</span></span> |

<span data-ttu-id="e09e3-142">已不再支援下列 .NET Core 版本。</span><span class="sxs-lookup"><span data-stu-id="e09e3-142">The following versions of .NET Core are no longer supported.</span></span> <span data-ttu-id="e09e3-143">這些下載仍會保持發佈：</span><span class="sxs-lookup"><span data-stu-id="e09e3-143">The downloads for these still remain published:</span></span>

- <span data-ttu-id="e09e3-144">3.0</span><span class="sxs-lookup"><span data-stu-id="e09e3-144">3.0</span></span>
- <span data-ttu-id="e09e3-145">2.2</span><span class="sxs-lookup"><span data-stu-id="e09e3-145">2.2</span></span>
- <span data-ttu-id="e09e3-146">2.0</span><span class="sxs-lookup"><span data-stu-id="e09e3-146">2.0</span></span>

## <a name="how-to-install-other-versions"></a><span data-ttu-id="e09e3-147">如何安裝其他版本</span><span class="sxs-lookup"><span data-stu-id="e09e3-147">How to install other versions</span></span>

[!INCLUDE [package-manager-switcher](./includes/package-manager-heading-hack-pkgname.md)]

## <a name="fedora-32-"></a><span data-ttu-id="e09e3-148">Fedora 32 ✔️</span><span class="sxs-lookup"><span data-stu-id="e09e3-148">Fedora 32 ✔️</span></span>

<span data-ttu-id="e09e3-149">.NET Core 3.1 適用于 Fedora 32 的預設封裝存放庫。</span><span class="sxs-lookup"><span data-stu-id="e09e3-149">.NET Core 3.1 is available in the default package repositories for Fedora 32.</span></span>

[!INCLUDE [linux-dnf-install-31](includes/linux-install-31-dnf.md)]

## <a name="fedora-31-"></a><span data-ttu-id="e09e3-150">Fedora 31 ✔️</span><span class="sxs-lookup"><span data-stu-id="e09e3-150">Fedora 31 ✔️</span></span>

[!INCLUDE [linux-prep-intro-generic](includes/linux-prep-intro-generic.md)]

```bash
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo wget -O /etc/yum.repos.d/microsoft-prod.repo https://packages.microsoft.com/config/fedora/31/prod.repo
```

[!INCLUDE [linux-dnf-install-31](includes/linux-install-31-dnf.md)]

## <a name="fedora-30-"></a><span data-ttu-id="e09e3-151">Fedora 30❌</span><span class="sxs-lookup"><span data-stu-id="e09e3-151">Fedora 30 ❌</span></span>

[!INCLUDE [linux-not-supported](includes/linux-not-supported-fedora.md)]

[!INCLUDE [linux-prep-intro-generic](includes/linux-prep-intro-generic.md)]

```bash
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo wget -O /etc/yum.repos.d/microsoft-prod.repo https://packages.microsoft.com/config/fedora/30/prod.repo
```

[!INCLUDE [linux-dnf-install-31](includes/linux-install-31-dnf.md)]

## <a name="fedora-29-"></a><span data-ttu-id="e09e3-152">Fedora 29❌</span><span class="sxs-lookup"><span data-stu-id="e09e3-152">Fedora 29 ❌</span></span>

[!INCLUDE [linux-not-supported](includes/linux-not-supported-fedora.md)]

[!INCLUDE [linux-prep-intro-generic](includes/linux-prep-intro-generic.md)]

```bash
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo wget -O /etc/yum.repos.d/microsoft-prod.repo https://packages.microsoft.com/config/fedora/29/prod.repo
```

[!INCLUDE [linux-dnf-install-30](includes/linux-install-30-dnf.md)]

## <a name="fedora-28-"></a><span data-ttu-id="e09e3-153">Fedora 28❌</span><span class="sxs-lookup"><span data-stu-id="e09e3-153">Fedora 28 ❌</span></span>

[!INCLUDE [linux-not-supported](includes/linux-not-supported-fedora.md)]

[!INCLUDE [linux-prep-intro-generic](includes/linux-prep-intro-generic.md)]

```bash
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo wget -O /etc/yum.repos.d/microsoft-prod.repo https://packages.microsoft.com/config/fedora/28/prod.repo
```

[!INCLUDE [linux-dnf-install-20](includes/linux-install-20-dnf.md)]

## <a name="fedora-27-"></a><span data-ttu-id="e09e3-154">Fedora 27❌</span><span class="sxs-lookup"><span data-stu-id="e09e3-154">Fedora 27 ❌</span></span>

[!INCLUDE [linux-not-supported](includes/linux-not-supported-fedora.md)]

[!INCLUDE [linux-prep-intro-generic](includes/linux-prep-intro-generic.md)]

```bash
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo wget -O /etc/yum.repos.d/microsoft-prod.repo https://packages.microsoft.com/config/fedora/27/prod.repo
```

[!INCLUDE [linux-dnf-install-20](includes/linux-install-20-dnf.md)]

## <a name="troubleshoot-the-package-manager"></a><span data-ttu-id="e09e3-155">針對套件管理員進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="e09e3-155">Troubleshoot the package manager</span></span>

<span data-ttu-id="e09e3-156">本節提供使用封裝管理員安裝 .NET Core 時，可能會收到的常見錯誤資訊。</span><span class="sxs-lookup"><span data-stu-id="e09e3-156">This section provides information on common errors you may get while using the package manager to install .NET Core.</span></span>

### <a name="failed-to-fetch"></a><span data-ttu-id="e09e3-157">無法提取</span><span class="sxs-lookup"><span data-stu-id="e09e3-157">Failed to fetch</span></span>

[!INCLUDE [package-manager-failed-to-fetch-rpm](includes/package-manager-failed-to-fetch-rpm.md)]

## <a name="snap"></a><span data-ttu-id="e09e3-158">抓取</span><span class="sxs-lookup"><span data-stu-id="e09e3-158">Snap</span></span>

[!INCLUDE [linux-install-snap](includes/linux-install-snap.md)]

## <a name="dependencies"></a><span data-ttu-id="e09e3-159">相依性</span><span class="sxs-lookup"><span data-stu-id="e09e3-159">Dependencies</span></span>

[!INCLUDE [linux-install-dependencies](includes/linux-install-dependencies.md)]

## <a name="scripted-install"></a><span data-ttu-id="e09e3-160">腳本式安裝</span><span class="sxs-lookup"><span data-stu-id="e09e3-160">Scripted install</span></span>

[!INCLUDE [linux-install-scripted](includes/linux-install-scripted.md)]

## <a name="manual-install"></a><span data-ttu-id="e09e3-161">手動安裝</span><span class="sxs-lookup"><span data-stu-id="e09e3-161">Manual install</span></span>

[!INCLUDE [linux-install-manual](includes/linux-install-manual.md)]

## <a name="next-steps"></a><span data-ttu-id="e09e3-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e09e3-162">Next steps</span></span>

- [<span data-ttu-id="e09e3-163">教學課程：使用 Visual Studio Code 建立具有 .NET Core SDK 的主控台應用程式</span><span class="sxs-lookup"><span data-stu-id="e09e3-163">Tutorial: Create a console application with .NET Core SDK using Visual Studio Code</span></span>](../tutorials/with-visual-studio-code.md)