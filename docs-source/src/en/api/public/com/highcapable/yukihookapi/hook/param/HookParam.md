---
pageClass: code-page
---

::: warning

The English translation of this page has not been completed, you are welcome to contribute translations to us.

You can use the **Chrome Translation Plugin** to translate entire pages for reference.

:::

# HookParam <span class="symbol">- class</span>

```kotlin:no-line-numbers
class HookParam internal constructor(private val creatorInstance: YukiMemberHookCreator, private var param: YukiHookCallback.Param?)
```

**Change Records**

`v1.0` `first`

`v1.1.0` `modified`

移动 `HookParamWrapper` 到 `YukiHookCallback.Param`

修正拼写错误的 **creater** 命名到 **creator**

**Function Illustrate**

> Hook 方法、构造方法的目标对象实现类。

## args <span class="symbol">- field</span>

```kotlin:no-line-numbers
val args: Array<Any?>
```

**Change Records**

在 `v1.0` 添加

**Function Illustrate**

> 获取当前 Hook 对象 `member` 或 `constructor` 的参数对象数组。

这里的数组每项类型默认为 `Any`，你可以使用 `args` 方法来实现 `ArgsModifyer.cast` 功能。

<h2 class="deprecated">firstArgs - field</h2>

**Change Records**

`v1.0` `first`

`v1.0.75` `removed`

请使用 `args(index = 0)` 或 `args().first()`

<h2 class="deprecated">lastArgs - field</h2>

**Change Records**

`v1.0` `first`

`v1.0.75` `removed`

请使用 `args().last()`

## instance <span class="symbol">- field</span>

```kotlin:no-line-numbers
val instance: Any
```

**Change Records**

`v1.0` `first`

**Function Illustrate**

> 获取当前 Hook 实例的对象。

::: danger

如果你当前 Hook 的对象是一个静态，那么它将不存在实例的对象。

:::

## instanceClass <span class="symbol">- field</span>

```kotlin:no-line-numbers
val instanceClass: Class<*>
```

**Change Records**

`v1.0` `first`

**Function Illustrate**

> 获取当前 Hook 实例的类对象。

## member <span class="symbol">- field</span>

```kotlin:no-line-numbers
val member: Member
```

**Change Records**

`v1.1.0` `added`

**Function Illustrate**

> 获取当前 Hook 对象的 `Member`。

在不确定 `Member` 类型为 `Method` 或 `Constructor` 时可以使用此方法。

## method <span class="symbol">- field</span>

```kotlin:no-line-numbers
val method: Method
```

**Change Records**

`v1.0` `first`

**Function Illustrate**

> 获取当前 Hook 对象的方法。

## constructor <span class="symbol">- field</span>

```kotlin:no-line-numbers
val constructor: Constructor
```

**Change Records**

`v1.0` `first`

**Function Illustrate**

> 获取当前 Hook 对象的构造方法。

## result <span class="symbol">- field</span>

```kotlin:no-line-numbers
var result: Any?
```

**Change Records**

`v1.0` `first`

**Function Illustrate**

> 获取、设置当前 Hook 对象的 `method` 或 `constructor` 的返回值。

## hasThrowable <span class="symbol">- field</span>

```kotlin:no-line-numbers
val hasThrowable: Boolean
```

**Change Records**

`v1.1.0` `added`

**Function Illustrate**

> 判断是否存在设置过的方法调用抛出异常。

## throwable <span class="symbol">- field</span>

```kotlin:no-line-numbers
val throwable: Throwable?
```

**Change Records**

`v1.1.0` `added`

**Function Illustrate**

> 获取设置的方法调用抛出异常。

## Throwable.throwToApp <span class="symbol">- i-ext-method</span>

```kotlin:no-line-numbers
fun Throwable.throwToApp()
```

**Change Records**

`v1.1.0` `added`

**Function Illustrate**

> 向 Hook APP 抛出异常。

使用 `hasThrowable` 判断当前是否存在被抛出的异常。

使用 `throwable` 获取当前设置的方法调用抛出异常。

仅会在回调方法的 `MemberHookCreator.beforeHook` 或 `MemberHookCreator.afterHook` 中生效。

::: danger

设置后会同时执行 **resultNull** 方法并将异常抛出给当前 Hook APP。

