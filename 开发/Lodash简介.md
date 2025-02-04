## 数组操作
### 1. 数组切块

将数组（array）拆分成多个 `size` 长度的区块，并将这些区块组成一个新数组。 如果`array` 无法被分割成全部等长的区块，那么最后剩余的元素将组成一个区块。
例:
```javascript
_.chunk(['a', 'b', 'c', 'd'], 2);
// => [['a', 'b'], ['c', 'd']]
_.chunk(['a', 'b', 'c', 'd'], 3);
// => [['a', 'b', 'c'], ['d']]
```

### 2.过滤非真值

创建一个新数组，包含原数组中所有的非假值元素。例如`false`, `null`,`0`, `""`, `undefined`, 和 `NaN` 都是被认为是“假值”。
例:
```javascript
_.compact([0, 1, false, 2, '', 3]);
// => [1, 2, 3]
```

### 3.值与数组链接

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
### 6. 数组填充

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

| 方法                | 作用                   | 查找方向           |
| ----------------- | -------------------- | -------------- |
| `_.findIndex`     | 查找**第一个**符合条件的元素的索引  | **从左到右（索引递增）** |
| `_.findLastIndex` | 查找**最后一个**符合条件的元素的索引 | **从右到左（索引递减）** |

---

#### 📌 `_.findIndex` 

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


---

#### 📌 `_.findLastIndex` 语法
```javascript
_.findLastIndex(array, predicate, [fromIndex=array.length-1])
```
- **从右到左**查找**最后一个匹配的索引**。
- 找不到返回 `-1`。

##### ✅ 示例
```javascript
let index = _.findLastIndex(users, user => !user.active);
console.log(index);
// => 2  （Charlie 是最后一个 `active: false` 的用户）
```


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

#### **✅ `_.findIndex` 从索引 2 开始**
```javascript
let index = _.findIndex(users, user => user.active, 2);
console.log(index); 
// => -1  （从索引 2 开始找，没有 `active: true`）
```
#### **✅ `_.findLastIndex` 从索引 1 开始**
```javascript
let index = _.findLastIndex(users, user => user.active, 1);
console.log(index);
// => 1  （索引 1 处的 `Bob` 符合条件）
```

---

#### **📌 总结**

|方法|方向|返回值|适用场景|
|---|---|---|---|
|`_.findIndex`|**从左到右**|第一个匹配项的索引|查找**最早出现**的匹配项|
|`_.findLastIndex`|**从右到左**|最后一个匹配项的索引|查找**最后出现**的匹配项|

#### **🚀 使用场景**

- `_.findIndex` **用于查找第一个符合条件的元素**
- `_.findLastIndex` **用于查找最后一个符合条件的元素**
- 结合 `fromIndex` **控制查找范围**

🔥 示例
```javascript
_.findIndex([5, 10, 15, 20], n => n > 10); 
// => 2 （索引 2 的 15 是第一个 >10 的数）

_.findLastIndex([5, 10, 15, 20], n => n > 10);
// => 3 （索引 3 的 20 是最后一个 >10 的数）
```

这两个方法在**数组查询、数据分析、过滤**等场景中非常有用！🚀

### 8. 数组扁平化

#### 📌 1. `_.flatten`（展开一层）

`_.flatten` **只展开一层嵌套**，不会递归展开更深层次的数组。

```javascript
let arr = [1, [2, 3], [4, [5, 6]]];

console.log(_.flatten(arr));
// => [1, 2, 3, 4, [5, 6]] （只展开一层）
```

#### 📌 2. `_.flattenDeep`（递归展开所有层）

`_.flattenDeep` 会**无限递归**展开，直到数组完全变成一维。

```javascript
let deepArr = [1, [2, [3, [4, 5]]]];

console.log(_.flattenDeep(deepArr));
// => [1, 2, 3, 4, 5] （完全展开）
```

