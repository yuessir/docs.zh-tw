---
title: 如何：在日期和時間運算中使用時區
ms.date: 04/10/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- time zones [.NET Framework], arithmetic operations
- arithmetic operations [.NET Framework], dates and times
- dates [.NET Framework], adding and subtracting
ms.assetid: 83dd898d-1338-415d-8cd6-445377ab7871
ms.openlocfilehash: af19145f7caa9dbe8630ae7593734769e98720d0
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84280916"
---
# <a name="how-to-use-time-zones-in-date-and-time-arithmetic"></a>如何：在日期和時間運算中使用時區

通常，當您使用或值來執行日期和時間算術時 <xref:System.DateTime> <xref:System.DateTimeOffset> ，結果不會反映任何時區調整規則。 即使日期和時間值的時區可清楚識別（例如，當屬性設定為時），也是如此 <xref:System.DateTime.Kind%2A> <xref:System.DateTimeKind.Local> 。 本主題說明如何對屬於特定時區的日期和時間值執行算數運算。 算術運算的結果將反映時區調整規則。

### <a name="to-apply-adjustment-rules-to-date-and-time-arithmetic"></a>將調整規則套用至日期和時間運算

1. 實作某種方法，以將日期和時間值與所屬時區緊密結合。 例如，宣告包含日期和時間值及其時區的結構。 下列範例會使用這個方法，將 <xref:System.DateTime> 值與時區連結。

   [!code-csharp[System.DateTimeOffset.Conceptual#6](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/cs/Conceptual6.cs#6)]
   [!code-vb[System.DateTimeOffset.Conceptual#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/vb/Conceptual6.vb#6)]

2. 藉由呼叫方法或方法，將時間轉換為國際標準時間（UTC） <xref:System.TimeZoneInfo.ConvertTimeToUtc%2A> <xref:System.TimeZoneInfo.ConvertTime%2A> 。

3. 對 UTC 時間執行算術運算。

4. 藉由呼叫方法，將時間從 UTC 轉換成原始時間的相關時區 <xref:System.TimeZoneInfo.ConvertTime%28System.DateTime%2CSystem.TimeZoneInfo%29?displayProperty=nameWithType> 。

## <a name="example"></a>範例

下列範例將兩個小時三十分鐘新增至 2008 年 3 月 9 日凌晨 1:30 中央標準時區。 時區轉換為日光節約時間會在三十分鐘後，也就是 2008 年 3 月 9 日 凌晨 2:00 加上兩個半小時。 由於本範例依照上一節所列的四個步驟進行，因此會正確回報產生的時間 2008 年 3 月 9 日 凌晨 2:00 加上兩個半小時。

[!code-csharp[System.DateTimeOffset.Conceptual#8](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/cs/Conceptual8.cs#8)]
[!code-vb[System.DateTimeOffset.Conceptual#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/vb/Conceptual8.vb#8)]

<xref:System.DateTime>和 <xref:System.DateTimeOffset> 值會從其所屬的任何時區解除關聯。 若要透過自動套用時區調整規則來執行日期和時間運算，則必須立即識別任何日期和時間值所屬的時區。 這表示日期和時間及其相關聯時區必須緊密結合。 有幾個方式可做到這點，包括下列各項︰

- 假設應用程式中使用的所有時間都是屬於特定時區。 雖然適用於某些情況，但是這種方式提供的彈性有限，可攜性也可能有限。

- 定義一種類型，而這個類型透過將日期和時間與其相關聯時區都包含為類型的欄位來緊密結合兩者。 程式碼範例中使用這種方式，以定義將日期和時間以及時區儲存在兩個成員欄位中的結構。

此範例說明如何對值執行算數運算， <xref:System.DateTime> 以便將時區調整規則套用至結果。 不過，您 <xref:System.DateTimeOffset> 可以輕鬆地使用值。 下列範例說明如何將原始範例中的程式碼調整為使用， <xref:System.DateTimeOffset> 而不是 <xref:System.DateTime> 值。

[!code-csharp[System.DateTimeOffset.Conceptual#7](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/cs/Conceptual6.cs#7)]
[!code-vb[System.DateTimeOffset.Conceptual#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/vb/Conceptual6.vb#7)]

請注意，如果此加法只是在值上執行 <xref:System.DateTimeOffset> ，而不先將它轉換成 UTC，則結果會反映正確的時間點，但其位移不會反映該時間指定之時區的。

## <a name="compiling-the-code"></a>編譯程式碼

這個範例需要：

- <xref:System>使用語句匯入的命名空間 `using` （在 c # 程式碼中為必要項）。

## <a name="see-also"></a>另請參閱

- [日期、時間和時區](index.md)
- [使用日期和時間執行算數運算](performing-arithmetic-operations.md)
