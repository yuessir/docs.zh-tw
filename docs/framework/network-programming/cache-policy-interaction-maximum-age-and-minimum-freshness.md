---
title: 快取原則互動 — 最長使用期限和最小有效期限
ms.date: 03/30/2017
helpviewer_keywords:
- time-based cache policies
- Revalidate policy
- cache [.NET Framework], time-based policies
- freshness of cached resources
- maximum age policy
- minimum freshness policy
- age of cached resources
ms.assetid: 6567d451-ecec-496c-95a3-a415b99ba52a
ms.openlocfilehash: 2ec958cc035ac62086cdd3e2844811accc181d47
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/15/2020
ms.locfileid: "71048807"
---
# <a name="cache-policy-interactionmaximum-age-and-minimum-freshness"></a>快取原則互動 — 最長使用期限和最小有效期限
為了協助確保將最新內容傳回給用戶端應用程式，用戶端快取原則與伺服器重新驗證需求的互動一律會導致最保守的快取原則。 本主題中的所有範例都會說明在 1 月 1 日快取並在 1 月 4 日到期之資源的快取原則。  
  
 下列範例說明最長使用期限 (`maxAge`) 與最小有效期限 (`minFresh`) 值的互動所造成的快取原則。  
  
- 如果快取原則設定 `maxAge` = 2 天，但未指定 `minFresh`，則會在 1 月 3 日重新驗證內容。  
  
- 根據 `maxAge`，如果快取原則設定 `maxAge` = 2 天且 `minFresh` = 1 天，則會在 1 月 3 日之前整理內容。 根據 `minFresh`，會在 1 月 3 日之前整理內容。 因此，必須在 1 月 3 日重新驗證內容。  
  
- 根據 `maxAge`，如果快取原則設定 `maxAge` = 2 天且 `minFresh` = 2 天，則會在 1 月 3 日之前整理內容。 根據 `minFresh`，會在 1 月 2 日之前整理內容。 因此，必須在 1 月 2 日重新驗證內容。  
  
## <a name="see-also"></a>另請參閱

- [網路應用程式的快取管理](cache-management-for-network-applications.md)
- [緩存策略](cache-policy.md)
- [以位置為基礎的快取原則](location-based-cache-policies.md)
- [Time-Based Cache Policies](time-based-cache-policies.md)
- [設定網路應用程式的快取功能](configuring-caching-in-network-applications.md)
- [快取原則互動 — 最長使用期限和最長過時](cache-policy-interaction-maximum-age-and-maximum-staleness.md)
