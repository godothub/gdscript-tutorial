# 数组方法 API文档摘要

> 对于类型化数组，部分方法的参数类型应根据数组类型而变化，**GDScript不会在传参时进行类型检查，类型不匹配时会造成预期外的情况**

# `bool all(method: Callable) const`

### **参数说明**

* **`method`**：一个用于评估元素是否满足指定条件谓词函数，签名为`func(Variant)->bool`

***

### 方法说明

检查数组中是否所有条件都满足给定谓词

`method`应匹配以下签名：

* 接收一个`Variant`参数（当前的数组元素）

* 返回一个`bool`

***

### **返回值**

对数组中的每一个元素调用给定的函数。

如果所有元素都令`method`返回`true`，或数组是空的，那么该方法返回`true`

如果有任意一个元素不满足条件，该方法会立刻返回`false`(该方法会尽可能早地返回以提高性能)

***

### 示例

```gdscript
func greater_than_5(number):
    return number > 5

func _ready():
    print([6, 10, 6].all(greater_than_5)) # 输出 true （3/3 元素被评估为真）。
    print([4, 10, 4].all(greater_than_5)) # 输出 false （1/3 元素被评估为真）。
    print([4, 4, 4].all(greater_than_5))  # 输出 false （0/3 元素被评估为真）。
    print([].all(greater_than_5))         # 输出 true （0/0 元素被评估为真）。

    # 与上面的第一行相同，但使用 lambda 函数。
    print([6, 10, 6].all(func(element): return element > 5)) # 输出 true
```



# `bool any(method: Callable) const`

### **参数说明**

* **`method`**：一个用于评估元素是否满足指定条件谓词函数，签名为`func(Variant)->bool`

***

### 方法说明

检查数组中是否任意条件满足给定谓词

`method`应匹配以下签名：

* 接收一个`Variant`参数（当前的数组元素）

* 返回一个`bool`

***

### **返回值**

对数组中的每一个元素调用给定的函数。

如果任意元素令`method`返回`true`，该方法会立刻返回`true`(该方法会尽可能早地返回以提高性能)

如果所有元素都不满足条件或数组是空的，则该方法返回`false`

***

### 示例

```gdscript
func greater_than_5(number):
    return number > 5

func _ready():
    print([6, 10, 6].any(greater_than_5)) # 输出 true （3 个元素被评估为真）。
    print([4, 10, 4].any(greater_than_5)) #输出 true （1 个元素被评估为真）。
    print([4, 4, 4].any(greater_than_5))  # 输出 false （0 个元素被评估为真）。
    print([].any(greater_than_5))         # 输出 false （0 个元素被评估为真）。

    # 与上面的第一行相同，但使用 lambda 函数。
    print([6, 10, 6].any(func(number): return number > 5)) # 输出 true
```



# `void append(value: Variant)`

### **参数说明**

* **`value`**：要追加的元素，应匹配数组的元素类型

***

### 方法说明

将 `value`追加到数组末尾（`push_back()` 的别名）。



# `void append_array(array: Array)`

### **参数说明**

* **`array`**：要追加的数组，应匹配数组的元素类型

***

### 方法说明

在数组末尾追加其他`array`。效率优于使用`+=`运算符拼接数组

***

### 示例：

```gdscript
var numbers = [1, 2, 3]
var extra = [4, 5, 6]
numbers.append_array(extra)
print(numbers) # 输出 [1, 2, 3, 4, 5, 6]
```



# `void assign(array: Array)`

### **参数说明**

* **`array`**：要赋值的数组，应匹配目标数组的元素类型

***

### 方法说明

将另一个 `array`的元素赋值到该数组中。该数组的大小将会调整为`array`相同大小

如果数组是有类型的，则执行类型转换。

该方法并非将`array`的引用赋值到该数组，该方法等效于浅拷贝`array`



# `Variant back() const`

### 方法说明

获取数组中的最后一个元素

***

### **返回值**

数组的最后一个元素。

如果数组为空，则失败并返回`null`

该方法与运算符`[]`不同，在发生错误时不会停止项目运行



