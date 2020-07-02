---
ms.openlocfilehash: d21b2e092d460fdfc367d0f490228ed44ad5c6cc
ms.sourcegitcommit: 63bb83322814f5e5e5c5b69939b14a3139a6ca7e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/25/2020
ms.locfileid: "85365637"
---
### <a name="built-in-support-for-winrt-is-removed-from-net"></a><span data-ttu-id="05e36-101">已從 .NET 移除 WinRT 的內建支援</span><span class="sxs-lookup"><span data-stu-id="05e36-101">Built-in support for WinRT is removed from .NET</span></span>

<span data-ttu-id="05e36-102">已移除在 .NET 中對[Windows 執行時間（WinRT）](/uwp/winrt-cref/winrt-type-system) api 耗用量的內建支援。</span><span class="sxs-lookup"><span data-stu-id="05e36-102">Built-in support for consumption of [Windows runtime (WinRT)](/uwp/winrt-cref/winrt-type-system) APIs in .NET is removed.</span></span>

#### <a name="version-introduced"></a><span data-ttu-id="05e36-103">引進的版本</span><span class="sxs-lookup"><span data-stu-id="05e36-103">Version introduced</span></span>

<span data-ttu-id="05e36-104">5.0 Preview 6</span><span class="sxs-lookup"><span data-stu-id="05e36-104">5.0 Preview 6</span></span>

#### <a name="change-description"></a><span data-ttu-id="05e36-105">變更描述</span><span class="sxs-lookup"><span data-stu-id="05e36-105">Change description</span></span>

<span data-ttu-id="05e36-106">之前，CoreCLR 可能會使用[Windows 中繼資料（WinMD）](/uwp/winrt-cref/winmd-files)檔案進行作用中，並使用 WinRT 類型。</span><span class="sxs-lookup"><span data-stu-id="05e36-106">Previously, CoreCLR could consume [Windows metadata (WinMD) files](/uwp/winrt-cref/winmd-files) to active and consume WinRT types.</span></span> <span data-ttu-id="05e36-107">從 .NET 5.0 開始，CoreCLR 不會再直接取用 WinMD 檔案。</span><span class="sxs-lookup"><span data-stu-id="05e36-107">Starting in .NET 5.0, CoreCLR can no longer consume WinMD files directly.</span></span>

<span data-ttu-id="05e36-108">如果您嘗試參考不受支援的元件，則會取得 <xref:System.IO.FileNotFoundException> 。</span><span class="sxs-lookup"><span data-stu-id="05e36-108">If you attempt to reference an unsupported assembly, you'll get a <xref:System.IO.FileNotFoundException>.</span></span> <span data-ttu-id="05e36-109">如果您啟用 WinRT 類別，則會取得 <xref:System.PlatformNotSupportedException> 。</span><span class="sxs-lookup"><span data-stu-id="05e36-109">If you activate a WinRT class, you'll get a <xref:System.PlatformNotSupportedException>.</span></span>

<span data-ttu-id="05e36-110">這項重大變更的原因如下：</span><span class="sxs-lookup"><span data-stu-id="05e36-110">This breaking change was made for the following reasons:</span></span>

- <span data-ttu-id="05e36-111">因此 WinRT 可以與 .NET 執行時間分開開發和改進。</span><span class="sxs-lookup"><span data-stu-id="05e36-111">So WinRT can be developed and improved separately from the .NET runtime.</span></span>
- <span data-ttu-id="05e36-112">適用于針對其他作業系統（例如 iOS 和 Android）提供之 interop 系統的對稱。</span><span class="sxs-lookup"><span data-stu-id="05e36-112">For symmetry with interop systems provided for other operating systems, such as iOS and Android.</span></span>
- <span data-ttu-id="05e36-113">若要利用其他 .NET 功能，例如 c # 功能、中繼語言（IL）連結，以及預先進行的（AOT）編譯。</span><span class="sxs-lookup"><span data-stu-id="05e36-113">To take advantage of other .NET features, such as C# features, intermediate language (IL) linking, and ahead-of-time (AOT) compilation.</span></span>
- <span data-ttu-id="05e36-114">以簡化 .NET 執行時間程式碼基底。</span><span class="sxs-lookup"><span data-stu-id="05e36-114">To simplify the .NET runtime codebase.</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="05e36-115">建議的動作</span><span class="sxs-lookup"><span data-stu-id="05e36-115">Recommended action</span></span>

- <span data-ttu-id="05e36-116">移除對[Microsoft.Windows.SDK.NET 套件](https://www.nuget.org/packages/microsoft.windows.sdk.net)[的參考，並將](https://www.nuget.org/packages/Microsoft.Windows.SDK.Contracts)其取代為參考。</span><span class="sxs-lookup"><span data-stu-id="05e36-116">Remove references to the [Microsoft.Windows.SDK.Contracts package](https://www.nuget.org/packages/Microsoft.Windows.SDK.Contracts) and replace them with references to the [Microsoft.Windows.SDK.NET package](https://www.nuget.org/packages/microsoft.windows.sdk.net).</span></span>

- <span data-ttu-id="05e36-117">使用[c #/WinRT](/windows/uwp/csharp-winrt/)工具鏈來產生或自訂 .net 5.0 和更新版本中的 WinRT api 和類型。</span><span class="sxs-lookup"><span data-stu-id="05e36-117">Use the [C#/WinRT](/windows/uwp/csharp-winrt/) tool chain to generate or customize WinRT APIs and types in .NET 5.0 and later versions.</span></span>

#### <a name="category"></a><span data-ttu-id="05e36-118">類別</span><span class="sxs-lookup"><span data-stu-id="05e36-118">Category</span></span>

<span data-ttu-id="05e36-119">Interop</span><span class="sxs-lookup"><span data-stu-id="05e36-119">Interop</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="05e36-120">受影響的 API</span><span class="sxs-lookup"><span data-stu-id="05e36-120">Affected APIs</span></span>

- <xref:System.IO.WindowsRuntimeStorageExtensions?displayProperty=fullName>
- <xref:System.IO.WindowsRuntimeStreamExtensions?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.WindowsRuntime?displayProperty=fullName>
- <xref:System.WindowsRuntimeSystemExtensions?displayProperty=fullName>
- <xref:Windows.Foundation.Point?displayProperty=fullName>
- <xref:Windows.Foundation.Size?displayProperty=fullName>
- <xref:Windows.UI.Color?displayProperty=fullName>

<!--

#### Affected APIs

- `T:System.IO.WindowsRuntimeStorageExtensions`
- `T: System.IO.WindowsRuntimeStreamExtensions`
- `N:System.Runtime.InteropServices.WindowsRuntime`
- `T:System.WindowsRuntimeSystemExtensions`
- `T:Windows.Foundation.Point`
- `T:Windows.Foundation.Size`
- `T:Windows.UI.Color`

-->