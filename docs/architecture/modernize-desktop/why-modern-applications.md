---
title: 使用現代化傳統型應用程式的理由
description: 深入瞭解桌上型電腦技術，例如 Windows Forms、WPF 和 UWP 的現代化世界。
ms.date: 09/16/2019
ms.openlocfilehash: f8b70ba9e0ee97a6e0938e3219ecd0d2324248ae
ms.sourcegitcommit: 9a4488a3625866335e83a20da5e9c5286b1f034c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/15/2020
ms.locfileid: "83423275"
---
# <a name="why-modern-desktop-applications"></a>使用現代化傳統型應用程式的理由

## <a name="introduction"></a>簡介

### <a name="a-story-of-one-company"></a>一家公司的故事

回到早期2000s，一家跨國公司開始開發分散式桌面解決方案，在公司不同分支之間交換資訊，並對集中式單元執行優化作業。 他們選擇了稱為 Windows Forms 的全新架構（也稱為 WinForms）來開發應用程式。 多年來，此專案已發展成成熟、經過妥善測試且經過時間證明的應用程式，包含數十萬行程式碼。 經過時間和 .NET Framework 2.0 已不再是最新的技術。 正在處理此應用程式的開發人員面臨困境。 他們想要在開發中使用最新的技術堆疊，並讓其應用程式看起來和「感覺」現代化。 同時，他們不想要捨棄已建立超過15年的絕佳產品，並從頭重新撰寫整個應用程式。

### <a name="your-story"></a>您的故事

您可能會在同一個船裡發現自己，其中有成熟的 Windows Forms 或 Windows Presentation Foundation （WPF）應用程式，已證明其在多年的可靠性。 您可能想要繼續使用這些應用程式數年。 同時，由於這些應用程式是在一段時間之前撰寫的，因此可能遺失現代化外觀、效能、與新裝置和平臺功能的整合等等的功能，讓他們覺得「舊科技」。 還有另一個問題，就是開發人員可能會擔心。 在處理舊版的 .NET Framework 版本和維護在一段時間之前撰寫的應用程式時，您可能會覺得不會學習新技術，也不會在建立現代化技術技能時遺失。 如果這是您的故事–這本書是您的經驗！

## <a name="desktop-applications-nowadays"></a>桌面應用程式現今

在引發網際網路之前，桌面應用程式是建立軟體系統的主要方法。 開發人員可以選擇任何程式設計語言，例如 COBOL、Fortran、VB6 或 c + +。 但他們在開發小型工具或複雜的分散式架構時，全都是桌面應用程式。

然後，網際網路技術開始驚人開發環境，並透過簡單的部署和簡化的散發程式，贏得更多更多工程師的優勢。 事實上，一旦 web 應用程式部署到生產環境，所有使用者都會獲得自動更新，對軟體的靈活性造成巨大的影響。

不過，網際網路基礎結構、基礎通訊協定和標準（例如 HTTP 和 HTML）不是設計來建立複雜的應用程式。 事實上，主要的開發工作其實只是一個目標：為 web 應用程式提供桌面應用程式所擁有的相同功能，例如快速的資料輸入和狀態管理。

雖然 web 和行動應用程式的步調日益增加，但在某些工作中，桌面應用程式仍會在效率和效能方面保留一個位置。 這就是為什麼有數百萬名開發人員使用 WPF 和 WinForms 建立專案，而這些應用程式的數量不斷成長。

以下是在您的開發中選擇桌面應用程式的一些原因：

- 桌面應用程式與使用者的電腦有更好的互動。
- 複雜計算的桌面應用程式效能遠高於 web 應用程式的效能。
- 在用戶端上執行自訂邏輯是可行的，但與 web 應用程式比較困難。
- 在桌面應用程式中使用多執行緒比較簡單且更有效率。
- 設計使用者介面（Ui）的學習曲線並不會太陡。 而對於 WinForms 而言，使用 Windows Forms 設計工具的拖放體驗，完全直覺化。
- 在不需要設定伺服器基礎結構，或是在意連線問題、防火牆和瀏覽器相容性的情況下，很容易就能開始編碼和測試您的演算法。
- 相較于 web 調試，調試功能強大。
- 對硬體裝置（例如相機、藍牙或卡片讀取器）的存取很容易。
- 因為此技術已有一段時間，所以有許多專家和知識庫可供開發桌面應用程式之用。

因此，如您所見，針對桌面開發是很好的原因。 這項技術已成熟且經過時間測試，開發週期很快，偵錯工具功能強大且有能力，而桌面應用程式的複雜性較少，而且可以更輕鬆地開始使用。

Microsoft 提供許多 UI 桌面技術，從1995引進的 Win32 到2016年發行的通用 Windows 平臺（UWP）。

