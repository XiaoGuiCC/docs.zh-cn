---
title: "如何：使用 Svcutil.exe 验证已编译的服务代码"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d0d820fb-41c2-45b8-8f22-0fa5aeebbbaa
caps.latest.revision: "8"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: 9aeeccc42d5fbbed34ffedf01712b208c98ec58e
ms.sourcegitcommit: ce279f2d7fe2220e6ea0a25a8a7a5370ddf8d9f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/02/2017
---
# <a name="how-to-use-svcutilexe-to-validate-compiled-service-code"></a>如何：使用 Svcutil.exe 验证已编译的服务代码
你可以使用[ServiceModel 元数据实用工具 (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)不承载服务的情况下检测服务实现和配置中的错误。  
  
### <a name="to-validate-a-service"></a>验证服务  
  
1.  将服务编译为可执行文件以及一个或多个相关程序集。  
  
2.  打开一个 SDK 命令提示  
  
3.  在命令提示符处，使用下面的格式启动 Svcutil.exe 工具。 有关的各种参数的详细信息，请参阅的服务 Validationsection [ServiceModel 元数据实用工具 (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)主题。  
  
    ```  
    svcutil.exe /validate /serviceName:<serviceConfigName>  <assemblyPath>*  
    ```  
  
     必须使用 `/serviceName` 选项来指示要验证的服务的配置名称。  
  
     `assemblyPath` 参数指定一个路径，该路径指向包含要验证的服务类型的服务以及一个或多个程序集的可执行文件。 可执行程序集必须具有关联的配置文件，以提供服务配置。 可以使用标准命令行通配符来提供多个程序集。  
  
## <a name="example"></a>示例  
 下面的命令验证在 myServiceHost.exe 可执行文件中实现的服务 myServiceName。  该服务的配置文件 (myServiceHost.exe.config) 自动进行加载。  
  
```  
svcutil /validate /serviceName:myServiceName myServiceHost.exe  
```  
  
## <a name="see-also"></a>另请参阅  
 [ServiceModel 元数据实用工具 (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)
