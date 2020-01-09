---
ms.openlocfilehash: db1d09c8c9e606b5327a42977a74a74703282d84
ms.sourcegitcommit: 79a2d6a07ba4ed08979819666a0ee6927bbf1b01
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74568195"
---
### <a name="net-core-30-follows-unicode-best-practices-when-replacing-ill-formed-utf-8-byte-sequences"></a><span data-ttu-id="27abd-101">.NET Core 3.0 在取代格式不正確的 UTF-8 位元組序列時，遵循 Unicode 最佳做法</span><span class="sxs-lookup"><span data-stu-id="27abd-101">.NET Core 3.0 follows Unicode best practices when replacing ill-formed UTF-8 byte sequences</span></span>

<span data-ttu-id="27abd-102">當 <xref:System.Text.UTF8Encoding> 類別在進行位元組到字元的轉碼作業期間遇到格式不正確的 UTF-8 位元組序列時，它會將該序列取代為輸出字串中的 '�' （U + FFFD 取代字元）字元。
</span><span class="sxs-lookup"><span data-stu-id="27abd-102">When the <xref:System.Text.UTF8Encoding> class encounters an ill-formed UTF-8 byte sequence during a byte-to-character transcoding operation, it will replace that sequence with a '�' (U+FFFD REPLACEMENT CHARACTER) character in the output string.</span></span> <span data-ttu-id="27abd-103">.NET Core 3.0 與舊版 .NET Core 和 .NET Framework 的不同之處，是遵循在轉碼作業期間執行此取代的 Unicode 最佳作法。</span><span class="sxs-lookup"><span data-stu-id="27abd-103">.NET Core 3.0 differs from previous versions of .NET Core and the .NET Framework by following the Unicode best practice for performing this replacement during the transcoding operation.</span></span>

<span data-ttu-id="27abd-104">這是改善整個 .NET 的 UTF-8 處理工作的一部分，包括新的 <xref:System.Text.Unicode.Utf8?displayProperty=nameWithType> 和 <xref:System.Text.Rune?displayProperty=nameWithType> 類型。</span><span class="sxs-lookup"><span data-stu-id="27abd-104">This is part of a larger effort to improve UTF-8 handling throughout .NET, including by the new <xref:System.Text.Unicode.Utf8?displayProperty=nameWithType> and <xref:System.Text.Rune?displayProperty=nameWithType> types.</span></span> <span data-ttu-id="27abd-105"><xref:System.Text.UTF8Encoding> 類型已獲得改善的錯誤處理機制，因此它會產生與新引進之類型一致的輸出。</span><span class="sxs-lookup"><span data-stu-id="27abd-105">The <xref:System.Text.UTF8Encoding> type was given improved error handling mechanics so that it produces output consistent with the newly introduced types.</span></span>

#### <a name="change-description"></a><span data-ttu-id="27abd-106">變更描述</span><span class="sxs-lookup"><span data-stu-id="27abd-106">Change description</span></span>