#### 📌 3. `_.flattenDepth(array, depth)`（自定义展开层数）
`_.flattenDepth` 允许**控制展开的层数**，默认是 `depth = 1`。
```javascript
let deepArr = [1, [2, [3, [4, 5]]]];

console.log(_.flattenDepth(deepArr, 2));
// => [1, 2, 3, [4, 5]] （展开 2 层）
```
#### **🔹 `_.flatten`、`_.flattenDeep`、`_.flattenDepth` 区别**

Lodash 提供了 **三种数组扁平化方法**，主要区别在于展开的层数。

| 方法                             | 作用          | 适用场景         |
| ------------------------------ | ----------- | ------------ |
| `_.flatten(array)`             | **扁平化 1 层** | 适用于浅层嵌套的数组   |
| `_.flattenDeep(array)`         | **递归展开所有层** | 适用于深度嵌套的数组   |

---

#### **🚀 纯 JavaScript 等价写法**

Lodash 的 `flatten` 可以用 ES6 `flat(depth)` 方法替代：
```javascript
let deepArr = [1, [2, [3, [4, 5]]]];

console.log(deepArr.flat()); 
// => [1, 2, 3, [4, 5]] （等价于 _.flatten）

console.log(deepArr.flat(Infinity)); 
// => [1, 2, 3, 4, 5] （等价于 _.flattenDeep）

console.log(deepArr.flat(2)); 
// => [1, 2, 3, [4, 5]] （等价于 _.flattenDepth(deepArr, 2)）
```

#### 📌 总结

|方法|作用|适用于|
|---|---|---|
|`_.flatten(array)`|**展开 1 层**|适用于**浅层嵌套**的数组|
|`_.flattenDeep(array)`|**递归展开所有层**|适用于**深度嵌套**的数组|
|`_.flattenDepth(array, depth)`|**展开指定层数**|适用于**部分展开**的情况|

#### **✅ 适用场景**

- **如果数据结构较浅**，用 `_.flatten`
- **如果数据层级不确定**，用 `_.flattenDeep`
- **如果需要控制展开层数**，用 `_.flattenDepth`

### 9. 键值对数组转换为对象

#### `_.fromPairs` **用于将键值对数组转换为对象**。

---

#### **📌 语法**

```javascript
_.fromPairs(pairs)
```

|参数|说明|
|---|---|
|`pairs`|**二维数组**，每个子数组包含 `[key, value]`|

- 数组的**第一个元素**作为对象的**键**，**第二个元素**作为对象的**值**。
- **如果有重复键**，后面的值会覆盖前面的值。

---

#### **📝 基本用法**

```javascript
let pairs = [['a', 1], ['b', 2], ['c', 3]];

console.log(_.fromPairs(pairs));
// => { a: 1, b: 2, c: 3 }
```

> **🔹 作用：将二维数组转换为对象**

---

#### **📌 处理重复键**

如果有重复的键，后面的值会覆盖前面的：

```javascript
let data = [['x', 10], ['y', 20], ['x', 50]];

console.log(_.fromPairs(data));
// => { x: 50, y: 20 }  （'x' 的值被 50 覆盖）
```

---

#### **🚀 纯 JavaScript 等价写法**

Lodash 的 `_.fromPairs` 可以用 `Object.fromEntries()` 替代：

```javascript
let pairs = [['a', 1], ['b', 2], ['c', 3]];

console.log(Object.fromEntries(pairs));
// => { a: 1, b: 2, c: 3 }
```

> **🔹 ES6 提供了 `Object.fromEntries()`，可以直接转换键值对数组**

---

#### **📌 `_.toPairs`（对象转键值对数组）**

`_.fromPairs` 的**逆操作**是 `_.toPairs`，可以将对象转换回键值对数组：
```javascript
let obj = { a: 1, b: 2, c: 3 };

console.log(_.toPairs(obj));
// => [['a', 1], ['b', 2], ['c', 3]]
```
---

#### **📌 总结**

