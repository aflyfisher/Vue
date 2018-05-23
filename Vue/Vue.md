##一、Vuejs简介
+ 一个轻量化的MVVM前端框架，和react,angular类似，<font color = red>是一个数据驱动和组件思想（核心思想）</font>
+ 不兼容低版本的额浏览器
+ 前端路由
+ 状态的管理
+
+ 虚拟DOM
##二、起步
###1.下载核心库Vue.js
可以通过npm、cnpm安装或者直接下载vue.js源文件使用`script`引用
###2.一个简单的例子：“hello，Vue”；
```html
<!-- 这里“{{}}”是一个装数据的模板(渲染模板) -->
    <div id="container">{{name}}</div>
```
```javascript
    var app = new Vue({//这里的变量app是一个指针指向Vue实例，
            el:"#container",//指定挂载的根元素，可以是选择器，也可以是DOM元素
            data:{//存储数据的地方
                name:"hello,Vue"
            }
        })
```
>注意：1.在Vue2.0中，Vue实例的挂载元素，可以是html中的任何元素，class类名，id名，标签名等,但是不能挂载在body上;
>2.Vue实例本身可以直接访问data中的源数据，也可以直接访问methods中定义的方法


##三、常用的指令
###1.什么是指令？
就是用来扩展HTML标签的功能的，比如通过`v-if`来控制元素的显示与否,`v-for`来实现循环...
###2.Vue中常用的指令（内置）:
1. **<font color = red>v-if</font>**:实现元素的显示和隐藏，是通过创建和删除元素来实现，
    基本语法：`v-if = 值为boolean的数据`；
    >扩展：1.`v-else`通常可以表示`v-if`的else块（相反嘛），一般而言`v-else`必须紧跟在`v-if`或者`v-else-if`后面；
    >2.给绑定有`v-if`或者`v-else`的元素添加key属性，可以防止当前元素是否被复用，key的值是唯一的。
***
2. **<font color = red>v-model</font>**:双向数据绑定，一般用于表单元素上（将Vue数据和表单元素的值value双向绑定起来），例如：
    ```html
        <h4>{{name}}</h4>
        <!-- 通过v-model将input元素的value属性值和name双向绑定了起来：结果是当修改input的value的时候，h4内的内容也会变化，当直接更改Vue数据name的时候,value也会跟着变化 -->
        <input type="text" v-model="name">
    ```
    ```javascript
        var app =  new Vue({
            el:"#container",
            data:{
                name:"张三",
                ageArr:[1,2,3],
                person:{
                    name:"李白",
                    pride:"诗歌",
                    sex:"男"
                }
            }
        })
    ```
***
3. **<font color = red>v-show</font>**:也用来显示或者隐藏元素,是通过css中的display实现；
    语法：`v-show = “值为boolean的数据”`
***
>**v-if和v-show：**
>一般来说，v-if 有更高的切换开销(因为涉及到元素的创建和销毁)，而 v-show 有更高的初始渲染开销。因此，如果需要非常频繁地切换，则使用 v-show 较好；如果在运行时条件很少改变，则使用 v-if 较好。
4. **<font color = red>v-for</font>**：实现循环，循环一个数据集合（可以是数组，也可以是对象）
    基本语法：`v-for = (item,[index]) in items`**<font color = red>[针对数组]</font>** 或者 `v-for = (item,[key],[index]) in items `**<font color = red>[针对对象]</font>**
    >注意：1.如果循环的是一个对象，那么`item`是该对象中的某一个属性的值，`key`就是该值对应的键名，`index`就是索属性的索引，如果循环的是一个数组，那么`item`是数组中的某一项，`index`是对应的下标。`item` 和`index`、`key`只是别名，当然自己可以自定义
    **2.可以通过指定”：key“属性为当前元素绑定唯一key，当更新数据的时候可以重用元素，效率更高,<font color = red>建议在循环的时候带上该属性</font>** 例如：
    ```html
         <ul>
            <li v-for="(item,key,index) in person" :key="index">{{item}},{{index}},{{key}}</li>
        </ul>
    ```
    **3.可以用template组件将要循环的部分包裹起来，组成一个整体来进行循环**，例如：
    ``` html
        <ul>
            <template v-for="(item,index) in team">
                <li>{{item.name}}</li>
                <li>{{item.age}}</li>
            </template>
        </ul>
    ```
    ```javascript
        team:[
                {name:"万钢",age:23},
                {name:"前进",age:09},
                {name:"后退",age:89},
                {name:"树上",age:38},
            ]
    ```
    **4.此外`v-for`还可以循循环整数，这里就不再赘述**
    **5. 当对数组进行操作的时候，以下方法可以使在v-for中实时体现和渲染**push(), pop(), shift(), unshift(), splice(), sort(), reverse()，这些方法又称为变异方法，因为他们操作的直接是原数组，非变异的方法如filter(),concat(),slice()等就不行了；
    **6.对象更改监测要注意的**
    >1.Vue不能监测对象属性的删除和添加，但是可以通过`Vue.set(object, key, value)`方法来动态为对象添加属性，或者`vm.$set(object, key,value)`方法也可以达到同样的效果，这里的object就是要更改的对象
***
5. **<font color = red>v-on</font>**:事件绑定，为元素绑定具体的事件；
    语法：`v-on:事件名 = “函数”`；
    简写：`@事件名 = "函数"`；
    >注意：1.<font color = red>在选项`methods`中定义的函数和方法</font>，访问Vue实例中`data`中的数据的时候必须要通过`this`来访问，而不能直接访问实例数据，函数中的`this`指向Vue实例本身（你懂的）；

    <font color = red>获取事件对象:</font>
     在函数中传参数`e`即可（调用的时候传入`$event`）,里面包含了该事件的一些相关信息，比如点击的位置，点击的DOM对象等
     ``` html
         <button type="button" class="btn btn-large btn-block btn-default" @click = "getEventObj('hello',$event)">{{buttontext}}</button>
     ```
      ``` javascript
        methods: {
            getEventObj:function(message,e){
                console.log(e);
                console.log(message)
            }
        }
      ```
    <font color = red>事件修饰符:</font>
    1. 阻止事件冒泡:`@click.stop = "方法名"`;
    2. 阻止默认行为:`@click.prevent = "方法名"`;
    3. 只有e.target是绑定事件的当前元素自身时触发：`@click.self`,点击当前元素的内部子元素不触发
    4. 只触发一次：`@click.once`
    >注意：事件修饰符可以嵌套（串联）

    <font color = red>鼠标事件修饰符：</font>
    1. 点击鼠标左键:`@click.left`;
    2. 点击鼠标中键:`@click.middle`;
    3. 点击鼠标右键:`@click.right`,一般要结合`.prevent`才行;
    <font color = red>键盘事件：</font>
    1. 回车：`@keyup.13`或者`@keyup.enter`(注意这里的`13`是键盘码,`enter`是键位别名);
    2. 方向键“上”：`@keyup.38`或者`@keyup.up`;
    3. 删除键del：`@keyup.??`或者`@keyup.delete`;
    4. 空格space：`@keyup.space`;
    5. 总之还有很多...
    6. 自定义键盘事件：例如,
        ```html
            <input type ="text" @keyup.a = "print"/>
            <input type ="text" @keyup.65 = "print"/>
        ```
        ```javascript
            Vue.config.keyCodes = {
                a:65,
                f1:112,
                aF1:[65,112]
            }
        ```
