---
ms.openlocfilehash: 19be8a7755d9b238ab6507eaa73319bddf39faa3
ms.sourcegitcommit: cbacb5d2cebbf044547f6af6e74a9de866800985
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/05/2020
ms.locfileid: "89497678"
---
### <a name="data-written-to-printsystemjobinfojobstream-must-be-in-xps-format"></a>寫入 PrintSystemJobInfo.JobStream 的資料必須是 XPS 格式

#### <a name="details"></a>詳細資料

<xref:System.Printing.PrintSystemJobInfo.JobStream> 屬性會公開列印工作的資料流。 使用者可藉由寫入此資料流，將原始資料傳送至基礎作業系統列印元件。從 Windows 8 和更新版本的 Windows 作業系統上的 .NET Framework 4.5 開始，寫入此資料流的資料必須是作為套件資料流的 XPS 格式。

#### <a name="suggestion"></a>建議

若要輸出列印的內容，您可以執行下列任何一項操作：<ul><li>使用 <xref:System.Windows.Xps.XpsDocumentWriter> 類別來輸出列印的內容。 這是建議的替代方案。</li><li>請確定傳送至 <xref:System.Printing.PrintSystemJobInfo.JobStream> 屬性所傳回之資料流的資料是作為套件資料流的 XPS 格式。</li></ul>

| 名稱    | 值       |
|:--------|:------------|
| 範圍   |Minor|
|版本|4.5|
|類型|執行階段|

#### <a name="affected-apis"></a>受影響的 API

- <xref:System.Printing.PrintSystemJobInfo.JobStream?displayProperty=nameWithType>

<!--

#### Affected APIs

- `P:System.Printing.PrintSystemJobInfo.JobStream`

-->
