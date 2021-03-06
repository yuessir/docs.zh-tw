---
title: '<paramref>-C # 程式設計指南'
description: 瞭解 XML <paramref> 標記。 此標記可讓您指定程式碼中的單字為參數。
ms.date: 07/20/2015
f1_keywords:
- paramref
- <paramref>
helpviewer_keywords:
- <paramref> C# XML tag
- paramref C# XML tag
ms.assetid: 756c24c1-f591-40e8-a838-559761539b0b
ms.openlocfilehash: 133f43abfaf349806404d6d37fb472e3145c51b7
ms.sourcegitcommit: 552b4b60c094559db9d8178fa74f5bafaece0caf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2020
ms.locfileid: "87381836"
---
# <a name="paramref-c-programming-guide"></a>\<paramref>（C # 程式設計手冊）

## <a name="syntax"></a>語法

```xml
<paramref name="name"/>
```

## <a name="parameters"></a>參數

- `name`

  要參考的參數名稱。 以雙引號 (" ") 將名稱括起來。

## <a name="remarks"></a>備註

`<paramref>`標記可讓您指定程式碼批註中的單字，例如在 `<summary>` 或區塊中 `<remarks>` 參考參數。 若要以某種不同方式 (例如，粗體或斜體字型) 格式化這個字組，您可以處理 XML 檔案。

使用[-doc](../../language-reference/compiler-options/doc-compiler-option.md)進行編譯，以處理檔案的檔批註。

## <a name="example"></a>範例

[!code-csharp[csProgGuideDocComments#7](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideDocComments/CS/DocComments.cs#7)]

## <a name="see-also"></a>另請參閱

- [C # 程式設計指南](../index.md)
- [建議使用的文件註解標籤](./recommended-tags-for-documentation-comments.md)
