---
layout: post
title:  "Javascript数组"
date:   2016-08-09 10:56:57 +0800
categories: jekyll update
---
### 1.1 Javascript中数组的定义

更多详细资料，请参看[MDN开发者文档] [MDN开发者文档]

[MDN开发者文档]: https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array

#### 1.1.1 定义

数组的标准定义是:`一个存储元素的线性集合(collection),元素可以通过索引来任意存取,索引通常是数字,用来计算元素之间存储位置的偏移量。`

JavaScript 中的数组是一种特殊的对象,用来表示偏移量的索引是该对象的属性。这些数字索引在内部被转换为字符串类型,这是因为 JavaScript 对象中的属性名必须是字符串。

#### 1.1.2 使用数组

>##### 创建数组

方法一：最简单的方式通过[ ]操作符声明一个数组变量：


{% highlight javascript %}

  var numArr = [];

{% endhighlight %}

>使用这种方式创建的数组，是一个长度为0的空数组。

{% highlight javascript %}

  console.log(numArr.length); // 显示 0

{% endhighlight %}


方法二：在声明数组变量时，直接在[ ]操作符内放入一组元素：

{% highlight javascript %}

  var numArr = [1,2,3,4,5];
  console.log(numArr.length); // 显示 5

{% endhighlight %}

方法二：调用Array构造函数创建数组：

{% highlight javascript %}

  var numArr = new Array();
  console.log(numArr.length); // 显示 0

{% endhighlight %}

同样，可以在构造函数传入一组元素作为数组的初始值：

{% highlight javascript %}

  var numArr = new Array(1,2,3,4,5);
  console.log(numArr.length); // 显示 5

{% endhighlight %}

最后，注意一点：`在调用Array的构造函数时，如果只传一个数值参数，该数值参数用来指定创建数组的长度：`

{% highlight javascript %}

  var numArr = new Array(10);
  console.log(numArr.length); // 显示 10,初始值均为 undefined

{% endhighlight %}

在脚本语言常见的一个特性是，`数组中的元素不必是同一种数据类型。`如下所示：

{% highlight javascript %}

  var multiArr = [1,'Jack','23','China',true,null];

{% endhighlight %}

`数组检测：调用ECMAScript5中新增的 Array.isArray()来判断一个对象是否是数组。`如下所示：

{% highlight javascript %}

  var num = 3;
  var arr = [1,2,5,7];
  console.log(Array.isArray(num));  // 显示 false
  console.log(Array.isArray(arr));  // 显示 true

{% endhighlight %}

>创建数组的几种方式。哪种方式最好？
`大多数 JavaScript 专家推荐使用 [] 操作符,和使用 Array 的构造函数相比,这种方式被认为效率更高。`

>##### 读写数组

在一条赋值语句中，可以使用 [ ] 操作符将数据赋给数组，也可以使用 [ ] 操作符读取数组中的元素。


#### 1.1.3 由字符串生成数组

`调用字符串对象的split()方法可以生成数组。`

该方法通过一些常见的分隔符,比如分隔单词的空格逗号等,将一个字符串分成几部分,并将每部分作为一个元素保存于一个新建的数组中。

{% highlight javascript %}

  var sentence = "I love Javascript";
  var words = sentence.split(" ");
  console.log(Array.isArray(words));  //  显示 true
  console.log(words); //  显示 ["I", "love", "Javascript"]

{% endhighlight %}

#### 1.1.4 对数组的整体性操作

>#### 数组的复制

当把一个数组赋值给另外一个数组时，只是为被赋值的数组增加了一个新的引用。也就是说当修改一个数组的值时，另一个数组的值也会改变。

>因为数组也是对象，是引用类型。赋值时，只是数组的变量的栈值相等，但是它们指向的还是同一块堆内存。

下面代码展示了这种情况：

{% highlight javascript %}

  var arr1 = [1,2,3,4];
  var arr2 = arr1;
  console.log(arr2);  //  显示  [1, 2, 3, 4]
  arr1[0] = 100;  
  console.log(arr2);  //  显示 [100, 2, 3, 4]
  console.log(arr1 === arr2);   // 显示 true

{% endhighlight %}

这种行为被称为`浅复制`，新数组依然指向原来的数组。
最好的方法是使用`深复制`，将原数组中的每一个元素都复制到一份到新的数组中。