|方法|作用|
|---|---|
|`_.fromPairs(array)`|**将键值对数组转换为对象**|
|`_.toPairs(object)`|**将对象转换为键值对数组**|

#### **✅ 适用场景**

- **当你需要从数组生成对象时**，使用 `_.fromPairs`
- **如果使用现代 JavaScript**，可以用 `Object.fromEntries()`
- **如果需要逆向转换**，使用 `_.toPairs`

Lodash 提供的 `_.fromPairs` 在某些老旧浏览器上兼容性更好，但在现代 JS 里，**推荐使用 `Object.fromEntries()`！** 🚀

### 10. 获取数组的第一个元素

#### 🔹 `_.head`（获取数组的第一个元素）

`_.head` 是 **Lodash** 中的一个非常简单而实用的函数，用于**获取数组的第一个元素**。它的功能等价于 JavaScript 原生的 `array[0]`，但提供了更好的兼容性，尤其在处理空数组时更加安全。

---

#### **📌 语法**

```javascript
_.head(array)
```

|参数|说明|
|---|---|
|`array`|需要获取第一个元素的数组|

- **返回值**：数组的第一个元素。如果数组为空，返回 `undefined`。

---

#### **📝 基本用法**
```javascript
let numbers = [10, 20, 30, 40];

console.log(_.head(numbers)); 
// => 10 （返回数组的第一个元素）

console.log(_.head([])); 
// => undefined （空数组返回 undefined）
```

---

#### **📌 与 JavaScript 原生方法的对比**

在 JavaScript 中，获取数组的第一个元素通常用 `array[0]`：
```javascript
let numbers = [10, 20, 30];
console.log(numbers[0]);
// => 10
```

而 `_.head` 的作用与之相同，但它更加安全：
```javascript
console.log(_.head([])); 
// => undefined （空数组返回 undefined）
```

如果你直接使用 `array[0]`，在数组为空时依然会得到 `undefined`，但 `_.head` 使得你更加明确地知道返回的是 `undefined`，同时提升了代码的可读性。

---

#### **📌 总结**

| 方法              | 作用                    | 备注                     |
| --------------- | --------------------- | ---------------------- |
| `_.head(array)` | **获取数组的第一个元素**        | 处理空数组时安全返回 `undefined` |
| `array[0]`      | **获取数组的第一个元素（原生 JS）** | 如果数组为空，返回 `undefined`  |

#### **✅ 适用场景**

- **获取数组的第一个元素**时使用 `_.head`，使代码更加清晰。
- **处理空数组时**，Lodash 会显式地返回 `undefined`，增加代码的可读性。

总的来说，如果你正在使用 Lodash，`_.head` 是一个简洁、直接的工具，非常适合从数组中获取第一个元素！ 🚀

### 11. 查找元素在数组中的索引

#### 🔹 `_.indexOf`

`_.indexOf` 是 **Lodash** 中的一个非常实用的函数，用于返回元素在数组中的**索引位置**。如果元素不存在，则返回 `-1`。

---

#### **📌 语法**

```javascript
_.indexOf(array, value, [fromIndex=0])
```

|参数|说明|
|---|---|
|`array`|要搜索的数组|
|`value`|要查找的值|
|`fromIndex`|（可选）从指定位置开始查找，默认为 `0`|

- **返回值**：元素在数组中的索引位置。如果未找到该元素，返回 `-1`。
- **`fromIndex`**：如果为负数，则从数组的**倒数第 `fromIndex` 个元素**开始查找。

---

#### **📝 基本用法**

```javascript
let numbers = [10, 20, 30, 40, 30];

console.log(_.indexOf(numbers, 30)); 
// => 2 （第一次出现 30 的索引是 2）

console.log(_.indexOf(numbers, 50)); 
// => -1 （没有找到 50，所以返回 -1）
```

---

#### **📌 从指定位置开始查找**