<span data-ttu-id="27abd-107">從 .NET Core 3.0 開始，將位元組轉換成字元時，<xref:System.Text.UTF8Encoding> 類別會根據 Unicode 最佳做法執行字元替代。</span><span class="sxs-lookup"><span data-stu-id="27abd-107">Starting with .NET Core 3.0, when transcoding bytes to characters, the <xref:System.Text.UTF8Encoding> class performs character substitution based on Unicode best practices.</span></span> <span data-ttu-id="27abd-108">使用的替代機制會在標題為_U + FFFD 替換為_[最大部分] 的標題中[，以12.0、秒3.9 （PDF）](https://www.unicode.org/versions/Unicode12.0.0/ch03.pdf)的形式加以描述。</span><span class="sxs-lookup"><span data-stu-id="27abd-108">The substitution mechanism used is described by [The Unicode Standard, Version 12.0, Sec. 3.9 (PDF)](https://www.unicode.org/versions/Unicode12.0.0/ch03.pdf) in the heading titled _U+FFFD Substitution of Maximal Subparts_.</span></span>

<span data-ttu-id="27abd-109">只有當輸入位元組序列包含格式不正確的 UTF-8 資料時，_才_會套用此行為。</span><span class="sxs-lookup"><span data-stu-id="27abd-109">This behavior _only_ applies when the input byte sequence contains ill-formed UTF-8 data.</span></span> <span data-ttu-id="27abd-110">此外，如果已使用 `throwOnInvalidBytes: true` 來建立 <xref:System.Text.UTF8Encoding> 實例（請參閱 [UTF8Encoding 的處理常式檔] （<xref:System.Text.UTF8Encoding.%23ctor(System.Boolean,System.Boolean)>），`UTF8Encoding` 實例會繼續在不正確輸入中擲回，而不是執行 U + FFFD 取代。</span><span class="sxs-lookup"><span data-stu-id="27abd-110">Additionally, if the <xref:System.Text.UTF8Encoding> instance has been constructed with `throwOnInvalidBytes: true` (see the [UTF8Encoding constructor documentation](<xref:System.Text.UTF8Encoding.%23ctor(System.Boolean,System.Boolean)>, the `UTF8Encoding` instance will continue to throw on invalid input rather than perform U+FFFD replacement.</span></span>

<span data-ttu-id="27abd-111">下圖說明這項變更與無效3位元組輸入的影響：</span><span class="sxs-lookup"><span data-stu-id="27abd-111">The following illustrates the impact of this change with an invalid 3-byte input:</span></span>

|<span data-ttu-id="27abd-112">3位元組輸入格式錯誤</span><span class="sxs-lookup"><span data-stu-id="27abd-112">Ill-formed 3-byte input</span></span>|<span data-ttu-id="27abd-113">.NET Core 3.0 之前的輸出</span><span class="sxs-lookup"><span data-stu-id="27abd-113">Output before .NET Core 3.0</span></span>|<span data-ttu-id="27abd-114">從 .NET Core 3.0 開始的輸出</span><span class="sxs-lookup"><span data-stu-id="27abd-114">Output starting with .NET Core 3.0</span></span>|
|---|---|---|
| `[ ED A0 90 ]` | <span data-ttu-id="27abd-115">`[ FFFD FFFD ]` （2個字元的輸出）</span><span class="sxs-lookup"><span data-stu-id="27abd-115">`[ FFFD FFFD ]` (2-character output)</span></span>| <span data-ttu-id="27abd-116">`[ FFFD FFFD FFFD ]` （3個字元的輸出）</span><span class="sxs-lookup"><span data-stu-id="27abd-116">`[ FFFD FFFD FFFD ]` (3-character output)</span></span>|

<span data-ttu-id="27abd-117">根據先前連結之 Unicode 標準 PDF 的_資料表 3-9_ ，這個3個字元的輸出是慣用的輸出。</span><span class="sxs-lookup"><span data-stu-id="27abd-117">This 3-char output is the preferred output, according to _Table 3-9_ of the previously linked Unicode Standard PDF.</span></span>

#### <a name="version-introduced"></a><span data-ttu-id="27abd-118">引進的版本</span><span class="sxs-lookup"><span data-stu-id="27abd-118">Version introduced</span></span>

<span data-ttu-id="27abd-119">3.0</span><span class="sxs-lookup"><span data-stu-id="27abd-119">3.0</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="27abd-120">建議的動作</span><span class="sxs-lookup"><span data-stu-id="27abd-120">Recommended action</span></span>

<span data-ttu-id="27abd-121">開發人員不需要採取任何動作。</span><span class="sxs-lookup"><span data-stu-id="27abd-121">No action is required on the part of the developer.</span></span>

#### <a name="category"></a><span data-ttu-id="27abd-122">分類</span><span class="sxs-lookup"><span data-stu-id="27abd-122">Category</span></span>

<span data-ttu-id="27abd-123">CoreFx</span><span class="sxs-lookup"><span data-stu-id="27abd-123">CoreFx</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="27abd-124">受影響的 API</span><span class="sxs-lookup"><span data-stu-id="27abd-124">Affected APIs</span></span>

- <xref:System.Text.UTF8Encoding.GetCharCount%2A?displayProperty=nameWithType>
- <xref:System.Text.UTF8Encoding.GetChars%2A?displayProperty=nameWithType>
- <xref:System.Text.UTF8Encoding.GetString(System.Byte[],System.Int32,System.Int32)?displayProperty=nameWithType>

<!--

### Affected APIs

- `Overload:System.Text.UTF8Encoding.GetCharCount`
- `Overload:System.Text.UTF8Encoding.GetChars`
- `M:System.Text.UTF8Encoding.GetString(System.Byte[],System.Int32,System.Int32)`

-->