{% highlight javascript %}

  function copy(arr1, arr2){
    for(var i=0; i<arr1.length; i++){
      arr2[i] = arr1[i];
    }
  }

  var oldArr = [1,2,3,4];
  var newArr = [];
  copy(oldArr,newArr);
  console.log(newArr);  // 显示 [1, 2, 3, 4]
  oldArr[0] = 100;
  console.log(oldArr);  // 显示 [100, 2, 3, 4]
  console.log(newArr);  // 显示 [1, 2, 3, 4]
  console.log(newArr === oldArr); // 显示 false

  /*使用 forEach 迭代方法实现 深复制*/

  var arr1 = [1,2,3,4];
  var arr2 = [];
  arr1.forEach(function(item,index,array){
    arr2[index] = item;
  });

  console.log(arr2);  // 显示 [1, 2, 3, 4]
  console.log(arr1 === arr2);  // 显示 false


  /* end*/

{% endhighlight %}

### 1.2 存取数组的函数

#### 1.2.1 查找元素

`indexOf()`函数，用来查找传进来的参数在目标数组中是否存在。

如果目标数组包含该参数，就返回该元素在数组中的索引；如果不包含，就返回 -1。

{% highlight javascript %}

  var arr = ['lisi','wangwu','zhaoliu'];  
  console.log(arr.indexOf('zhaoliu'));  // 显示 2
  console.log(arr.indexOf('liuwei')); // 显示 -1

{% endhighlight %}

如果数组中包含多个相同的元素，`indexOf()`函数总是返回`第一个`与参数相同的元素的索引。

有另外一个功能与之类似的函数：`lastIndexOf()`,该函数返回相同元素中最后一个元素的索引。如果没找到相同的元素，则返回 -1。

{% highlight javascript %}

  var arr = ['lisi','wangwu','zhaoliu','lisi'];  
  console.log(arr.lastIndexOf('lisi'));  // 显示 3

{% endhighlight %}

#### 1.2.2 数组的字符串表示

有两个方法可以将数组转换成字符串：`join()`和`toString()`。

这两个方法都返回一个包含数组所有元素的字符串，各元素之间用逗号分隔开。其中，`join()`参数可以指定进行分隔的分隔符。

{% highlight javascript %}

  var words = ["I","love","you"];
  var str1 = words.join();
  var str2 = words.join(" ");
  var str3 = words.toString();
  console.log(str1);  //  显示  I,love,you
  console.log(str2);  //  显示  I love you
  console.log(str3);  //  显示  I,love,you

{% endhighlight %}

#### 1.2.3 由已有数组创建新数组

`concat()`和`slice()`方法允许通过已有数组创建新数组。

`concat()`方法可以合并多个数组创建一个新数组，`slice()`方法截取一个数组的子集创建一个新数组。

`待续。。。。。。`

### 1.3 可变函数

#### 1.3.1 为数组添加元素

有两个方法可以为数组添加元素：`push()`和`unshift()`。

`push()`方法可向数组的末尾添加一个或多个元素，并返回新的长度。

`unshift()` 方法可向数组的开头添加一个或更多元素，并返回新的长度。
`unshift()`方法无法在 Internet Explorer 中正确地工作。

如下所示：

{% highlight javascript %}

  var arr1 = [1,2,3,4,5];
  var length1 = arr1.push(6);
  console.log(length1); //  显示  6
  console.log(arr1);  //  显示  [1,2,3,4,5,6]
  var length2 = arr1.push(7,8,9,10);
  console.log(length2); //  显示  10
  console.log(arr1);  //  显示  [1,2,3,4,5,6,7,8,9,10]
  var arr0 = [11,12,13,14];
  var length3 = arr1.push(arr0);
  console.log(length3); //  显示  11
  console.log(arr1);  //显示  [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, [11, 12, 13, 14]]

{% endhighlight %}

>说明：传入的参数为数组中的元素，而非数组。如果传入一个数组，只会把数组当作一个元素处理。如上所示，往数组中push一个数组，长度只增加一。

>`unshift()`方法的实现：因为在数组的开头添加元素远比在末尾难度大。如果不利用`unshift()`，则需要把后面的每个元素都相应地向后移动一个位置。

