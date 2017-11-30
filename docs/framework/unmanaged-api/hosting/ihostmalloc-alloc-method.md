---
title: "IHostMAlloc::Alloc 方法"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: IHostMAlloc.Alloc
api_location: mscoree.dll
api_type: COM
f1_keywords: IHostMAlloc::Alloc
helpviewer_keywords:
- Alloc method, IHostMAlloc interface [.NET Framework hosting]
- IHostMAlloc::Alloc method [.NET Framework hosting]
ms.assetid: a3007f5e-d75d-4b37-842b-704e9edced5e
topic_type: apiref
caps.latest.revision: "14"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 9cc4447424d1594f6fa86e07be659a6ba97f0427
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="ihostmallocalloc-method"></a><span data-ttu-id="0963f-102">IHostMAlloc::Alloc 方法</span><span class="sxs-lookup"><span data-stu-id="0963f-102">IHostMAlloc::Alloc Method</span></span>
<span data-ttu-id="0963f-103">主机从堆中分配指定的数量的内存的请求。</span><span class="sxs-lookup"><span data-stu-id="0963f-103">Requests that the host allocate the specified amount of memory from the heap.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="0963f-104">语法</span><span class="sxs-lookup"><span data-stu-id="0963f-104">Syntax</span></span>  
  
```  
HRESULT Alloc (  
    [in] SIZE_T  cbSize,   
    [in] EMemoryCriticalLevel dwCriticalLevel,   
    [out] void** ppMem  
);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="0963f-105">参数</span><span class="sxs-lookup"><span data-stu-id="0963f-105">Parameters</span></span>  
 `cbSize`  
 <span data-ttu-id="0963f-106">[in]以字节为单位的当前内存分配请求的大小。</span><span class="sxs-lookup"><span data-stu-id="0963f-106">[in] The size, in bytes, of the current memory allocation request.</span></span>  
  
 `dwCriticalLevel`  
 <span data-ttu-id="0963f-107">[in]之一[EMemoryCriticalLevel](../../../../docs/framework/unmanaged-api/hosting/ememorycriticallevel-enumeration.md)值，指示分配失败的影响。</span><span class="sxs-lookup"><span data-stu-id="0963f-107">[in] One of the [EMemoryCriticalLevel](../../../../docs/framework/unmanaged-api/hosting/ememorycriticallevel-enumeration.md) values, indicating the impact of an allocation failure.</span></span>  
  
 `ppMem`  
 <span data-ttu-id="0963f-108">[out]指向分配的内存或如果无法完成请求的 null 指针。</span><span class="sxs-lookup"><span data-stu-id="0963f-108">[out] A pointer to the allocated memory, or null if the request could not be completed.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="0963f-109">返回值</span><span class="sxs-lookup"><span data-stu-id="0963f-109">Return Value</span></span>  
  
|<span data-ttu-id="0963f-110">HRESULT</span><span class="sxs-lookup"><span data-stu-id="0963f-110">HRESULT</span></span>|<span data-ttu-id="0963f-111">描述</span><span class="sxs-lookup"><span data-stu-id="0963f-111">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="0963f-112">S_OK</span><span class="sxs-lookup"><span data-stu-id="0963f-112">S_OK</span></span>|<span data-ttu-id="0963f-113">`Alloc`已成功返回。</span><span class="sxs-lookup"><span data-stu-id="0963f-113">`Alloc` returned successfully.</span></span>|  
|<span data-ttu-id="0963f-114">HOST_E_CLRNOTAVAILABLE</span><span class="sxs-lookup"><span data-stu-id="0963f-114">HOST_E_CLRNOTAVAILABLE</span></span>|<span data-ttu-id="0963f-115">公共语言运行时 (CLR) 尚未加载到进程中，或 CLR 处于不能运行托管的代码或成功处理调用的状态。</span><span class="sxs-lookup"><span data-stu-id="0963f-115">The common language runtime (CLR) has not been loaded into a process, or the CLR is in a state in which it cannot run managed code or process the call successfully.</span></span>|  
|<span data-ttu-id="0963f-116">HOST_E_TIMEOUT</span><span class="sxs-lookup"><span data-stu-id="0963f-116">HOST_E_TIMEOUT</span></span>|<span data-ttu-id="0963f-117">调用操作已超时。</span><span class="sxs-lookup"><span data-stu-id="0963f-117">The call timed out.</span></span>|  
|<span data-ttu-id="0963f-118">HOST_E_NOT_OWNER</span><span class="sxs-lookup"><span data-stu-id="0963f-118">HOST_E_NOT_OWNER</span></span>|<span data-ttu-id="0963f-119">调用方不拥有该锁。</span><span class="sxs-lookup"><span data-stu-id="0963f-119">The caller does not own the lock.</span></span>|  
|<span data-ttu-id="0963f-120">HOST_E_ABANDONED</span><span class="sxs-lookup"><span data-stu-id="0963f-120">HOST_E_ABANDONED</span></span>|<span data-ttu-id="0963f-121">事件已被取消时被阻塞的线程，或者纤程正在等待它。</span><span class="sxs-lookup"><span data-stu-id="0963f-121">An event was canceled while a blocked thread or fiber was waiting on it.</span></span>|  
|<span data-ttu-id="0963f-122">E_FAIL</span><span class="sxs-lookup"><span data-stu-id="0963f-122">E_FAIL</span></span>|<span data-ttu-id="0963f-123">出现未知的灾难性故障。</span><span class="sxs-lookup"><span data-stu-id="0963f-123">An unknown catastrophic failure occurred.</span></span> <span data-ttu-id="0963f-124">如果某方法返回 E_FAIL，CLR 不再可用进程内。</span><span class="sxs-lookup"><span data-stu-id="0963f-124">When a method returns E_FAIL, the CLR is no longer usable within the process.</span></span> <span data-ttu-id="0963f-125">到托管方法的后续调用会返回 HOST_E_CLRNOTAVAILABLE。</span><span class="sxs-lookup"><span data-stu-id="0963f-125">Subsequent calls to hosting methods return HOST_E_CLRNOTAVAILABLE.</span></span>|  
|<span data-ttu-id="0963f-126">E_OUTOFMEMORY</span><span class="sxs-lookup"><span data-stu-id="0963f-126">E_OUTOFMEMORY</span></span>|<span data-ttu-id="0963f-127">可用于完成分配请求没有足够的内存。</span><span class="sxs-lookup"><span data-stu-id="0963f-127">Not enough memory was available to complete the allocation request.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="0963f-128">备注</span><span class="sxs-lookup"><span data-stu-id="0963f-128">Remarks</span></span>  
 <span data-ttu-id="0963f-129">CLR 获取到的接口指针`IHostMalloc`实例通过调用[ihostmemorymanager:: Createmalloc](../../../../docs/framework/unmanaged-api/hosting/ihostmemorymanager-createmalloc-method.md)方法。</span><span class="sxs-lookup"><span data-stu-id="0963f-129">The CLR gets an interface pointer to an `IHostMalloc` instance by calling the [IHostMemoryManager::CreateMalloc](../../../../docs/framework/unmanaged-api/hosting/ihostmemorymanager-createmalloc-method.md) method.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="0963f-130">要求</span><span class="sxs-lookup"><span data-stu-id="0963f-130">Requirements</span></span>  
 <span data-ttu-id="0963f-131">**平台：**请参阅[系统要求](../../../../docs/framework/get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="0963f-131">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="0963f-132">**标头：** MSCorEE.h</span><span class="sxs-lookup"><span data-stu-id="0963f-132">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="0963f-133">**库：**作为 MSCorEE.dll 中的资源</span><span class="sxs-lookup"><span data-stu-id="0963f-133">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="0963f-134">**.NET framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="0963f-134">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="0963f-135">另请参阅</span><span class="sxs-lookup"><span data-stu-id="0963f-135">See Also</span></span>  
 [<span data-ttu-id="0963f-136">IHostMemoryManager 接口</span><span class="sxs-lookup"><span data-stu-id="0963f-136">IHostMemoryManager Interface</span></span>](../../../../docs/framework/unmanaged-api/hosting/ihostmemorymanager-interface.md)  
 [<span data-ttu-id="0963f-137">IHostMalloc 接口</span><span class="sxs-lookup"><span data-stu-id="0963f-137">IHostMalloc Interface</span></span>](../../../../docs/framework/unmanaged-api/hosting/ihostmalloc-interface.md)