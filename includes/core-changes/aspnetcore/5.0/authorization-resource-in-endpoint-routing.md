---
ms.openlocfilehash: 2b88ab7cfdd7a0a0a770b305ecd0200afd9a9b4b
ms.sourcegitcommit: 2543a78be6e246aa010a01decf58889de53d1636
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/17/2020
ms.locfileid: "86441542"
---
### <a name="authorization-resource-in-endpoint-routing-is-httpcontext"></a>授權：端點路由中的資源是 HttpCoNtext

使用 ASP.NET Core 3.1 中的端點路由時，用於授權的資源就是端點。 這種方法不足以取得路由資料（）的存取權 <xref:Microsoft.AspNetCore.Routing.RouteData> 。 先前在 MVC 中， <xref:Microsoft.AspNetCore.Http.HttpContext> 已傳入資源，可讓您存取端點（ <xref:Microsoft.AspNetCore.Http.Endpoint> ）和路由資料。 這種變更可確保傳遞給授權的資源一律為 `HttpContext` 。

#### <a name="version-introduced"></a>引進的版本

5.0 Preview 7

#### <a name="old-behavior"></a>舊的行為

使用端點路由和授權中介軟體（ <xref:Microsoft.AspNetCore.Authorization.AuthorizationMiddleware> ）或[[授權]](xref:Microsoft.AspNetCore.Authorization.AuthorizeAttribute)屬性時，傳遞給授權的資源就是相符的端點。

#### <a name="new-behavior"></a>新的行為

端點路由會將傳遞 `HttpContext` 至授權。

#### <a name="reason-for-change"></a>變更的原因

您可以從取得端點 `HttpContext` 。 不過，沒有任何方法可以從端點取得路由資料之類的專案。 非端點路由中的功能遺失。

#### <a name="recommended-action"></a>建議的動作

如果您的應用程式使用端點資源，請 <xref:Microsoft.AspNetCore.Http.EndpointHttpContextExtensions.GetEndpoint%2A> 在上呼叫 `HttpContext` 以繼續存取端點。

在 ASP.NET Core 5.0 Preview 8 和更新版本中，您可以使用還原成舊的行為 <xref:System.AppContext.SetSwitch%2A> 。 例如：

```csharp
AppContext.SetSwitch(
    "Microsoft.AspNetCore.Authorization.SuppressUseHttpContextAsAuthorizationResource",
    isEnabled: true);
```

#### <a name="category"></a>類別

ASP.NET Core

#### <a name="affected-apis"></a>受影響的 API

無

<!--

#### Affected APIs

Not detectable via API analysis

-->