{% highlight javascript %}

  var arr = [1,2,3,4];
  for(var i = arr.length; i >=0; i--){
    arr[i] = arr[i-1];
  }
  arr[0] = 0;
  console.log(arr); //显示 [0, 1, 2, 3, 4]

{% endhighlight %}

>考虑 `push()` 和 `contact()` 两者的区别

看下面的代码：

{% highlight javascript %}

  var arr1 = [1,2,3];
  var arr2 = [4,5,6];
  var arr3 = arr1.concat(arr2);

  console.log(arr3.length); //  显示 6
  console.log(arr3); // 显示 [1, 2, 3, 4, 5, 6]

  var arr3 = [1,2,3];
  var arr4 = [4,5,6];
  var len = arr3.push(arr4);

  console.log(len); //  显示 4
  console.log(arr3.length); //  显示 4
  console.log(arr3); // 显示 [1, 2, 3, [4, 5, 6]]

{% endhighlight %}

由上述代码可以看出两者区别在于：

①返回值不同。`concat()`返回的是的新生成的数组，而`push()`返回数组新的长度（`length` 属性值）。
②实现机制不同。`push()` 遇到数组参数时，把整个数组参数作为一个元素；而 `concat()` 则是拆开数组参数，一个元素一个元素地加进去。
`push()` 直接改变当前数组；`concat()` 不改变当前数组，而是生成新的数组。

`push()`也可以通过调用`apply()`方法合并数组，实现`concat()`一样的效果。如下所示：

{% highlight javascript %}

  var arr1 = [1,2,3];
  var arr2 = [4,5,6];
  Array.prototype.push.apply(arr1,arr2);
  // arr1.push.apply(arr1,arr2);
  console.log(arr1);  // 显示 [1, 2, 3, 4, 5, 6]

{% endhighlight %}





#### 1.3.2 从数组中删除元素

有两个方法可以为数组删除元素：`pop()`和`shift()`。

使用 `pop()` 方法可以删除数组末尾的元素，并返回数组的最后一个元素。

使用 `shift()` 方法可以删除数组的第一个元素，并返回数组的第一个元素。

`pop()` 和 `shift()` 方法都将删掉的元素作为方法的返回值返回,因此可以使用一个变量来保存删除的元素。

{% highlight javascript %}

  var num1 = [1,2,3,4];
  num1.shift();
  console.log(num1);  //  显示 [2, 3, 4]
  var num2 = [1,2,3,4];
  var first = num2.shift();
  console.log(first); //  显示 1

{% endhighlight %}

#### 1.3.3 从数组中间位置添加和删除元素

使用`splice()`方法可以为数组添加、删除或者替换元素，根据参数的不同实现不同的功能。并返回被删除的项目。该方法会改变原始数组。

使用`splice()`方法需要提供如下参数：

第一个参数，起始索引（规定添加/删除项目的位置，使用负数可从数组结尾处规定位置）

第二个参数，需要删除的元素的个数(添加元素是该参数设为0)

第三个参数，想要添加进数组的元素。

示例一：使用`splice()删除`元素

{% highlight javascript %}

  var nums = [1,2,3,4,5];
  var del = nums.splice(0,2);
  console.log(nums);  //  显示  [3,4,5]
  console.log(del); //  显示  [1,2]

{% endhighlight %}


示例二：使用`splice()添加`元素

{% highlight javascript %}

  
  var nums = [1,2,5];
  nums.splice(2,0,3,4);
  console.log(nums);  //  显示  [1,2,3,4,5]

{% endhighlight %}

示例三：使用`splice()替换`元素

{% highlight javascript %}
  
  var nums = [1,2,3,4,100,200,300,8];
  nums.splice(4,3,5,6,7);
  console.log(nums);  //  显示  [1, 2, 3, 4, 5, 6, 7, 8]

{% endhighlight %}

#### 1.3.4 为数组排序

`reverse()` 方法用于颠倒数组中元素的顺序。该方法会改变原来的数组，而不会创建新的数组。

`sort()`方法用于对数组的元素进行排序。该方法会改变原来的数组，而不会创建新的数组。

排序的都是按照字符串的字母顺序进行排序的。

如下示例：

{% highlight javascript %}

  var arr = ['cd','ac','ab','aa','zs'];
  console.log(arr.reverse()); //  显示  ["zs", "aa", "ab", "ac", "cd"]
  console.log(arr.sort());  //  显示  ["aa", "ab", "ac", "cd", "zs"]