# `int bsearch(value: Variant, before: bool = true) const`

### **参数说明**

* **`value`**：要查找的值

* **`before`**：可选，默认为 `true`。如果为 `true`，返回的索引指示元素会插在所有等于 `value` 的元素之前；否则插在之后。

***

### 方法说明

该方法用于在**已排序数组中**使用二分查找算法查找 `value` 的位置，也可以告诉你应该把它插入到哪里才能保证数组仍然是有序的

**对未排序的数组调用该方法将会有意外行为**

***

### **返回值**

已排序数组中`value`的索引。

如果找不到，则返回`value`应该被插入到数组的哪个位置以保持数组被排序。

如果`before`为`false`，则返回的索引位于数组中所有等于`value`的元素之后

***

### 示例

```gdscript
var numbers = [2, 4, 8, 10]
var idx = numbers.bsearch(7)

numbers.insert(idx, 7)
print(numbers) # 输出 [2, 4, 7, 8, 10]

var fruits = ["Apple", "Lemon", "Lemon", "Orange"]
print(fruits.bsearch("Lemon", true))  # 输出 1，位于第一个 "Lemon"。
print(fruits.bsearch("Lemon", false)) # 输出 3，位于 "Orange"。
```



# `int bsearch_custom(value: Variant, func: Callable, before: bool = true) const`

### **参数说明**

* **`value`**：要查找位置的参考值。

* **`func`**：用于比较的谓词函数，接收 `(element, value)` 两个参数，返回`bool`，指示数组元素`element`是否应该排在`value`后面。

* **`before`**：可选，默认为 true。如果为 true，返回的索引指示元素会插在所有等于 value 的元素之前；否则插在之后。

***

### 方法说明

在**已排序数组中**使用二分查找算法查找 `value` 的位置。
如果找到了等值项，根据 `before` 参数返回插入位置；
如果没找到，则返回应插入的位置以保持排序（依据`func`参数)。

注意：数组必须先使用 `sort_custom(func)` 排好序，否则结果不可预期

***

### **返回值**

应插入 `value` 的索引位置，以保持数组使用 `func` 排序后的顺序。

***

### 示例

```gdscript
func sort_by_amount(a, b):
    return a[1] < b[1]

func _ready():
    var my_items = [["Tomato", 2], ["Kiwi", 5], ["Rice", 9]]

    var apple = ["Apple", 5]
    # "Apple" 被插入在 "Kiwi" 之前。
    my_items.insert(my_items.bsearch_custom(apple, sort_by_amount, true), apple)

    var banana = ["Banana", 5]
    # "Banana" 被插入在 "Kiwi" 之后。
    my_items.insert(my_items.bsearch_custom(banana, sort_by_amount, false), banana)

    print(my_items)
    # 输出：
    # [["Tomato", 2], ["Apple", 5], ["Kiwi", 5], ["Banana", 5], ["Rice", 9]]
```



# `void clear()`

### 方法说明

移除该数组中的所有元素

相当于调用 `resize()` 时指定大小为 0。



# `int count(value: Variant) const`

### **参数说明**

* **`value`**：要计数的元素。

***

### 方法说明

获取`value`在数组中出现的次数。如果你想统计**满足某个条件的元素数量**，可以用 `reduce()` 实现

***

### **返回值**

数组中 `value` 出现的次数。



# `Array duplicate(deep: bool = false) const`

### **参数说明**

* **`deep`**：是否进行深拷贝。默认为 `false`（浅拷贝）。

***

### 方法说明

拷贝一份该数组的副本

***

### **返回值**

该数组的一个副本。

如果 `deep == false`：浅拷贝，嵌套的数组或字典会**共享引用**。

如果 `deep == true`：深拷贝，嵌套的数组或字典也会被**递归复制**，互不影响。



# `void erase(value: Variant)`

### **参数说明**

* **`value`**：要移除的目标元素

***

### 方法说明

查找并移除数组中**第一个**与 `value` 相等的元素。

