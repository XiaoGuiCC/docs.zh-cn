---
title: "部分信任功能兼容性"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a36a540b-1606-4e63-88e0-b7c59e0e6ab7
caps.latest.revision: "75"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: f36d944814adaf4a90a04715c60f2fe732cb544a
ms.sourcegitcommit: ce279f2d7fe2220e6ea0a25a8a7a5370ddf8d9f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/02/2017
---
# <a name="partial-trust-feature-compatibility"></a>部分信任功能兼容性
在部分受信任的环境中运行时，[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 支持一个有限的功能子集。 部分信任中支持的功能围绕 [Supported Deployment Scenarios](../../../../docs/framework/wcf/feature-details/supported-deployment-scenarios.md) 主题中所述的一组特定的方案而设计。  
  
## <a name="minimum-permission-requirements"></a>最低权限要求  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 在通过以下任一标准命名权限集运行的应用程序中支持一个功能子集：  
  
-   “中等信任”权限  
  
-   “Internet 区域”权限  
  
 在部分受信任的应用程序中，如果尝试以受到更多限制的权限来使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] ，可能会在运行时导致安全异常。  
  
## <a name="contracts"></a>协定  
 在部分信任环境下运行时，协定受到以下限制：  
  
-   实现 `[ServiceContract]` 接口的服务类必须为 `public` 类，且必须有一个 `public` 构造函数。 如果该服务类定义 `[OperationContract]` 方法，则这些方法必须为 `public`方法。 如果该服务类实现 `[ServiceContract]` 接口，且 `private`接口为 `[ServiceContract]` 接口，则这些方法实现可以为显式实现或 `public`实现。  
  
-   在使用 `[ServiceKnownType]` 属性时，指定的方法必须为 `public`方法。  
  
-   `[MessageContract]` 类及其成员可以为 `public`。 如果 `[MessageContract]` 类是在应用程序程序集中定义的，则该类可以为 `internal` 类并拥有 `internal` 成员。  
  
## <a name="system-provided-bindings"></a>系统提供的绑定  
 在部分信任环境中完全支持 <xref:System.ServiceModel.BasicHttpBinding> 和 <xref:System.ServiceModel.WebHttpBinding> 。 仅对传输安全模式支持 <xref:System.ServiceModel.WSHttpBinding> 。  
  
 在部分信任环境中运行时，不支持使用除 HTTP 之外的传输的绑定（例如 <xref:System.ServiceModel.NetTcpBinding>、 <xref:System.ServiceModel.NetNamedPipeBinding>或 <xref:System.ServiceModel.NetMsmqBinding>）。  
  
## <a name="custom-bindings"></a>自定义绑定  
 在部分信任环境中可以创建和使用自定义绑定，但必须遵循本节中指定的限制。  
  
### <a name="transports"></a>传输  
 允许的传输绑定元素仅为 <xref:System.ServiceModel.Channels.HttpTransportBindingElement> 和 <xref:System.ServiceModel.Channels.HttpsTransportBindingElement>。  
  
### <a name="encoders"></a>编码器  
 允许以下编码器：  
  
-   文本编码器 (<xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement>)。  
  
-   二进制编码器 (<xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement>)。  
  
-   Web 消息编码器 (<xref:System.ServiceModel.Channels.WebMessageEncodingBindingElement>)。  
  
 不支持消息传输优化机制 (MTOM) 编码器。  
  
### <a name="security"></a>安全性  
 部分受信任的应用程序可以使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]的传输级别安全功能来保护其通信。 不支持消息级安全。 将绑定配置为使用消息级别的安全会在运行时导致异常。  
  
### <a name="unsupported-bindings"></a>不支持的绑定  
 不支持使用可靠消息传递、事务或消息级安全的绑定。  
  
## <a name="serialization"></a>序列化  
 在部分信任环境中支持 <xref:System.Runtime.Serialization.DataContractSerializer> 和 <xref:System.Xml.Serialization.XmlSerializer> 。 但是，使用 <xref:System.Runtime.Serialization.DataContractSerializer> 时需要遵循以下条件：  
  
-   所有可序列化的 `[DataContract]` 类型必须为 `public`。  
  