{% endhighlight %}

但是如果数组元素是数字类型，`sort()`方法的排序结果如下所示：

{% highlight javascript %}

  var nums = [3,2,1,11,100,4,200];
  nums.sort();
  console.log(nums);  //  显示  [1, 100, 11, 2, 200, 3, 4]

{% endhighlight %}

为了实现按照数字大小的顺序进行排序，需要给`sort()`方法传入一个比较函数。

如果按照`升序`排序：
{% highlight javascript %}

  function compare(a,b){
    return a - b;
  }
  arr.sort(compare);

{% endhighlight %}

如果按照`降序`排序：
{% highlight javascript %}

  function compare(a,b){
    return b - a;
  }
  arr.sort(compare);

{% endhighlight %}

如下所示：

{% highlight javascript %}

  var nums1 = [3,2,1,11,100,4,200];
  nums1.sort(function(a,b){
    return a - b;
  });
  console.log(nums1); //  显示  [1, 2, 3, 4, 11, 100, 200]

  var nums2 = [30,2,1,11,10,43,200];
  nums2.sort(function(a,b){
    return b - a;
  });
  console.log(nums2); //  显示  [200, 43, 30, 11, 10, 2, 1]

{% endhighlight %}


### 1.4 迭代器( Iterator )方法

迭代方法是对数组中每个元素应用一个函数，可以返回一个值、一组值或者一个新数组。

该函数会接收3个参数：数组每项的`值(item)`、该项在数组中的`索引(index)`和数组对象`本身(array)`。

#### 1.4.1 不生成新数组的迭代器方法

`♦️ forEach()函数`

该方法接收一个函数作为参数，对数组中的每个元素使用该函数。

{% highlight javascript %}

  var nums = [0,1,2,3,4,5,6,7,8,9];
  var power = [];
  nums.forEach(function(item,index,array){
    power.push(item*index);
  });
  console.log(power); // 显示 [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

{% endhighlight %}

`♦️ every()函数`

该方法接受一个返回值为布尔类型的函数,对数组中的每个元素使用该函数。

如果对于所有的元素,该函数均返回true,则该方法返回true。

{% highlight javascript %}

  var num1 = [2,4,6,8,10];
  var isEven = num1.every(function(item,index,array){
    return item % 2 == 0;
  });

  if(isEven){
    console.log("all numbers are even!");
  }else{
    console.log("not all numbers are even!");
  }

{% endhighlight %}

>上述运行输出结果： all numbers are even!

`♦️ some()函数`

该方法也接受一个返回值为布尔类型的函数。

只要有一个元素使得该函数返回 true,该方法就返回 true。

{% highlight javascript %}

  var num1 = [1,2,3,5,7,9];
  var isEven = num1.some(function(item,index,array){
    return item % 2 == 0;
  });

  if(isEven){
    console.log("some numbers are even!");
  }else{
    console.log("no numbers are even!");
  }

{% endhighlight %}

>上述运行输出结果： some numbers are even!

`♦️ reduce()函数`  
`♦️ reduceRight()函数`

该方法会从一个累加值开始,不断对累加值和数组中的后续元素调用该函数,直到数组中的最后一个元素,最后返回得到的累加值。

传给`reduce()`和`reduceRight()`的函数接收4个参数：`前一个值(prev)`、`当前值(cur)`、`项的索引(index)`和数组本身的`对象(array)`。

这两个函数的区别就是方向不同，`reduce()`函数从第一个开始遍历，`reduceRight()`函数从最后一个开始遍历。

{% highlight javascript %}

  var num1 = [1,2,3,4,5];
  num1.reduce(function(prev,cur,index,array){
    var sum = prev + cur;
    console.log(prev+" + "+cur+" = "+sum);
    return sum;
  });

{% endhighlight %}

>上述运行输出结果：

`
  1 + 2 = 3
  3 + 3 = 6
  6 + 4 = 10
  10 + 5 = 15
  15
`

#### 1.4.2 生成新数组的迭代器方法

有两个迭代方法可以产生新数组：`map()`和`filter()`。

`map()`函数与`forEach()`函数功能相同，对数组每个元素使用某个函数，区别是它会返回一个新的数组。

