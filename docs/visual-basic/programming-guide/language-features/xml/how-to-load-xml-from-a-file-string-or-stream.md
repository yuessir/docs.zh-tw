---
title: 如何：從檔案、字串或資料流載入 XML
ms.date: 07/20/2015
helpviewer_keywords:
- XML [Visual Basic], loading
- LINQ to XML [Visual Basic], loading XML from files
ms.assetid: 2b02dcec-4cca-4575-b4ad-89ceb87b984c
ms.openlocfilehash: 7f2a961ebb7ecd4fc0512e141b4a437be87bec0e
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84392284"
---
# <a name="how-to-load-xml-from-a-file-string-or-stream-visual-basic"></a>如何：從檔案、字串或資料流載入 XML (Visual Basic)

您可以使用數種方法來建立[XML 常](../../../language-reference/xml-literals/index.md)值，並以外部來源（例如檔案、字串或資料流程）的內容填入。 下列範例會顯示這些方法。

[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]

## <a name="to-load-xml-from-a-file"></a>從檔案載入 XML

若要從檔案填入 XML 常值（例如） <xref:System.Xml.Linq.XElement> 或 <xref:System.Xml.Linq.XDocument> 物件，請使用 `Load` 方法。 這個方法可以接受檔案路徑、文字資料流程或 XML 資料流程做為輸入。

下列程式碼範例示範 <xref:System.Xml.Linq.XDocument.Load%28System.String%29> 如何使用方法，將 <xref:System.Xml.Linq.XDocument> 文字檔中的 XML 填入物件。

[!code-vb[VbXMLSamples#43](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples15.vb#43)]

## <a name="to-load-xml-from-a-string"></a>從字串載入 XML

若要從字串填入 XML 常值（例如 <xref:System.Xml.Linq.XElement> 或 <xref:System.Xml.Linq.XDocument> 物件），您可以使用 `Parse` 方法。

下列程式碼範例示範 <xref:System.Xml.Linq.XDocument.Parse%28System.String%29?displayProperty=nameWithType> 如何使用方法，將 <xref:System.Xml.Linq.XDocument> 字串中的 XML 填入物件。

[!code-vb[VbXMLSamples#47](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples15.vb#47)]

## <a name="to-load-xml-from-a-stream"></a>從資料流程載入 XML

若要從資料流程填入 XML 常值（例如 <xref:System.Xml.Linq.XElement> 或 <xref:System.Xml.Linq.XDocument> 物件），您可以使用 `Load` 方法或 <xref:System.Xml.Linq.XNode.ReadFrom%2A?displayProperty=nameWithType> 方法。

下列程式碼範例示範 <xref:System.Xml.Linq.XNode.ReadFrom%2A> 如何使用方法，以 xml 資料流程的 <xref:System.Xml.Linq.XDocument> xml 填入物件。

[!code-vb[VbXMLSamples#46](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples15.vb#46)]

## <a name="see-also"></a>另請參閱

- <xref:System.Xml.Linq.XDocument.Load%2A?displayProperty=nameWithType>
- <xref:System.Xml.Linq.XElement.Load%2A?displayProperty=nameWithType>
- <xref:System.Xml.Linq.XElement.Parse%2A?displayProperty=nameWithType>
- <xref:System.Xml.Linq.XDocument.Parse%2A?displayProperty=nameWithType>
- <xref:System.Xml.Linq.XNode.ReadFrom%2A?displayProperty=nameWithType>
- [XML 常值](../../../language-reference/xml-literals/index.md)
- [XML](index.md)
- [在 Visual Basic 中管理 XML](manipulating-xml.md)
