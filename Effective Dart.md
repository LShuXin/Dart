# Effective Dart

在过去的几年里，我们编写了大量的 Dart 代码， 也从中收获了很多经验和教训， 我们将与你分享这些经验，这些经验将有助于你编写出一致、健壮、高效的代码。 这里包含两主题：

1. **保持一致** 当谈论到格式、命名、参数相关规则时，其中那种规则更好， 得出的结论通常是主观的，而且无法达成一致。 但是我们知道，客观上保持*一致*是非常有益的。

   如果两段代码看起来不同，那他们就应该有不同的含义。 当一段突出的代码吸引到你的注意时，那他就应该有吸引你的理由。

2. **保持精简** Dart 会让开发者感到很亲切， 因此它继承了许多与 C，Java，JavaScript 及其他语言相同的语句和表达式。 我们之所以开发 Dart 语言，是因为这些语言提供了很多改进的空间。 我们提供了很多新的特性， 比如字符串插值、初始化范式等， 以帮助你更简单，更轻松地表达意图。

   如果有多种方式来描述一件事情， 那么你通常应该选择其中最简洁的方式。 这并不意味着你要像 [code golf](https://en.wikipedia.org/wiki/Code_golf) （代码高尔夫挑战赛）一样，将所有代码塞到一行中。 目标是让代码*简约*，而不是*密集*。

Dart analyzer 包括一个 linter 可以帮助你编写一致性的，优秀的代码。 如果 linter 包含规则，那么它将会帮助你遵守这些准则，准则包含规则的链接。比如下面的示例：

Linter rule: [prefer_collection_literals](https://dart-lang.github.io/linter/lints/prefer_collection_literals.html)

获取帮助 [开启 linter 规则](https://www.dartcn.com/guides/language/analysis-options#enabling-linter-rules), 查看文档 [自定义静态分析](https://www.dartcn.com/guides/language/analysis-options).

## 指南

我们将指南分成几个单独的页面以便于消化：：

- **[风格指南](https://www.dartcn.com/guides/language/effective-dart/style)** – 这定义了布局和组织代码的规则， [dartfmt](https://github.com/dart-lang/dart_style#readme) 的实现使用同样的规则。指南中还指定了标识符的格式： `camelCase`，`using_underscores` 等。
- **[文档注释指南](https://www.dartcn.com/guides/language/effective-dart/documentation)** – 这会告诉你关于如何编写注释文档的一切内容。 包括文档注释，常规的普通代码注释。
- **[使用指南](https://www.dartcn.com/guides/language/effective-dart/usage)** – 这将教你如何充分利用语言功能来实现功能。 例如语句和表达式相关的内容，则会在这里介绍。
- **[设计指南](https://www.dartcn.com/guides/language/effective-dart/design)** – 这是一份宽松的指南，但是覆盖范围最广。 这里涵盖了如何为库设计一致的、可用的 API。例如类型签名或声明相关内容， 则会在这里介绍。

有关所有指南的链接，参考 [summary](https://www.dartcn.com/guides/language/effective-dart/#summary-of-all-rules)。

## 如何阅读本指南

每个指南都分为了几个部分。每个部分包含一些详细的准则。 每条准则都以下面其中的一个词作为开头：

- **要** 准则所描述的内容应该始终被遵守。 不应该以任何的理由来偏离违背这些准则。
- **不要** 准则所描述的内容是相反的： 描述的几乎从来不是一个好注意。 幸运的是，我们不会像其他语言有那么多这样的准则，因为我们没有太多的历史包袱。
- **推荐** 准则所描述的内容*应该*被遵守。 但是在有些情况下，可能有更好的或者更合理的做法。 请确保在你完全理解准则的情况下，再忽视这些准则。
- **避免** 准则与 “推荐” 准则相反： 显然，这些事不应该做，但不排除在极少数场合下有充分的理由可以使用。
- **考虑** 准则所描述的内容可以遵守，也可以不遵守。 取决于具体的情况、先前的做法以及自己的偏好。

这听起来好像有点小题大做。其实并没有那么糟糕。大部分的准则都是常识，也符合我们的认知。 最终要达到的目标是写出优雅，可读，可维护的代码。

## 词汇表

为了使指南保持简洁， 我们使用一些简写术语来指代不同的 Dart 结构。

- **库成员** 是一个顶级字段，getter 方法，setter 方法，或者函数， 基本上，任何顶级的东西都不会是一种类型。
- **类成员** 是一个类内部声明的构造函数，字段，getter 方法，setter 方法，函数，或者操作符。 类成员可以是实例的或者静态的，抽象的或者具体的。
- **成员** 是一个库成员或者是类成员。
- **变量** 通常是指顶级变量，参数和局部变量。 它不包括静态或实例的字段。
- **类型** 是任意命名类型的声明：一个类、 typedef、或者 enum。
- **属性** 是一个顶级变量，getter 方法（在一个类或者顶级实例或静态类中）， setter（同getter），或者字段（示例或静态类）。 大致上任何“字段式”命名构造。

## 所有准则摘要

### Style

**标识符**

- [**要** 使用 `UpperCamelCase` 风格命名类型。](https://www.dartcn.com/guides/language/effective-dart/style#要-使用-uppercamelcase-风格命名类型)
- [**要** 在`库`，`包`，`文件夹`，`源文件`中使用 `lowercase_with_underscores` 方式命名。 {#do-name-libraries-and-source-files-using-lowercase_with_underscores}](https://www.dartcn.com/guides/language/effective-dart/style#要-在库包文件夹源文件中使用-lowercase_with_underscores-方式命名-do-name-libraries-and-source-files-using-lowercase_with_underscores)
- [**要** 用 `lowercase_with_underscores` 风格命名库和源文件名。](https://www.dartcn.com/guides/language/effective-dart/style#要-用-lowercase_with_underscores-风格命名库和源文件名)
- [**要** 使用 `lowercase_with_underscores` 风格命名导入的前缀。](https://www.dartcn.com/guides/language/effective-dart/style#要-使用-lowercase_with_underscores-风格命名导入的前缀)
- [**要** 使用 `lowerCamelCase` 风格来命名其他的标识符。](https://www.dartcn.com/guides/language/effective-dart/style#要-使用-lowercamelcase-风格来命名其他的标识符)
- [**推荐** 使用 `lowerCamelCase` 来命名常量。](https://www.dartcn.com/guides/language/effective-dart/style#推荐-使用-lowercamelcase-来命名常量)
- [**要** 把超过两个字母的首字母大写缩略词和缩写词当做一般单词来对待。](https://www.dartcn.com/guides/language/effective-dart/style#要-把超过两个字母的首字母大写缩略词和缩写词当做一般单词来对待)
- [**不要** 使用前缀字母](https://www.dartcn.com/guides/language/effective-dart/style#不要-使用前缀字母)

**顺序**

- [**要** 把 “dart:” 导入语句放到其他导入语句之前。](https://www.dartcn.com/guides/language/effective-dart/style#要-把-dart-导入语句放到其他导入语句之前)
- [**要** 把 “package:” 导入语句放到项目相关导入语句之前。](https://www.dartcn.com/guides/language/effective-dart/style#要-把-package-导入语句放到项目相关导入语句之前)
- [**推荐** 把外部扩展 “package:” 导入语句放到其他语句之前。](https://www.dartcn.com/guides/language/effective-dart/style#推荐-把外部扩展-package-导入语句放到其他语句之前)
- [**要** 把导出（export）语句作为一个单独的部分放到所有导入语句之后。](https://www.dartcn.com/guides/language/effective-dart/style#要-把导出export语句作为一个单独的部分放到所有导入语句之后)
- [**要** 按照字母顺序来排序每个部分中的语句。](https://www.dartcn.com/guides/language/effective-dart/style#要-按照字母顺序来排序每个部分中的语句)

**格式化**

- [**要** 使用 `dartfmt` 格式化你的代码。](https://www.dartcn.com/guides/language/effective-dart/style#要-使用-dartfmt-格式化你的代码)
- [**考虑** 修改你的代码让格式更友好。](https://www.dartcn.com/guides/language/effective-dart/style#考虑-修改你的代码让格式更友好)
- [**避免** 单行超过 80 个字符。](https://www.dartcn.com/guides/language/effective-dart/style#避免-单行超过-80-个字符)
- [**要** 对所有流控制结构使用花括号。](https://www.dartcn.com/guides/language/effective-dart/style#要-对所有流控制结构使用花括号)

### Documentation

**注释**

- [**要** 像句子一样来格式化注释。](https://www.dartcn.com/guides/language/effective-dart/documentation#要-像句子一样来格式化注释)
- [**不要** 使用块注释作用作解释说明。](https://www.dartcn.com/guides/language/effective-dart/documentation#不要-使用块注释作用作解释说明)

**文档注释**

- [**要** 使用 `///` 文档注释来注释成员和类型。](https://www.dartcn.com/guides/language/effective-dart/documentation#要-使用--文档注释来注释成员和类型)
- [**推荐** 为公开发布的 API 编写文档注释。](https://www.dartcn.com/guides/language/effective-dart/documentation#推荐-为公开发布的-api-编写文档注释)
- [**考虑** 编写库级别（library-level）的文档注释。](https://www.dartcn.com/guides/language/effective-dart/documentation#考虑-编写库级别library-level的文档注释)
- [**推荐** 为私有API 编写文档注释。](https://www.dartcn.com/guides/language/effective-dart/documentation#推荐-为私有api-编写文档注释)
- [**要** 要在文档注释开头有一个单句总结。](https://www.dartcn.com/guides/language/effective-dart/documentation#要-要在文档注释开头有一个单句总结)
- [**要** 让文档注释的第一句从段落中分开。](https://www.dartcn.com/guides/language/effective-dart/documentation#要-让文档注释的第一句从段落中分开)
- [**避免** 与周围上下文冗余。](https://www.dartcn.com/guides/language/effective-dart/documentation#避免-与周围上下文冗余)
- [**推荐** 用第三人称来开始函数或者方法的文档注释。](https://www.dartcn.com/guides/language/effective-dart/documentation#推荐-用第三人称来开始函数或者方法的文档注释)
- [**推荐** 使用名词短语来开始变量、getter、setter 的注释。](https://www.dartcn.com/guides/language/effective-dart/documentation#推荐-使用名词短语来开始变量gettersetter-的注释)
- [**推荐** 使用名词短语来开始库和类型注释。](https://www.dartcn.com/guides/language/effective-dart/documentation#推荐-使用名词短语来开始库和类型注释)
- [**考虑** 在文档注释中添加示例代码。](https://www.dartcn.com/guides/language/effective-dart/documentation#考虑-在文档注释中添加示例代码)
- [**要** 使用方括号在文档注释中引用作用域内的标识符。](https://www.dartcn.com/guides/language/effective-dart/documentation#要-使用方括号在文档注释中引用作用域内的标识符)
- [**要** 使用散文的方式来描述参数、返回值以及异常信息。](https://www.dartcn.com/guides/language/effective-dart/documentation#要-使用散文的方式来描述参数返回值以及异常信息)
- [**要** 把注释文档放到注解之前。](https://www.dartcn.com/guides/language/effective-dart/documentation#要-把注释文档放到注解之前)

**Markdown**

- [**避免** 过度使用 markdown。](https://www.dartcn.com/guides/language/effective-dart/documentation#避免-过度使用-markdown)
- [**避免** 使用 HTML 来格式化文字。](https://www.dartcn.com/guides/language/effective-dart/documentation#避免-使用-html-来格式化文字)
- [**推荐** 使用反引号标注代码。](https://www.dartcn.com/guides/language/effective-dart/documentation#推荐-使用反引号标注代码)

**如何写注释**

- [**推荐** 简洁.](https://www.dartcn.com/guides/language/effective-dart/documentation#推荐-简洁)
- [**避免** 缩写和首字母缩写词，除非很常见。](https://www.dartcn.com/guides/language/effective-dart/documentation#避免-缩写和首字母缩写词除非很常见)
- [**推荐** 使用 “this” 而不是 “the” 来引用实例成员。](https://www.dartcn.com/guides/language/effective-dart/documentation#推荐-使用-this-而不是-the-来引用实例成员)

### Usage

**库**

- [**要** 在 `part of` 中使用字符串。](https://www.dartcn.com/guides/language/effective-dart/usage#要-在-part-of-中使用字符串)
- [**不要** 导入 package 中 `src` 目录下的库。](https://www.dartcn.com/guides/language/effective-dart/usage#不要-导入-package-中-src-目录下的库)
- [**建议** 使用相对路径在导入你自己 package 中的 `lib` 目录。](https://www.dartcn.com/guides/language/effective-dart/usage#建议-使用相对路径在导入你自己-package-中的-lib-目录)

**字符串**

- [**要** 使用临近字符字的方式连接字面量字符串。](https://www.dartcn.com/guides/language/effective-dart/usage#要-使用临近字符字的方式连接字面量字符串)
- [**推荐** 使用插值的形式来组合字符串和值。](https://www.dartcn.com/guides/language/effective-dart/usage#推荐-使用插值的形式来组合字符串和值)
- [**避免** 在字符串插值中使用不必要的大括号。](https://www.dartcn.com/guides/language/effective-dart/usage#避免-在字符串插值中使用不必要的大括号)

**集合**

- [**要** 尽可能的使用集合字面量。](https://www.dartcn.com/guides/language/effective-dart/usage#要-尽可能的使用集合字面量)
- [**不要** 使用 `.length` 来判断一个集合是否为空。](https://www.dartcn.com/guides/language/effective-dart/usage#不要-使用-length-来判断一个集合是否为空)
- [**考虑** 使用高阶（higher-order）函数来转换集合数据。](https://www.dartcn.com/guides/language/effective-dart/usage#考虑-使用高阶higher-order函数来转换集合数据)
- [**避免** 在 `Iterable.forEach()` 中使用字面量函数。](https://www.dartcn.com/guides/language/effective-dart/usage#避免-在-iterableforeach-中使用字面量函数)
- [**不要** 使用 `List.from()` 除非想修改结果的类型。](https://www.dartcn.com/guides/language/effective-dart/usage#不要-使用-listfrom-除非想修改结果的类型)
- [**要** 使用 `whereType()` 按类型过滤集合。](https://www.dartcn.com/guides/language/effective-dart/usage#要-使用-wheretype-按类型过滤集合)
- [**不要** 使用 `cast()`，如果有更合适的方法。](https://www.dartcn.com/guides/language/effective-dart/usage#不要-使用-cast如果有更合适的方法)
- [**避免** 使用 `cast()` 。](https://www.dartcn.com/guides/language/effective-dart/usage#避免-使用-cast-)

**函数**

- [**要** 使用函数声明的方式为函数绑定名称。](https://www.dartcn.com/guides/language/effective-dart/usage#要-使用函数声明的方式为函数绑定名称)
- [**不要** 使用 lambda 表达式来替代 tear-off。](https://www.dartcn.com/guides/language/effective-dart/usage#不要-使用-lambda-表达式来替代-tear-off)

**参数**

- [**要** 使用 `=` 来分隔参数名和参数默认值。](https://www.dartcn.com/guides/language/effective-dart/usage#要-使用--来分隔参数名和参数默认值)
- [**不要** 显式的为参数设置 `null` 值。](https://www.dartcn.com/guides/language/effective-dart/usage#不要-显式的为参数设置-null-值)

**变量**

- [**不要** 显示的为参数初始化 `null` 值。](https://www.dartcn.com/guides/language/effective-dart/usage#不要-显示的为参数初始化-null-值)
- [**避免** 保存可计算的结果。](https://www.dartcn.com/guides/language/effective-dart/usage#避免-保存可计算的结果)

**成员**

- [**不要** 为字段创建不必要的 getter 和 setter 方法。](https://www.dartcn.com/guides/language/effective-dart/usage#不要-为字段创建不必要的-getter-和-setter-方法)
- [**推荐** 使用 `final` 关键字来创建只读属性。](https://www.dartcn.com/guides/language/effective-dart/usage#推荐-使用-final-关键字来创建只读属性)
- [**考虑** 对简单成员使用 `=>` 。](https://www.dartcn.com/guides/language/effective-dart/usage#考虑-对简单成员使用--)
- [**不要** 使用 `this.` ，在重定向命名函数和避免冲突的情况下除外。](https://www.dartcn.com/guides/language/effective-dart/usage#不要-使用-this-在重定向命名函数和避免冲突的情况下除外)
- [**要** 尽可能的在定义变量的时候初始化变量值。](https://www.dartcn.com/guides/language/effective-dart/usage#要-尽可能的在定义变量的时候初始化变量值)

**构造函数**

- [**要** 尽可能的使用初始化形式。](https://www.dartcn.com/guides/language/effective-dart/usage#要-尽可能的使用初始化形式)
- [**不要** 在初始化形式中做类型注释。](https://www.dartcn.com/guides/language/effective-dart/usage#不要-在初始化形式中做类型注释)
- [**要** 用 `;` 来替代空的构造函数体 `{}`。](https://www.dartcn.com/guides/language/effective-dart/usage#要-用--来替代空的构造函数体-)
- [**不要** 使用 `new` 。](https://www.dartcn.com/guides/language/effective-dart/usage#不要-使用-new-)
- [**不要** 冗余地使用 `const` 。](https://www.dartcn.com/guides/language/effective-dart/usage#不要-冗余地使用-const-)

**错误处理**

- [**避免** 使用没有 `on` 语句的 catch。](https://www.dartcn.com/guides/language/effective-dart/usage#避免-使用没有-on-语句的-catch)
- [**不要** 丢弃没有使用 `on` 语句捕获的异常。](https://www.dartcn.com/guides/language/effective-dart/usage#不要-丢弃没有使用-on-语句捕获的异常)
- [**要** 只在代表编程错误的情况下才抛出实现了 `Error` 的异常。](https://www.dartcn.com/guides/language/effective-dart/usage#要-只在代表编程错误的情况下才抛出实现了-error-的异常)
- [**不要** 显示的捕获 `Error` 或者其子类。](https://www.dartcn.com/guides/language/effective-dart/usage#不要-显示的捕获-error-或者其子类)
- [**要** 使用 `rethrow` 来重新抛出捕获的异常。](https://www.dartcn.com/guides/language/effective-dart/usage#要-使用-rethrow-来重新抛出捕获的异常)

**异步**

- [**推荐** 使用 async/await 而不是直接使用底层的特性。](https://www.dartcn.com/guides/language/effective-dart/usage#推荐-使用-asyncawait-而不是直接使用底层的特性)
- [**不要** 在没有有用效果的情况下使用 `async` 。](https://www.dartcn.com/guides/language/effective-dart/usage#不要-在没有有用效果的情况下使用-async-)
- [**考虑** 使用高阶函数来转换事件流（stream）](https://www.dartcn.com/guides/language/effective-dart/usage#考虑-使用高阶函数来转换事件流stream)
- [**避免** 直接使用 Completer 。](https://www.dartcn.com/guides/language/effective-dart/usage#避免-直接使用-completer--)
- [**要** 使用 `Future` 对 `FutureOr` 参数进行测试，以消除参数可能是 `Object` 类型的歧义。](https://www.dartcn.com/guides/language/effective-dart/usage#要-使用-futuret-对-futureort-参数进行测试以消除参数可能是-object-类型的歧义)

### Design

**命名**

- [**要** 使用一致的术语。](https://www.dartcn.com/guides/language/effective-dart/design#要-使用一致的术语)
- [**避免** 缩写。](https://www.dartcn.com/guides/language/effective-dart/design#避免-缩写)
- [**推荐** 把最具描述性的名词放到最后。](https://www.dartcn.com/guides/language/effective-dart/design#推荐-把最具描述性的名词放到最后)
- [**考虑** 尽量让代码看起来像普通的句子。](https://www.dartcn.com/guides/language/effective-dart/design#考虑-尽量让代码看起来像普通的句子)
- [**推荐** 使用名词短语来命名不是布尔类型的变量和属性。](https://www.dartcn.com/guides/language/effective-dart/design#推荐-使用名词短语来命名不是布尔类型的变量和属性)
- [**推荐** 使用非命令式动词短语命名布尔类型的变量和属性。](https://www.dartcn.com/guides/language/effective-dart/design#推荐-使用非命令式动词短语命名布尔类型的变量和属性)
- [**考虑** 省略命名布尔*参数*的动词。](https://www.dartcn.com/guides/language/effective-dart/design#考虑-省略命名布尔参数的动词)
- [**考虑** 为布尔属性或变量取“肯定”含义的名字。](https://www.dartcn.com/guides/language/effective-dart/design#考虑-为布尔属性或变量取肯定含义的名字)
- [**推荐** 使用命令式动词短语来命名带有副作用的函数或者方法。](https://www.dartcn.com/guides/language/effective-dart/design#推荐-使用命令式动词短语来命名带有副作用的函数或者方法)
- [**考虑** 使用名词短语或者非命令式动词短语命名返回数据为主要功能的方法或者函数。](https://www.dartcn.com/guides/language/effective-dart/design#考虑-使用名词短语或者非命令式动词短语命名返回数据为主要功能的方法或者函数)
- [**考虑** 使用命令式动词短语命名一个函数或方法，若果你希望它的执行能被重视。](https://www.dartcn.com/guides/language/effective-dart/design#考虑-使用命令式动词短语命名一个函数或方法若果你希望它的执行能被重视)
- [**避免** 在方法命名中使用 `get` 开头。](https://www.dartcn.com/guides/language/effective-dart/design#避免-在方法命名中使用-get-开头)
- [**推荐** 使用 `to___()` 来命名把对象的状态转换到一个新的对象的函数。](https://www.dartcn.com/guides/language/effective-dart/design#推荐-使用-to___-来命名把对象的状态转换到一个新的对象的函数)
- [**推荐** 使用 `as___()` 来命名把原来对象转换为另外一种表现形式的函数。](https://www.dartcn.com/guides/language/effective-dart/design#推荐-使用-as___-来命名把原来对象转换为另外一种表现形式的函数)
- [**避免** 在方法或者函数名称中描述参数。](https://www.dartcn.com/guides/language/effective-dart/design#避免-在方法或者函数名称中描述参数)
- [**要** 在命名参数时，遵循现有的助记符约定。](https://www.dartcn.com/guides/language/effective-dart/design#要-在命名参数时遵循现有的助记符约定)

**库**

- [**推荐** 使用私有声明。](https://www.dartcn.com/guides/language/effective-dart/design#推荐-使用私有声明)
- [**考虑** 声明多个类在一个库中。](https://www.dartcn.com/guides/language/effective-dart/design#考虑-声明多个类在一个库中)

**类**

- [**避免** 避免为了使用一个简单的函数而去定义一个单一成员的抽象类](https://www.dartcn.com/guides/language/effective-dart/design#避免-避免为了使用一个简单的函数而去定义一个单一成员的抽象类)
- [**避免** 定义仅包含静态成员的类。](https://www.dartcn.com/guides/language/effective-dart/design#避免-定义仅包含静态成员的类)
- [**避免** 集成一个不期望被集成的类。](https://www.dartcn.com/guides/language/effective-dart/design#避免-集成一个不期望被集成的类)
- [**要** 把能够继承的说明添加到文档中，如果这个类可以继承。](https://www.dartcn.com/guides/language/effective-dart/design#要-把能够继承的说明添加到文档中如果这个类可以继承)
- [**避免** 去实现一个不期望成为接口的类（该类不想作为接口被实现）。](https://www.dartcn.com/guides/language/effective-dart/design#避免-去实现一个不期望成为接口的类该类不想作为接口被实现)
- [**要** 对支持接口的类在文档注明](https://www.dartcn.com/guides/language/effective-dart/design#要-对支持接口的类在文档注明)
- [**避免** 去 mixin 一个不期望被 mixin 的类](https://www.dartcn.com/guides/language/effective-dart/design#避免-去-mixin-一个不期望被-mixin-的类)
- [**要** 对支持 mixin 的类在文档注明](https://www.dartcn.com/guides/language/effective-dart/design#要-对支持-mixin-的类在文档注明)

**构造函数**

- [**考虑** 在类支持的情况下，指定构造函数为 `const`。](https://www.dartcn.com/guides/language/effective-dart/design#考虑-在类支持的情况下指定构造函数为--const)

**成员**

- [**推荐** 指定字段或顶级变量为 `final` 。](https://www.dartcn.com/guides/language/effective-dart/design#推荐-指定字段或顶级变量为-final-)
- [**要** 对概念上是访问的属性使用 getter 方法。](https://www.dartcn.com/guides/language/effective-dart/design#要-对概念上是访问的属性使用-getter-方法)
- [**要** 对概念上是修改的属性使用 setter 方法。](https://www.dartcn.com/guides/language/effective-dart/design#要-对概念上是修改的属性使用-setter-方法)
- [**不要** 在没有对应的 getter 的情况下定义 setter。](https://www.dartcn.com/guides/language/effective-dart/design#不要-在没有对应的-getter-的情况下定义-setter)
- [**避免** 从返回类型为 `bool` ， `double` ， `int` 或 `num` 的成员返回 `null` 。](https://www.dartcn.com/guides/language/effective-dart/design#避免-从返回类型为-bool--double--int-或-num-的成员返回-null-)
- [**避免** 为了书写流畅，而从方法中返回 `this` 。](https://www.dartcn.com/guides/language/effective-dart/design#避免-为了书写流畅而从方法中返回-this-)

**类型**

- [**推荐** 为类型不明显的公共字段和公共顶级变量指定类型注解。](https://www.dartcn.com/guides/language/effective-dart/design#推荐-为类型不明显的公共字段和公共顶级变量指定类型注解)
- [**考虑** 为类型不明显的私有字段和私有顶级变量指定类型注解。](https://www.dartcn.com/guides/language/effective-dart/design#考虑-为类型不明显的私有字段和私有顶级变量指定类型注解)
- [**避免** 为初始化的局部变量添加类型注解。](https://www.dartcn.com/guides/language/effective-dart/design#避免-为初始化的局部变量添加类型注解)
- [**避免** 在函数表达式上注解推断的参数类型。](https://www.dartcn.com/guides/language/effective-dart/design#避免-在函数表达式上注解推断的参数类型)
- [**避免** 在泛型调用中参数类型的冗余使用。](https://www.dartcn.com/guides/language/effective-dart/design#避免-在泛型调用中参数类型的冗余使用)
- [**要** 在 Dart 推断类型错误的时候进行类型注解。](https://www.dartcn.com/guides/language/effective-dart/design#要-在-dart-推断类型错误的时候进行类型注解)
- [**推荐** 使用 `dynamic` 注解替换推断失败的情况。](https://www.dartcn.com/guides/language/effective-dart/design#推荐-使用-dynamic-注解替换推断失败的情况)
- [**推荐** 使 function 类型注解的特征更明显](https://www.dartcn.com/guides/language/effective-dart/design#推荐-使-function-类型注解的特征更明显)
- [**不要** 为 setter 方法指定返回类型。](https://www.dartcn.com/guides/language/effective-dart/design#不要-为-setter-方法指定返回类型)
- [**不要** 使用弃用的 typedef 语法。](https://www.dartcn.com/guides/language/effective-dart/design#不要-使用弃用的-typedef-语法)
- [**推荐** 优先使用内联函数类型，而后是 typedef 。](https://www.dartcn.com/guides/language/effective-dart/design#推荐-优先使用内联函数类型而后是-typedef-)
- [**考虑** 在参数上使用函数类型语法。](https://www.dartcn.com/guides/language/effective-dart/design#考虑-在参数上使用函数类型语法)
- [**要** 为类型是任何对象的参数使用 `Object` 注解，而不是 `dynamic` 。](https://www.dartcn.com/guides/language/effective-dart/design#要-为类型是任何对象的参数使用-object-注解而不是-dynamic-)
- [**要** 使用 `Future` 作为无法回值异步成员的返回类型。](https://www.dartcn.com/guides/language/effective-dart/design#要-使用-futurevoid-作为无法回值异步成员的返回类型)
- [**避免** 使用 `FutureOr` 作为返回类型。](https://www.dartcn.com/guides/language/effective-dart/design#避免-使用-futureort-作为返回类型)

**参数**

- [**避免** 布尔类型的位置参数。](https://www.dartcn.com/guides/language/effective-dart/design#避免-布尔类型的位置参数)
- [**避免** 在调用者需要省略前面参数的方法中，使用位置可选参数。](https://www.dartcn.com/guides/language/effective-dart/design#避免-在调用者需要省略前面参数的方法中使用位置可选参数)
- [**避免** 强制参数去接受一个特定表示”空参数”的值。](https://www.dartcn.com/guides/language/effective-dart/design#避免-强制参数去接受一个特定表示空参数的值)
- [**要** 使用开始为闭区间，结束为开区间的半开半闭区间作为接受范围。](https://www.dartcn.com/guides/language/effective-dart/design#要-使用开始为闭区间结束为开区间的半开半闭区间作为接受范围)

**相等**

- [**要** 对重写 `==` 操作符的类，重写 `hashCode` 方法。](https://www.dartcn.com/guides/language/effective-dart/design#要-对重写--操作符的类重写-hashcode-方法)
- [**要** 让 `==` 操作符的相等遵守数学规则。](https://www.dartcn.com/guides/language/effective-dart/design#要-让--操作符的相等遵守数学规则)
- [**避免** 为可变类自定义相等。](https://www.dartcn.com/guides/language/effective-dart/design#避免-为可变类自定义相等)
- [**不要** 在自定义 `==` 操作符中检查 `null` 。](https://www.dartcn.com/guides/language/effective-dart/design#不要-在自定义--操作符中检查-null-)