-   `[DataMember]` 类型中的所有可序列化的 `[DataContract]` 字段或属性必须是公共字段或属性并且可以读取/写入。 在部分受信任的应用程序中运行 [时，不支持](http://go.microsoft.com/fwlink/?LinkID=98854) 只读 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 字段的序列化和反序列化。  
  
-   在部分信任环境中， `[Serializable]`/ISerializable 编程模型不受支持。  
  
-   必须在代码或计算机级别配置 (machine.config) 中指定已知类型。 出于安全方面的原因，不能在应用程序级配置中指定已知类型。  
  
-   实现 <xref:System.Runtime.Serialization.IObjectReference> 的类型在部分受信任的环境中会引发异常。  
  
 有关在部分受信任的应用程序中安全使用 [T:System.Runtime.Serialization.DataContractSerializer](../../../../docs/framework/wcf/feature-details/partial-trust-best-practices.md) 的更多安全信息，请参见 <xref:System.Runtime.Serialization.DataContractSerializer> 中的“序列化”一节。  
  
### <a name="collection-types"></a>集合类型  
 一些集合类型可实现 <xref:System.Collections.Generic.IEnumerable%601> 和 <xref:System.Collections.IEnumerable>。 示例包括实现 <xref:System.Collections.Generic.ICollection%601>的类型。 这些类型可以实现 `public` 的 `GetEnumerator()`实现和 `GetEnumerator()`的显式实现。 在此情况下， <xref:System.Runtime.Serialization.DataContractSerializer> 调用 `public` 的 `GetEnumerator()`，而不调用 `GetEnumerator()`的显式实现。 如果所有 `GetEnumerator()` 实现都不是 `public` 而全部是显式实现，则 <xref:System.Runtime.Serialization.DataContractSerializer> 调用 `IEnumerable.GetEnumerator()`。  
  
 对于集合类型，当 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 在部分信任环境中运行时，如果 `GetEnumerator()` 实现都不是 `public`或都不是显示接口实现，则引发安全异常。  
  
### <a name="netdatacontractserializer"></a>NetDataContractSerializer  
 在部分信任环境中， <xref:System.Collections.Generic.List%601>不支持许多 .NET Framework 集合类型，如 <xref:System.Collections.ArrayList>、 <xref:System.Collections.Generic.Dictionary%602> 、 <xref:System.Collections.Hashtable> 和 <xref:System.Runtime.Serialization.NetDataContractSerializer> 。 这些类型设置了 `[Serializable]` 属性，如前面“序列化”一节中所述，此属性在部分信任环境中不受支持。 <xref:System.Runtime.Serialization.DataContractSerializer> 以特殊方式处理集合，因而能够避开此限制， <xref:System.Runtime.Serialization.NetDataContractSerializer> 没有这类机制可避开此限制。  
  
 在部分信任环境中， <xref:System.DateTimeOffset> 不支持 <xref:System.Runtime.Serialization.NetDataContractSerializer> 类型。  
  
 在部分信任环境中运行时，无法将代理项用于 <xref:System.Runtime.Serialization.NetDataContractSerializer> （使用 <xref:System.Runtime.Serialization.SurrogateSelector> 机制）。 请注意，此限制适用于使用代理项，而不适用于序列化代理项。  
  
## <a name="enabling-common-behaviors-to-run"></a>使常见行为能够运行  
 服务或终结点行为未用标记<xref:System.Security.AllowPartiallyTrustedCallersAttribute>特性 (APTCA) 添加到[ \<commonBehaviors >](../../../../docs/framework/configure-apps/file-schema/wcf/commonbehaviors.md)在部分信任中运行的应用程序时，将不会运行配置文件节发生此情况时引发环境和任何异常。 若要强制运行常见行为，必须执行下列选项之一：  
  
-   使用 <xref:System.Security.AllowPartiallyTrustedCallersAttribute> 属性标记常见行为，以使其在部署为部分信任应用程序时能够运行。 请注意，可以在计算机上设置注册表项，以防运行标有 APTCA 的程序集。 方法。  
  
-   确保在将应用程序作为完全受信任的应用程序部署时，用户不能修改代码访问安全设置，从而无法在部分信任环境中运行该应用程序。 如果用户可以这样做，则不会运行该行为，且不引发任何异常。 若要确保这一点，请参阅**levelfinal**选项使用[Caspol.exe （代码访问安全策略工具）](../../../../docs/framework/tools/caspol-exe-code-access-security-policy-tool.md)。  
  
 [!INCLUDE[crexample](../../../../includes/crexample-md.md)] 常见行为，请参阅 [How to: Lock Down Endpoints in the Enterprise](../../../../docs/framework/wcf/extending/how-to-lock-down-endpoints-in-the-enterprise.md)方法。  
  
## <a name="configuration"></a>配置  
 除一种例外情况之外，部分受信任的代码只能加载本地 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 文件中的 `app.config` 配置节。 要加载引用 machine.config 或根 web.config 文件中的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 节的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 配置节，需要 ConfigurationPermission(Unrestricted)。 如果没有此权限，则对本地配置文件之外的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 配置节（行为、绑定）的引用会导致在加载配置时产生异常。  
  
 一个例外情况是序列化的已知类型配置，如本主题中的“序列化”一节所述。  
  
> [!IMPORTANT]
>  仅当在完全信任环境下运行时，才支持配置扩展。  
  
## <a name="diagnostics"></a>诊断  
  
### <a name="event-logging"></a>事件日志记录  
 部分信任环境下支持有限的事件日志记录。 事件日志中仅记录服务激活错误和跟踪/消息日志记录错误。 为了避免向事件日志写入过多消息，一个进程最多可以记录 5 个事件。  
  
### <a name="message-logging"></a>消息日志记录  
 在部分信任环境中运行 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 时，无法进行消息日志记录。 如果在部分信任下启用消息日志记录，不会出现服务激活失败，但不记录消息。  
  
### <a name="tracing"></a>跟踪  
 在部分信任环境中运行时可使用有限的跟踪功能。 在配置文件的 <`listeners`> 元素中，可以添加的类型仅有 <xref:System.Diagnostics.TextWriterTraceListener> 和新的 <xref:System.Diagnostics.EventSchemaTraceListener>。 使用标准的 <xref:System.Diagnostics.XmlWriterTraceListener> 可能会造成日志不完整或不正确。  
  
 支持的跟踪源有：  
  
-   <xref:System.ServiceModel>  
  
-   <xref:System.Runtime.Serialization>  
  
-   <xref:System.IdentityModel.Claims>、 <xref:System.IdentityModel.Policy>、 <xref:System.IdentityModel.Selectors>和 <xref:System.IdentityModel.Tokens>。  
  
 不支持下面的跟踪源：  
  
-   CardSpace  
  
-   <xref:System.IO.Log>  

-   [System.ServiceModel.Internal.TransactionBridge](https://msdn.microsoft.com/library/system.servicemodel.internal.transactionbridge.aspx)]
  
 不应指定下面的 <xref:System.Diagnostics.TraceOptions> 枚举成员：  
  
-   <xref:System.Diagnostics.TraceOptions.Callstack?displayProperty=nameWithType>  
  
-   <xref:System.Diagnostics.TraceOptions.ProcessId?displayProperty=nameWithType>  
  
 在部分信任环境中使用跟踪时，应确保应用程序具有足够的权限来存储跟踪侦听器的输出。 例如，在使用 <xref:System.Diagnostics.TextWriterTraceListener> 将跟踪输出写入到文本文件中时，应确保应用程序具有成功写入到跟踪文件中所需的必要的 FileIOPermission。  
  
> [!NOTE]
>  为了避免重复错误在跟踪文件中造成泛滥， [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 会在第一次安全失败之后禁用资源或操作跟踪。 对于在第一次尝试访问资源或执行操作时出现的每个失败的资源访问，将会有一个异常跟踪。  
  
## <a name="wcf-service-host"></a>WCF 服务主机  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务主机不支持部分信任。 如果需要在部分信任环境中使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务，请不要使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中的 [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] 服务库项目模板生成服务， 而应通过选择 [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] 服务网站模板在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中创建新的网站，该网站可以在支持 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 部分信任的 Web 服务器中承载服务。  
  
## <a name="other-limitations"></a>其他限制  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 通常仅限于由主机应用程序带来的安全注意事项。 例如，如果在 XAML 浏览器应用程序 (XBAP) 中承载 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] ，则遵循 XBAP 限制，如 [Windows Presentation Foundation 部分信任安全](http://go.microsoft.com/fwlink/?LinkId=89138)所示。  
  
 在部分信任环境中运行 indigo2 时，不启用以下的其他功能：  
  
-   Windows Management Instrumentation (WMI)  
  
-   事件日志记录仅部分启用（请参见“ **诊断** ”一节的讨论）。  
  
-   性能计数器  
  
 使用在部分信任环境中不支持 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 功能可能会导致在运行时产生异常。  
  
## <a name="unlisted-features"></a>未列出的功能  
 若要在部分信任环境中运行时发现不可用的信息或操作，最好的方法是尝试在 `try` 块的内部访问资源或执行操作，然后 `catch` 失败。 为了避免重复错误在跟踪文件中造成泛滥， [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 会在第一次安全失败之后禁用资源或操作跟踪。 对于在第一次尝试访问资源或执行操作时出现的每个失败的资源访问，将会有一个异常跟踪。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.ServiceModel.Channels.HttpTransportBindingElement>  
 <xref:System.ServiceModel.Channels.HttpsTransportBindingElement>  
 <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement>  
 <xref:System.ServiceModel.Channels.WebMessageEncodingBindingElement>  
 [支持的部署方案](../../../../docs/framework/wcf/feature-details/supported-deployment-scenarios.md)  
 [部分信任最佳实践](../../../../docs/framework/wcf/feature-details/partial-trust-best-practices.md)
