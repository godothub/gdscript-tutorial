# 迭代器接口

GDScript 的 `for ... in ...` 不只能遍历 `Array`、`Dictionary`、`String`、`PackedArray` 等内置类型。只要一个对象实现了 GDScript 约定的迭代器接口，它也可以直接放在 `for` 循环右侧。

这个页面讲的是 GDScript 语言层面的迭代协议；设计模式章节里的“迭代器模式”讲的是更通用的面向对象设计思想。两者相关，但不是同一个东西。

## 什么时候使用

当你写的是普通数组或字典时，不需要自己实现迭代器接口。只有在下面这些情况中，它才有实际价值：

* 你封装了一个自定义集合，不想暴露内部数组。
* 你希望用 `for item in object` 这种写法遍历自定义对象。
* 你需要生成一个范围、序列或筛选结果，但不想提前创建完整数组。
* 你希望调用方只关心“遍历结果”，不关心对象内部如何存储数据。

自定义对象要支持 `for` 遍历，需要实现这三个方法：

```gdscript
func _iter_init(iter: Array) -> bool
func _iter_next(iter: Array) -> bool
func _iter_get(iter: Variant) -> Variant
```

## 执行流程

`for value in object:` 大致会按下面的顺序工作：

1. Godot 创建一个单元素数组作为迭代状态，例如 `[null]`。
2. 调用 `_iter_init(iter)` 初始化状态。如果返回 `false`，循环直接结束。
3. 调用 `_iter_get(iter[0])` 取得当前值，并赋给循环变量。
4. 执行循环体。
5. 调用 `_iter_next(iter)` 推进到下一个状态。如果返回 `true`，回到第 3 步；如果返回 `false`，循环结束。

注意：`_iter_init()` 和 `_iter_next()` 收到的是状态数组 `iter`，而 `_iter_get()` 收到的是 `iter[0]` 的当前值。

## 最小示例

下面这个 `IntRange` 会生成一个包含首尾值的整数范围：

```gdscript
class IntRange:
    var start: int
    var stop: int

    func _init(start_value: int, stop_value: int) -> void:
        start = start_value
        stop = stop_value

    func _iter_init(iter: Array) -> bool:
        iter[0] = start
        return iter[0] <= stop

    func _iter_next(iter: Array) -> bool:
        iter[0] += 1
        return iter[0] <= stop

    func _iter_get(iter: Variant) -> Variant:
        return iter


func _ready() -> void:
    for number in IntRange.new(2, 4):
        print(number)
```

输出：

```text
2
3
4
```

这个例子里，`iter[0]` 存的是当前数字，所以 `_iter_get()` 直接返回它。

## 遍历自定义集合

下面的 `StaticArray` 用内部数组保存数据，但调用方可以像遍历普通数组一样遍历它：

```gdscript
class StaticArray:
    var _items: Array

    func _init(values: Array) -> void:
        _items = values.duplicate(true)

    func size() -> int:
        return _items.size()

    func is_empty() -> bool:
        return _items.is_empty()

    func get_element(index: int) -> Variant:
        assert(index >= 0, "Index must be non-negative.")
        assert(index < _items.size(), "Index out of bounds.")
        return _items[index]

    func set_element(index: int, value: Variant) -> void:
        assert(index >= 0, "Index must be non-negative.")
        assert(index < _items.size(), "Index out of bounds.")
        _items[index] = value

    func _iter_init(iter: Array) -> bool:
        iter[0] = 0
        return iter[0] < _items.size()

    func _iter_next(iter: Array) -> bool:
        iter[0] += 1
        return iter[0] < _items.size()

    func _iter_get(iter: Variant) -> Variant:
        return _items[int(iter)]


func _ready() -> void:
    var inventory := StaticArray.new(["Potion", "Gold", "Key"])

    for item in inventory:
        print(item)
```

输出：

```text
Potion
Gold
Key
```

这个例子里，`iter[0]` 存的是当前下标，所以 `_iter_get()` 根据下标返回内部数组中的元素。

## 常见错误

不要把迭代状态存在对象字段里，例如 `_iter_index`。这样写在单层循环中可能能工作，但如果同一个对象被嵌套遍历，内层循环会覆盖外层循环的状态。

```gdscript
var values := StaticArray.new([1, 2, 3])

for a in values:
    for b in values:
        print(a, b)
```

上面这种代码要求每一层循环都有独立状态。把状态存在 `iter[0]` 里，可以让 Godot 为每次循环维护自己的状态。

另外要注意：

* `_iter_init()` 必须为第一次迭代设置有效状态。
* 空集合应该在 `_iter_init()` 中返回 `false`。
* `_iter_next()` 应该先推进状态，再判断是否还能继续。
* `_iter_get()` 收到的是当前状态值，不是状态数组。
* 遍历过程中修改集合内容会让结果变得难以预测，通常应避免这样做。
