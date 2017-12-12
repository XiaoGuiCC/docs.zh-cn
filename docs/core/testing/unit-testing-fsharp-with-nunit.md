---
title: "使用 dotnet test 和 NUnit 在 .NET Core 中进行 F# 库的单元测试"
description: "使用 dotnet test 和 NUnit 分步构建一个示例解决方案，在此交互式体验中学习 .NET Core 中的 F# 单元测试概念。"
author: rprouse
ms.date: 12/01/2017
ms.topic: article
dev_langs: fsharp
ms.prod: .net-core
ms.openlocfilehash: 27a7bb889fd736294252da39b1839b2197b8df03
ms.sourcegitcommit: 401c4427a3ec0d1263543033b3084039278509dc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/06/2017
---
# <a name="unit-testing-f-libraries-in-net-core-using-dotnet-test-and-nunit"></a>使用 dotnet test 和 NUnit 在 .NET Core 中进行 F# 库的单元测试

本教程介绍分步构建示例解决方案的交互式体验，以了解单元测试概念。 如果希望使用预构建解决方案学习本教程，请在开始前[查看或下载示例代码](https://github.com/dotnet/docs/tree/master/samples/core/getting-started/unit-testing-with-fsharp-nunit/)。 有关下载说明，请参阅[示例和教程](../../samples-and-tutorials/index.md#viewing-and-downloading-samples)。

## <a name="creating-the-source-project"></a>创建源项目

打开 shell 窗口。 创建一个名为 unit-testing-with-fsharp 的目录，以保留该解决方案。
在此新目录中，运行 [`dotnet new sln`](../tools/dotnet-new.md) 创建新的解决方案。 这样便于管理类库和单元测试项目。
在解决方案库中，创建 MathService 目录。 目录和文件结构目前如下所示：

```
/unit-testing-with-fsharp
    unit-testing-with-fsharp.sln
    /MathService
```

将 MathService 作为当前目录，然后运行 [`dotnet new classlib -lang F#`](../tools/dotnet-new.md) 以创建源项目。  为了使用由测试驱动的开发 (TDD)，需对数学服务创建故障实现：

```fsharp
module MyMath =
    let sumOfSquares xs = raise (System.NotImplementedException("You haven't written a test yet!"))
```

将目录更改回 unit-testing-with-fsharp 目录。 运行 [`dotnet sln add .\MathService\MathService.fsproj`](../tools/dotnet-sln.md) 向解决方案添加类库项目。

## <a name="install-the-nunit-project-template"></a>安装 NUnit 项目模板

创建测试项目之前，需安装 NUnit 测试项目模板。 仅需在新建 NUnit 项目的开发人员计算机上安装一次。 运行 [`dotnet new -i NUnit3.DotNetNew.Template`](../tools/dotnet-new.md) 以安装 NUnit 模板.

 ```
 dotnet new -i NUnit3.DotNetNew.Template
 ```

## <a name="creating-the-test-project"></a>创建测试项目

接下来，创建 MathService.Tests 目录。 下图显示了它的目录结构：

```
/unit-testing-with-fsharp
    unit-testing-with-fsharp.sln
    /MathService
        Source Files
        MathService.fsproj
    /MathService.Tests
```

将 MathService.Tests 目录作为当前目录，并使用 [`dotnet new nunit -lang F#`](../tools/dotnet-new.md) 创建一个新项目。 这会创建一个将 NUnit 用作测试框架的测试项目。 生成的模板在 MathServiceTests.fsproj 中配置测试运行程序：

```xml
<ItemGroup>
  <PackageReference Include="Microsoft.NET.Test.Sdk" Version="15.5.0" />
  <PackageReference Include="NUnit" Version="3.9.0" />
  <PackageReference Include="NUnit3TestAdapter" Version="3.9.0" />
</ItemGroup>
```

测试项目需要其他包创建和运行单元测试。 在上一步中，`dotnet new` 已添加 NUnit 和 NUnit 测试适配器。 现在，将 `MathService` 类库作为另一个依赖项添加到项目中。 使用 [`dotnet add reference`](../tools/dotnet-add-reference.md) 命令：

```
dotnet add reference ../MathService/MathService.fsproj
```

可以在 GitHub 上的[示例存储库](https://github.com/dotnet/docs/blob/master/samples/core/getting-started/unit-testing-with-fsharp/MathService.Tests/MathService.Tests.fsproj)中看到整个文件。

最终的解决方案布局将如下所示：

```
/unit-testing-with-fsharp
    unit-testing-with-fsharp.sln
    /MathService
        Source Files
        MathService.fsproj
    /MathService.Tests
        Test Source Files
        MathServiceTests.fsproj
```

在 unit-testing-with-fsharp 目录中执行 [`dotnet sln add .\MathService.Tests\MathService.Tests.fsproj`](../tools/dotnet-sln.md)。

## <a name="creating-the-first-test"></a>创建第一个测试

TDD 方法要求编写一个失败的测试，使其通过测试，然后重复该过程。 打开 Tests.fs 并添加以下代码：

```fsharp
namespace MathService.Tests

open System
open NUnit.Framework
open MathService

[<TestFixture>]
type TestClass () =

    [<Test>]
    member this.TestMethodPassing() =
        Assert.True(true)

    [<Test>]
     member this.FailEveryTime() = Assert.True(false)
```

`[<TestFixture>]` 属性表示包含测试的类。 `[<Test>]` 属性表示由测试运行程序运行的测试方法。 在 unit-testing-with-fsharp 目录中，执行 [`dotnet test`](../tools/dotnet-test.md) 以构建测试和类库，然后运行测试。 NUnit 测试运行程序包含要运行测试的程序入口点。 `dotnet test` 使用已创建的单元测试项目启动测试运行程序。

这两个测试演示了最基本的已通过测试和未通过测试。 `My test` 通过，而 `Fail every time` 未通过。 现在创建针对 `sumOfSquares` 方法的测试。 `sumOfSquares` 方法返回输入序列中的所有奇整数值的平方和。 可以以迭代的方式创建可验证此功能的测试，而非尝试同时写入所有的函数。 若要让每个测试都通过，意味着要针对此方法创建必要的功能。

可以编写的最简单的测试是调用包含所有偶数的 `sumOfSquares`，它的结果应该是一个空整数序列。  此测试如下所示：

```fsharp
[<Test>]
member this.TestEvenSequence() =
    let expected = Seq.empty<int> |> Seq.toList
    let actual = MyMath.sumOfSquares [2; 4; 6; 8; 10]
    Assert.That(actual, Is.EqualTo(expected))
```

请注意已将 `expected` 序列转换为列表。 NUnit 框架依赖于许多标准 .NET 类型。 此依赖关系表示公共接口和预期结果支持 <xref:System.Collections.ICollection>，而非 <xref:System.Collections.IEnumerable>。

运行此测试时，会看到测试失败。 尚未创建实现。 在起作用的 `Mathservice` 类中编写最简单的代码，以生成此测试：

```csharp
let sumOfSquares xs =
    Seq.empty<int> |> Seq.toList
```

在 unit-testing-with-fsharp 目录中，再次运行 `dotnet test`。 `dotnet test` 命令构建 `MathService` 项目，然后构建 `MathService.Tests` 项目。 构建这两个项目后，该命令将运行此单项测试。 测试通过。

## <a name="completing-the-requirements"></a>完成要求

你已经通过了一个测试，现在可以编写更多测试。 下一个简单示例使用的序列包含的唯一奇数为 `1`。 数值 1 较为简单，因为 1 的平方是 1。 下一个测试如下所示：

```fsharp
[<Test>]
member public this.SumOnesAndEvens() =
    let expected = [1; 1; 1; 1]
    let actual = MyMath.sumOfSquares [2; 1; 4; 1; 6; 1; 8; 1; 10]
    Assert.That(actual, Is.EqualTo(expected))
```

如果执行 `dotnet test`，新测试将失败。 必须更新 `sumOfSquares` 方法才能处理此新测试。 必须筛选出序列中的所有偶数值，以使此测试通过。 可以编写一个小筛选器函数并使用 `Seq.filter` 来实现此目的：

```fsharp
let private isOdd x = x % 2 <> 0

let sumOfSquares xs =
    xs
    |> Seq.filter isOdd
    |> Seq.toList
```

注意对 `Seq.toList` 的调用。 它会创建一个列表，此列表将实现 <xref:System.Collections.ICollection> 接口。

还要执行一个步骤：计算每个奇数的平方值。 从编写新测试开始：

```fsharp
[<Test>]
member public this.TestSquaresOfOdds() =
    let expected = [1; 9; 25; 49; 81]
    let actual = MyMath.sumOfSquares [1; 2; 3; 4; 5; 6; 7; 8; 9; 10]
    Assert.That(actual, Is.EqualTo(expected))
```

可以通过映射操作传递经过筛选的序列来计算每个奇数的平方，以此方式来修复测试的缺陷：

```fsharp
let private square x = x * x
let private isOdd x = x % 2 <> 0

let sumOfSquares xs =
    xs
    |> Seq.filter isOdd
    |> Seq.map square
    |> Seq.toList
```

你已生成一个小型库和该库的一组单元测试。 你已将解决方案结构化，使添加新包和新测试成为了正常工作流的一部分。 你已将多数的时间和精力集中在解决应用程序的目标上。