---
title: 比較運算子
ms.date: 07/20/2015
helpviewer_keywords:
- comparison operators [Visual Basic], comparing strings
- comparison operators [Visual Basic], comparing objects
- strings [Visual Basic], comparing
- comparison operators [Visual Basic]
- string comparison [Visual Basic], operators
- objects [Visual Basic], comparing
- numbers [Visual Basic], comparing
- Visual Basic code, operators
- string comparison [Visual Basic]
- numeric values [Visual Basic], comparing
- comparison operators [Visual Basic], comparing numeric values
- operators [Visual Basic], comparison
ms.assetid: 0b570339-5407-474f-8421-e183a8b303ee
ms.openlocfilehash: 7a93928ff95e307c64149da7ab21476ffd4fa77d
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84388825"
---
# <a name="comparison-operators-in-visual-basic"></a>Comparison Operators in Visual Basic
比較運算子會比較兩個運算式，並傳回 `Boolean` 代表其值關聯性的值。 有運算子可比較數值、比較字串的運算子，以及比較物件的運算子。 這裡將討論這三種類型的運算子。  
  
## <a name="comparing-numeric-values"></a>比較數值  
 Visual Basic 使用六個數值比較運算子來比較數值。 每個運算子都會接受兩個評估為數值之運算式的運算元。 下表列出運算子，並顯示各項的範例。  
  
|運算子|測試的條件|範例|  
|--------------|----------------------|--------------|  
|`=`等效|第一個運算式的值是否等於秒的值？|`23`   `=`   `33    ' False`<br /><br /> `23`   `=`   `23    ' True`<br /><br /> `23`   `=`   `12    ' False`|  
|`<>`等|第一個運算式的值是否與第二個運算式的值不相等？|`23`   `<>`   `33    ' True`<br /><br /> `23`   `<>`   `23    ' False`<br /><br /> `23`   `<>`   `12    ' True`|  
|`<`（小於）|第一個運算式的值是否小於第二個的值？|`23`   `<`   `33    ' True`<br /><br /> `23`   `<`   `23    ' False`<br /><br /> `23`   `<`   `12    ' False`|  
|`>`（大於）|第一個運算式的值是否大於第二個的值？|`23`   `>`   `33    ' False`<br /><br /> `23`   `>`   `23    ' False`<br /><br /> `23`   `>`   `12    ' True`|  
|`<=`（小於或等於）|第一個運算式的值是否小於或等於第二個運算式的值？|`23`   `<=`   `33    ' True`<br /><br /> `23`   `<=`   `23    ' True`<br /><br /> `23`   `<=`   `12    ' False`|  
|`>=`（大於或等於）|第一個運算式的值是否大於或等於第二個運算式的值？|`23`   `>=`   `33    ' False`<br /><br /> `23`   `>=`   `23    ' True`<br /><br /> `23`   `>=`   `12    ' True`|  
  
## <a name="comparing-strings"></a>比較字串  
 Visual Basic 使用[Like 運算子](../../../language-reference/operators/like-operator.md)和數值比較運算子來比較字串。 `Like`運算子可讓您指定模式。 然後，字串會與模式進行比較，如果相符，則結果會是 `True` 。 否則，結果為 `False`。 數值運算子可讓您根據 `String` 其排序次序來比較值，如下列範例所示。  
  
 `"73" < "9"`  
  
 `' The result of the preceding comparison is True.`  
  
 前述範例中的結果是 `True` 因為第一個字串中的第一個字元會在第二個字串的第一個字元之前排序。 如果第一個字元相等，則比較會繼續在兩個字串中的下一個字元，依此類推。 您也可以使用等號比較運算子來測試字串是否相等，如下列範例所示。  
  
 `"734" = "734"`  
  
 `' The result of the preceding comparison is True.`  
  
 如果一個字串是另一個的前置詞，例如 "aa" 和 "aaa"，則較長的字串會被視為大於較短的字串。 下列範例將說明這點。  
  
 `"aaa" > "aa"`  
  
 `' The result of the preceding comparison is True.`  
  
 排序次序是根據的設定，以二進位比較或文字比較為基礎 `Option Compare` 。 如需詳細資訊，請參閱[Option Compare 語句](../../../language-reference/statements/option-compare-statement.md)。  
  
## <a name="comparing-objects"></a>比較物件  
 Visual Basic 會比較兩個物件參考變數與[Is 運算子](../../../language-reference/operators/is-operator.md)和[IsNot 運算子](../../../language-reference/operators/isnot-operator.md)。 您可以使用其中一個運算子來判斷兩個參考變數是否參考相同的物件實例。 下列範例將說明這點。  
  
 [!code-vb[VbVbalrOperators#65](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#65)]  
  
 在上述範例中，會 `x Is y` 評估為 `True` ，因為這兩個變數都參考相同的實例。 請使用下列範例來對比此結果。  
  
 [!code-vb[VbVbalrOperators#66](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#66)]  
  
 在上述範例中， `x Is y` 會評估為 `False` ，因為雖然變數會參考相同類型的物件，但它們會參考該類型的不同實例。  
  
 當您想要測試兩個未指向相同實例的物件時， `IsNot` 運算子可讓您避免與的文法笨拙組合 `Not` `Is` 。 下列範例將說明這點。  
  
 [!code-vb[VbVbalrOperators#67](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#67)]  
  
 在上述範例中， `If a IsNot b` 相當於 `If Not a Is b` 。  
  
### <a name="comparing-object-type"></a>比較物件類型  
 您可以使用 [...] 運算式來測試物件是否為特定類型。 `TypeOf` `Is` 語法如下所示：  
  
 `TypeOf <objectexpression> Is <typename>`  
  
 當 `typename` 指定介面類別型時， `TypeOf` `Is` 如果物件會執行 `True` 介面類別型，則 ... 運算式會傳回。 當 `typename` 是類別類型時， `True` 如果物件是所指定類別的實例或衍生自指定類別的類別，則運算式會傳回。 下列範例將說明這點。  
  
 [!code-vb[VbVbalrOperators#68](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#68)]  
  
 在上述範例中， `TypeOf x Is Control` 運算式會評估為 `True` ，因為的類型 `x` 是 `Button` ，它會繼承自 `Control` 。  
  
 如需詳細資訊，請參閱[TypeOf 運算子](../../../language-reference/operators/typeof-operator.md)。  
  
## <a name="see-also"></a>另請參閱

- [數值比較](value-comparisons.md)
- [比較運算子](../../../language-reference/operators/comparison-operators.md)
- [運算子](../../../language-reference/operators/index.md)
- [Visual Basic 的算術運算子](arithmetic-operators.md)
- [Visual Basic 中的串連運算子](concatenation-operators.md)
- [Visual Basic 中的邏輯運算子和位元運算子](logical-and-bitwise-operators.md)
