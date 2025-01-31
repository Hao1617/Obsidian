## 数组操作
### 1. 将数组拆分成多个指定大小的块

将数组（array）拆分成多个 `size` 长度的区块，并将这些区块组成一个新数组。 如果`array` 无法被分割成全部等长的区块，那么最后剩余的元素将组成一个区块。
例:
```javascript
_.chunk(['a', 'b', 'c', 'd'], 2);
// => [['a', 'b'], ['c', 'd']]
_.chunk(['a', 'b', 'c', 'd'], 3);
// => [['a', 'b', 'c'], ['d']]
```

### 2.移除数组中的假值，返回一个新的数组，仅包含真值。

创建一个新数组，包含原数组中所有的非假值元素。例如`false`, `null`,`0`, `""`, `undefined`, 和 `NaN` 都是被认为是“假值”。
例:
```javascript
_.compact([0, 1, false, 2, '', 3]);
// => [1, 2, 3]
```

### 3.**合并数组和其他值**，返回一个新的数组

创建一个新数组，将`array`与任何数组 或 值连接在一起。
例:
```javascript
var array = [1];
var other = _.concat(array, 2, [3], [[4]]);
 
console.log(other);
// => [1, 2, 3, [4]]
 
console.log(array);
// => [1]
```

### 4.  获取两个数组的差集

用于**比较两个数组，返回原数组中不包含在另一个数组中的元素**。
####  difference

##### 参数

1. `array` _(Array)_: 要检查的数组。
2. `[values]` _(...Array)_: 排除的值。
##### 返回值

##### 例:

```javascript
_.difference([3, 2, 1], [4, 2]);
// => [3, 1]
```
####  `differenceBy`

##### 参数

1. `array` _(Array)_: 要检查的数组。
2. `[values]` _(...Array)_: 排除的值。
3. `[iteratee=_.identity]` _(Array|Function|Object|string)_: iteratee 调用每个元素。
##### 返回值

_(Array)_: 返回一个过滤值后的新数组。
_(Array)_: 返回一个过滤值后的新数组。

##### 例:

```javascript
_.differenceBy([3.1, 2.2, 1.3], [4.4, 2.5], Math.floor);
// => [3.1, 1.3]
 
// The `_.property` iteratee shorthand.
_.differenceBy([{ 'x': 2 }, { 'x': 1 }], [{ 'x': 1 }], 'x');
// => [{ 'x': 2 }]
```

#### `differenceWith`

##### 参数

1. `array` _(Array)_: 要检查的数组。
2. `[values]` _(...Array)_: 排除的值。
3. `[iteratee=_.identity]` _(Array|Function|Object|string)_: iteratee 调用每个元素。

##### 返回值
_(Array)_: 返回一个过滤值后的新数组。

##### 例:

```javascript
_.differenceBy([3.1, 2.2, 1.3], [4.4, 2.5], Math.floor);
// => [3.1, 1.3]
 
// The `_.property` iteratee shorthand.
_.differenceBy([{ 'x': 2 }, { 'x': 1 }], [{ 'x': 1 }], 'x');
// => [{ 'x': 2 }]
```
- `_.differenceWith` 用于**获取两个数组的差集**，但它允许使用**自定义比较函数**，而不像 `_.differenceBy` 只能基于属性或转换函数比较。
- **适用场景**：
    - 需要**深度比较对象**（如 `_.isEqual`）。
    - 需要**部分匹配**（如只比较对象的某些属性）。

##### 区别：`_.difference`、`_.differenceBy`、`_.differenceWith`

| 方法                                            | 比较方式             | 适用于                             |
| --------------------------------------------- | ---------------- | ------------------------------- |
| `_.difference(array, values)`                 | **严格相等 (`===`)** | 适用于**基本类型**（数字、字符串等）            |
| `_.differenceBy(array, values, iteratee)`     | **基于迭代函数的值**     | 适用于**数据转换后进行比较**（如取整数部分、比较对象属性） |
| `_.differenceWith(array, values, comparator)` | **使用自定义比较函数**    | 适用于**更复杂的比较逻辑**（如对象深度比较）        |
**如果需要更灵活的比较方式，`_.differenceWith` 更适合！**

### 5. 删除数组中的元素

#### `drop`（从左侧移除 `n` 个元素）

##### 参数

1. `array` _(Array)_: 要查询的数组。
2. `[n=1]` _(number)_: 要去除的元素个数。

##### 返回值

