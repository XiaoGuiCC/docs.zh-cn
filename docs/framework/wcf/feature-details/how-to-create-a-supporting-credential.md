---
title: "如何：创建支持凭据"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d0952919-8bb4-4978-926c-9cc108f89806
caps.latest.revision: "9"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: a460a3fdd48813801b18af5a896252134687816d
ms.sourcegitcommit: ce279f2d7fe2220e6ea0a25a8a7a5370ddf8d9f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/02/2017
---
# <a name="how-to-create-a-supporting-credential"></a>如何：创建支持凭据
自定义安全方案可能要求提供多个凭据。 例如，某个服务可能要求客户端不仅提供用户名和密码，还要提供能够证明客户端用户已满 18 岁的凭据。 第二个凭据是*支持凭据*。 本主题说明如何在 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 客户端中实现此类凭据。  
  
> [!NOTE]
>  支持凭据的规范是 WS-SecurityPolicy 规范的一部分。 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Web 服务安全规范](http://go.microsoft.com/fwlink/?LinkId=88537)。  
  
## <a name="supporting-tokens"></a>支持令牌  
 简单地说，当使用消息安全，*主凭据*始终用于保护消息 （例如，X.509 证书或 Kerberos 票证）。  
  
 如规范所定义，使用的安全绑定*令牌*来保护消息交换。 A*令牌*是的表示形式的安全凭据。  
  
 安全绑定使用在安全绑定策略中标识的主令牌来创建签名。 此签名称为*消息签名*。  
  
 还可以指定其他令牌，以扩充与消息签名相关联的令牌所提供的声明。  
  
## <a name="endorsing-signing-and-encrypting"></a>认可、签名和加密  
 支持凭据会导致*支持令牌*消息中传输。 WS-SecurityPolicy 规范定义了四种将支持令牌附加到消息的方法，如下表所述。  
  
|用途|描述|  
|-------------|-----------------|  
|签名|支持令牌包含在安全标头中，并由消息签名进行签名。|  
|认可|*认可令牌*签署消息签名。|  
|签名和认可|签名的认可令牌对从消息签名生成的整个 `ds:Signature` 元素进行签名，并由该消息签名对自己进行签名；也就是说，两种令牌（用于消息签名的令牌和已签名的认可令牌）互相进行签名。|  
|签名和加密|签名的加密支持令牌是在 `wsse:SecurityHeader` 中出现时还进行加密的签名支持令牌。|  
  
## <a name="programming-supporting-credentials"></a>对支持凭据进行编程  
 若要创建使用必须创建的支持令牌的服务[ \<customBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)。 ([!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [如何： 创建自定义绑定使用 SecurityBindingElement](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)。)  
  
 创建自定义绑定的第一步是创建一个安全绑定元素，该元素可以是以下三种类型之一：  
  
-   <xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement>  
  
-   <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement>  
  
-   <xref:System.ServiceModel.Channels.TransportSecurityBindingElement>  
  
 所有类都继承自 <xref:System.ServiceModel.Channels.SecurityBindingElement>，它包含四个相关属性：  
  
-   <xref:System.ServiceModel.Channels.SecurityBindingElement.EndpointSupportingTokenParameters%2A>  
  
-   <xref:System.ServiceModel.Channels.SecurityBindingElement.OperationSupportingTokenParameters%2A>  
  
-   <xref:System.ServiceModel.Channels.SecurityBindingElement.OptionalEndpointSupportingTokenParameters%2A>  
  
-   <xref:System.ServiceModel.Channels.SecurityBindingElement.OptionalOperationSupportingTokenParameters%2A>  
  
#### <a name="scopes"></a>范围  
 支持凭据存在两个范围：  
  
-   *支持令牌的终结点*支持所有操作的终结点。 即，每当调用任何终结点操作，都可以使用该支持令牌表示的凭据。  
  
-   *操作支持令牌*支持特定终结点操作。  
  
 正如属性名所指示的那样，支持凭据可能是必需的，也可能是可选的。 即，如果支持凭据存在，则使用支持凭据（尽管不是必需的），但如果支持凭据不存在，身份验证也不会失败。  
  
## <a name="procedures"></a>过程  
  
#### <a name="to-create-a-custom-binding-that-includes-supporting-credentials"></a>创建一个包含支持凭据的自定义绑定  
  
1.  创建一个安全绑定元素。 下面的示例创建一个 <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement>，该元素具有 `UserNameForCertificate` 身份验证模式。 使用 <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateUserNameForCertificateBindingElement%2A> 方法。  
  
2.  将支持参数添加到由适当的属性（`Endorsing`、`Signed`、`SignedEncrypted` 或 `SignedEndorsed`）返回的类型集合中。 <xref:System.ServiceModel.Security.Tokens> 命名空间中的类型包括常用类型，如 <xref:System.ServiceModel.Security.Tokens.X509SecurityTokenParameters>。  
  
## <a name="example"></a>示例  
  
### <a name="description"></a>描述  
 下面的示例创建 <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> 的一个实例，并将 <xref:System.ServiceModel.Security.Tokens.KerberosSecurityTokenParameters> 类的一个实例添加到 Endorsing 属性返回的集合中。  
  
### <a name="code"></a>代码  
 [!code-csharp[c_SupportingCredential#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_supportingcredential/cs/source.cs#1)]  
  
## <a name="see-also"></a>另请参阅  
 [如何： 创建自定义绑定使用 SecurityBindingElement](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)
