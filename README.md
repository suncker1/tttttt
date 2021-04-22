大家都清楚处在不同环境下的this的指向问题，咱们来康康下面滴代码：
```javascript
var nut = 1
function chestnut(){
    this.nut = 2;
}
chestnut();
console.log(nut)
```
我们在这里声明了一个全局变量nut并赋值为1，调用chestnut函数，函数中使用了this，this指向了window，函数执行后全局变量nut的值为2。

![](https://github.com/suncker1/tttttt/blob/master/img/1.png)

浏览器验证一下，结果是2没有问题。但是事情并没有这么简单，咱们用node重新执行一下上述滴代码~

![](https://github.com/suncker1/tttttt/blob/master/img/2.png)

尴尬了…为啥是1捏？？？



一模一样的代码在node中运行出来的结果居然不一样，这其实是因为this的指向问题，但是这个指向和我们通常认知中的指向是不一样的。这个指向问题是由于node工作原理造成的。

>浏览器直接在全局范围执行脚本文件
而在Node中，Node将代码隐藏在一个立即被调用的匿名函数中，我们可以使用global来访问全局范围

咱们将this打印出来康康：
```javascript
var nut = 1
function chestnut(){
    this.nut = 2;
    console.log("chestnut函数中的this：",this)
}
chestnut();
console.log(nut)
console.log("全局中的this：",this)
```
浏览器中的this：

![](https://github.com/suncker1/tttttt/blob/master/img/3.png)

chestnut函数中的this指向了window，全局的this也是指向了window。

node中的this：

![](https://github.com/suncker1/tttttt/blob/master/img/4.png)

在外部打印的一个this，指向了一个空对象{}，其实在node中运行的任何文件都被包裹在一个`{}`中，所以脚本文件都是在自己的闭包中执行, 类似于：
```javascript
{
    (function(){
        //脚本文件
    })()
}
```
chestnut函数中的this没有指定的执行上下文，所以它指向了global对象，我们给chestnut函数中的this赋值时，this是挂靠在global对象上的，所以它不会去改变全局中的this值。
