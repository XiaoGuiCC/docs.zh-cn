---
title: DeliveryRequirementsAttribute
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 40c5435c-a325-4cf8-9dd0-d6e24b4a56a3
caps.latest.revision: "8"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: 172f7df4f028c1ddc0f5565e95291e857ee6fa1d
ms.sourcegitcommit: ce279f2d7fe2220e6ea0a25a8a7a5370ddf8d9f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/02/2017
---
# <a name="deliveryrequirementsattribute"></a>DeliveryRequirementsAttribute
DeliveryRequirementsAttribute  
  
## <a name="syntax"></a>语法  
  
```  
class DeliveryRequirementsAttribute : Behavior  
{  
  string QueuedDeliveryRequirements;  
  boolean RequireOrderedDelivery;  
  string TargetContract;  
};  
```  
  
## <a name="methods"></a>方法  
 DeliveryRequirementsAttribute 类未定义任何方法。  
  
## <a name="properties"></a>属性  
 DeliveryRequirementsAttribute 类具有以下属性：  
  
### <a name="queueddeliveryrequirements"></a>QueuedDeliveryRequirements  
 数据类型：String  
  
 访问类型：只读  
  
 指定服务的绑定是否支持协定。  
  
### <a name="requireordereddelivery"></a>RequireOrderedDelivery  
 数据类型：Boolean  
  
 访问类型：只读  
  
 指定绑定是否支持已排序消息。  
  
### <a name="targetcontract"></a>TargetContract  
 数据类型：String  
  
 访问类型：只读  
  
 该类应用到的协定。  
  
## <a name="requirements"></a>要求  
  
|MOF|已在 Servicemodel.mof 中声明。|  
|---------|-----------------------------------|  
|命名空间|已在 root\ServiceModel 中定义|  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.ServiceModel.DeliveryRequirementsAttribute>
