##es6数组方法
####不会改变原数组的方法：
+  `map`
+  `reduce`
+  `filter`
####会改变原数组值的方法
+  `sort`
+  `reverse`
####`map`方法，对数组的每一项进行操作，传入回调函数
####`reduce`方法，相当于一个累计器传入回调函数
####`filter` 方法用来迭代一个数组，并且按给出的条件过滤出符合的元素。
`filter` 方法传入一个回调函数，这个回调函数会携带一个参数，参数为当前迭代的项（我们叫它 val ）
回调函数返回 true 的项会保留在数组中，返回 false 的项会被过滤出数组。

**使用 filter 来创建一个新数组，新数组的值是 oldArray 中值小于6的元素。不许改变原数组 oldArray 。**

```js
var oldArray = [1,2,3,4,5,6,7,8,9,10];

// 只能在这一行下面写代码

var newArray = oldArray.filter(function(val){
  return val < 6;
});
```
####sort 方法,sort 方法将改变原数组，返回被排序后的数组。
+  sort 可以把比较函数作为参数传入,比较函数有返回值，
+  如果没有传入比较函数，它将把值全部转成字符串，并按照字母顺序进行排序

+  使用比较函数的原理（摘自Adobe说明）：
此方法使用语法和参数顺序 Array.sort(compareFunction, sortOptions)，其参数定义如下：
compareFunction - 一个用来确定数组元素排序顺序的比较函数。此参数是可选的。比较函数应该用两个参数进行比较。给定元素 A 和 B，compareFunction 的结果可以具有负值、0 或正值：
若返回值为负，则表示 A 在排序后的序列中出现在 B 之前。
若返回值为 0，则表示 A 和 B 具有相同的排序顺序。
若返回值为正，则表示 A 在排序后的序列中出现在 B 之后。

**下面的例子将展示 sort 的使用，传入的比较函数把元素按照从小到大的顺序进行排列**
```js
var array = [1, 12, 21, 2];
array.sort(function(a, b) {
  return a - b;
});
```
#### reverse 方法来翻转数组。
```js
var myArray = [1, 2, 3];
myArray.reverse();
```
####`concat`方法可以用来把两个数组的内容合并到一个数组中。
concat 方法的参数应该是一个数组。参数中的数组会拼接在原数组的后面，并作为一个新数组返回。

**使用 .concat() 将 concatMe 拼接到 oldArray 后面，并且赋值给 newArray。**

```js
var oldArray = [1,2,3];
var newArray = [];

var concatMe = [4,5,6];

// 只能在这一行下面写代码

newArray = oldArray.concat(concatMe);
```
#### split 方法按指定分隔符将字符串分割为数组。
+  你要给 split 方法传递一个参数，这个参数将会作为一个分隔符

**使用空格（ " " ）来分割字符串。
**
```js
var string = "Split me into an array";
var array = [];

// 只能在这一行下面写代码

array = string.split(" ");
```
####join 使用 join 方法来把数组转换成字符串，
+  里面的每一个元素可以用你指定的连接符来连接起来，这个连接符就是你要传入的参数。

**使用 join 方法，连接符为' '把数组 joinMe 转化成字符串 joinedString.**
```js
var joinMe = ["Split","me","into","an","array"];
var joinedString = '';

// 只能在这一行下面写代码

joinedString = joinMe.join(" ");
```
####Array.from() 
Array.from方法用于将两类对象转为真正的数组：类似数组的对象（array-like object）和可遍历（iterable）的对象
```js
let arrayLike = {
    '0': 'a',
    '1': 'b',
    '2': 'c',
    length: 3
};

// ES5的写法
var arr1 = [].slice.call(arrayLike); // ['a', 'b', 'c']

// ES6的写法
let arr2 = Array.from(arrayLike); // ['a', 'b', 'c']
// 字符串也可以转换
Array.from('hello')
// ['h', 'e', 'l', 'l', 'o']
```
####Array.from还可以接受第二个参数，作用类似于数组的map方法，用来对每个元素进行处理，将处理后的值放入返回的数组。
```js
Array.from(arrayLike, x => x * x);
// 等同于
Array.from(arrayLike).map(x => x * x);

Array.from([1, 2, 3], (x) => x * x)
// [1, 4, 9]
```
####Array.of()
Array.of方法用于将一组值，转换为数组。
```js
Array.of(3, 11, 8) // [3,11,8]
Array.of(3) // [3]
Array.of(3).length // 1
```
####数组实例的 find() 和 findIndex()
数组实例的`find`方法，用于找出第一个符合条件的数组成员。它的参数是一个回调函数，所有数组成员依次执行该回调函数，直到找出第一个返回值为true的成员，然后返回该成员。如果没有符合条件的成员，则返回undefined。
```js
[1, 4, -5, 10].find((n) => n < 0)
// -5
```
上面代码中，`find`方法的回调函数可以接受三个参数，依次为当前的值、当前的位置和原数组。

