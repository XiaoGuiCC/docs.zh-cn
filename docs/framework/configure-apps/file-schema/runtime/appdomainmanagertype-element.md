---
title: "&lt;p e&gt;元素"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- appDomainManagerType element
- <appDomainManagerType> element
ms.assetid: ae8d5a7e-e7f7-47f7-98d9-455cc243a322
caps.latest.revision: "7"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 56d68efe176540ba82ec7b86f35678905ebc970b
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="ltappdomainmanagertypegt-element"></a>&lt;p e&gt;元素
指定用作默认应用程序域的应用程序域管理器的类型。  
  
 \<configuration>  
\<运行时 >  
\<p e >  
  
## <a name="syntax"></a>语法  
  
```xml  
<appDomainManagerAssembly   
   value="type name" />  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|`value`|必需的特性。 指定的类型，包括用作进程内的默认应用程序域的应用程序域管理器的命名空间的名称。|  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含有关程序集绑定和垃圾回收的信息。|  
  
## <a name="remarks"></a>备注  
 若要指定应用程序域管理器的类型，你必须同时指定此元素与[ \<appDomainManagerAssembly >](../../../../../docs/framework/configure-apps/file-schema/runtime/appdomainmanagerassembly-element.md)元素。 如果未指定任一这些元素，另一个被忽略。  
  
 加载默认应用程序域后，<xref:System.TypeLoadException>如果中由指定的程序集不存在指定的类型，将引发[ \<appDomainManagerAssembly >](../../../../../docs/framework/configure-apps/file-schema/runtime/appdomainmanagerassembly-element.md)元素; 和进程无法将到开始日期。  
  
 当指定默认应用程序域的应用程序域管理器类型时，从默认应用程序域创建其他应用程序域继承的应用程序域管理器类型。 使用<xref:System.AppDomainSetup.AppDomainManagerType%2A?displayProperty=nameWithType>和<xref:System.AppDomainSetup.AppDomainManagerAssembly%2A?displayProperty=nameWithType>属性以指定新的应用程序域不同的应用程序域管理器类型。  
  
 指定的应用程序域管理器类型要求应用程序具有完全信任。 （例如，在桌面上运行的应用程序具有完全信任。）如果应用程序不具有完全信任，<xref:System.TypeLoadException>引发。  
  
 类型和命名空间的格式是相同的格式用于<xref:System.Type.FullName%2A?displayProperty=nameWithType>属性。  
  
 此配置元素可仅用于[!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)]及更高版本。  
  
## <a name="example"></a>示例  
 下面的示例演示如何指定进程的默认应用程序域的应用程序域管理器是`MyMgr`键入`AdMgrExample`程序集。  
  
```xml  
<configuration>  
   <runtime>  
      <appDomainManagerType value="MyMgr" />  
      <appDomainManagerAssembly   
         value="AdMgrExample, Version=1.0.0.0, Culture=neutral, PublicKeyToken=6856bccf150f00b3" />  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.AppDomainSetup.AppDomainManagerType%2A?displayProperty=nameWithType>  
 <xref:System.AppDomainSetup.AppDomainManagerAssembly%2A?displayProperty=nameWithType>  
 [\<appDomainManagerAssembly > 元素](../../../../../docs/framework/configure-apps/file-schema/runtime/appdomainmanagerassembly-element.md)  
 [运行时设置架构](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)  
 [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)  
 [SetAppDomainManagerType 方法](../../../../../docs/framework/unmanaged-api/hosting/iclrcontrol-setappdomainmanagertype-method.md)
