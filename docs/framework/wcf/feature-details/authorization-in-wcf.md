---
title: WCF 的授權
ms.date: 03/30/2017
helpviewer_keywords:
- authorization [WCF]
- security [WCF], authorization
ms.assetid: 8ea0b552-af65-45b0-a157-c6c111b8ce5e
ms.openlocfilehash: d67d64dcf0003de28775ac947f8b5f72d7c2ba2a
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84597627"
---
# <a name="authorization-in-wcf"></a>WCF 的授權
授權是控制資源 (例如服務或檔案) 存取與權限的程序。 本節中的主題說明如何以各種方式在 Windows Communication Foundation （WCF）中執行這項基本工作。  
  
## <a name="in-this-section"></a>本節內容  
 [存取控制機制](access-control-mechanisms.md)  
 提供 WCF 中授權機制的簡要概述，以及建議的用法。  
  
 [如何：利用 PrincipalPermissionAttribute 類別限制存取](../how-to-restrict-access-with-the-principalpermissionattribute-class.md)  
 示範限制存取具有 之服務的程序。  
  
 [HOW TO：使用 ASP.NET 角色提供者搭配服務](how-to-use-the-aspnet-role-provider-with-a-service.md)  
 逐步解說服務的設定，讓它能夠使用 ASP.NET 的角色提供者功能。  
  
 [如何：使用 ASP.NET 授權管理員角色提供者搭配服務](how-to-use-the-aspnet-authorization-manager-role-provider-with-a-service.md)  
 ASP.NET 可以使用 [授權管理員] 來管理網站的授權。 WCF 也可以利用 ASP.NET/Authorization Manager 組合來授權用戶端。  
  
 [使用身分識別模型來管理宣告與授權](managing-claims-and-authorization-with-the-identity-model.md)  
 解釋對宣告型授權使用「識別模型」基礎結構的基本概念。  
  
 [委派和模擬](delegation-and-impersonation-with-wcf.md)  
 解釋委派與模擬之間的差異。  
  
## <a name="reference"></a>參考  
 <xref:System.ServiceModel.Security>  
  
 <xref:System.ServiceModel.Description.PrincipalPermissionMode>  
  
 <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior>  
  
 <xref:System.Security.Permissions.PrincipalPermissionAttribute>  
  
## <a name="related-sections"></a>相關章節  
 [驗證](authentication-in-wcf.md)  
  
## <a name="see-also"></a>請參閱

- [安全性總覽](security-overview.md)
- [Windows Server AppFabric 的資訊安全模型](https://docs.microsoft.com/previous-versions/appfabric/ee677202(v=azure.10))
