---
ms.openlocfilehash: 2c8a5c1ec87918a91600a3557c679a42cae74896
ms.sourcegitcommit: b7a8b09828bab4e90f66af8d495ecd7024c45042
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87556321"
---
### <a name="principalpermissionattribute-is-obsolete-as-error"></a>PrincipalPermissionAttribute 已淘汰為錯誤

此函式 <xref:System.Security.Permissions.PrincipalPermissionAttribute> 已過時，並會產生編譯時期錯誤。 您無法具現化此屬性，或將它套用至方法。

#### <a name="change-description"></a>變更描述

在 .NET Framework 和 .NET Core 上，您可以使用屬性來標注方法 <xref:System.Security.Permissions.PrincipalPermissionAttribute> 。 例如：

```csharp
[PrincipalPermission(SecurityAction.Demand, Role = "Administrators")]
public void MyMethod()
{
    // Code that should only run when the current user is an administrator.
}
```

從 .NET 5.0 開始，您無法將 <xref:System.Security.Permissions.PrincipalPermissionAttribute> 屬性套用至方法。 屬性的構造函式已過時，並產生編譯時期錯誤。 不同于其他 obsoletion 警告，您無法隱藏此錯誤。

#### <a name="reason-for-change"></a>變更的原因

類型與子 <xref:System.Security.Permissions.PrincipalPermissionAttribute> 類別的其他類型一樣， <xref:System.Security.Permissions.SecurityAttribute> 是的一部分。NET 的代碼啟用安全性 (CAS) 基礎結構。 在 .NET Framework 2.x-4.x 中， <xref:System.Security.Permissions.PrincipalPermissionAttribute> 即使應用程式是在完全信任的情況下執行，執行時間還是會在方法專案上強制執行注釋。 .NET Core 和 .NET 5.0 和更新版本不支援 CAS 屬性，而執行時間會忽略它們。

從 .NET Framework 到 .NET Core 和 .NET 5.0 的行為差異，可能會導致「失敗開啟」案例，其中的存取權應該已被封鎖，但改為允許。 若要避免「失敗開啟」案例，您無法再于以 .NET 5.0 或更新版本為目標的程式碼中套用屬性。

#### <a name="version-introduced"></a>引進的版本

5.0 Preview 7

#### <a name="recommended-action"></a>建議的動作

如果您遇到 obsoletion 錯誤，則必須採取動作。

- **如果您要將屬性套用至 ASP.NET MVC 動作方法：**

  請考慮使用 ASP。NET 的內建授權基礎結構。 下列程式碼示範如何使用屬性標注控制器 <xref:System.Web.Mvc.AuthorizeAttribute> 。 ASP.NET 執行時間會先授權使用者，然後再執行此動作。

  ```csharp
  using Microsoft.AspNetCore.Authorization;

  namespace MySampleApp
  {
      [Authorize(Roles = "Administrator")]
      public class AdministrationController : Controller
      {
          public ActionResult MyAction()
          {
              // This code won't run unless the current user
              // is in the 'Administrator' role.
          }
      }
  }
  ```

  如需詳細資訊，請參閱[ASP.NET Core 中以角色為基礎的授權](/aspnet/core/security/authorization/roles)和[ASP.NET Core 中的授權簡介](/aspnet/core/security/authorization/introduction)。

- **如果您要將屬性套用至 web 應用程式內容外部的程式庫程式碼：**

  在方法的開頭手動執行檢查。 這可以藉由使用方法來完成 <xref:System.Security.Principal.IPrincipal.IsInRole(System.String)?displayProperty=nameWithType> 。

  ```csharp
  using System.Threading;

  void DoSomething()
  {
      if (Thread.CurrentPrincipal == null
          || !Thread.CurrentPrincipal.IsInRole("Administrators"))
      {
          throw new Exception("User is anonymous or isn't an admin.");
      }

      // Code that should run only when user is an administrator.
  }
  ```

#### <a name="category"></a>類別

- Core .NET 程式庫
- 安全性

#### <a name="affected-apis"></a>受影響的 API

- <xref:System.Security.Permissions.PrincipalPermissionAttribute?displayProperty=fullName>

<!--

#### Affected APIs

- `T:System.Security.Permissions.PrincipalPermissionAttribute`

-->
