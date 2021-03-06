---
title: HOW TO：加入資料服務參考（WCF Data Services）
ms.date: 08/24/2018
helpviewer_keywords:
- WCF Data Services, configuring
ms.assetid: 62c6f318-3ee1-433a-b7a3-efa234c3034c
ms.openlocfilehash: 42d89cf87b5fe9bbdb229f10cd6a0e340d4c08fd
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/07/2019
ms.locfileid: "70790746"
---
# <a name="how-to-add-a-data-service-reference-wcf-data-services"></a>作法：加入資料服務參考（WCF Data Services）

您可以使用 Visual Studio 中的 [**加入服務參考**] 對話方塊，將參考新增至 WCF Data Services。 這樣可以讓您更輕鬆地在 Visual Studio 開發的用戶端應用程式中存取資料服務。 當您完成此程序時，會根據從資料服務取得的中繼資料產生資料類別。 如需詳細資訊，請參閱[產生資料服務用戶端程式庫](generating-the-data-service-client-library-wcf-data-services.md)。

## <a name="add-a-data-service-reference"></a>加入資料服務參考

1. (選擇性) 如果資料服務不是方案的一部分且尚未執行，請啟動資料服務，並且記下資料服務的 URI。

2. 在 Visual Studio 的**方案總管**中，以滑鼠右鍵按一下用戶端專案，然後選取 [**加入** > **服務參考**]。

3. 如果資料服務是目前方案的一部分，請按一下 [**探索**]。

     -或-

     在 [**位址**] 文字方塊中，輸入資料服務的基底 URL，例如`http://localhost:1234/Northwind.svc`，然後按一下 [**移至**]。

4. 選取 [確定]。

     新的程式碼檔案，其中包含可存取資料服務資源並與之互動的資料類別，會加入至專案。

## <a name="see-also"></a>另請參閱

- [快速入門](quickstart-wcf-data-services.md)