如果数组中没有这个值，就什么也不做（不会报错)。
移除后，**后面的元素会整体往前移动一位**，所以在**大数组中频繁使用可能会影响性能**。

**不要在遍历数组时调用 `erase()`！**  这会导致奇怪的行为发生



# `void fill(value: Variant)`

### **参数说明**

* **`value`**：要填充进每个元素的值。

***

### 方法说明

把数组的每个元素都设置成给定的 `value`。

常和 `resize()` 一起用，用于创建初始化好的数组

**注意：如果 `value` 是引用类型（比如 `Object`、`Array`、`Dictionary`），数组里的每一项都会共享同一个引用**，不是独立副本！

***

### 示例

```gdscript
var array = []
array.resize(5)
array.fill(2)
print(array)  # 输出 [2, 2, 2, 2, 2]
```



# **`Array filter(method: Callable) const`**

### 参数说明

* **`method`**：用于判断是否保留元素的谓词函数，接收一个元素，返回 `true` 表示保留，`false` 表示过滤掉。

***

### 方法说明

对数组中的每个元素调用 `method`，返回一个**只包含返回值为 true 的元素的新数组**。

适合用来做筛选操作，比如找出所有偶数、正数、特定条件下的对象等等

***

### 返回值

一个包含通过筛选条件的元素的新数组。

***

### **示例**

```gdscript
func is_even(number):
    return number % 2 == 0

func _ready():
    print([1, 4, 5, 8].filter(is_even))
    # 输出: [4, 8]

    # 使用 lambda 方式实现同样功能
    print([1, 4, 5, 8].filter(func(number): return number % 2 == 0))
```



# `int find(what: Variant, from: int = 0) const`

### 参数说明

* **`what`**：要查找的元素。

* **`from`**：起始索引（可选，默认为 0）。

***

### 方法说明

查找从 `from` 开始查找 `what` 在数组中**首次出现的索引**。

如果没找到，返回 -1。

搜索时是**强类型匹配**的，比如 `7` 和 `7.0` 不被视为相等（`int` ≠ `float`）。

要判断元素是否存在可以使用 `has()`，或者 GDScript 的 `in` 关键字

***

### 返回值

`what` 首次出现的索引，找不到则返回 `-1`。



# **`int find_custom(method: Callable, from: int = 0) const`**

### 参数说明

* **`method`**：用于判断元素是否符合条件的谓词函数，接收一个元素，返回 `true` 表示找到目标。

* **`from`**：搜索起始索引（可选，默认为 0）。

***

### 方法说明

从 `from` 开始遍历数组，调用 `method(element)`，返回第一个使 `method` 返回 `true` 的元素的索引。

如果没有符合条件的元素，则返回 `-1`。

适合用来找**第一个满足特定条件**的元素位置，比如第一个偶数、第一个非空字符串、符合属性的对象等等

如果你**只想知道有没有符合条件的元素**，请使用 `any()`

***

### 返回值

符合条件的第一个元素的索引，找不到返回 `-1`。

***

### 示例

```gdscript
func is_even(number):
    return number % 2 == 0

func _ready():
    print([1, 3, 4, 7].find_custom(is_even.bind()))
    # 输出: 2 （第一个偶数是 4，索引为 2）
```

# `Variant front() const`

### 方法说明

获取数组的**第一个元素**。

如果数组为空，返回 `null`，**不会报错也不会中断程序**，和 `array[0]` 不一样

***

### 返回值

数组的第一个元素，若数组为空则为 `null`。

相关：见 `back()` 用于获取最后一个元素。

# `Variant get(index: int) const`

### 参数说明

* **`index`**：要访问的元素索引。

***

### 方法说明

获取数组中给定索引的元素。与 `array[index]` 效果相同，就是更显式一点

***

### 返回值

指定索引位置的元素。

# `int get_typed_builtin() const`

### 方法说明

获取和这个类型化数组相关联的内置类型

如果这是个**类型化数组**，返回其元素的内置类型（比如 `TYPE_INT`、`TYPE_STRING`等）。
否则返回 `TYPE_NIL`（表示不是类型化的）。

