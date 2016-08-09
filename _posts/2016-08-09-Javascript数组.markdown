---
layout: post
title:  "Javascript数组"
date:   2016-08-09 10:56:57 +0800
categories: jekyll update
---
### 1.1 Javascript中数组的定义

#### 1.1.1 定义

数组的标准定义是:`一个存储元素的线性集合(collection),元素可以通过索引来任意存取,索引通常是数字,用来计算元素之间存储位置的偏移量。`

JavaScript 中的数组是一种特殊的对象,用来表示偏移量的索引是该对象的属性。这些数字索引在内部被转换为字符串类型,这是因为 JavaScript 对象中 的属性名必须是字符串。

#### 1.1.2 使用数组

>##### 创建数组

方法一：最简单的方式通过[]操作符声明一个数组变量：


{% highlight javascript %}

  var numArr = [];

{% endhighlight %}

>使用这种方式创建的数组，是一个长度为0的空数组。

{% highlight javascript %}

  console.log(numArr.length); // 显示 0

{% endhighlight %}


方法二：在声明数组变量时，直接在[]操作符内放入一组元素：

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






























￼
















































I hope you are enjoy stay here!
Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: http://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