:::

**Function Example**

Hook 过程中的异常仅会作用于 (Xposed) 宿主环境，目标 Hook APP 不会受到影响。

若想将异常抛给 Hook APP，可以直接使用如下方法。

> The following example

```kotlin
injectMember {
    method {
        // ...
    }
    beforeHook {
        RuntimeException("Test Exception").throwToApp()
    }
}
```

::: danger

向 Hook APP 抛出异常<u>**会对其暴露被 Hook 的事实**</u>，是不安全的，容易被检测，请按实际场景合理使用。

:::

## result <span class="symbol">- method</span>

```kotlin:no-line-numbers
inline fun <reified T> result(): T?
```

**Change Records**

`v1.0.75` `added`

**Function Illustrate**

> 获取当前 Hook 对象的 `method` 或 `constructor` 的返回值 `T`。

<h2 class="deprecated">firstArg - method</h2>

**Change Records**

`v1.0.66` `added`

`v1.0.75` `removed`

<h2 class="deprecated">lastArgs - method</h2>

**Change Records**

`v1.0.66` `added`

`v1.0.75` `removed`

## instance <span class="symbol">- method</span>

```kotlin:no-line-numbers
inline fun <reified T> instance(): T
```

**Change Records**

`v1.0` `first`

**Function Illustrate**

> 获取当前 Hook 实例的对象 `T`。

**Function Example**

你可以通过 `instance` 方法轻松使用泛型 `cast` 为目标对象的类型。

> The following example

```kotlin
instance<Activity>().finish()
```

## args <span class="symbol">- method</span>

```kotlin:no-line-numbers
fun args(): ArgsIndexCondition
```

**Change Records**

`v1.0.75` `added`

**Function Illustrate**

> 获取当前 Hook 对象的 `method` 或 `constructor` 的参数数组下标实例化类。

## args <span class="symbol">- method</span>

```kotlin:no-line-numbers
fun args(index: Int): ArgsModifyer
```

**Change Records**

`v1.0` `first`

`v1.0.75` `modified`

默认值 `index = 0` 移动到新的使用方法 `args().first()`

**Function Illustrate**

> 获取当前 Hook 对象的 `method` 或 `constructor` 的参数实例化对象类。

**Function Example**

你可以通过 `args` 方法修改当前 Hook 实例的方法、构造方法的参数内容。

你可以直接使用 `set` 方法设置 `param` 为你的目标实例，接受 `Any` 类型。

::: danger

请确保 **param** 类型为你的目标实例类型。

:::

> The following example

```kotlin
args(index = 0).set("modify the value")
```

你可以这样直接设置第一位 `param` 的值。

> The following example

```kotlin
args().first().set("modify the value")
```

你还可以直接设置最后一位 `param` 的值。

> The following example

```kotlin
args().last().set("modify the value")
```

你还可以使用 `setNull` 方法设置 `param` 为空。

> The following example

```kotlin
args(index = 1).setNull()
```

你还可以使用 `setTrue` 方法设置 `param` 为 `true`。

::: danger

请确保 **param** 类型为 **Boolean**。

:::

> The following example

```kotlin
args(index = 1).setTrue()
```

你还可以使用 `setFalse` 方法设置 `param` 为 `false`。

::: danger

请确保 **param** 类型为 **Boolean**。

:::

> The following example

```kotlin
args(index = 1).setFalse()
```

## callOriginal <span class="symbol">- method</span>

```kotlin:no-line-numbers
fun callOriginal(): Any?
```

```kotlin:no-line-numbers
fun <T> callOriginal(): T?
```

**Change Records**

`v1.1.0` `added`

**Function Illustrate**

> 执行原始 `Member`。

调用自身未进行 Hook 的原始 `Member` 并调用原始参数执行。

**功能实例**

此方法可以 `invoke` 原始未经 Hook 的 `Member` 对象，取决于原始 `Member` 的参数。

调用自身原始的方法不会再经过当前 `beforeHook`、`afterHook` 以及 `replaceUnit`、`replaceAny`。

比如我们 Hook 的这个方法被这样调用 `test("test value")`，使用此方法会调用其中的 `"test value"` 作为参数。

> The following example