_(Array)_: 返回`array`剩余切片。
##### 例:

```javascript
_.drop([1, 2, 3]);
// => [2, 3]
 
_.drop([1, 2, 3], 2);
// => [3]
 
_.drop([1, 2, 3], 5);
// => []
 
_.drop([1, 2, 3], 0);
// => [1, 2, 3]
```

#### `dropRight`（从右侧移除 `n` 个元素）

##### 参数

1. `array` _(Array)_: 要查询的数组。
2. `[n=1]` _(number)_: 要去除的元素个数。

##### 返回值

_(Array)_: 返回`array`剩余切片。

##### 例:

```javascript
_.dropRight([1, 2, 3]);
// => [1, 2]
 
_.dropRight([1, 2, 3], 2);
// => [1]
 
_.dropRight([1, 2, 3], 5);
// => []
 
_.dropRight([1, 2, 3], 0);
// => [1, 2, 3]
```

#### `dropWhile`（按条件从左侧移除）

##### 参数

1. `array` _(Array)_: 要查询的数组。
2. `[predicate=_.identity]` _(Function)_: 这个函数会在每一次迭代调用。

##### 返回值

_(Array)_: 返回`array`剩余切片。

##### 例:

```javascript
var users = [
  { 'user': 'barney',  'active': false },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': true }
];
 
_.dropWhile(users, function(o) { return !o.active; });
// => objects for ['pebbles']
 
// The `_.matches` iteratee shorthand.
_.dropWhile(users, { 'user': 'barney', 'active': false });
// => objects for ['fred', 'pebbles']
 
// The `_.matchesProperty` iteratee shorthand.
_.dropWhile(users, ['active', false]);
// => objects for ['pebbles']
 
// The `_.property` iteratee shorthand.
_.dropWhile(users, 'active');
// => objects for ['barney', 'fred', 'pebbles']
```

#### `dropRightWhile`（按条件从右侧移除）

##### 参数

1. `array` _(Array)_: 要查询的数组。
2. `[predicate=_.identity]` _(Function)_: 这个函数会在每一次迭代调用。

##### 返回值

_(Array)_: 返回`array`剩余切片。

##### 例:

```javascript
var users = [
  { 'user': 'barney',  'active': true },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': false }
];
 
_.dropRightWhile(users, function(o) { return !o.active; });
// => objects for ['barney']
 
// The `_.matches` iteratee shorthand.
_.dropRightWhile(users, { 'user': 'pebbles', 'active': false });
// => objects for ['barney', 'fred']
 
// The `_.matchesProperty` iteratee shorthand.
_.dropRightWhile(users, ['active', false]);
// => objects for ['barney']
 
// The `_.property` iteratee shorthand.
_.dropRightWhile(users, 'active');
// => objects for ['barney', 'fred', 'pebbles']
```

#### 总结

| 方法                                   | 删除方向 | 删除方式        | 适用于                    |
| ------------------------------------ | ---- | ----------- | ---------------------- |
| `_.drop(array, n)`                   | 从左侧  | 删除前 `n` 个元素 | 直接删除**固定数量**的前 `n` 个元素 |
| `_.dropRight(array, n)`              | 从右侧  | 删除后 `n` 个元素 | 直接删除**固定数量**的后 `n` 个元素 |
| `_.dropWhile(array, predicate)`      | 从左侧  | 按**条件**删除   | 按条件删除**左侧的连续元素**       |
| `_.dropRightWhile(array, predicate)` | 从右侧  | 按**条件**删除   | 按条件删除**右侧的连续元素**       |

🔥 **选择指南**
- **直接删除固定数量** → `_.drop(n)` / `_.dropRight(n)`
- **按条件删除左侧元素** → `_.dropWhile`
- **按条件删除右侧元素** → `_.dropRightWhile`
💡 **面试技巧**：
- `_.drop(n)` / `_.dropRight(n)` 适用于**固定数量删除**，**不会受内容影响**。
- `_.dropWhile` / `_.dropRightWhile` 适用于**条件删除**，**遇到不满足条件的元素就停止**。
- **删除是**"连续的"**，只要遇到第一个不符合的，就不会再删了。**
### 6. 填充元素

#### `_.fill`（填充数组的方法）

`_.fill` 用于**修改原数组**，用指定的值填充数组的全部或部分元素。

##### 📌 语法

```javascript
_.fill(array, value, [start=0], [end=array.length])
```

