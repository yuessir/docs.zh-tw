---
title: 標準控制項的 UI 自動化支援
description: 取得針對 Windows Presentation Foundation （WPF）、Win32 和 Windows Forms 所開發的應用程式中，標準控制項的 UI 自動化支援的相關資訊。
ms.date: 03/30/2017
helpviewer_keywords:
- controls, UI Automation support for
- UI Automation, support for standard controls
ms.assetid: 3770ea8a-2655-4add-9c59-fe0610ad5084
ms.openlocfilehash: 17916a6978008439e91caae00d8b6f26045f9018
ms.sourcegitcommit: 87cfeb69226fef01acb17c56c86f978f4f4a13db
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2020
ms.locfileid: "87166115"
---
# <a name="ui-automation-support-for-standard-controls"></a>標準控制項的 UI 自動化支援
> [!NOTE]
> 這份文件適用於想要使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 命名空間中定義之 Managed <xref:System.Windows.Automation> 類別的 .NET Framework 開發人員。 如需 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]的最新資訊，請參閱 [Windows Automation API：UI 自動化](/windows/win32/winauto/entry-uiauto-win32)。  
  
 本主題包含針對 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] 、Win32 和 Windows Forms 架構所開發之應用程式中的標準控制項支援的相關資訊。  
  
<a name="Windows_Presentation_Foundation_Controls"></a>
## <a name="windows-presentation-foundation-controls"></a>Windows Presentation Foundation 控制項  
 提供資訊或支援使用者互動的所有 [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] 控制項項目，都有 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]的完整原生支援。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]看不見其他如面板等的項目。  
  
<a name="Win32_Controls"></a>
## <a name="win32-controls"></a>Win32 控制項  
 大部分的 Win32 控制項都會 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 透過 UIAutomationClientsideProviders.dll 中的用戶端提供者公開至。 此組件會自動註冊為用於使用者介面自動化用戶端應用程式。  
  
 僅針對第6版*ComCtrl32.dll*的控制項提供完整支援。  
  
 支援的控制項如下。  
  
|類別名稱|控制項類型|  
|----------------|------------------|  
|Button|Button|  
|Button|RadioButton|  
|按鈕|群組|  
|按鈕|CheckBox|  
|按鈕|Hyperlink|  
|按鈕|SplitButton|  
|按鈕|CheckBox|  
|ComboBoxEx32|ComboBox|  
|ComboBox|ComboBox|  
|編輯|Document|  
|編輯|編輯|  
|SysLink|Hyperlink|  
|靜態|Text|  
|靜態|映像|  
|SysIPAddress32|自訂|  
|SysHeader32|Header/HeaderItem|  
|SysListView32|DataGrid|  
|SysListView32|清單|  
|ListBox|清單|  
|ListBox|ListItem|  
|#32768|功能表|  
|#32768|MenuItem|  
|msctls_progress32|進度列|  
|RichEdit|文件。 請參閱附註。|  
|RichEdit20A|Document|  
|RichEdit20W|Document|  
|RichEdit50W|Document|  
|ScrollBar|滑桿|  
|msctls_trackbar32|滑桿|  
|msctls_updown32|Spinner|  
|msctls_statusbar32|StatusBar|  
|SysTabControl32|索引標籤|  
|SysTabControl32|TabItem|  
|ToolbarWindow32|ToolBar|  
|ToolbarWindow32|MenuItem|  
|ToolbarWindow32|按鈕|  
|ToolbarWindow32|CheckBox|  
|ToolbarWindow32|RadioButton|  
|ToolbarWindow32|Separator|  
|tooltips_class32|ToolTip|  
|#32774|ToolTip|  
|ReBarWindow32|工具列|  
|SysTreeView32|樹狀結構|  
|SysTreeView32|TreeItem|  
  
 **注意**只有 Windows Vista 隨附的版本（RichEd20.dll 3.1 版和更新版本，以及 MsftEdit.dll 4.1 版和更新版本）才支援 RichEdit 控制項。  
  
 不支援的控制項如下。  
  
|類別名稱|控制項類型|  
|----------------|------------------|  
|SysAnimate32|映像|  
|SysPager|Spinner|  
|SysDateTimePick32|自訂|  
|SysMonthCal32|行事曆|  
|MS_WINNOTE|工具提示|  
|VBBubble|工具提示|  
|ScrollBar (當做獨立控制項使用時)|滑桿|  
|SuperGrid|自訂|  
  
<a name="Windows_Forms_Controls"></a>
## <a name="windows-forms-controls"></a>Windows Form 控制項  
 Windows Forms 控制項會 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 透過 UIAutomationClientsideProviders.dll 中的用戶端提供者公開至。 此組件會自動註冊為用於使用者介面自動化用戶端應用程式。  
  
 一般來說，支援 Win32 通用控制項的 managed 包裝函式 Windows Forms 控制項 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 。 支援的控制項如下。  
  
|類別名稱|  
|----------------|  
|按鈕|  
|CheckBox|  
|CheckedListBox|  
|ColorDialog|  
|ComboBox|  
|FolderBrowser|  
|FontDialog|  
|GroupBox|  
|HscrollBar|  
|ImageList|  
|標籤|  
|ListBox|  
|ListView|  
|MainMenu/ContextMenu|  
|MonthCalendar|  
|NotifyIcon|  
|OpenFileDialog|  
|PageSetupDialog|  
|PrintDialog|  
|進度列|  
|RadioButton|  
|RichTextBox|  
|SaveFileDialog|  
|ScrollableControl|  
|SoundPlayer|  
|StatusBar|  
|TabControl/TabPage|  
|TextBox|  
|計時器|  
|工具列|  
|ToolTip|  
|TrackBar|  
|TreeView|  
|VscrollBar|  
|WebBrowser|  
  
 下列控制項 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 只會透過其 Microsoft Active Accessibility 的支援來公開。 部分功能可能無法使用。  
  
|控制項名稱|  
|------------------|  
|BindingSource|  
|DataGrid|  
|DataGridView|  
|DataNavigator|  
|DomainUpDown|  
|ErrorProvider|  
|FlowLayoutPanel|  
|表單|  
|LinkLabel|  
|HelpProvider|  
|MaskedTextBox|  
|MenuStrip/ContextMenuStrip|  
|NumericUpDown|  
|面板|  
|PictureBox|  
|PrintDocument|  
|PrintPreview-Control|  
|PrintPreview-Dialog|  
|PropertyGrid|  
|UserControl|  
|ToolStrip|  
|TableLayoutPanel|  
|SplitContainer/SplitterPanel|  
|Splitter|  
|RaftingContainer|  
|StatusStrip|  
  
## <a name="see-also"></a>另請參閱

- [UI 自動化控制項類型](ui-automation-control-types.md)
