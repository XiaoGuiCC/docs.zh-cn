---
title: /quiet
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: devlang-visual-basic
ms.topic: article
f1_keywords:
- /quiet
- quiet
helpviewer_keywords:
- -quiet compiler option [Visual Basic]
- /quiet compiler option [Visual Basic]
- quiet compiler option [Visual Basic]
ms.assetid: 5d77fa23-4c50-4708-8535-649912b098e8
caps.latest.revision: "11"
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: 3b816cadb9d805d57a14e9b5df553654dd8167af
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="quiet"></a>/quiet
阻止编译器显示与语法相关的错误和警告的代码。  
  
## <a name="syntax"></a>语法  
  
```  
/quiet  
```  
  
## <a name="remarks"></a>备注  
 默认情况，`/quiet` 是无效的。 当编译器报告与语法相关的错误或警告时，它还将输出从源代码行。 对于应用程序分析编译器输出，它可能会更方便编译器输出的诊断的文本。  
  
 在下面的示例中，`Module1`输出包括源代码，而无需在编译时错误`/quiet`。  
  
```  
Module Module1  
    Sub Main()  
        x()  
    End Sub  
End Module  
```  
  
 输出：  
  
 `E:\test\t2.vb(3) : error BC30451: Name 'x' is not declared.`  
  
 `x`  
  
 `~`  
  
 使用编译`/quiet`，则编译器输出仅如下：  
  
 `E:\test\t2.vb(3) : error BC30451: Name 'x' is not declared.`  
  
> [!NOTE]
>  `/quiet`选项不是可从 Visual Studio 开发环境中; 仅当从命令行进行编译时，它才可用。  
  
## <a name="example"></a>示例  
 下面的代码编译`T2.vb`并且不显示与语法相关编译器诊断的代码：  
  
```  
vbc /quiet t2.vb  
```  
  
## <a name="see-also"></a>另请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)  
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