![Microsoft 桌面技術](./media/why-modern-applications/microsoft-desktop-technologies.png)

根據 Telerik 在2016年4月發行的問卷，建立 Windows 傳統型應用程式最熱門的技術是 Windows Forms、WPF 和 UWP。

![Telerik 問卷，顯示 Windows Forms、WPF 和 UWP 做為最熱門的桌面技術](./media/why-modern-applications/telerik-survey.png)

您可以使用 c # 和 Visual Basic 在其中之一進行開發，但讓我們進一步瞭解。

### <a name="windows-forms"></a>Windows Forms

第一次發行于2002，Windows Forms 是受控架構，而且是以 Windows 圖形裝置介面（GDI）引擎為基礎的最舊、最常使用的桌面技術。 它提供了在 Visual Studio 中開發使用者介面的順暢拖放體驗。  同時，Windows Forms 依賴 Visual Studio 的設計工具做為開發 UI 的主要方式，因此從程式碼建立視覺元件並不簡單。

下列清單摘要說明 Windows Forms 的主要特性：

- 成熟的技術，其中包含許多程式碼範例和檔。
- 功能強大且具生產力的設計工具。 設計 UI 「從程式碼」並不方便。
- 學習設計工具的拖放體驗，以輕鬆且直覺的方式學習。
- 在任何 Windows 版本上都支援。
- 支援 .NET Core 3.0 和更新版本。

### <a name="wpf"></a>WPF

WPF 會根據 XAML 語言規格，讓 UI 與程式碼之間有清楚的分隔。 XAML 提供了諸如範本、樣式和系結等功能，適合用來建立大型應用程式。 如同 Windows Forms，它是受控架構，但設計是模組化且可重複使用。

以下是 WPF 的主要功能：

- 成熟的技術。
- 設計師可供使用，但是開發人員通常會偏好使用宣告式 XAML，從程式碼建立設計。
- 學習曲線的較陡峭會比 Windows Forms。
- 在任何 Windows 版本上都支援。
- 支援 .NET Core 3.0 和更新版本。

### <a name="uwp"></a>UWP

UWP 不只是 WPF 和 Windows Forms 這類展示架構，也是平臺本身。 此平臺具有：

- 它自己的 API 集合（Windows 執行階段 API）。
- 新的部署系統（MSIX）
- 現代化的應用程式生命週期模型（適用于低電量的電池耗用量）。
- 新的資源管理系統（根據 PRI 檔案）。

平臺的建立是為了支援各種類型的輸入系統（像是筆墨、觸控、遊戲台、滑鼠、鍵盤、注視等），並考慮效能和低電池耗用量的所有形式因素。 基於這些理由，Windows 10 OS 的 shell 會使用 UWP 平臺的元件。

![UWP 結構](./media/why-modern-applications/uwp-structure.png)

UWP 包含以 XAML 為基礎的呈現架構（例如 WPF），但有一些重要的差異，例如：

- 應用程式會在應用程式容器中執行。 應用程式容器可控制 UWP 應用程式可以存取的資源。
- 僅在 Windows 10 上支援。
- 您可以透過 Microsoft Store 部署應用程式，以更輕鬆地進行部署。
- 設計為 Windows 執行階段 API 的一部分。
- 包含一組廣泛的豐富內建控制項，以及可透過每幾個月更新的 Microsoft UI 程式庫 NuGet 套件（WinUI Library）提供的其他控制項。

## <a name="a-tale-of-two-platforms"></a>兩個平臺的故事

過去20年來，當 UI 桌面技術不斷成長，並遵循從 Windows Forms 到 UWP 的路徑時，硬體也會從具有小型 CRT 監視器的權數電腦單位演變到高 DPI 監視器，以及具有不同資料輸入技術（例如觸控和筆跡）的輕量平板電腦和手機。 這些變更會導致建立兩個不同的概念：桌面應用程式和現代化應用程式。 現代化應用程式是一種，它會考慮不同的裝置外型規格、各種輸入和輸出方法，並在沙箱執行模型上執行時運用新式桌面功能。 另一方面，（傳統）傳統型應用程式是一種應用程式，它需要具有高密度控制項的穩固 UI，且最適合使用滑鼠和鍵盤操作。

下表描述兩個概念之間的差異：

