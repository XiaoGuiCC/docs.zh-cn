---
title: "类中的 let 绑定 (F#)"
description: "了解如何通过使用 let 绑定的类定义中定义私有字段和私有函数对于 F # 类。"
keywords: "visual f#, f#, 函数编程"
author: cartermp
ms.author: phcart
ms.date: 05/16/2016
ms.topic: language-reference
ms.prod: .net
ms.technology: devlang-fsharp
ms.devlang: fsharp
ms.assetid: 9d3710f5-68b1-4e4c-b02b-27fe018f20e8
ms.openlocfilehash: 1337cc0794e366e8c39745f5c45065362c9c38c9
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2017
---
# <a name="let-bindings-in-classes"></a>类中的 let 绑定

可以通过定义私有字段和 F # 类的私有函数`let`类定义中的绑定。


## <a name="syntax"></a>语法

```fsharp
// Field.
[static] let [ mutable ] binding1 [ and ... binding-n ]

// Function.
[static] let [ rec ] binding1 [ and ... binding-n ]
```

## <a name="remarks"></a>备注
上面的语法显示类标题和继承声明之后但在任何成员定义之前。 语法是类似的`let`外部类，但类中定义的名称的绑定都具有仅限于类的作用域。 A`let`绑定创建的私有字段或函数; 来公开数据或函数公开，声明属性或成员方法。

A`let`绑定，它不是静态称为实例`let`绑定。 实例`let`绑定执行创建对象时。 静态`let`绑定是类，该类可保证执行之前将首先使用该类型的静态初始值设定项的一部分。

实例中的代码`let`绑定可以使用主构造函数的参数。

特性和可访问性修饰符不允许对`let`类中的绑定。

下面的代码示例阐释几种类型的`let`类中的绑定。

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-1/snippet3001.fs)]

输出如下所示。

```
10 52 1 204
```

## <a name="alternative-ways-to-create-fields"></a>用于创建字段的其他方法
你还可以使用`val`关键字来创建私有字段。 使用时`val`关键字，该字段不建议提供一个值时创建对象，，但改为使用默认值初始化。 有关详细信息，请参阅[显式字段： val 关键字](explicit-fields-the-val-keyword.md)。

可以使用成员定义和添加关键字，还定义一个类私有字段`private`到定义。 这很有用，如果您希望无需重写你的代码更改成员的可访问性。 有关详细信息，请参阅[访问控制](../access-control.md)。

## <a name="see-also"></a>另请参阅
[成员](index.md)

[类中的 `do` 绑定](do-bindings-in-classes.md)

[`let`绑定](../functions/let-bindings.md)
