---
ms.openlocfilehash: d75dc2caa3a002b9d34ac74f2c5c5e192281c0df
ms.sourcegitcommit: 97ce5363efa88179dd76e09de0103a500ca9b659
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/13/2020
ms.locfileid: "86281290"
---
### <a name="default-activityidformat-is-w3c"></a>預設 ActivityIdFormat 為 W3C

活動 () 的預設識別碼格式 <xref:System.Diagnostics.Activity.DefaultIdFormat?displayProperty=nameWithType> 現在為 <xref:System.Diagnostics.ActivityIdFormat.W3C?displayProperty=nameWithType> 。

#### <a name="change-description"></a>變更描述

W3C 活動識別碼格式是在 .NET Core 3.0 中引進，做為階層式識別碼格式的替代方式。 不過，若要保留相容性，W3C 格式不會在 .NET 5.0 之前設為預設值。 .NET 5.0 中的預設值已變更，因為[W3C 格式已經過](https://www.w3.org/TR/trace-context/)核准，並在多個語言的實現方面獲得吸引力。

如果您的應用程式以非 .NET 5.0 或更新版本的平臺為目標，則會遇到舊的行為，其中 <xref:System.Diagnostics.ActivityIdFormat.Hierarchical> 是預設格式。 這個預設適用于平臺 net45 +、netstandard 1.1 + 和 netcoreapp (1.x、2.x 和 3.x) 。 在 .NET 5.0 和更新版本中， <xref:System.Diagnostics.Activity.DefaultIdFormat?displayProperty=nameWithType> 會設為 <xref:System.Diagnostics.ActivityIdFormat.W3C?displayProperty=nameWithType> 。

#### <a name="version-introduced"></a>引進的版本

5.0 Preview 7

#### <a name="recommended-action"></a>建議的動作

如果您的應用程式與用於分散式追蹤的識別碼無關，則不需要採取任何動作。 程式庫（例如 ASP.NET Core 和） <xref:System.Net.Http.HttpClient> 可以使用或傳播的兩個版本 <xref:System.Diagnostics.ActivityIdFormat> 。

如果您需要與現有系統的互通性，或目前的系統依賴識別碼的格式，您可以將設定為來保留舊的行為 <xref:System.Diagnostics.Activity.DefaultIdFormat> <xref:System.Diagnostics.ActivityIdFormat.Hierarchical?displayProperty=nameWithType> 。 或者，您可以使用下列三種方式之一來設定 AppCoNtext 參數：

- 在專案檔中。

  ```xml
  <ItemGroup>
    <RuntimeHostConfigurationOption Include="System.Diagnostics.DefaultActivityIdFormatIsHierarchial" Value="true" />
  </ItemGroup>
  ```

- 在 [ *runtimeconfig.js*檔案] 中。

  ```json
  {
      "runtimeOptions": {
          "configProperties": {
              "System.Diagnostics.DefaultActivityIdFormatIsHierarchial": true
          }
      }
  }
  ```

- 透過環境變數。

  設定 `DOTNET_SYSTEM_DIAGNOSTICS_DEFAULTACTIVITYIDFORMATISHIERARCHIAL` 為 `true` 或1。

#### <a name="category"></a>類別

Core .NET 程式庫

#### <a name="affected-apis"></a>受影響的 API

- <xref:System.Diagnostics.Activity.DefaultIdFormat?displayProperty=fullName>

<!--

#### Affected APIs

- `P:System.Diagnostics.Activity.DefaultIdFormat`

-->