***

### 返回值

类型化数组的元素类型，对应 `Variant.Type` 常量；若非类型化数组则为 `TYPE_NIL`。

# `StringName get_typed_class_name() const`

### 方法说明

获取和这个类型化数组相关联的内置类名

如果数组是一个 `Object` 类型的类型化数组，返回它绑定的类名。
否则，返回一个空的 `StringName`。

可配合 `Object.get_class()` 使用进行类型判断

***

### 返回值

类型化数组的类名，或空 `StringName`。

# `Variant get_typed_script() const`

### 方法说明

获取和这个类型化数组相关联的脚本（Script 实例），如果有的话。
如果没有绑定脚本，就返回 `null`。

***

### 返回值

数组关联的 `Script`实例，若无则为 `null`。

# `bool has(value: Variant) const`

### 参数说明

* **`value`**：要查找的目标值。

***

### 方法说明

检查数组中是否包含指定的 `value`，**有就返回 true，没有就返回 false**

在 GDScript 中，相当于使用 `in` 运算符，比如：

```gdscript
if 4 in [2, 4, 6, 8]:
    print("里面有 4！")  # 会输出
```

注意：比较时会**严格区分类型**，`7`（`int`） 和 `"7"`（`string`）是不同的，`7.0`（`float`）也不等于 `7`（`int`）！

***

### 返回值

布尔值，表示是否包含该元素。

***

### 示例

```gdscript
print(["inside", 7].has("inside"))  # 输出 true
print(["inside", 7].has("outside")) # 输出 false
print(["inside", 7].has(7))         # 输出 true
print(["inside", 7].has("7"))       # 输出 false
```

# `int hash() const`

### 方法说明

返回一个代表该数组内容的 32 位哈希值（整数）。

这个值可以用于快速比较、放入哈希表等情况

**哈希相同不等于数组一定相同**（可能发生哈希冲突）
**但！哈希不同的数组一定是不同的**

***

### 返回值

数组及其内容的哈希值（整数类型）。

# `int insert(position: int, value: Variant)`

### 参数说明

* **`position`**：要插入的位置（从 0 开始）。

* **`value`**：要插入的新元素。

***

### 方法说明

在数组中的 `position` 位置插入 `value`。
`position` 必须介于 `0 ~ size()` 之间，否则会失败～

插入后，所有在该位置后的元素都会**往后挪一格**，所以在大数组里频繁插入可能会稍微卡卡的！

***

### 返回值

成功返回 `OK`，失败时返回错误码（`Error` 枚举中的值）。

# `bool is_empty() const`

### 方法说明

如果数组是空的（长度为 0），就返回 `true`。
是 `[]` 就算空～超简单的状态判断

***

### 返回值

`true` 表示数组为空，`false` 表示有内容。

# `bool is_read_only() const`

### 方法说明

检查该数组是否是**只读的**。

只读数组不能删改元素

如果你用 `const` 声明这个数组（在 GDScript 中），它就是只读的～不能增删改元素，只能乖乖看不能动，但`var`声明的只读数组可以将一个新的数组实例赋予它解除只读状态！

***

### 返回值

如果数组是只读的返回 `true`，否则返回 `false`。

# `bool is_same_typed(array: Array) const`

### 参数说明

* **`array`**：另一个要比较类型的数组。

***

### 方法说明

比较两个数组是否是**相同类型化**的数组

如果两者都有类型化定义，且类型相同，就返回 `true`。

***

### 返回值

类型一样就返回 `true`，不一样就返回 `false`。

# `bool is_typed() const`

### 方法说明

判断这个数组是不是**类型化数组**（typed array）
类型化数组只能包含某个指定类型的元素，在 GDScript 里可以用静态类型定义

***

### 返回值

如果是类型化数组，返回 `true`；否则为 `false`。

***

### 示例

```gdscript
var numbers: Array[float] = [0.2, 4.2, -2.0]
print(numbers.is_typed()) # 输出 true
```

# `void make_read_only()`

### 方法说明

