# 紧缩数组方法 API文档摘要

紧缩数组除字节数组`PackedByteArray`外，都有22个功能相同、签名相似的方法

# 非字节数组通用方法

# `bool append(value: float / int / Vector2 ...)`

### 参数说明

* **`value`**：要追加的元素，类型应和该 `Packed` 数组对应（如 `float`、`int`、`String`、`Vector2` 等）

***

### 方法说明

向数组末尾追加一个元素(`push_back()`的别名)

***

### 返回值

是否成功追加，返回 `true` 或 `false`



# `void append_array(array: PackedInt32Array / PackedFloat32Array ...)`

### 参数说明

* **`array`**: 另一个同类型的 Packed 紧缩数组，将被整体追加到当前数组末尾。

***

### 方法说明

将传入的数组内容整体追加到当前数组后方，性能优于使用`+=`运算符拼接数组



# `int bsearch(value: int / float / Vector2 / ..., before: bool = true)`

### 参数说明

* **`value`**：要查找的目标值，类型应与数组匹配

* **`before`**（可选）：默认为 `true`。如果为 `true`，返回的索引指示元素会插在所有等于 `value` 的元素之前；否则插在之后。

***

### 方法说明

使用**二分查找**在排序好的数组中查找目标值的位置：

* 如果找到，返回其索引

* 如果没找到，返回可插入该值以维持排序的位置

若数组未排序，则结果不可预期

对于三个向量类型和两个浮点数类型的紧缩数组，如果数组中包含NaN，则这个方法的结果可能不准确。

***

### 返回值

目标值在数组中的索引，或应插入的位置



# **`void clear()`**

### 方法说明

清空数组，相当于 `resize(0)`



# **`int count(value: int / float / Vector2 / ...)`**

### 参数说明

* **`value`**：要统计出现次数的值，需与数组元素类型一致

***

### 方法说明

统计数组中 `value` 出现了多少次

对于三个向量类型和两个浮点数类型的紧缩数组，如果数组中包含NaN，则这个方法的结果可能不准确。

***

### 返回值

一个整数，表示目标值的出现次数



# **`PackedInt32Array / PackedFloat32Array / ... duplicate()`**

### 方法说明

拷贝一份该数组的副本

新数组与原数组内容相同，但为不同实例，彼此独立

### 返回值

该数组的副本



# **`void fill(value: int / float / Vector2 / ...)`**

### 参数说明

* **`value`**：填充用的值，应与数组类型一致

***

### 方法说明

把数组里的**每个元素都变成同一个值，** 适合配合 `resize()` 一起使用

对于三个向量类型和两个浮点数类型的紧缩数组，如果数组中包含NaN，则这个方法的结果可能不准确。



# **`int find(value: int / float / Vector2 / ..., from: int = 0)`**

### 参数说明

* **`value`**：要查找的元素

* **`from`**（可选）：起始查找位置，默认是数组开头

***

### 方法说明

查找 `value` 在数组中的首次出现位置
如果没找到，就返回 `-1`

对于三个向量类型和两个浮点数类型的紧缩数组，如果数组中包含NaN，则这个方法的结果可能不准确。

***

### 返回值

元素首次出现的索引，或 -1（表示未找到）



# **`int get(index: int)`**

### 参数说明

* **`index`**：目标索引位置

***

### 方法说明

返回数组中指定位置的元素，等同于 `array[index]` 的效果

***

### 返回值

对应索引处的值



# **`bool has(value: int / float / Vector2 / ...)`**

### 参数说明

* **`value`**：要查找的值，类型需与数组一致

***

### 方法说明

判断数组中是否**包含某个值**，有就返回 `true`，否则返回 `false`

也可以用 `in` 运算符来写更简洁的语法

对于三个向量类型和两个浮点数类型的紧缩数组，如果数组中包含NaN，则这个方法的结果可能不准确。

***

### 返回值

