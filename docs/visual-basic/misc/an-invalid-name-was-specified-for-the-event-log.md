---
title: 指定給事件記錄檔的名稱無效
ms.date: 07/20/2015
ms.assetid: b1b158bd-f13f-4371-a8af-31c0e86ae6be
ms.openlocfilehash: 70b1de2a3776a9c68260cc431b65e754d7247a0c
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84412919"
---
# <a name="an-invalid-name-was-specified-for-the-event-log"></a>指定給事件記錄檔的名稱無效
指定給事件記錄檔的名稱無效。 這通常是名稱中有無效的字元、檔案名稱空白或檔案名稱太長的結果。  
  
## <a name="to-correct-this-error"></a>更正這個錯誤  
  
- 如果指定的名稱超過八個字元，請確定該名稱未與其他事件記錄檔的名稱相衝突。 判斷此名稱是否唯一時，只會評估前八個字元。  
  
- 如果提供路徑，請確定已正確地剖析該路徑。  
  
- 檢查名稱中沒有無效的字元。 不能在檔案名稱中使用的字元包括 `<`、 `>`、 `:`、 `"`、 `/`、 `\`和 `|`。  
  
## <a name="see-also"></a>另請參閱

- [作法：剖析檔案路徑](../developing-apps/programming/drives-directories-files/how-to-parse-file-paths.md)
- [作法：重新命名檔案](../developing-apps/programming/drives-directories-files/how-to-rename-a-file.md)