####数组实例的findIndex方法的用法与find方法非常类似，返回第一个符合条件的数组成员的位置，如果所有成员都不符合条件，则返回-1。
```js
[1, 5, 10, 15].findIndex(function(value, index, arr) {
  return value > 9;
}) // 2
```
####数组实例的fill()
fill方法使用给定值，填充一个数组。
```js
new Array(3).fill(7)
// [7, 7, 7]

['a', 'b', 'c'].fill(7)
// [7, 7, 7]
```
`fill`方法还可以接受第二个和第三个参数，用于指定填充的起始位置和结束位置。
```js
['a', 'b', 'c'].fill(7, 1, 2)
// ['a', 7, 'c']
```
###字符串
####翻转字符串
先把字符串转化成数组，再借助数组的reverse方法翻转数组顺序，最后把数组转化成字符串。

```js
/*reverseString("hello") 应该返回一个字符串
reverseString("hello") 应该返回 "olleh".
reverseString("Howdy") 应该返回 "ydwoH".
reverseString("Greetings from Earth") 应该返回 "htraE morf sgniteerG".*/

function reverseString(str) {
  // 请把你的代码写在这里
  return str;
}

reverseString("hello");
function reverseString(str) {
  return str.split("").reverse().join("");
}
reverseString("hello");
reverseString("Howdy");
reverseString("Greetings from Earth");

```
####计算一个整数的阶乘
阶乘通常简写成 n!

例如: 5! = 1 * 2 * 3 * 4 * 5 = 120
```js
/* factorialize(5) 应该返回一个数字
factorialize(5) 应该返回 120.
factorialize(10) 应该返回 3628800.
factorialize(20) 应该返回 2432902008176640000.
factorialize(0) 应该返回 1.*/
function factorialize(num) {
  // 请把你的代码写在这里
  if (num === 0) {
    return 1;
  } else {
    return num*factorialize(num-1);
  }
}

factorialize(5);
factorialize(10);
factorialize(20);
factorialize(0);
```
####replace() 方法返回一个由替换值替换一些或所有匹配的模式后的新字符串。模式可以是一个字符串或者一个[正则表达式](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/RegExp), 替换值可以是一个字符串或者一个每次匹配都要调用的函数。
+  原字符串不会改变
+  str.replace(regexp|substr, newSubStr|function)
```js
regexp 
(pattern)
一个[RegExp
](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/RegExp) 对象或者其字面量。该正则所匹配的内容会被第二个参数的返回值替换掉。

substr 
(pattern)
一个要被 newSubStr
 替换的
[字符串
](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/String)。其被视为一整个字符串，而不是一个正则表达式。仅仅是第一个匹配会被替换。

newSubStr
 (replacement)
 用于替换掉第一个参数在原字符串中的匹配部分的[字符串
](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/String)。该字符串中可以内插一些特殊的变量名。参考下面的[使用字符串作为参数](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/replace#使用字符串作为参数)。

function
 (replacement)
一个用来创建新子字符串的函数，该函数的返回值将替换掉第一个参数匹配到的结果。参考下面的[指定一个函数作为参数](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/replace#指定一个函数作为参数)。
```
 
**toLowerCase() 会将调用该方法的字符串值转为小写形式，并返回。**