一个布尔值，指示值是否存在于数组中，存在则返回`true`，否则为`false`



# **`int insert(at_index: int, value: int / float / Vector2 / ...)`**

### 参数说明

* **`at_index`**：插入的位置（0 到数组末尾之间）

* **`value`**：要插入的值

***

### 方法说明

在数组指定位置插入新元素

之后的元素都会整体往后挪动一个位置。

***

### 返回值

如果插入成功，返回 `OK`；失败时返回对应错误码



# **`bool is_empty() const`**

### 方法说明

判断数组是否为空

***

### 返回值

如果数组为空返回`true`，否则返回`false`

# **`bool push_back(value: int / float / Vector2 / ...)`**

### 参数说明

* **`value`**：要添加的元素，需与数组类型一致

***

### 方法说明

把一个元素追加到数组的末尾

是 `append()` 的另一个名字

***

### 返回值

返回一个布尔值，指示是否成功添加元素



# **`void remove_at(index: int)`**

### 参数说明

* **`index`**：要移除的元素位置（不能为负数）

***

### 方法说明

移除数组中指定位置的元素，后面的元素都会整体前移一位



# **`int resize(new_size: int)`**

### 参数说明

* **`new_size`**：要设定的新长度

***

### 方法说明

更改数组大小

* 增大时自动填充数组类型的默认值

* 缩小时从尾部截断

效率比逐个 `push_back()` 高得多

***

### 返回值

如果成功，返回 `OK`；失败时返回对应错误码



# **`void reverse()`**

### 方法说明

把数组中的元素顺序整个翻转，前变后、后变前



# **`int rfind(value: int / float / Vector2 / ..., from: int = -1)`**

### 参数说明

* **`value`**：要找的目标值

* **`from`**（可选）：从哪个索引开始往前查找，默认为数组末尾，如果为负数则被视为相对于数组的结尾。

***

### 方法说明

从后往前找某个值在数组中**最后一次出现的位置**
找不到就返回 `-1`

对于三个向量类型和两个浮点数类型的紧缩数组，如果数组中包含NaN，则这个方法的结果可能不准确。

***

### 返回值

目标值最后一次出现的索引，如果没找到则返回`-1`



# **`void set(index: int, value: int / float / Vector2 / ...)`**

### 参数说明

* **`index`**：要修改的目标位置

* **`value`**：要设置的新值，类型需匹配数组元素类型

***

### 方法说明

设置指定位置的元素为新值
和 `array[index] = value` 一样的效果



# **`int size() const`**

### 方法说明

获取数组当前的长度

***

### 返回值

一个整数，表示数组当前的长度



# **`PackedInt32Array / PackedFloat32Array / ... slice(begin: int, end: int = 0x7FFFFFFF) const`**

### 参数说明

* **`begin`**：起始索引（包含）

* **`end`**（可选）：结束索引（不包含），默认会切到数组末尾

***

### 方法说明

返回从 `begin` 到 `end` 之间的**新数组切片**～不影响原数组本体。

支持负索引（表示从尾部数起），非常灵活方便

例如 `arr.slice(1)` 等同于 `arr.slice(1, arr.size())` ，`arr.slice(0, -2)`等同于`arr.slice(0, arr.size() - 2)`

***

### 返回值

一个新的 PackedArray，包含所选范围的元素



# **`void sort()`**

### 方法说明

将数组中的元素按升序排列

使用内置比较规则（即“小于”关系），较小的值在前，较大的值在后

对于三个向量类型和两个浮点数类型的紧缩数组，如果数组中包含NaN，则这个方法的结果可能不准确。



# **`PackedByteArray to_byte_array() const`**

### 方法说明

将当前 `PackedArray`转换为字节数组（`PackedByteArray`），不同类型的元素将按照**特定的方式编码为字节序列**。
返回的新数组不修改原数组，适合序列化、保存或网络传输等用途

**字节数组`PackedByteArray`不具备该方法**

***

### 编码差异说明

