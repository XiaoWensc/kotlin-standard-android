
# 资源文件命名规范
- 资源文件需带上模块前缀
- layout文件命名
    - Activity 的 layout 已 module_activity 开头
    - Fragment 的 layout 已 module_fragment 开头
    - Dialog 的 layout 已 module_dialog 开头
    - include 的 layout 已 module_include 开头
    - RecyclerView 的 item layout 已 module_recycle_item 开头
- drawable 资源命名规则
    - 模块名_业务功能描述_控件描述_控件状态限定词；如：`module_login_btn_pressed, module_tabs_icon_home_normal`
- anim 资源命名规则
    - 模块名_逻辑名称_[方向 | 序号]；如：`module_fade_in , module_fade_out , module_push_down_in , module_loading_grey_001`
- color 资源命名规则
    - 使用#AARRGGBB 格式, 写入 module_colors.xml 文件中
    - 模块名_逻辑名称_颜色；如: 
    ```
    <color name="module_btn_bg_color">#33b5e5e5</color>
    ```
- dimen 资源命名规则
    - 使用小写单词+下划线方式命名，写入module_dimens.xml 文件中
    - 模块名_描述信息；如：
    ```
    <dimen name="module_horizontal_line_height">1dp</dimen>
    ```
- style 资源命名规则
    - 采用“ 父style 名称.当前style 名称”方式命名，写入module_styles.xml 文件中，首字母大写
    - 如：
    ```
    <style name="ParentTheme.ThisActivityTheme">
    …
    </style>
    ```
- string 资源文件命名
    - 写入module_strings.xml 文件中
    - 字符串以小写单词+下划线的方式命名；如：`moudule_login_tips,module_homepage_notice_desc`
- id 资源命名
    - 以驼峰法命名，View 组件的资源id 建议以View 的缩写作为前缀。
    - 常用缩写表如下：
        > | 控件        | 缩写            | 
        > | :------------: | :------------: | 
        > | LinearLayout            | ll         |
        > | RelativeLayout            | rl         |
        > | ConstraintLayout            | cl         |
        > | RecyclerView            | rv         |
        > | ScollView            | sv         |
        > | TextView            | tv         |
        > | Button            | btn         |
        > | ImageView            | iv         |
        > | CheckBox            | cb         |
        > | RadioButton            | rb         |
        > | EditText            | input         |