可以通过 `fromIndex` 参数指定从数组的某个位置开始查找：
```javascript
let numbers = [10, 20, 30, 40, 30];

console.log(_.indexOf(numbers, 30, 3));
// => 4 （从索引 3 开始查找，返回第一个匹配 30 的索引，结果是 4）
```
- **如果 `fromIndex` 为负数**，它会从数组的**倒数第几个元素**开始查找：

js

复制编辑

`console.log(_.indexOf(numbers, 30, -3)); // => 4 （从倒数第 3 个位置开始查找，返回第一个匹配 30 的索引，结果是 4）`

---

#### **📌 与 JavaScript 原生方法对比**

在 JavaScript 中，`indexOf` 也是一个常用方法，功能与 Lodash 中的 `_.indexOf` 非常相似：
```javascript
let numbers = [10, 20, 30, 40, 30];

console.log(numbers.indexOf(30));
// => 2 （第一次出现 30 的索引是 2）

console.log(numbers.indexOf(50));
// => -1 （没有找到 50，返回 -1）
```

---

#### **🚀 总结**

| 方法                        | 作用                         | 备注           |
| ------------------------- | -------------------------- | ------------ |
| `_.indexOf(array, value)` | **查找元素在数组中的第一个匹配索引**       | 如果未找到返回 `-1` |
| `array.indexOf(value)`    | **原生 JS 查找元素在数组中的第一个匹配索引** | 同样返回 `-1`    |

#### **✅ 适用场景**

- **查找数组中元素的位置**时，可以使用 `_.indexOf`。
- **控制查找位置**时，使用 `fromIndex` 来指定从数组哪个位置开始查找。
- 对于 **较简单的查找需求**，`_.indexOf` 和原生 `indexOf` 都是很好的选择。

总的来说，如果你的项目中已经引入 Lodash，使用 `_.indexOf` 是一个非常简洁且一致的做法！ 🚀

### 12. 获取数组的所有元素，除了最后一个

#### 🔹 `_.initial`

`_.initial` 是 **Lodash** 中的一个数组处理方法，用于获取数组的所有元素，**除了最后一个**。它类似于原生 JavaScript 的 `array.slice(0, -1)`，但提供了更清晰的语义。

---

#### **📌 语法**

```javascript
_.initial(array)
```

|参数|说明|
|---|---|
|`array`|需要处理的数组|

- **返回值**：返回一个新数组，包含原数组的所有元素，**但不包括最后一个元素**。

---

#### **📝 基本用法**

```javascript
let numbers = [10, 20, 30, 40];

console.log(_.initial(numbers));
// => [10, 20, 30] （返回除了最后一个元素以外的数组）

let emptyArray = [];
console.log(_.initial(emptyArray));
// => [] （空数组返回空数组）
```

---

#### **📌 与 JavaScript 原生方法对比**

在 JavaScript 中，你可以使用 `array.slice(0, -1)` 来实现类似的功能：

```javascript
let numbers = [10, 20, 30, 40];

console.log(numbers.slice(0, -1));
// => [10, 20, 30]  （返回除了最后一个元素的数组）
```

- **`slice(0, -1)`** 会从数组的第一个元素开始切片，直到倒数第二个元素，实际上与 `_.initial` 完全相同。

---

#### **🚀 总结**

|方法|作用|备注|
|---|---|---|
|`_.initial(array)`|**返回数组除了最后一个元素的所有元素**|处理空数组时返回空数组|
|`array.slice(0, -1)`|**原生 JavaScript：返回数组除了最后一个元素的所有元素**|功能相同|

#### **✅ 适用场景**

- **需要获取数组所有元素，除了最后一个**，使用 `_.initial` 可以让代码更加清晰。
- **如果你更倾向于原生 JavaScript**，可以使用 `slice(0, -1)`，两者效果相同。

`_.initial` 是一个非常简洁的方法，它的**语义清晰**，使得代码的意图更加直观。如果你的项目已经引入 Lodash，这个方法就是一个非常好的选择！ 🚀