|   | 現代化應用程式 | 桌面應用程式 |
| --- | --- | --- |
| 安全性 | 包含執行 &amp; 的絕佳基本概念。 專門設計來尊重使用者的隱私權、管理電池壽命，以及專注于保護裝置安全。  | 使用者系統 &amp; 管理員的安全性層級。 您具有登錄和硬碟資料夾的原生存取權。 |
| 部署 | 安裝和更新是由平臺所管理。   | MSI，自訂安裝 &amp; 程式會更新。 傳統上，開發人員和 IT 管理員的問題來源是一項難題。  |
| 發佈 | 信任 &amp; 的散發已簽署套件。 散發是從信任的來源執行，而不是從 web。  | Web、SCCM &amp; 自訂散發。 無法控制安裝的內容，會影響整台機器。   |
| UI | 新式 UI。 不同的輸入機制、筆墨、觸控、遊戲台、鍵盤、滑鼠等。  | Windows Forms，WPF，MFC。 專為適用于密集 UI 的滑鼠和鍵盤而設計，可從桌面取得最高的生產力。  |
| 資料 | 雲端優先資料與深入解析。 雲端中的真實來源。 深入瞭解您的應用程式會發生什麼情況，以及它的執行方式。  | 本機資料。 傳統的桌面應用程式通常需要一些本機資料。  |
| 設計 | 專為重複使用而設計。 在不同平臺、前端和後端之間重複使用，盡可能在許多地方執行資產。  | 僅適用于 Windows 桌面  |

為了讓開發人員能夠建立應用程式的最佳工具，Microsoft 致力於將這些概念放在一起，也就是讓開發人員更清楚地瞭解平臺，以提供最大的優勢。 為了達到此目的，Microsoft 在兩個平臺之間執行了雙向的工作。

![現代化應用程式與桌面應用程式之間的雙向成果](./media/why-modern-applications/bidirectional-effort.png)

1. 將桌面應用程式案例移到現代化應用程式平臺。 傳統的桌面開發仍然很熱門，因為它能解決特定案例的狀況。 採用這些常見的桌上型電腦案例，並將它們帶入現代化桌面平臺，讓平臺具備完整的功能。

    ![將桌面應用程式案例移到現代化應用程式平臺](./media/why-modern-applications/desktop-to-modern.png)

1. 將現代化應用程式功能移至桌面應用程式。 若現有的桌面應用程式需要一種方式來運用現代化功能，而不需從頭重新撰寫，則新式應用程式平臺的功能會被推送到桌面應用程式。

    ![將現代化應用程式功能移至桌面應用程式](./media/why-modern-applications/modern-to-desktop.png)

在本書中，我們將著重于第二個部分，並示範如何將現有的桌面應用程式現代化。

## <a name="paths-to-modernization"></a>現代化的路徑

本指南的結構反映了三個不同的軸來完成現代化：現代化功能、部署和安裝。

### <a name="modern-features"></a>現代化功能

假設您有一個可運作的 Windows Forms 應用程式，您公司的銷售代表會用它來填寫客戶訂單。 有一項新的需求可讓客戶使用 tablet 畫筆來簽署訂單。 在現今的作業系統和技術中，手寫功能是原生的，但在開發應用程式時無法使用。

此路徑會向您示範如何將新式桌面功能運用在現有的桌面開發中。

### <a name="deployment"></a>部署

現代化的開發週期已經有更多的壓力，可以讓您靈活地瞭解如何將新版本的應用程式部署到每一位使用者。 由於 Windows Forms 和 WPF 應用程式是以必須存在於電腦上的特定 .NET Framework 版本為基礎，因此無法利用新的 .NET Framework 版本功能，而不需要 IT 人員介入的風險，也就是在相同電腦上執行的其他應用程式有副作用。 它的創新步調有限，可讓開發人員隨時掌握過時的 .NET Framework 版本。

自 .NET Core 3.0 推出之後，您可以利用新的方法來並行部署多個版本的 .NET Core，並指定每個應用程式應該設為目標的 .NET Core 版本。 如此一來，您就可以在某個應用程式中使用最新的功能，同時相信您不會中斷任何其他應用程式。

### <a name="installation"></a>安裝

桌面應用程式一律會依賴某種安裝流程，使用者才可以開始使用它們。 這個事實帶給遊戲一組技術，從 MSI 和 ClickOnce 到自訂安裝程式，甚至是 XCOPY 部署。 其中任何一種方法都會處理精密的問題，因為應用程式需要一種方法來存取電腦上的共用資源。 有時候安裝需要存取登錄來插入或更新新的索引鍵值，有時會更新主要應用程式所參考的共用 Dll。 這會造成使用者的困擾，因為您在安裝某些應用程式之後，您的電腦永遠不會相同，即使您之後卸載也一樣。

在本書中，我們將介紹使用 MSIX 來安裝應用程式的新方式，以解決先前所述的問題。 您將瞭解如何輕鬆地為您的應用程式設定封裝、安裝和更新。

>[!div class="step-by-step"]
>[上一個](index.md) 
>[下一步](whats-new-dotnet-core.md)