{% highlight javascript %}

  var words = ["Do","It","Yourself"];
  var letters = words.map(function(item,index,array){
    return item[0];
  });
  console.log(letters);   // 显示  ["D", "I", "Y"]
  console.log(letters.join(""));    //  显示 DIY

{% endhighlight %}

`filter()`和 `every()` 类似,传入一个返回值为布尔类型的函数。和 `every()` 方法不同的是, 当对数组中的所有元素应用该函数,结果均为 true 时,该方法并不返回 true,而是返回 一个新数组,该数组包含应用该函数后结果为 true 的元素。

下面是一个例子:

{% highlight javascript %}

  var grades = [];
  for(var i=0; i<20; i++){
    grades.push(Math.floor(Math.random()*101));
  }
  console.log(grades);  
//[47, 17, 8, 67, 21, 68, 71, 83, 74, 21, 73, 39, 74, 85, 22, 99, 96, 51, 0, 89]
  var passGrades = grades.filter(function(item,index,array){
    return item > 60;
  });
  console.log(passGrades);  
//[67, 68, 71, 83, 74, 73, 74, 85, 99, 96, 89]


{% endhighlight %}


### 1.5 二维和多维数组

#### 1.5.1 创建二维数组

二维数组类似一种由行和列构成的数据表格。在JavaScript中创建二维数组,需要先创建一个数组,然后让数组的每个元素也是一个数组。
通过扩展JavaScript数组对象,为 其增加了一个新方法,该方法根据传入的参数,设定了数组的行数、列数和初始值。
下面是这个方法的定义:

{% highlight javascript %}

  Array.martix = function(row,col,init){
    var arr = [];
    for(var i=0; i<row; i++){
      var colArr = [];
      for(var j=0; j<col; j++){
        colArr[j] = init;
      }
      arr[i] = colArr;
    }
    return arr;
  }

  console.log(Array.martix(5,5,0));
  /*运行结果：

  [
    [ 0, 0, 0, 0, 0 ],
    [ 0, 0, 0, 0, 0 ],
    [ 0, 0, 0, 0, 0 ],
    [ 0, 0, 0, 0, 0 ],
    [ 0, 0, 0, 0, 0 ] 
  ]
  */

{% endhighlight %}

#### 1.5.2 处理二维数组元素

处理二维数组中的元素,有两种最基本的方式:按列访问和按行访问。对于两种方式,我们均使用一组嵌入式的 for 循环。对于按列访问,外层循环对应行,内 层循环对应列。

如下所示：

{% highlight javascript %}

  var grades = [[90,78,65,49],[99,87,57,79],[100,38,85,49],[89,67,86,59]];
  var total = 0;
  var average = 0;
  for( var row=0; row<grades.length; row++ ){
      for( var col=0; col<grades[row].length; col++){
        total+=grades[row][col];
      }
    console.log("学生"+(row+1)+" average:"+total/grades[row].length);
    total = 0;
    average = 0;
  }

  /*运行结果：

    学生1 average:70.5
    学生2 average:80.5
    学生3 average:68
    学生4 average:75.25

  */

{% endhighlight %}

>内层循环由下面这个表达式控制: `col < grades[row].length` 这个表达式之所以可行,是因为每一行都是一个数组,我们可以使用数组的 length 属性判断每行包含多少列。

>对于参差不齐的稀疏数组 JavaScript 处理方法不变，因为每一行的长度是可以通过计算得到的。



### 1.6 ECMAScript6 数组的扩展

`♦️♦️ Array.from() 函数`

`Array.from`方法用于将两类对象转换成真正的数组：`类似数组的对象(array-like object)`和`可遍历(iterable)对象`。

在ES5中对于类数组对象(类数组对象的本质特征就是`必须具有length属性`)，可以使用 `Array.prototype.slice.call(arguments)` 将其转换成真正的数组。

如下所示：

{% highlight javascript %}

  var obj = {
    '0' : 'a',
    '1' : 'b',
    '2' : 'c',
    'length' : 3
  }

  var arr1 = Array.prototype.slice.call( obj ); 

  //亦可以写成： var arr1 = [].slice.call( obj );
  console.log(arr1);  //  显示  ["a", "b", "c"]

  var arr2 = Array.from( obj );
  console.log(arr2);  //  显示  ["a", "b", "c"]

{% endhighlight %}

