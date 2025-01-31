## 数组操作
### 1. 拆分多个长度的区块
将数组（array）拆分成多个 `size` 长度的区块，并将这些区块组成一个新数组。 如果`array` 无法被分割成全部等长的区块，那么最后剩余的元素将组成一个区块。
例:
```javascript
_.chunk(['a', 'b', 'c', 'd'], 2);
// => [['a', 'b'], ['c', 'd']]
_.chunk(['a', 'b', 'c', 'd'], 3);
// => [['a', 'b', 'c'], ['d']]
```
### 2.创建新数组，包含原数组中所有的非假值元素
创建一个新数组，包含原数组中所有的非假值元素。例如`false`, `null`,`0`, `""`, `undefined`, 和 `NaN` 都是被认为是“假值”。
例:
```javascript
_.compact([0, 1, false, 2, '', 3]);
// => [1, 2, 3]
```
### 3.创建新数组，将`array`与任何数组 或 值连接在一起。
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
### 4. 创建一个新数组，这个数组中的值，为第一个数字（`array` 参数）排除了给定数组中的值。
创建一个具有唯一`array`值的数组，每个值不包含在其他给定的数组中。（注：即创建一个新数组，这个数组中的值，为第一个数字（`array` 参数）排除了给定数组中的值。）该方法使用[`SameValueZero`](http://ecma-international.org/ecma-262/6.0/#sec-samevaluezero)做相等比较。结果值的顺序是由第一个数组中的顺序确定。
例:
```javascript
_.difference([3, 2, 1], [4, 2]);
// => [3, 1]
```
### 5. 获取两个数组的差集
##### 参数
1. `array` _(Array)_: 要检查的数组。
2. `[values]` _(...Array)_: 排除的值。
3. `[iteratee=_.identity]` _(Array|Function|Object|string)_: iteratee 调用每个元素。
##### 返回值
_(Array)_: 返回一个过滤值后的新数组。
例:
```javascript
_.differenceBy([3.1, 2.2, 1.3], [4.4, 2.5], Math.floor);
// => [3.1, 1.3]
 
// The `_.property` iteratee shorthand.
_.differenceBy([{ 'x': 2 }, { 'x': 1 }], [{ 'x': 1 }], 'x');
// => [{ 'x': 2 }]
```
## **区别：`differenceBy` vs `differenceWith`**

|方法|适用场景|例子|
|---|---|---|
|`_.differenceBy(array, values, iteratee)`|只基于**某个属性**或**转换函数**比较|`_.differenceBy([{x:1}, {x:2}], [{x:1}], 'x')`|
|`_.differenceWith(array, values, comparator)`|允许使用**自定义比较函数**|`_.differenceWith([{x:1, y:2}], [{x:1, y:3}], (a, b) => a.x === b.x)`|

**如果你需要更灵活的比较方式，`_.differenceWith` 更适合！** 🚀
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