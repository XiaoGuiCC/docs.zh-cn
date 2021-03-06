---
title: "ICorDebugManagedCallback::LoadAssembly 方法"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorDebugManagedCallback.LoadAssembly
api_location: mscordbi.dll
api_type: COM
f1_keywords: ICorDebugManagedCallback::LoadAssembly
helpviewer_keywords:
- LoadAssembly method [.NET Framework debugging]
- ICorDebugManagedCallback::LoadAssembly method [.NET Framework debugging]
ms.assetid: 55cb673a-e240-43a6-a406-6912e7c0fe66
topic_type: apiref
caps.latest.revision: "13"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 1e59853f8f0ac61f89fc0efe0fb63f4ad7e6e0e7
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="icordebugmanagedcallbackloadassembly-method"></a>ICorDebugManagedCallback::LoadAssembly 方法
通知调试器已成功加载公共语言运行时 (CLR) 程序集。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT LoadAssembly (  
    [in] ICorDebugAppDomain *pAppDomain,  
    [in] ICorDebugAssembly  *pAssembly  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pAppDomain`  
 [in]指向表示程序集已在其中加载的应用程序域的 ICorDebugAppDomain 对象的指针。  
  
 `pAssembly`  
 [in]指向表示程序集的 icor 调试程序集对象的指针。  
  
## <a name="requirements"></a>要求  
 **平台：**请参阅[系统要求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorDebug.idl、 CorDebug.h  
  
 **库：** CorGuids.lib  
  
 **.NET framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [UnloadAssembly 方法](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback-unloadassembly-method.md)  
 [ICorDebugManagedCallback 接口](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback-interface.md)
