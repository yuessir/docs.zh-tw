---
title: 為運算子
ms.date: 07/20/2015
f1_keywords:
- vb.is
helpviewer_keywords:
- comparison operators [Visual Basic]
- equivalent objects
- TypeOf...Is expression
- Is operator [Visual Basic]
ms.assetid: 8045a6c8-2a83-45b6-ad47-d09a704c656d
ms.openlocfilehash: 1c2d87ef0a8202332c87af552f488d652c400213
ms.sourcegitcommit: 9c45035b781caebc63ec8ecf912dc83fb6723b1f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "88812259"
---
# <a name="is-operator-visual-basic"></a>是運算子 (Visual Basic) 

比較兩個物件參考變數。

## <a name="syntax"></a>Syntax

```vb
result = object1 Is object2
```

## <a name="parts"></a>組件

 `result`  
 必要。 任何 `Boolean` 值。  
  
 `object1`  
 必要。 任何 `Object` 名稱。  
  
 `object2`  
 必要。 任何 `Object` 名稱。  
  
## <a name="remarks"></a>備註

`Is`運算子會判斷兩個物件參考是否參考相同的物件。 但是，它不會執行值比較。 如果 `object1` 和 `object2` 兩者都參考完全相同的物件實例，則為 `result` `True` ; 如果沒有，則 `result` 為 `False` 。

> [!NOTE]
> `Is`關鍵字也可用於[Select .。。Case 語句](../statements/select-case-statement.md)。
  
## <a name="example"></a>範例

下列範例會使用 `Is` 運算子來比較物件參考的配對。 結果會指派給一個 `Boolean` 值，表示兩個物件是否相同。

[!code-vb[VbVbalrOperators#27](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#27)]

如先前的範例所示，您可以使用 `Is` 運算子來測試早期繫結和晚期繫結的物件。

## <a name="use-typeof-operator-with-is-operator"></a>使用 TypeOf 運算子搭配 Is 運算子

`Is` 運算子也可以搭配 `TypeOf` 關鍵字使用，以建立一個 `TypeOf` ... `Is` 運算式，以測試物件變數是否與資料類型相容。 例如：

```vb
If TypeOf sender Is Button Then
```

## <a name="see-also"></a>另請參閱

- [TypeOf 運算子](typeof-operator.md)
- [IsNot 運算子](isnot-operator.md)
- [Comparison Operators in Visual Basic](../../programming-guide/language-features/operators-and-expressions/comparison-operators.md)
- [Visual Basic 中的運算子優先順序](operator-precedence.md)
- [依功能列出運算子](operators-listed-by-functionality.md)
- [運算子和運算式](../../programming-guide/language-features/operators-and-expressions/index.md)
