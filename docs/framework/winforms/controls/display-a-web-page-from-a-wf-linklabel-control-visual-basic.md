---
title: "如何：通过 Windows 窗体 LinkLabel 控件显示网页 (Visual Basic)"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-winforms
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: vb
f1_keywords: LinkLabel1_LinkClicked
helpviewer_keywords:
- examples [Windows Forms], LinkLabel control
- Web pages [Windows Forms], displaying
- linking [Windows Forms], to Web pages from forms
- Windows Forms, linking to Web pages
- LinkLabel control [Windows Forms], examples
ms.assetid: 477a7398-5971-4de3-b24c-f49f32bdb28a
caps.latest.revision: "7"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: 38ef165dc655fedbf682a21220d6a76532b18f6a
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="how-to-display-a-web-page-from-a-windows-forms-linklabel-control-visual-basic"></a>如何：通过 Windows 窗体 LinkLabel 控件显示网页 (Visual Basic)
此示例在默认浏览器中显示网页，用户单击 Windows 窗体时<xref:System.Windows.Forms.LinkLabel>控件。  
  
## <a name="example"></a>示例  
  
```vb  
Private Sub Form1_Load(ByVal sender As System.Object, ByVal e _  
As System.EventArgs) Handles MyBase.Load  
    LinkLabel1.Text = "Click here to get more info."  
    LinkLabel1.Links.Add(6, 4, "www.microsoft.com")  
End Sub  
Private Sub LinkLabel1_LinkClicked(ByVal sender As System.Object, ByVal _  
e As System.Windows.Forms.LinkLabelLinkClickedEventArgs) Handles _  
LinkLabel1.LinkClicked  
    System.Diagnostics.Process.Start(e.Link.LinkData.ToString())  
End Sub  
```  
  
## <a name="compiling-the-code"></a>编译代码  
 此示例需要：  
  
-   名为 Windows 窗体`Form1`。  
  
-   名为 `LinkLabel1` 的 <xref:System.Windows.Forms.LinkLabel> 控件。  
  
-   有效的 Internet 连接。  
  
## <a name="net-framework-security"></a>.NET Framework 安全性  
 调用<xref:System.Diagnostics.Process.Start%2A>方法要求完全信任。 有关更多信息，请参见<xref:System.Security.SecurityException>。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Windows.Forms.LinkLabel>  
 [LinkLabel 控件](../../../../docs/framework/winforms/controls/linklabel-control-windows-forms.md)