```kotlin
injectMember {
    method {
        name = "test"
        param(StringType)
        returnType = StringType
    }
    afterHook {
        // <方案1> 不使用泛型，不获取方法执行结果，调用将使用原方法传入的 args 自动传参
        callOriginal()
        // <方案2> 使用泛型，已知方法执行结果参数类型进行 cast
        // 假设返回值为 String，失败会返回 null，调用将使用原方法传入的 args 自动传参
        val value = callOriginal<String>()
    }
}
```

## invokeOriginal <span class="symbol">- method</span>

```kotlin:no-line-numbers
fun invokeOriginal(vararg args: Any?): Any?
```

```kotlin:no-line-numbers
fun <T> invokeOriginal(vararg args: Any?): T?
```

**Change Records**

`v1.0` `first`

`v1.1.0` `modified`

不再需要使用 `member.invokeOriginal` 进行调用

**Function Illustrate**

> 执行原始 `Member`。

调用自身未进行 Hook 的原始 `Member` 并自定义 `args` 执行。

**功能实例**

此方法可以 `invoke` 原始未经 Hook 的 `Member` 对象，可自定义需要调用的参数内容。

调用自身原始的方法不会再经过当前 `beforeHook`、`afterHook` 以及 `replaceUnit`、`replaceAny`。

比如我们 Hook 的这个方法被这样调用 `test("test value")`，使用此方法可自定义其中的 `args` 作为参数。

> The following example

```kotlin
injectMember {
    method {
        name = "test"
        param(StringType)
        returnType = StringType
    }
    afterHook {
        // <方案1> 不使用泛型，不获取方法执行结果
        invokeOriginal("test value")
        // <方案2> 使用泛型，已知方法执行结果参数类型进行 cast，假设返回值为 String，失败会返回 null
        val value = invokeOriginal<String>("test value")
    }
}
```

## resultTrue <span class="symbol">- method</span>

```kotlin:no-line-numbers
fun resultTrue()
```

**Change Records**

`v1.0` `first`

**Function Illustrate**

> 设置当前 Hook 对象方法的 `result` 返回值为 `true`。

::: danger

请确保 **result** 类型为 **Boolean**。

:::

## resultFalse <span class="symbol">- method</span>

```kotlin:no-line-numbers
fun resultFalse()
```

**Change Records**

`v1.0` `first`

**Function Illustrate**

> 设置当前 Hook 对象方法的 `result` 返回值为 `false`。

::: danger

请确保 **result** 类型为 **Boolean**。

:::

## resultNull <span class="symbol">- method</span>

```kotlin:no-line-numbers
fun resultNull()
```

**Change Records**

`v1.0` `first`

**Function Illustrate**

::: warning

此方法将强制设置 Hook 对象方法的 **result** 为 **null**。

:::

## ArgsIndexCondition <span class="symbol">- class</span>

```kotlin:no-line-numbers
inner class ArgsIndexCondition internal constructor()
```

**Change Records**

`v1.0.75` `added`

**Function Illustrate**

> 对方法参数的数组下标进行实例化类。

### first <span class="symbol">- method</span>

```kotlin:no-line-numbers
fun first(): ArgsModifyer
```

**Change Records**

`v1.0.75` `added`

**Function Illustrate**

> 获取当前 Hook 对象的 `method` 或 `constructor` 的参数数组第一位。

### last <span class="symbol">- method</span>

```kotlin:no-line-numbers
fun last(): ArgsModifyer
```

**Change Records**

`v1.0.75` `added`

**Function Illustrate**

> 获取当前 Hook 对象的 `method` 或 `constructor` 的参数数组最后一位。

## ArgsModifyer <span class="symbol">- class</span>

```kotlin:no-line-numbers
inner class ArgsModifyer internal constructor(private val index: Int)
```

**Change Records**

`v1.0` `first`

**Function Illustrate**

> 对方法参数的修改进行实例化类。

### cast <span class="symbol">- method</span>

```kotlin:no-line-numbers
fun <T> cast(): T?
```

**Change Records**

`v1.0.66` `added`

`v1.0.68` `modified`

修改 ~~`of`~~ 为 `cast`

**Function Illustrate**

> 得到方法参数的实例对象 `T`。

### byte <span class="symbol">- method</span>

```kotlin:no-line-numbers
fun byte(): Byte?
```