在实际应用中，常见的类数组的对象是DOM操作返回的`NodeList集合`（具有length属性），以及函数内部的`arguments对象`（保存函数实参，具有length属性）。Array.from都可以将它们转为真正的数组。

{% highlight javascript %}

  //  NodeList 对象
  var pList = document.querySelectorAll('p');
  var pArr = Array.from(pList);
  console.log(Array.isArray(pArr)); //  true

  //  arguments 对象
  function fun(){
    var args = Array.from(arguments);
    // ......
  }

{% endhighlight %}

`Array.from`函数还可以接受第二个参数，作用类似于数组的`map`方法，用来对每个数组进行处理，将处理后的值放入返回的新数组。

{% highlight javascript %}

  var obj = {
    '0' : 1,
    '1' : 2,
    '2' : 3,
    'length' : 3
  }

  Array.from(obj,elem => elem * elem);
  //  等同于
  Array.from(obj).map(function(item,index,array){
    return item * item;
  });
  //结果： [1, 4, 9]

{% endhighlight %}

下面列子展示取出一组DOM结点的文本内容。

{% highlight javascript %}

  var pList = document.querySelectorAll('p');
  var pText = Array.from(pList,text => text.textContent);
  console.log(pText);

{% endhighlight %}

`♦️♦️ Array.of() 函数`

`Array.of`方法用于将一组值转换成数组。
这个函数弥补了数组构造函数`Array()`的不足，因为参数个数不同会导致`Array()`的结果存在差异。
只有当参数个数不少于2个时，`Array()`才会返回由参数组成的新数组。当参数个数只有一个时，实际上指定数组的长度。
而`Array.of`总是返回参数组组成的数组。如果没有参数，就返回一个空数组。

`Array.of`方法可以用以下代码模拟实现：

{% highlight javascript %}

function ArrayOf(){
  return [].slice.call(arguments);
}

{% endhighlight %}

`♦️♦️ find()和findIndex()函数`

数组实例的`find`方法，用于找出第一个符合条件的数组成员。它的参数是一个回调函数，所有数组成员依次执行该回调函数，直到找出第一个返回值为true的成员，然后返回该成员。
如果没有符合条件的成员，则返回undefined。

{% highlight javascript %}

[1,5,10,15].find(function(item,index,array){
  return item > 9;
}); //  显示 10

{% endhighlight %}

数组实例的`findIndex`方法的用法与`find`方法类似，返回第一个符合条件的数组成员的索引位置，如果所有成员都不符合条件，则返回 -1。

{% highlight javascript %}

[1,5,10,15].findIndex(function(item,index,array){
  return item > 9;
}); //  显示 2

[1,5,10,15].findIndex(function(item,index,array){
  return item > 16;
}); //  显示 -1

{% endhighlight %}

注意，这两个方法都可以发现NaN，弥补了数组的IndexOf方法的不足。

`[NaN].indexOf(NaN)`返回 -1

`[1,2,NaN].findOf(elem => Object.is(NaN,elem))`返回 2

♦️ 关于 `Object.is()`方法与`" === "`操作符 ♦️

{% highlight javascript %}

  NaN === NaN;  //  false
  Object.is(NaN,NaN); //  true

  0 === -0; //  true
  Object.is(0,-0);  //  false

  0 === +0; //  true
  Object.is(0,+0);  //  false

{% endhighlight %}

`♦️♦️ includes()函数`

数组实例的`includes()`方法返回一个布尔值，表示某个数组是否包含给定的值。

{% highlight javascript %}

  [1,2,3,NaN].includes(3);  //  true
  [1,2,3,NaN].includes(0);  //  false
  [1,2,3,NaN].includes(NaN);  //  true

{% endhighlight %}

`indexOf`方法也可以检查是否包含某个值。

`indexOf`方法存在两个缺点：①不够语义化，其含义是找到参数值的第一出线位置，所以要比较是否不等以-1，表达不够直观；②其内部使用严格相等运算符(===)进行判断，会导致对NaN出现误判。

`[NaN].indexOf(NaN)`返回 -1

`[NaN].includes[NaN]`返回 true








When you do something beautiful and nobody noticed,do not be sad. For the sun every morning is aabeautiful spectacle and yet most of the audience still sleeps.





I hope you are enjoy stay here!
Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: http://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