| 参数             | 说明                                    |
| -------------- | ------------------------------------- |
| `array`        | 需要填充的数组（**会被修改**）                     |
| `value`        | 用于填充数组的值                              |
| `start` _(可选)_ | **起始索引**（默认 `0`）                      |
| `end` _(可选)_   | **结束索引**（默认 `array.length`，不包含 `end`） |
##### 📝 基本用法

```javascript
let arr = [1, 2, 3, 4, 5];
_.fill(arr, '*');
console.log(arr);
// => ['*', '*', '*', '*', '*']
```
**解析**：

- `_.fill(arr, '*')` **把数组所有元素替换成 `*`**。
- **注意**：`_.fill` **会修改原数组**，不像 `map` 会返回一个新数组。

---

##### 🎯 只填充部分元素

你可以用 `start` 和 `end` 只填充**指定范围内的元素**。
```javascript
let arr = [1, 2, 3, 4, 5];
_.fill(arr, '*', 1, 4);
console.log(arr);
// => [1, '*', '*', '*', 5]
```

**解析**：

- **`start=1`，`end=4`**，所以填充的是**索引 `1, 2, 3`**（不包含 `4`）。
- **索引 0 和 4 没变**。

---

#####  🚀 结合 `Array(n)` 创建填充数组

如果想创建一个**固定长度、填充默认值的数组**，可以配合 `Array(n)`：
```javascript
_.fill(Array(5), 0);
// => [0, 0, 0, 0, 0]
```
**解析**：

- `Array(5)` 创建一个长度为 5 的数组。
- `_.fill(..., 0)` 把所有元素填充为 `0`。

---

##### **🎯 填充对象（所有元素共享引用）**

```javascript
let arr = _.fill(Array(3), { a: 1 });
console.log(arr);
// => [{ a: 1 }, { a: 1 }, { a: 1 }]

arr[0].a = 2;
console.log(arr);
// => [{ a: 2 }, { a: 2 }, { a: 2 }]
```
**解析**：

- `_.fill(Array(3), { a: 1 })` 填充了**同一个对象引用**。
- **修改一个元素**，所有元素都会变（因为指向同一个对象）。

✅ **解决方案（深拷贝不同对象）**
```javascript
let arr = _.fill(Array(3), _.cloneDeep({ a: 1 }));
```

---

##### 📌 总结

|方法|作用|
|---|---|
|`_.fill(array, value)`|用 `value` 填充整个数组（修改原数组）|
|`_.fill(array, value, start, end)`|只填充**索引 `start` 到 `end-1`** 的部分|
|`_.fill(Array(n), value)`|创建一个长度 `n` 的数组，并填充 `value`|
|**⚠️ 填充对象时要注意**|默认是**同一对象引用**，修改一个会影响所有|

📌 **常见用途**

- **初始化数组**（填充默认值）
- **重置数据**（批量改成相同值）
- **指定范围填充**（局部修改）

##### 参数

1. `array` _(Array)_: 要填充改变的数组。
2. `value` _(*)_: 填充给 `array` 的值。
3. `[start=0]` _(number)_: 开始位置（默认0）。
4. `[end=array.length]` _(number)_:结束位置（默认array.length）。

##### 返回值

_(Array)_: 返回 `array`。

##### 例子

```javascript
var array = [1, 2, 3];
_.fill(array, 'a');
console.log(array);
// => ['a', 'a', 'a']
_.fill(Array(3), 2);
// => [2, 2, 2]
_.fill([4, 6, 8, 10], '*', 1, 3);
// => [4, '*', '*', 10]
```
### 7. 查找索引


#### **🔍 `_.findIndex` vs `_.findLastIndex`（Lodash 查找索引）**

这两个方法都用于查找**符合条件的元素的索引**，但**查找方向不同**：

|方法|作用|查找方向|
|---|---|---|
|`_.findIndex`|查找**第一个**符合条件的元素的索引|**从左到右（索引递增）**|
|`_.findLastIndex`|查找**最后一个**符合条件的元素的索引|**从右到左（索引递减）**|

---

#### **📌 `_.findIndex` 语法**

```javascript
_.findIndex(array, predicate, [fromIndex=0])
```
- **从左到右**查找**第一个匹配的索引**。
- 找不到返回 `-1`。

##### **✅ 示例**