让数组变成**只读模式**，之后你就不能增删元素或改动顺序

注意：**嵌套的 `Dictionary`或 `Array`不会被影响**，它们仍然可以修改。

在 GDScript 中，如果你用 `const` 声明一个数组，它默认就是只读的了

# `Array map(method: Callable) const`

### 参数说明

* **`method`**：一个重映射函数，拥有一个参数接收数组的元素并返回一个新值。

***

### 方法说明

对数组的每个元素调用 `method`，重映射该数组，即把**返回的值组成一个新数组**！
相当于把数组“变形”成另一个数组

常用于元素的批量转换，比如数字翻倍、对象提取属性等。

***

### 返回值

一个新数组，包含 `method` 返回的所有值。

***

### 示例

```gdscript
func double(number):
    return number * 2

func _ready():
    print([1, 2, 3].map(double))
    # 输出: [2, 4, 6]

    # 使用 lambda
    print([1, 2, 3].map(func(element): return element * 2))

```

# `Variant max() const`

### 方法说明

获取数组中的最大值～前提是所有元素**能比较**（例如都为数值、字符串等）。

如果元素不能比较，就会返回 `null`

想使用自定义规则获取最大值？用 `reduce()` 更灵活

***

### 返回值

最大值，或 `null`（元素不可比较时）。

# `Variant min() const`

### 方法说明

获取数组中的最小值，和 `max()` 一样，要求所有元素可以进行比较。

如果不能比较（比如混合了对象和数字），会返回 `null`。

***

### 返回值

最小值，或 `null`（元素不可比较时）。

# `Variant pick_random() const`

### 方法说明

从数组中随机选一个元素并返回，就像抽盲盒一样

如果数组是空的，会生成一个错误，并返回 `null`。

使用的是全局随机种子，跟 `randi()`、`shuffle()` 是一家的～
想要结果可预测？可以先用 `seed()` 设置随机种子！

***

### 返回值

数组中的随机一个元素，空数组时为 `null`。

***

### 示例

```gdscript
print([1, 2, 3.25, "Hi"].pick_random())  # 可能输出任意一项
```

# `Variant pop_at(position: int)`

### 参数说明

* **`position`**：要移除的索引，可以为负数（表示从数组尾部往前数）。

***

### 方法说明

移除并返回数组中指定位置的元素。

如果数组是空的，返回 `null`。

如果 `position` 越界，会报错

移除后，后面的元素会整体前移一格，**大数组频繁操作会稍微卡**～

***

### 返回值

被移除的元素，失败时为 `null`。

# `Variant pop_back()`

### 方法说明

移除并返回数组中**最后一个元素**。

如果数组为空，返回 `null`，**不会报错**

相关方法：想移前面的？可以用 `pop_front()`

***

### 返回值

被移除的最后一个元素，数组为空时为 `null`。

# `Variant pop_front()`

### 方法说明

移除并返回数组的**第一个元素**。

如果数组是空的，就返回 `null`，不会报错

移除后，后面的元素都会往前挪动一格

**大数组频繁使用可能会有性能消耗**

***

### 返回值

被移除的第一个元素，数组为空时为 `null`。

# `void push_back(value: Variant)`

### 参数说明

* **`value`**：要添加的新元素。

***

### 方法说明

在数组**末尾**添加一个元素，可以用于模拟栈结构

相关操作：想从前面添加？用 `push_front()`

# `void push_front(value: Variant)`

### 参数说明

* **`value`**：要添加的新元素。

***

### 方法说明

在数组**开头**添加一个元素，把它插在最前面

添加后，原本所有元素的索引都会整体往后移一格！

所以如果数组很大，频繁使用会有性能负担

相关操作：从末尾添加可以用 `push_back()`

# **`Variant reduce(method: Callable, accum: Variant = null) const`**

### 参数说明

* **`method`**：用于处理每个元素的函数，接收两个参数：当前累计值（`accum`）和数组当前元素。

* **`accum`**：初始累计值（可选）。如果是 `null`，将使用数组的第一个元素作为初始值，从第二个开始遍历。