| 原始类型                                             | 每元素编码字节数    | 编码格式说明                          |
| ------------------------------------------------ | ----------- | ------------------------------- |
| PackedInt32Array                                 | 4 字节        | 每个整数以 32 位（4 字节）形式编码            |
| PackedInt64Array                                 | 8 字节        | 每个整数以 64 位（8 字节）形式编码            |
| PackedFloat32Array                               | 4 字节        | 每个浮点数以 IEEE 754 单精度编码           |
| PackedFloat64Array                               | 8 字节        | 每个浮点数以 IEEE 754 双精度编码           |
| PackedColorArray                                 | 4 字节 × 4 通道 | 每个颜色的 R/G/B/A 通道分别编码为 4 字节      |
| PackedVector2Array / Vector3Array / Vector4Array | 4 字节 × 每个分量 | 每个 float 分量编码为 4 字节，依次存储        |
| PackedStringArray                                | 不定长度        | 每个字符串以 UTF-8 编码，并追加一个 null 字节结尾 |

字符串结尾会追加一个`null`字节作为结尾标记，例如：`"Hello" → [72, 101, 108, 108, 111, 0]`

多出来的 `0`（null 字节）就是结尾标记，表示字符串结束



编码后的字节数组长度就是原始数组长度乘字节数，例如:

int32数组编码后的长度为：`int32_arr.size() * 4`

float64数组编码后的长度为：`float64_arr.size() * 8`

由于字符串数组中每个字符串因不同的语言和内容，字节长度都不一定一致，因此不能使用上面的方法计算

***

### 返回值

一个新的 `PackedByteArray`，包含对应编码后的字节数据



# 字节数组特有方法

字节数组包含非字节数组所拥有的除去`to_byte_array()`外的所有21个通用方法，同时也提供了将各种类型编码为字节或从字节解码的方法

### 数据压缩 / 解压相关

* `compress(compression_mode: int = 0)`
  使用指定压缩模式(`FileAccess.CompressionMode`) 压缩数据，返回新的 PackedByteArray。

* `decompress(buffer_size: int, compression_mode: int = 0)`
  解压数据，需提供预估的解压后大小 `buffer_size`，返回新的 PackedByteArray。

* `decompress_dynamic(max_output_size: int, compression_mode: int = 0)`
  解压数据，无需提前知道大小，但允许设置最大解压限制，`-1`表示不限制，压缩模式只支持 `brotli`/`gzip`/`deflate`，返回新的 PackedByteArray。

### 数据解码（decode）

所有 `decode_*()` 方法都从指定的字节偏移处读取对应类型的值。

字节数不足时，读取失败则返回`0.0`或`null`

#### 浮点数：

* `decode_half(offset)`：解码 16 位 float（半精度）

* `decode_float(offset)`：解码 32 位 float（单精度）

* `decode_double(offset)`：解码 64 位 float（双精度）

#### 有符号整数：

* `decode_s8(offset)`：解码 8 位有符号整数

* `decode_s16(offset)`：解码 16 位有符号整数

* `decode_s32(offset)`：解码 32 位有符号整数

* `decode_s64(offset)`：解码 64 位有符号整数

#### 无符号整数：

* `decode_u8(offset)`：解码 8 位无符号整数

* `decode_u16(offset)`：解码 16 位无符号整数

* `decode_u32(offset)`：解码 32 位无符号整数

* `decode_u64(offset)`：解码 64 位无符号整数

#### Variant 解码

* `decode_var(offset, allow_objects = false)`
  从偏移位置解码一个 Variant，支持复杂类型，可选是否允许 `Object` 类型，当数据是派生自`Object`的类型而`allow_objects`为`false`时，则返回`null`。

* `decode_var_size(offset, allow_objects = false)`
  获取从偏移位置开始的 Variant 数据所占的字节大小。要求起始位置后至少有 4 个字节的数据，否则会失败。

### 编码方法（encode）