```javascript
let users = [
  { id: 1, name: 'Alice', active: false },
  { id: 2, name: 'Bob', active: true },
  { id: 3, name: 'Charlie', active: false }
];

let index = _.findIndex(users, user => user.active);
console.log(index); 
// => 1  （Bob 是第一个 `active: true` 的用户）
```

---

#### **📌 `_.findLastIndex` 语法**
```javascript
_.findLastIndex(array, predicate, [fromIndex=array.length-1])
```
- **从右到左**查找**最后一个匹配的索引**。
- 找不到返回 `-1`。

##### **✅ 示例**
```javascript
let index = _.findLastIndex(users, user => !user.active);
console.log(index);
// => 2  （Charlie 是最后一个 `active: false` 的用户）
```

---

#### **🎯 对比：`_.findIndex` vs `_.findLastIndex`**
```javascript
let numbers = [1, 2, 3, 4, 5, 6, 2, 8];

let firstIndex = _.findIndex(numbers, num => num === 2);
console.log(firstIndex); 
// => 1  （第一个 2 的索引）

let lastIndex = _.findLastIndex(numbers, num => num === 2);
console.log(lastIndex); 
// => 6  （最后一个 2 的索引）
```
---

#### **🚀 结合 `fromIndex` 控制搜索起点**

你可以指定 `fromIndex` 来调整查找范围。

##### **✅ `_.findIndex` 从索引 2 开始**

js

复制编辑

``let index = _.findIndex(users, user => user.active, 2); console.log(index);  // => -1  （从索引 2 开始找，没有 `active: true`）``

##### **✅ `_.findLastIndex` 从索引 1 开始**

js

复制编辑

``let index = _.findLastIndex(users, user => user.active, 1); console.log(index); // => 1  （索引 1 处的 `Bob` 符合条件）``

---

#### **📌 总结**

|方法|方向|返回值|适用场景|
|---|---|---|---|
|`_.findIndex`|**从左到右**|第一个匹配项的索引|查找**最早出现**的匹配项|
|`_.findLastIndex`|**从右到左**|最后一个匹配项的索引|查找**最后出现**的匹配项|

##### **🚀 使用场景**

- `_.findIndex` **用于查找第一个符合条件的元素**
- `_.findLastIndex` **用于查找最后一个符合条件的元素**
- 结合 `fromIndex` **控制查找范围**

🔥 **示例**

js

复制编辑

`_.findIndex([5, 10, 15, 20], n => n > 10);  // => 2 （索引 2 的 15 是第一个 >10 的数）  _.findLastIndex([5, 10, 15, 20], n => n > 10); // => 3 （索引 3 的 20 是最后一个 >10 的数）`

这两个方法在**数组查询、数据分析、过滤**等场景中非常有用！🚀

##### 参数

1. `array` _(Array)_: 要搜索的数组。
2. `[predicate=_.identity]` _(Array|Function|Object|string)_: 这个函数会在每一次迭代调用。
3. `[fromIndex=0]` _(number)_: The index to search from.

##### 返回值

_(number)_: 返回找到元素的 索引值（index），否则返回 `-1`。

##### 例子

```javascript
var users = [
  { 'user': 'barney',  'active': false },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': true }
];
 
_.findIndex(users, function(o) { return o.user == 'barney'; });
// => 0
 
// The `_.matches` iteratee shorthand.
_.findIndex(users, { 'user': 'fred', 'active': false });
// => 1
 
// The `_.matchesProperty` iteratee shorthand.
_.findIndex(users, ['active', false]);
// => 0
 
// The `_.property` iteratee shorthand.
_.findIndex(users, 'active');
// => 2

```

#### `findLastIndex` 

##### 参数

1. `array` _(Array)_: 要搜索的数组。
2. `[predicate=_.identity]` _(Array|Function|Object|string)_: 这个函数会在每一次迭代调用。
3. `[fromIndex=array.length-1]` _(number)_: The index to search from.

##### 返回值

_(number)_: 返回找到元素的 索引值（index），否则返回 `-1`。

##### 例子

```javascript
var users = [
  { 'user': 'barney',  'active': true },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': false }
];
 
_.findLastIndex(users, function(o) { return o.user == 'pebbles'; });
// => 2
 
// The `_.matches` iteratee shorthand.
_.findLastIndex(users, { 'user': 'barney', 'active': true });
// => 0
 
// The `_.matchesProperty` iteratee shorthand.
_.findLastIndex(users, ['active', false]);
// => 2
 
// The `_.property` iteratee shorthand.
_.findLastIndex(users, 'active');
// => 0
```