# Kotlin 代码格式规范
## 1. 空格换行
### 1.1 空格
if、for、catch等关键字与其后的（(）之间应当添加一个空格
```
// WRONG!
for(i in 0..1) {
}

// Okay
for (i in 0..1) {
}
```
else、catch等关键字与其后的（}）之间应当添加一个空格
```
// WRONG!
}else {
}

// Okay
} else {
}
```
左花括号（{）前应当添加一个空格.
```
// WRONG!
if (list.isEmpty()){
}

// Okay
if (list.isEmpty()) {
}
```
双目运算符的左右各添加一个空格.
```
// WRONG!
val two = 1+1

// Okay
val two = 1 + 1
```
对于类似的运算符同样适用:

Lambda表达式箭头运算符（->）
```
// WRONG!
ints.map { value->value.toString() }

// Okay
ints.map { value -> value.toString() }
```
例外情况（不应在其左右添加空格）:

使用双冒号运算符（::）引用类成员时
```
// WRONG!
val toString = Any :: toString

// Okay
val toString = Any::toString
```
点运算符（.）
```
// WRONG
it . toString()

// Okay
it.toString()
```
范围运算符（…）
```
// WRONG
for (i in 1 .. 4) print(i)

// Okay
for (i in 1..4) print(i)
```
当且仅当在类定义（继承、实现）及泛型中使用where约束的冒号前（:）应当添加一个空格
```
// WRONG!
class Foo: Runnable

// Okay
class Foo : Runnable

// WRONG
fun <T: Comparable> max(a: T, b: T)

// Okay
fun <T : Comparable> max(a: T, b: T)

// WRONG
fun <T> max(a: T, b: T) where T: Comparable<T>

// Okay
fun <T> max(a: T, b: T) where T : Comparable<T>
```
逗号（,）及冒号（:）之后，应当添加一个空格
```
// WRONG!
val oneAndTwo = listOf(1,2)

// Okay
val oneAndTwo = listOf(1, 2)

// WRONG!
class Foo :Runnable

// Okay
class Foo : Runnable
```
行尾双斜杠（//）注释的左右各添加至少一个空格
```
// WRONG!
var debugging = false//disabled by default

// Okay
var debugging = false // disabled by default
```
### 1.2 换行
在一个类中的属性、构造函数、方法、内部类等成员之间，应添加一个空白换行。例外情况：

两个连续的属性之间（没有其他代码）不强制要求添加空行，但建议根据业务逻辑，使用空行进行分组隔离
```
private var groupAVar1 = 0
private var groupAVar2 = 0
private var groupAVar3 = 0

private var groupBVar1 = 1
private var groupBVar2 = 1
private var groupBVar3 = 1
```
## 2. 大括号
单行的when语句分支、单行的if语句（用于代替三目运算符）不强制要求添加大括号

除以上情况外，任何使用if、when、for、do、while语句时，对于其有效作用域都必须加上大括号。

## 3. 缩进
每次开始书写一个新的代码块时，使用4个空格进行缩进，在代码块结束时，恢复之前的缩进级别，该级别适用于整个块中的代码和注释。

## 4. 枚举类
无函数及文档的常量枚举类，可以定义在一行
```
enum class Answer { YES, NO, MAYBE }
```

## 5. 注解
含有参数的注解，各占一行
```
@Retention(SOURCE)
@Target(FUNCTION, PROPERTY_SETTER, FIELD)
annotation class Global
```

## 6. 命名
### 6.1 包名
包名必须使用小写字母，连续单词直接拼接即可，不允许使用下划线
```
// Okay
package com.example.deepspace
// WRONG!
package com.example.deepSpace
// WRONG!
package com.example.deep_space
```
### 6.2 类名
类名（包括接口名）必须使用首字母大写的驼峰式命名（PascalCase）

类名和接口名建议使用名词或名词短语（例：Character、List），但接口名有时候可为形容词或形容词短语（例：Callable）

测试类建议以Test作为后缀名

### 6.3 方法名
方法名必须使用首字母小写驼峰式命名（camelCase），通常为动词或动词短语（例：stop、handleMessage）

仅在测试方法用于区分逻辑时可以使用下划线，其他情况不允许使用下划线命名
```
@Test fun pop_emptyStack() {
    // …
}
```

### 6.4 常量名
常量命名全部大写，使用下划线连接各单词，通常为名词或名词短语

常量定义的标准：使用val定义，无自定义get方法，内容不可变且无其他影响的属性，包括不可变类型、不可变类型的集合，及使用const修饰的纯量和字符串
```
const val NUMBER = 5
val NAMES = listOf("Alice", "Bob")
val AGES = mapOf("Alice" to 35, "Bob" to 32)
val COMMA_JOINER = Joiner.on(',') // Joiner is immutable
val EMPTY_ARRAY = arrayOf<SomeMutableType>()
```
常量的定义：

建议使用top-level的形式，直接定义在.kt文件中
纯量和字符串形式的常量，必须使用const修饰

**不建议在object或companion object中定义常量，避免开辟不必要的内存空间**
```
// Good
private const val SAMPLE_CONST = 100
class TestClass {
    // Some things
}
// Not Good
class TestClass {
    companion object {
        const val SAMPLE_CONST = 100
    }
}
// Forbidden
class TestClass {
    companion object {
        val SAMPLE_CONST = 100
    }
}
```

### 6.5 非常量名
非常量以首字母小写的驼峰式命名（camelCase），适用于实例属性、本地属性和参数名，通常为名词及名词短语
```
val variable = "var"
val nonConstScalar = "non-const"
val mutableCollection: MutableSet<String> = HashSet()
val mutableElements = listOf(mutableInstance)
val mutableValues = mapOf("Alice" to mutableInstance, "Bob" to mutableInstance2)
val logger = Logger.getLogger(MyClass::class.java.name)
val nonEmptyArray = arrayOf("these", "can", "change")
```

## 7. 注释
### 7.1 格式
建议使用如下的基本的KDoc形式或单行注释
```
/**
 * A func for other use.
 * 
 * @param aParam The first parameter, Type: String?
 * @param bParam The second parameter, Type: Int
 * @return Boolean The result
 */
fun exportFunc(aParam: String?, bParam: Int) : Boolean {
    return false
}

/** An especially short bit of KDoc. */
```
未实现、未完成的方法、类，如需要提交代码，建议添加TODO
```
fun incompleteFunc() {
    // TODO To be finished.
}
```
public方法、变量、常量（即对外部暴露的内容）建议用doc的形式编写注释，私有内容不做强制要求，方法建议对参数、返回值进行说明，以便使用者参考，尽快理解含义