**Change Records**

`v1.0.68` `added`

**Function Illustrate**

> 得到方法参数的实例对象 Byte。

### int <span class="symbol">- method</span>

```kotlin:no-line-numbers
fun int(): Int
```

**Change Records**

`v1.0.66` `added`

`v1.0.68` `modified`

修改 ~~`ofInt`~~ 为 `int`

**Function Illustrate**

> 得到方法参数的实例对象 Int。

### long <span class="symbol">- method</span>

```kotlin:no-line-numbers
fun long(): Long
```

**Change Records**

`v1.0.66` `added`

`v1.0.68` `modified`

修改 ~~`ofLong`~~ 为 `long`

**Function Illustrate**

> 得到方法参数的实例对象 Long。

### short <span class="symbol">- method</span>

```kotlin:no-line-numbers
fun short(): Short
```

**Change Records**

`v1.0.66` `added`

`v1.0.68` `modified`

修改 ~~`ofShort`~~ 为 `short`

**Function Illustrate**

> 得到方法参数的实例对象 Short。

### double <span class="symbol">- method</span>

```kotlin:no-line-numbers
fun double(): Double
```

**Change Records**

`v1.0.66` `added`

`v1.0.68` `modified`

修改 ~~`ofDouble`~~ 为 `double`

**Function Illustrate**

> 得到方法参数的实例对象 Double。

### float <span class="symbol">- method</span>

```kotlin:no-line-numbers
fun float(): Float
```

**Change Records**

`v1.0.66` `added`

`v1.0.68` `modified`

修改 ~~`ofFloat`~~ 为 `float`

**Function Illustrate**

> 得到方法参数的实例对象 Float。

### string <span class="symbol">- method</span>

```kotlin:no-line-numbers
fun string(): String
```

**Change Records**

`v1.0.66` `added`

`v1.0.68` `modified`

修改 ~~`ofString`~~ 为 `string`

**Function Illustrate**

> 得到方法参数的实例对象 String。

### char <span class="symbol">- method</span>

```kotlin:no-line-numbers
fun char(): Char
```

**Change Records**

`v1.0.68` `added`

**Function Illustrate**

> 得到方法参数的实例对象 Char。

### boolean <span class="symbol">- method</span>

```kotlin:no-line-numbers
fun boolean(): Boolean
```

**Change Records**

`v1.0.66` `added`

`v1.0.68` `modified`

修改 ~~`ofBoolean`~~ 为 `boolean`

**Function Illustrate**

> 得到方法参数的实例对象 Boolean。

### any <span class="symbol">- method</span>

```kotlin:no-line-numbers
fun any(): Any?
```

**Change Records**

`v1.0.77` `added`

**Function Illustrate**

> 得到方法参数的实例对象 Any。

### array <span class="symbol">- method</span>

```kotlin:no-line-numbers
inline fun <reified T> array(): Array<T>
```

**Change Records**

`v1.0.68` `added`

**Function Illustrate**

> 得到方法参数的实例对象 Array。

### list <span class="symbol">- method</span>
```kotlin:no-line-numbers
inline fun <reified T> list(): List<T>
```

**Change Records**

`v1.0.68` `added`

**Function Illustrate**

> 得到方法参数的实例对象 List。

### set <span class="symbol">- method</span>

```kotlin:no-line-numbers
fun <T> set(any: T?)
```

**Change Records**

`v1.0` `first`

**Function Illustrate**

> 设置方法参数的实例对象。

### setNull <span class="symbol">- method</span>

```kotlin:no-line-numbers
fun setNull()
```

**Change Records**

`v1.0` `first`

**Function Illustrate**

> 设置方法参数的实例对象为 `null`。

### setTrue <span class="symbol">- method</span>

```kotlin:no-line-numbers
fun setTrue()
```

**Change Records**

`v1.0` `first`

**Function Illustrate**

> 设置方法参数的实例对象为 `true`。

::: danger

请确保目标对象的类型是 **Boolean**。

:::

### setFalse <span class="symbol">- method</span>

```kotlin:no-line-numbers
fun setFalse()
```

**Change Records**

`v1.0` `first`

**Function Illustrate**

> 设置方法参数的实例对象为 `false`。

::: danger

请确保目标对象的类型是 **Boolean**。

:::