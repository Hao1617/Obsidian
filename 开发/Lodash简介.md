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
#### `dropWhile`（按条件从左侧移除）
#### `dropRightWhile`（按条件从右侧移除）

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
例:
例:
例:
例:
例:
例:
例:
例:
例:
例:
例:
例:
例:
例:
例:
例:
例:
例:
例:
例:
例:
例:
例:
例:
例:
例:
例:
例:
例:
例:
例:
例:
例:
例:
例:
例:
例:
例:
例:
例:
例: