---
title: "如何：通过修改 DBML 文件生成自定义代码"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-ado
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 50ad597a-8598-42d3-82dd-fc7d702ebc37
caps.latest.revision: "2"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 743e938df0b9c7f12a9c3a11a4b5558137add529
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="how-to-generate-customized-code-by-modifying-a-dbml-file"></a>如何：通过修改 DBML 文件生成自定义代码
你可以生成[!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)]或 C# 源代码从数据库标记语言 (.dbml) 元数据文件。 此方法提供了一个在生成应用程序映射代码前自定义默认 .dbml 文件的机会。 这是一项高级功能。  
  
 此过程中的步骤如下：  
  
1.  生成 .dbml 文件。  
  
2.  使用编辑器修改此 .dbml 文件。 请注意，此 .dbml 文件必须通过 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] .dbml 文件的架构定义 (.xsd) 文件的验证。 有关详细信息，请参阅[LINQ to SQL 中的代码生成](../../../../../../docs/framework/data/adonet/sql/linq/code-generation-in-linq-to-sql.md)。  
  
3.  生成 [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)] 或 C# 源代码。  
  
 下面的示例使用 SQLMetal 命令行工具。 有关详细信息，请参阅 [SqlMetal.exe（代码生成工具）](../../../../../../docs/framework/tools/sqlmetal-exe-code-generation-tool.md)。  
  
## <a name="example"></a>示例  
 下面的代码从 Northwind 示例数据库生成 .dbml 文件。 您可以使用数据库的名称或 .mdf 文件的名称作为数据库元数据的源。  
  
```  
sqlmetal /server:myserver /database:northwind /dbml:mymeta.dbml  
sqlmetal /dbml:mymeta.dbml mydbfile.mdf  
```  
  
## <a name="example"></a>示例  
 下面的代码从 .dbml 文件生成 [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)] 或 C# 源代码文件。  
  
```  
sqlmetal /namespace:nwind /code:nwind.vb /language:vb DBMLFile.dbml  
sqlmetal /namespace:nwind /code:nwind.cs /language:csharp DBMLFile.dbml  
```  
  
## <a name="see-also"></a>另请参阅  
 [LINQ to SQL 中的代码生成](../../../../../../docs/framework/data/adonet/sql/linq/code-generation-in-linq-to-sql.md)  
 [SqlMetal.exe（代码生成工具）](../../../../../../docs/framework/tools/sqlmetal-exe-code-generation-tool.md)  
 [创建对象模型](../../../../../../docs/framework/data/adonet/sql/linq/creating-the-object-model.md)