***

### 方法说明

对数组从头到尾遍历，每次调用 `method(accum, element)` 来更新累计值，最终返回这个累计结果

用它可以做：

* 累加/求和

* 自定义最大值/最小值比较

* 条件统计

* 构造复杂结构…

相关方法：
`map()` → 变形，`filter()` → 筛选，`any()` `all()` → 条件判断

***

### 返回值

最终累计出来的结果。

***

### 示例①：求和

```gdscript
func sum(accum, number):
    return accum + number

func _ready():
    print([1, 2, 3].reduce(sum, 0))  # 输出 6
    print([1, 2, 3].reduce(sum, 10)) # 输出 16

    # 使用 lambda 表达式
    print([1, 2, 3].reduce(func(accum, number): return accum + number, 10))

```

***

### 示例②：自定义比较，取最大向量

```gdscript
func is_length_greater(a, b):
    return a.length() > b.length()

func _ready():
    var arr = [Vector2i(5, 0), Vector2i(3, 4), Vector2i(1, 2)]
    var longest_vec = arr.reduce(func(max, vec): return vec if is_length_greater(vec, max) else max)
    print(longest_vec)  # 输出 (3, 4)

```

***

### 示例③：条件计数（计算偶数数量）

```gdscript
func is_even(number):
    return number % 2 == 0

func _ready():
    var arr = [1, 2, 3, 4, 5]
    var even_count = arr.reduce(func(count, next): return count + 1 if is_even(next) else count, 0)
    print(even_count)  # 输出 2
```

# **`void remove_at(position: int)`**

### 参数说明

* **`position`**：要移除的元素索引（必须为非负数）。

***

### 方法说明

移除数组中指定位置的元素，移除后后面的元素会整体往前挪

如果索引无效，会失败（可能报错）

想按**值**移除元素 → 用 `erase()`

想**返回**被移除的值 → 用 `pop_at()`

想移除最后一个元素：`resize(arr.size() - 1)` 就行

# `int resize(size: int)`

### 参数说明

* **`size`**：新的数组长度。

***

### 方法说明

把数组的长度改成 `size`：

* **变短**时，会砍掉末尾元素

* **变长**时，会在末尾添加默认值（通常是 `null`，也可能是类型默认值）

性能比一个个 `append()` 高很多，推荐初始化用它！

***

### 返回值

成功返回 `OK`，失败返回其他 `Error` 类型。

# `void reverse()`

### 方法说明

把数组中的元素顺序整个翻转，前变后、后变前！超简单又常用的操作

# `int rfind(what: Variant, from: int = -1) const`

### 参数说明

* **`what`**：要查找的目标值

* **`from`**：从哪个索引开始反向查找，默认是 -1（即从末尾开始）

***

### 方法说明

从 `from` 开始，**反向查找**目标元素 `what`，返回最后一次出现的索引。

没找到就返回 `-1`
和 `find()` 相对，一个从前往后，一个从后往前！

***

### 返回值

目标值最后一次出现的索引，如果没找到则返回`-1`

# `int rfind_custom(method: Callable, from: int = -1) const`

### 参数说明

* **`method`**：用于评估的谓词函数，接收元素，返回 `true`/`false`。

* **`from`**：从哪个索引开始反向查找，默认是 -1（从末尾）

***

### 方法说明

从数组末尾开始，查找**最后一个满足 `method` 返回 `true`** 的元素索引。

没找到就返回 `-1`
和 `find_custom()` 相对，一个正向找，一个反向找！

***

### 返回值

目标值通过`method`筛选后最后一次出现的索引，如果没找到则返回`-1`

# **`void set(index: int, value: Variant)`**

### 参数说明

* **`index`**：要设置的元素索引。

* **`value`**：要赋的新值。

***

### 方法说明

把数组中指定位置 `index` 的元素改成 `value`
不会改变数组的长度！就只是把那个位置的值**换掉**！

相当于 `array[index] = value` 的写法

# `void shuffle()`

### 方法说明

