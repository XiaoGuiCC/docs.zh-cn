---
title: "如何：调用模型定义的函数作为对象方法"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-ado
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
ms.assetid: 33bae8a8-4ed8-4a1f-85d1-c62ff288cc61
caps.latest.revision: "3"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: a934cd8c122a1564c034f8578e8bad680ba919a6
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="how-to-call-model-defined-functions-as-object-methods"></a>如何：调用模型定义的函数作为对象方法
本主题介绍如何将模型定义函数作为 <xref:System.Data.Objects.ObjectContext> 对象的方法调用或作为自定义类的静态方法调用。 A*模型定义函数*是在概念模型中定义的函数。 本主题中的过程介绍如何直接调用这些函数，而不是从 LINQ to Entities 查询中调用它们。 有关调用模型定义函数中的 LINQ to Entities 查询的信息，请参阅[如何： 在查询中的 Call Model-Defined 函数](../../../../../../docs/framework/data/adonet/ef/language-reference/how-to-call-model-defined-functions-in-queries.md)。  
  
 无论您是将模型定义函数作为 <xref:System.Data.Objects.ObjectContext> 方法调用，还是作为自定义类的静态方法调用，首先都必须使用 <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute> 将该方法映射到模型定义函数。 但是，当您定义 <xref:System.Data.Objects.ObjectContext> 类的方法时，必须使用 <xref:System.Data.Objects.ObjectContext.QueryProvider%2A> 属性公开 LINQ 提供程序，而当您定义自定义类的静态方法时，必须使用 <xref:System.Linq.IQueryable.Provider%2A> 属性公开 LINQ 提供程序。 有关更多信息，请参见下述过程后面的示例。  
  
 下面的这些过程高度概括了将模型定义函数作为 <xref:System.Data.Objects.ObjectContext> 对象的方法调用和作为自定义类的静态方法调用的信息。 后面的示例提供了有关这些过程中各个步骤的更多详细信息。 这些过程假定您在概念模型中定义了一个函数。 有关详细信息，请参阅[如何： 在概念模型中定义自定义函数](http://msdn.microsoft.com/en-us/0dad7b8b-58f6-4271-b238-f34810d68e5f)。  
  
### <a name="to-call-a-model-defined-function-as-a-method-on-an-objectcontext-object"></a>将模型定义函数作为 ObjectContext 对象的方法调用  
  
1.  添加一个源文件，以扩展派生自 <xref:System.Data.Objects.ObjectContext> 类（该类由实体框架工具自动生成）的分部类。 在单独的源文件中定义 CLR 存根可防止在重新生成文件时丢失所做的更改。  
  
2.  将一个公共语言运行时 (CLR) 方法添加到 <xref:System.Data.Objects.ObjectContext> 类，该方法可执行以下操作：  
  
    -   映射到在概念模型中定义的函数。 若要映射方法，必须将 <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute> 应用于此方法。 请注意，此特性的 <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute.NamespaceName%2A> 和 <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute.FunctionName%2A> 参数分别是概念模型的命名空间名称和概念模型中的函数名称。 LINQ 的函数名称解析区分大小写。  
  
    -   返回由 <xref:System.Linq.IQueryProvider.Execute%2A> 属性返回的 <xref:System.Data.Objects.ObjectContext.QueryProvider%2A> 方法的结果。  
  
3.  将此方法作为 <xref:System.Data.Objects.ObjectContext> 类的实例的一个成员调用。  
  
### <a name="to-call-a-model-defined-function-as-static-method-on-a-custom-class"></a>将模型定义函数作为自定义类的静态方法调用  
  
1.  向应用程序添加一个类，该类带有一个静态方法，可执行以下操作：  
  
    -   映射到在概念模型中定义的函数。 若要映射方法，必须将 <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute> 应用于此方法。 请注意，此特性的 <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute.NamespaceName%2A> 和 <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute.FunctionName%2A> 参数分别是概念模型的命名空间名称和概念模型中的函数名称。  
  
    -   接受 <xref:System.Linq.IQueryable> 参数。  
  
    -   返回由 <xref:System.Linq.IQueryProvider.Execute%2A> 属性返回的 <xref:System.Linq.IQueryable.Provider%2A> 方法的结果。  
  
2.  将此方法作为自定义类的一个静态成员调用  
  
## <a name="example"></a>示例  
 **模型定义函数作为 ObjectContext 对象的方法调用**  
  
 下面的示例演示如何将模型定义函数作为 <xref:System.Data.Objects.ObjectContext> 对象的一个方法调用。 该示例使用[AdventureWorks 销售模型](http://msdn.microsoft.com/en-us/f16cd988-673f-4376-b034-129ca93c7832)。  
  
 请考虑下面的概念模型函数，它可返回指定产品的产品收入。 (有关将函数添加到概念模型的信息，请参阅[如何： 在概念模型中定义自定义函数](http://msdn.microsoft.com/en-us/0dad7b8b-58f6-4271-b238-f34810d68e5f)。)  
  
 [!code-xml[DP L2E Methods on ObjectContext#4](../../../../../../samples/snippets/xml/VS_Snippets_Data/dp l2e methods on objectcontext/xml/adventureworks.edmx#4)]  

## <a name="example"></a>示例  
 下面的代码向 `AdventureWorksEntities` 类添加了一个方法，该方法映射到上述的概念模型函数。  
  
 [!code-csharp[DP L2E Methods on ObjectContext#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e methods on objectcontext/cs/program.cs#2)]
 [!code-vb[DP L2E Methods on ObjectContext#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e methods on objectcontext/vb/class1.vb#2)]  
  
## <a name="example"></a>示例  
 下面的代码调用上面的方法，以显示指定产品的产品收入：  
  
 [!code-csharp[DP L2E Methods on ObjectContext#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e methods on objectcontext/cs/program.cs#3)]
 [!code-vb[DP L2E Methods on ObjectContext#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e methods on objectcontext/vb/module1.vb#3)]  
  
## <a name="example"></a>示例  
 下面的示例演示如何调用一个返回集合（作为 <xref:System.Linq.IQueryable%601> 对象）的模型定义函数。 请考虑下面的概念模型函数，它可返回给定产品 ID 的所有 `SalesOrderDetails`。  
  
 [!code-xml[DP L2E Methods on ObjectContext#7](../../../../../../samples/snippets/xml/VS_Snippets_Data/dp l2e methods on objectcontext/xml/adventureworks.edmx#7)]  
  
## <a name="example"></a>示例  
 下面的代码向 `AdventureWorksEntities` 类添加了一个方法，该方法映射到上述的概念模型函数。  
  
 [!code-csharp[DP L2E Methods on ObjectContext#8](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e methods on objectcontext/cs/program.cs#8)]
 [!code-vb[DP L2E Methods on ObjectContext#8](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e methods on objectcontext/vb/class1.vb#8)]  
  
## <a name="example"></a>示例  
 下面的代码示例调用此方法。 请注意，返回的 <xref:System.Linq.IQueryable%601> 查询将进一步优化，以返回每个 `SalesOrderDetail` 的行合计。  
  
 [!code-csharp[DP L2E Methods on ObjectContext#9](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e methods on objectcontext/cs/program.cs#9)]
 [!code-vb[DP L2E Methods on ObjectContext#9](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e methods on objectcontext/vb/module1.vb#9)]  
  
## <a name="example"></a>示例  
 **模型定义函数作为自定义类的静态方法调用**  
  
 下一个示例演示如何将模型定义函数作为自定义类的静态方法调用。 该示例使用[AdventureWorks 销售模型](http://msdn.microsoft.com/en-us/f16cd988-673f-4376-b034-129ca93c7832)。  
  
> [!NOTE]
>  当您将模型定义函数作为自定义类的静态方法调用时，此模型定义函数必须接受集合且在集合中返回值的聚合。  
  
 请考虑下面的概念模型函数，它可返回 SalesOrderDetail 集合的产品收入。 (有关将函数添加到概念模型的信息，请参阅[如何： 在概念模型中定义自定义函数](http://msdn.microsoft.com/en-us/0dad7b8b-58f6-4271-b238-f34810d68e5f)。)。  
  
 [!code-xml[DP L2E Methods on ObjectContext#1](../../../../../../samples/snippets/xml/VS_Snippets_Data/dp l2e methods on objectcontext/xml/adventureworks.edmx#1)]
  
## <a name="example"></a>示例  
 下面的代码向应用程序添加了一个类，该类包含一个映射到上述概念模型函数的静态方法。  
  
 [!code-csharp[DP L2E Methods on ObjectContext#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e methods on objectcontext/cs/program.cs#5)]
 [!code-vb[DP L2E Methods on ObjectContext#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e methods on objectcontext/vb/class1.vb#5)]  
  
## <a name="example"></a>示例  
 下面的代码调用上面的方法，以显示指定 SalesOrderDetail 集合的产品收入：  
  
 [!code-csharp[DP L2E Methods on ObjectContext#6](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e methods on objectcontext/cs/program.cs#6)]
 [!code-vb[DP L2E Methods on ObjectContext#6](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e methods on objectcontext/vb/module1.vb#6)]  
  
## <a name="see-also"></a>另请参阅  
 [.edmx 文件概述](http://msdn.microsoft.com/en-us/f4c8e7ce-1db6-417e-9759-15f8b55155d4)  
 [在 LINQ to Entities 查询](../../../../../../docs/framework/data/adonet/ef/language-reference/queries-in-linq-to-entities.md)  
 [在 LINQ to Entities 查询中调用函数](../../../../../../docs/framework/data/adonet/ef/language-reference/calling-functions-in-linq-to-entities-queries.md)
