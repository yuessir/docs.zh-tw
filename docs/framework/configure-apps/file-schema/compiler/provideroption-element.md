---
title: <providerOption> 項目
ms.date: 03/30/2017
f1_keywords:
- provideroption
helpviewer_keywords:
- <provideroption> element
- providerOptions
- provideroption element
ms.assetid: 014f2e0b-c0b5-4fc4-92d3-73f02978b2a1
ms.openlocfilehash: c8ba5b9a0680f5e5102c13eb5bb0c1904a168c07
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "79155397"
---
# <a name="provideroption-element"></a>\<providerOption> 項目
指定語言提供者的編譯器版本屬性。  

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.codedom>**](system-codedom-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<compilers>**](compilers-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<compiler>**](compiler-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<providerOption>**

## <a name="syntax"></a>語法  
  
```xml  
<providerOption  
  name="option-name"  
  value="option-value"  
/>  
```  
  
## <a name="attributes-and-elements"></a>屬性和項目  
 下列章節說明屬性、子元素和父元素。  
  
### <a name="attributes"></a>屬性  
  
|屬性|描述|  
|---------------|-----------------|  
|`name`|必要屬性。<br /><br /> 指定選項的名稱;例如，"CompilerVersion"。|  
|`value`|必要屬性。<br /><br /> 指定選項的值。例如，"v 3.5"。|  
  
### <a name="child-elements"></a>子元素  
 無。  
  
### <a name="parent-elements"></a>父項目  
  
|元素|描述|  
|-------------|-----------------|  
|[\<configuration>元素](../configuration-element.md)|Common Language Runtime 與 .NET Framework 應用程式使用的所有組態檔中的根項目。|  
|[\<system.codedom>元素](system-codedom-element.md)|指定可用語言提供者的編譯器組態設定。|  
|[\<compilers>元素](compilers-element.md)|編譯器設定元素的容器;包含零個或多個 `<compiler>` 元素。|  
|[\<compiler>元素](compiler-element.md)|指定語言提供者的編譯器組態屬性。|  
  
## <a name="remarks"></a>備註  
 在 .NET Framework 版本3.5 中，程式碼檔物件模型（CodeDOM）程式碼提供者可以使用專案來支援提供者特定選項 `<providerOption>` 。  
  
 .NET Framework 3.5 包含更新的 .NET Framework 2.0 元件，並提供新的版本3.5 元件，其中包含新的類型。 Microsoft c # 和 Visual Basic 程式碼提供者包含在 .NET Framework 2.0 元件中，但已更新為支援3.5 版編譯器。 根據預設，更新後的程式碼提供者會產生2.0 版編譯器的程式碼。 您可以使用 `<providerOption>` 元素，將目標編譯器版本變更為3.5。 若要這麼做，請為屬性指定 "CompilerVersion"， `name` 並為屬性指定 "v 3.5" `value` 。 您必須在版本號碼之前加上小寫的 "v"。  
  
 您可以藉由將專案新增 `<providerOption>` 至 .NET Framework 2.0 machine.config 或根 web.config 檔案，將版本規格設為全域。 如果您在 Machine.config 檔案中將預設的編譯器版本更新為3.5，則可以使用 `<providerOption>` 應用程式佈建檔中的專案，以每個應用程式為基礎，將它變更回2.0。  
  
 CodeDOM 程式碼提供者實作者可以藉由提供採用類型參數的函式，來處理自訂選項 `providerOptions` <xref:System.Collections.Generic.IDictionary%602> 。  
  
## <a name="example"></a>範例  
 下列範例示範如何指定應該使用 c # 程式碼提供者的3.5 版。  
  
```xml  
<configuration>  
  <system.codedom>  
    <compilers>  
      <!-- zero or more compiler elements -->  
      <compiler  
        language="c#;cs;csharp"  
        extension=".cs"  
        type="Microsoft.CSharp.CSharpCodeProvider, System,
          Version=2.0.3600.0, Culture=neutral,
          PublicKeyToken=b77a5c561934e089"  
        compilerOptions="/optimize"  
        warningLevel="1" >  
          <providerOption  
            name="CompilerVersion"  
            value="v3.5" />  
      </compiler>  
    </compilers>  
  </system.codedom>  
</configuration>  
```  
  
## <a name="see-also"></a>另請參閱

- <xref:System.CodeDom.Compiler.CompilerInfo>
- <xref:System.CodeDom.Compiler.CodeDomProvider>
- [設定檔架構](../index.md)
- [\<compilers>元素](compilers-element.md)
- [指定完整的類型名稱](../../../reflection-and-codedom/specifying-fully-qualified-type-names.md)
- [編譯之編譯器的 compiler 項目 (ASP.NET 設定結構描述)](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/a15ebt6c(v=vs.100))