把数组中的元素**顺序随机打乱**
就像洗扑克牌一样！用来做随机内容、抽奖系统超合适

使用的是全局随机种子（`randi()` 那套），

想要结果可预测？请配合 `seed()` 使用！

# `int size() const`

### 方法说明

返回数组当前包含的元素数量。

空数组（`[]`）总是返回 0。
想判断数组是否为空，用 `is_empty()` 更直白

***

### 返回值

数组的长度（整数）。

# `Array slice(begin: int, end: int = 0x7FFFFFFF, step: int = 1, deep: bool = false) const`

### 参数说明

* **`begin`**：起始索引（包含）。

* **`end`**：结束索引（不包含），默认为很大的值（`Int32`的最大值，代表结尾）。

* **`step`**：步长，默认 1，可负数表示反向。

* **`deep`**：是否进行深拷贝，默认 `false`。

***

### 方法说明

切片数组，从数组中提取一部分片段，组成一个新的数组～可控制：

* 从哪儿开始到哪儿结束；

* 每几个元素取一次；

* 是否反向提取；

* 是否复制嵌套的 `Array`和 `Dictionary`结构（deep copy）。

支持负数索引（从后往前数）

`step < 0` 时数组会被**反向切**，注意 `begin > end` 才有内容！

***

### 返回值

一个新的数组，包含切出来的内容。

***

### 示例

```gdscript
var letters = ["A", "B", "C", "D", "E", "F"]

print(letters.slice(0, 2))       # ["A", "B"]
print(letters.slice(2, -2))      # ["C", "D"]
print(letters.slice(-2, 6))      # ["E", "F"]

print(letters.slice(0, 6, 2))    # ["A", "C", "E"]
print(letters.slice(4, 1, -1))   # ["E", "D", "C"]

```

# `void sort()`

### 方法说明

将数组的元素按**升序**排列，使用标准的 小于（`<`） 比较方式。

支持混合类型（只要能比大小），但注意排序是**不稳定的**，例如 `2` 和 `2.0` 排完后顺序可能会变动。

### 示例

```gdscript
var numbers = [10, 5, 2.5, 8]
numbers.sort()
print(numbers) # 输出 [2.5, 5, 8, 10]

```

# `void sort_custom(func: Callable)`

### 参数说明

* **`func`**：自定义比较函数。接收两个参数，例如：`a` 和 `b`，如果 `a` 应排在 `b` 前面，则返回 `true`。

***

### 方法说明

使用自定义的函数对数组排序，你可以按自己的逻辑排序内容，比如按名字、数值、对象字段、字典 key 等等！

超灵活，适合复杂结构～也能搭配 `lambda` 用法更简洁！
同样是**不稳定排序**，且**不要使用随机返回值**，否则会引发奇怪问题

C# 中不支持该方法，请使用 LINQ 中的 [`System.Linq.Enumerable.OrderBy`](https://learn.microsoft.com/en-us/dotnet/api/system.linq.enumerable.orderby)

排序算法不稳定（相等元素顺序可能变化）

`func` 的返回值必须**一致且可比较**，不要用 `randi()` 之类随机行为！

***

### 示例①：按数组中第二项升序排

```gdscript
func sort_ascending(a, b):
    return a[1] < b[1]

func _ready():
    var my_items = [["Tomato", 5], ["Apple", 9], ["Rice", 4]]
    my_items.sort_custom(sort_ascending)
    print(my_items) # [["Rice", 4], ["Tomato", 5], ["Apple", 9]]

```

***

### 示例②：按名字降序（lambda）

```gdscript
my_items.sort_custom(func(a, b): return a[0] > b[0])
# 输出 [["Apple", 9], ["Tomato", 5], ["Rice", 4]]
```

***

### 示例③：自然字符串排序（按 1,2,10,11 排）

```gdscript
var files = ["newfile1", "newfile2", "newfile10", "newfile11"]
files.sort_custom(func(a, b): return a.naturalnocasecmp_to(b) < 0)
# 输出 ["newfile1", "newfile2", "newfile10", "newfile11"]
```
