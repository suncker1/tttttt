大家都清楚处在不同环境下this的指向问题，咱们来康康下面滴代码：
```javascript
var nut = 1
function chestnut(){
 this.nut = 2;
}
chestnut();
console.log(nut)
``` 
我们在这里声明了一个全局变量nut并赋值为1，调用chestnut函数，函数中使用了this，this指向了window，函数执行后全局变量nut的值为2。
![图注:大少公众号](http://img.blog.csdn.net/20171012163602706) 

但是事情并没有这么简单，咱们用node重新执行一下上述滴代码~
![图注:大少公众号](http://img.blog.csdn.net/20171012163602706) 
尴尬了...为啥是1捏？？？
