---
title: 委派類別 '<classname>' 沒有 Invoke 方法，因此這個類型的運算式不可成為方法呼叫的目標
ms.date: 07/20/2015
f1_keywords:
- vbc30220
- bc30220
helpviewer_keywords:
- BC30220
ms.assetid: 6be0d61c-f2f9-4f9b-ab90-8871a0d7206d
ms.openlocfilehash: 27be97ba2930791bcb9012c824bc418a0089b037
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84409708"
---
# <a name="delegate-class-classname-has-no-invoke-method-so-an-expression-of-this-type-cannot-be-the-target-of-a-method-call"></a>委派類別 '\<classname>' 沒有 Invoke 方法，因此這個類型的運算式不可成為方法呼叫的目標
`Invoke`透過委派的呼叫失敗，因為 `Invoke` 不是在委派類別上執行。  
  
 **錯誤識別碼：** BC30220  
  
## <a name="to-correct-this-error"></a>更正這個錯誤  
  
1. 請確定已使用語句建立委派類別的實例 `Dim` ，而且已使用運算子將程式指派給委派實例 `AddressOf` 。  
  
2. 找出用來執行委派類別的程式碼，並確定它會實作為程式 `Invoke` 。  
  
## <a name="see-also"></a>另請參閱

- [委派](../../programming-guide/language-features/delegates/index.md)
- [Delegate 陳述式](../statements/delegate-statement.md)
- [AddressOf 運算子](../operators/addressof-operator.md)
- [Dim 陳述式](../statements/dim-statement.md)