这些方法会将数值编码成二进制字节写入数组，从 `byte_offset` 开始，必须保证数组已有足够的空间！

#### 浮点数编码

* `encode_half(offset, value)`：将 float 编码为 16 位（2 字节）

* `encode_float(offset, value)`：将 float 编码为 32 位（4 字节）

* `encode_double(offset, value)`：将 float 编码为 64 位（8 字节）

#### 有符号整数编码

* `encode_s8(offset, value)`：8 位（1 字节）

* `encode_s16(offset, value)`：16 位（2 字节）

* `encode_s32(offset, value)`：32 位（4 字节）

* `encode_s64(offset, value)`：64 位（8 字节）

#### 无符号整数编码

* `encode_u8(offset, value)`：8 位（1 字节）

* `encode_u16(offset, value)`：16 位（2 字节）

* `encode_u32(offset, value)`：32 位（4 字节）

* `encode_u64(offset, value)`：64 位（8 字节）

#### Variant 编码

* `encode_var(offset, value, allow_objects = false)`
  将 `Variant` 编码为字节数据，返回写入的字节数。支持大部分类型，如果禁止`Object`序列化，即`allow_objects`为`false`，则只会将其ID进行序列化

### 从字节数组还原到字符串

* `get_string_from_ascii()`
  按照 **ASCII/Latin-1** 解码每个字节为字符，速度快但不支持多字节字符；适合内容全是英文或老式西文编码（是 `String.to_ascii_buffer()` 的逆运算）。

* `get_string_from_utf8()`
  按照 **UTF-8** 解码，支持全球语言字符；解析用户输入建议优先使用它（是 `String.to_utf8_buffer()` 的逆运算）。

* `get_string_from_utf16()`
  按照 **UTF-16** 解码，需注意字节序问题（有 BOM 自动识别，否则按系统默认）；是 `String.to_utf16_buffer()` 的逆运算。

* `get_string_from_utf32()`
  按照 **UTF-32** 解码，同样依赖字节序；是 `String.to_utf32_buffer()` 的逆运算。

* `get_string_from_wchar()`
  按照 **宽字符编码**（Windows 上为 UTF-16，其他平台为 UTF-32）解码，跨平台时要留意平台差异；是 `String.to_wchar_buffer()` 的逆运算。

#### 该用哪一个？

* 不确定来源、要万无一失：用 `get_string_from_utf8()`

* 肯定全是英文/Latin-1：可以考虑 `get_string_from_ascii()`，快一些

* 与平台 API、C/C++ 交互：考虑 `wchar`、`utf16`、`utf32`

* 和你用 `String.to_*_buffer()` 的配对原则就是 —— “谁转的，就找谁还原”

### 类型转换：Byte → PackedXXXArray

这些方法会把 `PackedByteArray` 转换成对应类型的紧缩数组，原理就是按照固定字节块大小（按类型）来“切片重组”

输入数据如果不是合法的对应格式，长度不一致会返回空数组并报错，数据不合法则对应元素会转换为默认值`0.0`

* `to_float32_array()`：每 4 字节 → 一个 float（32 位浮点数），大小需是 4 的倍数。

* `to_float64_array()`：每 8 字节 → 一个 double（64 位浮点数），大小需是 8 的倍数。

* `to_int32_array()`：每 4 字节 → 一个 int32，大小需是 4 的倍数。

* `to_int64_array()`：每 8 字节 → 一个 int64，大小需是 8 的倍数

* `to_color_array()`

* `to_vector2_array()`/`to_vector3_array`/`to_vector4_array`

### 其他实用方法（ByteArray 专属）

* `has_encoded_var(byte_offset: int, allow_objects: bool = false) const`
  判断从指定字节偏移位置开始是否可以解码出合法的 Variant；默认不允许 `Object`类型。

* `hex_encode() const`
  将数组内容编码为字符串形式的十六进制（每个字节转成两位 hex），适合调试或生成校验值等。
