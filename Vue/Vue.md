##一、Vuejs简介
+ 一个轻量化的MVVM前端框架，和react,angular类似，<font color = red>是一个数据驱动和组件思想（核心思想）</font>
+ 不兼容低版本的额浏览器
+ 前端路由
+ 状态的管理
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
##四、属性的绑定
语法:`v-bind:attr = “data”`,常用于元素属性的绑定，简写"`:attr = `"
1.  特殊属性的绑定class;
    **方式一**:通过变量的形式"`:class = dd`",这里的`dd`是`data`中的数据;
    ``` html
        <style>
            .fcolor{
                color: red
            }
            .fwight{
                font-weight:700
            }
            .italit{
                font-style:italic
            }
        </style>
        <p :class = "fontColor">{{btn}}</p>
        <!-- 只拥有fcolor类名 -->
    ```
    ``` javascript
        data:{
            btn:"点我一下试试",
            fontColor:"fcolor",
            fontWeight:"fwight",
            classer:{
                as:true,
                bs:false,
                cs:true
            },
            isTrue:true
        }
    ```
    **方式二**:通过数组的形式"`:class = [dd,ee]`",将同时拥有`dd`和`ee`所代表的类名;
    ``` html
         <p :class = "[fontColor,fontWeight]">{{btn}}</p>
         <!-- 同时拥有fcolor和fweight的类名 -->
    ```
    数组里面的对象
    ``` html
        <p :class = "[fontColor,fontWeight,{italit:istrue}]">{{btn}}</p>
        <!-- 将拥有 fcolor、fweight、italit三个类名 -->
    ```
    **方式三**:通过对象的方式:"`:class = {aa:true,bb:true,...}`"这里`aa`和`bb`就是`class`名，结果是将拥有`aa`和`bb`两个类名;（**<font color = red>推荐（因为更加灵活）</font>**）
    ``` html
         <p :class = "classer" >{{btn}}</p>
         <!-- 将拥有类名as，cs，没有bs -->
    ```
    **方式四**：通过一个返回对象的计算属性(**<font color = red>常用</font>**)；
2. 特殊属性的绑定style(不常用，不再赘述);
##五、模板
###5.1 简介
Vue.js是使用基于html的模板语法，可以将DOM和Vue中的数据绑定起来，其实模板就是`{{}}`,用来进行数据绑定，并显示在页面中
###5.2 数据绑定的方式
>注意:在Vue实例的挂载元素上使用 `v-cloak`,将避免出现闪烁的过程，要结合css
+ 双向绑定：使用`v-model`，将数据和表单元素双向绑定起来
+ 单向绑定：
    1. 使用`{{}}`;
    2. 使用`v-bind`;
    3. `v-html`和`v-text`;两者的区别是前者可以识别标签，而后者不能识别（和原生js中的`innerHTML`与`innerText`差不多）
+ 其他指令：
    1. v-once:数据只绑定一次,也就是说当vue数据发生改变的时候并不会重新渲染
``` html
    <!-- 显示为 hello，Vue -->
    <span>{{msg}}</span>
    <!-- 显示为 hello，world  -->
    <span v-once >{{msg}}</span>
```
``` javascript
    var app = new Vue({
        el:"#container",
        data:{
            msg:"hello,world!",
            vhtml:"<span>张三</span>"
        }
    })
    app.msg = "hello,Vue"
```
1. v-pre:不进行渲染，直接原样显示
##六、过滤器
###6.1 简介
用来过滤模型数据，在显示之前进行数据处理和筛选（按照一定的格式输出）
语法:`{{data|filter1(参数)|filter2(参数)...}}`(可以串联的哦)
或者:v-bind:property= "data|filter1(参数)|..."
###6.2 内置过滤器
Vue2.0已经没有了内置的过滤器
第三方工具库：loadsh
###6.3 自定义过滤器
分类:全局过滤器和局部过滤器；
#### 6.3.1全局过滤器
定义：顾名思义就是在所有的Vue实例中均可以使用
语法：`Vue.filter("过滤器ID",过滤器函数)`，
>注意：
>1. 这里的过滤器函数可以传参数，第一个参数是要操作的数据`value`，从第二个参数开始依次是自己传递的其他参数。
>2. 定义全局过滤器的时候要写在Vue实例之前
``` html
    <h3>{{num|addZero}}</h3>
    <h3>{{numFloat|parse(3)}}</h3>
```
``` javascript
    //数字前后加0
    Vue.filter("addZero",function name(value) {
        return value>9?value:"0"+value
    });
    // 保留几位小数
    Vue.filter("parse",function(value,num){
        return value.toFixed(num)
    })
```
####6.3.2 自定义局部过滤器
语法：在Vue实例中使用`filters`选项，值为对象。内部是键值（回调函数）对的形式，例如：
``` html
    <h3>{{msg|toUpperCase}}</h3>
```
``` javascript
    var app = new Vue({
        el:"#container",
        data:{
            msg:"hello,world!",
            istrue:true,
            num:9,
            numFloat:123.921312,
        },
        filters: {
            toUpperCase:function(value){
                return value.toUpperCase()
            }
        }
    })
```
##七、发送ajax请求；
###7.1简介
Vue本身不具有ajax请求的能力，需要使用axios等插件来实现，axios是一个基于Promise的HTTP请求客户端，
用来发送ajax请求，Vue2.0官方推荐使用的，同时不再对vue-resource进行维护和更新
###7.2使用axios发送ajax请求
####7.2.1 安装axios并引用；
npm install axios -s；
或者直接引用axios源文件；
####7.2.2 基本用法

+ ` axios(options).then(callback).catch(callback)`
    这里的`then`代表成功的时候的回调函数，`catch`则代表失败的时候回调函数，`options`是一个对象---含有`method`（请求类型）、`url`（请求路径）等选项。
+ `axios.get(url,options)`
    注意传递参数的方式：
    1. 直接绑在`url`后面用`&`链接，
    2. 在`options`对象的`params`选项中
``` html
    <button v-on:click="send">发送ajax请求</button>
    <button v-on:click="sendGet">发送Get请求</button>
```
``` javascript
    var app = new Vue({
        el:"#container",
        data:{
            msg:"hello,world!"
        },
        methods: {
            // 基本的axios请求
            send:function(){
                axios({
                    method:"get",
                    url:"../json/user.json"
                }).then((result) => {
                    console.log(result)
                }).catch((err) => {
                    console.log(err)
                });
            },
            // 发送get请求，带参数
            sendGet:function(){
                axios.get("../json/user.json",{
                    params:{
                        id:9527
                    }
                }).then((result) => {
                    console.log(result)
                }).catch((err) => {
                    console.log(err)
                });
            }
        }
    })
```
+ `axios.post(url,[data],options)`
axios默认发送数据的时候，数据格式是 Request Payload，并不是我们常用的formData格式，所以参数必须以键值对的形式传参，不能以json形式传参
传参的方式：
1. 拼接字符串；
``` javascript
    axios.post("../json/user.json","name=张三&age=12").then(callback).catch(callback)
```
1. 使用`transformRequest`，在请求发送之前将发送的数据进行转换
2. 如果是模块化开发，可以使用qs模块进行转换
###7.3使用vue-resource发送跨域请求
####7.3.1 安装vue-resurce安装并引用；
>cnpm install vue-resource -s;
####7.3.2 基本用法
>使用this.$http发送请求，详细用法请参考官网或者github;
1. `this.$http.get(url,option)`;
2. `this.$http.jsonp(url,option)`
3. ...
例如:
``` javascript
    methods: {
        sendAjax:function(){
            // 这里的this指向的是Vue实例
            this.$http.jsonp(url,{
                params:{//参数
                    word:"abs"
                }
                //除了params对象（传参），还有其他的参数，要根据需要
            }).then((result) => {
                console.log(result)
            }).catch((err) => {
                console.log(err)
            });
        }
    }
```
##八.Vue的生命周期
Vue实例从创建到销毁的过程，称之为Vue实例的**生命周期**，共有八个阶段:
1. `beforeCreate`：Vue实例已经创建完成，还未进行数据的观测以及事件的配置
2. `created`：实例已经创建完成，并且已经进行数据的观测和事件的配置<font color = red>（常用，用于初始化数据）</font>
3. `beforeMount`：模板编译之前，还没挂载到元素
4. `mounted`：已经完成编译，并且完成了挂载，也就是说此时才会渲染页面，进行数据的展示<font color = red>（常用）</font>
5.` beforeUpdate`：在实例更新之前
6. `updated`:实例更新之后
7. `beforeDestroy`：实例销毁之前
8. `destroyed`：实例销毁之后
``` javascript
    var app = new Vue({
        el:"#container",
        data:{
            name:"我出来了！"
        },
        beforeCreate:function(){//不常用，还没观测数据呢，要其何用？？
            alert("Vue实例已经创建完成，还未进行数据的观测以及事件的配置，根本还不知道自己有那些数据和事件")
            // 实例创建完成，但还没开始监视数据与事件
        },
        created:function () {//常用,常用于数据的初始化
            alert("实例已经创建完成，并且已经进行数据的观测和事件的配置，知道了自己装了多少货")
        },
        beforeMount:function () {
            alert("模板编译之前，还没挂载到元素，也就是还没挂载到container元素，更别提渲染了")
        },
        mounted:function () {//常用
            alert("模板编译之后，此次才会渲染界面，才能在页面上看到数据的展示，已经完成了挂载，渲染是顺理成章的事情")
        },
        beforeUpdate:function () {
            alert("实例更新之前，这里的实例是Vue实例，只要实例的任何一部分做了更改都将触发该钩子函数")
        },
        updated:function () {
            alert("实例更新之后，同上")
        },
        beforeDestroy:function () {
            alert("实例销毁之前")
        },
        destroyed:function () {
            alert("实例销毁之后")
        },
        methods: {
            updateData:function(){
                this.name = "我被更新啦"
                // 会调用beforeUpdate和updated两个钩子函数
            },
            destroy:function(){
                this.$destroy()
                // 会调用beforeDestroy和destroyed两个钩子函数
            }
        }
    })
```
##九.计算属性
###9.1 基本用法
计算属性像`data`选项一样也是用来存储数据的（你懂的），但具有以下几个特点：
+ 数据可以进行逻辑处理操作
+ 对计算属性中的数据进行监视
###9.2计算属性 VS 方法
将计算属性的get函数定义为一个方法也可以实现类似的功能（用某个函数也可以实现）
``` javascript
    computed: {
        numj:function(){
            return this.number-1;
        }
    },
    methods: {
        numjm:function(){
            return this.number-1
        }
    }
```
``` html
    <!-- 计算属性实现的 -->
    <h3>{{number}}</h3>
    <h3>{{numj}}</h3>
    <!-- 方法实现的 -->
    <h3>{{numjm()}}</h3>
```
区别：
+ 计算属性是基于它的依赖进行更新（要改变计算属性，不能直接改，而要改变该计算属性的依赖才行），只有当相关依赖发生变化的时候才会改变
+ 计算属性是有缓存的，只要相关依赖没有发生变化，多次访问计算属性的得到的是之前缓存得到的结果，不会多次执行
###9.3 get和set
计算属性由两部分组成，`get`和`set`，分别是获取计算属性和更改计算属性，默认只有`get`,`set`函数只有当直接改变计算属性的时候才会执行（你懂的）。
``` javascript
    data:{
        news:"临颍县一高"
    },
    computed: {
        school:{
            get:function(){
                return this.news+"是我的母校"
            },
            set:function(){
                alert("计算属性new被改变了")
            }
        }
    },
    methods: {
        changeClass:function(){
            this.school = "安徽大学"//由于是直接改变了计算属性school，会执行set函数，但显示还是原来的样子
        }
    }
```
##十.Vue实例的属性和方法
###10.1 属性
1. `vm.$el` 获取Vue实例挂载的DOM元素
2. `vm.$data` 获取Vue实例的data属性
3. `vm.$options`  可以获取Vue实例自定义的属性,例如：vm.$options.name
``` javascript
    var app = new Vue({
        el:"#container",
        data:{
            msg:"hello,world!",
            number:10,
            news:"临颍县一高"
        },
        // 自定义属性
        name:1212
    })
```
1. `vm.$refs` 可以用来获取所refs属性的元素（只获取其中一个） 如`app.$refs.hello`;
``` html
<!-- 只获取最后一个 -->
    <h4 ref="hello">{{msg}}</h4>
    <h4 ref="hello">{{msg}}</h4>
    <h4 ref="hello">{{msg}}</h4>
    <h4 ref="hello">{{msg}}</h4>
```

###10.2 方法
1. `vm.$mount()` 手动挂载Vue实例的挂载元素
``` javascript
    var app1 = new Vue({
        data:{
            msg:"欢迎回来"
        }
    })
    app1.$mount("#container1")
```
2. `vm.$destroy()` 销毁Vue实例(一般并不常用)
3. `vm.$nextTick()` 等到DOM完成更新后再执行callback，一般在修改数据之后，执行此方法，以便能够获取更新后的DOM
``` javascript
    app.news = "临颍县第一高级中学";
    console.log(app.$refs.school.innerHTML)//临颍县一高
    // 为啥不是临颍县第一高级中学？？这是因为当执行上面的代码的时候DOM还没更新完，Vue实现响应式并不是数据发生改变之后DOM立即变化，而是按照一定的策略进行的，但是这需要时间！！
    // 也就是说，执行完  `app.news = "临颍县第一高级中学"`;数据发生了变化，但是立即就会执行下面的代码`console.log(app.$refs.school.innerHTML)`,只不过在执行该行代码的时候DOM还没来得更新完成，所以取到的依然是”临颍县一高“；
    // 那我要是偏要获取更新后的DOM呢，那就使用该方法了，只需要将第二行代码放到`callback`中
    app.$nextTick(function(){
        // 当DOM完成更新后才会执行里面的代码，临颍县第一高级中学
        console.log(app.$refs.school.innerHTML)
    })
```
1. `vm.$set(object,key，value)`
    给对象类型的数据object，添加属性key,值为value
2. `vm.$delete(object,key)`
    删除对象类型的数据object的属性key
``` javascript
    var app = new Vue({
        el:"#container",
        data:{
            msg:"hello,world!",
            number:10,
            news:"你好，2018！",
            user:{
                name:"张三",
                age:9
            }
        },
        methods: {
            // 给data中的对象类型的数据user添加属性height，使其值为189
            addAttribute:function(){
                this.$set(this.user,"height",189)
            },
            // 删除user对象中的name属性
            deleteAttr:function(){
                this.$delete(this.user,"name")
            }
        }
    })
```
3. `vm.$watch(data,callback[,options])`
用来观察和监测Vue实例中数据的变化，有两种使用场景:
``` javascript
    // 1. 如果被监测的数据data是一个对象，那么一般要这样子使用,
    app.$watch("user",function(oldValue,newValue){
        console.log("旧值："+oldvalue+",新值："+newValue)
    },{deep:true})
    // options是一个对象，deep：true表示深度监视（只要对象中的属性发生了变化就会执行callback函数）

    // 2.如果被监测的data不是引用类型的值，那么一般这样使用；这里的oldValue是改变前的值，newValue是改变后的值
    app.$watch("number",function(oldValue,newValue){
        console.log("旧值："+oldvalue+",新值："+newValue)
    })
```
不过一般而言，可以在Vue实例的`watch`选项中进行数据监视,所以上述代码可以写为：
``` javascript
    watch: {//使用vue实例提供的watch选项
        // 监测number数据
        number:function(old,newv){
            console.log("原值是"+old+",新值是"+newv);
        },
        //监测user对象
        user:{
            handler:function(){
                console.log("user被改变了");
            },
            deep:true//深度监视，当对象中的属性发生变化的时候，就会触发callback
        }
    }
```
##十一、自定义指令
有的情况下，你仍然需要对普通 DOM 元素进行底层操作，这时候就会用到自定义指令
分类：Vue自定义指令分为全局自定义指令和局部自定义指令；
###11.1 自定义全局指令
> 注意： 使用自定义指令的时候，须要在指令id前面加前缀“v-”，例如本例子就是`v-hello`
语法:`Vue.directive(指令id,指令对象)`，例如：
``` javascript
    Vue.directive("hello",{
        // 五个钩子函数....
        // 当自定义指令第一次被绑定到元素的时候会触发此回调函数，只调用一次(因为绑定的行为只有一次嘛)，可以用来执行初始化操作
        bind:function(){//常用
            console.log("自定义指令被绑定到了元素中")
        },
        inserted:function(){
            console.log("被绑定的元素插入到DOM中的时候调用")
        },
        update:function(){//也常用
            console.log("当被绑定的元素所在的模板更新的时候调用")
        },
        componentUpdated:function(){
            console.log("当被绑定元素所在的模板完成一次更新周期时调用，也就是更新之后调用")
        },
        unbind:function(){
            console.log("指令和元素解绑的时候调用此函数")
        }
    })
    // Vue实例
    var app = new Vue({
        el:"#container",
        data:{
            msg:"hello,San!"
        },
        methods:{
            // 执行此方法的时候，会调用`update`的钩子函数，因为绑定元素所在的模板发生了变化
            changeMsg:function(){
                this.msg = "hello,萝卜白菜！"
            }
        }
    })
```
``` html
    <h3 v-hello>{{msg}}</h3>
    <button @click="changeMsg">改变数据</button>
```
####11.1.1 自定义指令钩子函数中的参数
由于在自定义指令中最常用的是`bind`和`update`钩子函数,所以就以此为例，来介绍一下自定义指令中钩子函数中的一些参数（其他阶段的也是如此：）
``` javascript
    Vue.directive("world",{
        bind:function(el,binding){
            console.log(el);//指令所绑定的DOM元素
            el.style.color = "green";
            console.log(binding);//一个对象
            // binding.value 指令绑定的值 例如 v-world = “msg”；msg是Vue数据
            console.log(binding.value);//hello,san
            // binding.expression 指令绑定值的字符串形式，返回”msg“本身
            console.log(binding.expression),//msg;
            //binding.args 传递给指令的参数
            console.log(binding.args)//yu
             // binding.modifiers 一个包含修饰符的对象 例如:v-world.hehe.haha,,这里的hehe，haha就是修饰符
            console.log(binding.modifiers)
            // binding.name    指令的id名，不包含v-前缀；
        }
    })
```
``` html
    <h1 v-world = "msg">{{msg}}</h1>
    <h1 v-world:yu>{{msg}}</h1>
    <h1 v-world.he.hu.la>{{msg}}</h1>
```
####11.1.2 简化写法
在定义全局指令的时候，有一种简化写法：
语法：`Vue.directive(指令id,callback)`
> 这里的`callback`函数，相当于`bind`和`update`的钩子函数
例如
``` javascript
    //  传入一个简单的函数，bind和update的时候调用
    Vue.directive("hehda",function(el,binding){
        console.log(1121);
        console.log(el);
        console.log(binding)
    })
```
###11.2 局部自定义指令
语法：使用Vue实例中的`directives`选项，例如
``` javascript
    /*
    定义局部自定义指令
    */
    var app = new Vue({
        el:"#container",
        data:{
            msg:"hello,San!"
        },
        methods:{
            // 会调用`update`的钩子函数
            changeMsg:function(){
                this.msg = "hello,萝卜白菜！"
            }
        },
        //局部自定义指令
        directives: {
            //hahah是指令id名
            hahah:{
                // 钩子函数...
                bind:function(){
                    // this指向window
                    alert(this.lili)
                }
            }
        }
    })
```
##12.过渡和动画
###1.简介
Vue在插入、更新、和移除DOM的时候，提供了多种不同的方式应用过渡效果，但是其本质上还是使用的是CSS3的原理：
transition和animation
### 2.基本用法
使用`transition`组件,将要执行动画的元素放在该组件内；为该组件定义一个属性`name`,如下:
``` html
     <transition name="fade" mode="">
        <p class="param" v-show="isShow"></p>
    </transition>
```
``` css
        .param{
            width: 100px;
            height: 100px;
            background: red;
            /* opacity: 0; */
        }
        .fade-enter-active{
            transition: all 5s linear;
            width: 100px;
            height: 100px;
            opacity: 1
        }
        .fade-leave-active{
            transition: all 5s linear;
            width: 0px;
            height: 0px;
            opacity: 0
        }
        .fade-enter{
            width: 0px;
            height: 0px;
            opacity: 0
        }
        /*  */
        .fade-leave{
            width: 100px;
            height: 100px;
            opacity: 1
        }
```
这里，属性`name`的值`fade`就是定义动画的类名的前缀，如：`fade-enter-active`,`fade-enter`,`fade-leave-active`,`fade-leave`,其中：
1. `fade-enter`/`fade-leave`:定义(进入/离开)动画开始的时候的第一帧位置（状态），也就是说执行(进入/离开)动画前的那一刻状态；
2. `fade-enter-active`/`fade-leave-active`: 定义(进入/离开)动画运行阶段（动画结束时的状态），你需要把动画的属性放在这里，如时长，动画执行方式等；
3. `fade-enter-to`/`fade-leave-to`:定义(进入/离开)过渡的结束状态
不过还是官网的图例比较清晰一点......
![Vue过渡](img/transition.png)
>总结： 简单来说，所谓的进入动画，就是元素从'看不见'到'看得见'的过程,同理，离开动画就是从'看得见'到‘看不见’的过程
###3.过渡动画的钩子函数
Vue为执行过渡动画的元素在不同的阶段定义了不同的钩子函数，这里有主要有
1. `before-enter`:动画进入之前执行
2. `enter`：动画开始进入时执行
3. `after-enter`：动画进入之后执行
4. `before-leave`：动画离开之前执行
5. `leave`：动画离开时执行
6. `after-leave`：动画离开后执行
例如：
``` html
     <transition name="fade" mode=""
        @before-enter = "beforeEnter"
        @enter = "enter"
        @after-enter = "afterEnter"
        @before-leave = "beforeLeave"
        @leave = "leave"
        @after-leave = "afterLeave"
        >
            <p class="param" v-show="isShow"></p>
        </transition>
```
``` javascript
 methods: {
                showHide: function () {
                    this.isShow = !this.isShow
                },
                //
                beforeEnter: (el) => {
                    alert("动画进入之前执行");
                    //这里的参数el是执行动画的DOM元素
                },
                enter:function(el){
                    alert("动画进入时执行")
                },
                afterEnter:function(el){
                    alert("动画进入之后执行");
                    el.style.background = "yellow"
                },
                beforeLeave:function(el){
                    alert("动画离开之前执行")
                },
                leave:function(el){
                    alert("动画离开时执行")
                },
                afterLeave:function(el){
                    alert("动画离开之后执行");
                    el.style.background = "red"
                }
            }
```
###4.多元素动画
`<transition>`组件内部只能有一个根元素，如果有多个更元素就不行了，但是如果有多个元素该怎么办呢？
就是今天要说的`<transition-group>`组件
###4.1 用法
``` html
<!-- 注意要给组件<transition-group>中的每一个根元素绑定唯一的属性key -->
    <transition-group name="fade" mode="" >
        <p class="param" v-bind:key="keu" v-show="isShow"></p>
        <p class="param" v-bind:key="kes" v-show="isShow"></p>
    </transition-group>
```
其他和`<transition>`差不多<hr/>
## 13.组件
###13.1 简介
组件（component）是Vue.js核心的功能之一，组件可以扩展`html`元素，封装可重用的代码，或者可以说组件是自定义标签（对象）
###13.2 定义组件的两种方式；
1. 先创建组件构造器，然后由组件构造器创建组件
 ``` javascript
    // 方式一：创建组件构造器，然后通过构造器创建Vue组件；
    // 1.通过Vue.extend()创建组件构造器；
    let ex = Vue.extend({
        template:'<h2>你好</h2>'
    });
    // 2.通过Vue.component(组件id，组件构造器)
    Vue.component('hello-world', ex);
        let app = new Vue({
            el:'#container',
            data:{
                msg:" i am back!"
            }
        })
 ```
 2. 直接创建组件
   使用`Vue.component(组件id,[options])`创建组件
``` javascript
    // 方式2 直接创建组件
    Vue.component('hello-msg',{
        template:'<h3>我的天啊</h3>'
    })
```
###13.3 组件的分类；
Vue中的组件分为全局组件和局部组件；顾名思义，全局组件在任何地方放都可以使用，而局部组件只能在当前Vue实例的环境中使用。
####13.3.1 全局组件
能够在全局环境中使用的组件，其语法如下：
``` javascript
    Vue.component("hello", {
        // 这里的template是该组件的模板
            template:'<h3>{{componMsg}}</h3>',
            data:function(){
                return {
                    componMsg:'必须是一个函数'
                }
            }
        })
        // 在组件中存储数据的时候必须要以函数的形式，return一个对象即可
```
####13.3.2 局部组件
使用`Vue`实例的`components`选项,该选项是一个对象，具体如下：
``` javascript
    let app = new Vue({
        el:'#container',
        data:{
            msg:'hehe'
        },
        components: {
            'haha':{
                template:'<h1>{{greeting}}</h1>',//模板
                data:function(){//组件内的数据
                    return {
                        greeting:'早上好！'
                    }
                }
            }
        }
    })
```
###13.3 使用模板
当组件模板中的内容比较复杂的时候，可以使用动态模板；通过一个自定义标签`template`来包裹住模板内容；根据`template`标签上的id来和组件一一对应；例如：
``` javascript
     // 那么当组件模板的结构比较复杂的时候，可以使用动态模板；
    //  组件的id名一般采用‘-’式的
        Vue.component('my-name',{
            template:'#just',
            data:function(){
                return {
                    nameArr: ['Tom','Jack','Load','John']
                };
            }
        });
```
html部分：
``` html
<!-- 模板内容通过id来和组件确定，包裹着的内容有且只有一个根元素 -->
    <template id="just">
        <ul>
            <li v-for = "item in nameArr">{{item}}</li>
        </ul>
    </template>
```
###13.4 动态组件
使用`<component is = ""></component>`组件，多个组件使用同一个挂载点（`component`组件所在位置），然后动态地在他们之间切换。例如：
``` javascript
    Vue.component('my-name', {
            template: '#just',
            data: function () {
                return {
                    nameArr: ['Tom', 'Jack', 'Load', 'John'],
                    animal:'cat'
                };
            }
        });
        // 组件2
        Vue.component('my-earth', {
            template:'<h2>{{name}}</h2>',
            data:function(){
                return {
                    name:'地球'
                };
            }
        });
        // 局部组件
        let app = new Vue({
            el: '#container',
            data: {
                msg: 'hehe',
                flag:true,
                flage:'my-earth'
            },
            methods:{
                showcompo:function(){
                    this.flag = !this.flag;
                }
            }
        })
        // 现在flage是my-earth，所以会显示id为my-earth的组件，然后通过改变flage的值来显示不同的组件
```
``` html
     <component :is="flage"></component>
```
通过属性`is`绑定组件id，来确定那个组件显示,那个组件不显示。
`keep-alive`组件，可以将切换出去的组件（不显示的组件，非活动组件）缓存起来，保存状态（不用重新渲染组件），默认每次切换都会销毁和重新创建组件,一旦这样子做，会提高效率的；
``` html
    <keep-alive>
          <component :is="flage"></component>
     </keep-alive>
     <!-- 缓存，component组件中的所有待显示的自=组件 -->
```
### 13.5 父子组件和组件间数据的传递
#### 13.5.1 父子组件
在一个组件内部定义另一个组件,称为父子组件
>子组件只能在父组件内部使用
``` javascript
     let app = new Vue({// 根组件
            el: '#container',
            data: {
                msg: 'hehe',
                flag:true,
                flage:'my-earth'
            },
            components: {
                'my-hello':{// 父组件
                    template:'#hello',
                    data () {
                        return {
                            name:'李白',
                            user:{id:'9527',name:'唐伯虎',age:25},
                            address:'陕西省西安市雁塔区锦业二路付村花园'
                        };
                    },
                    components: {
                        'my-world':{// 子组件
                            template:'#world',
                            data () {
                                return {
                                    empire:'唐'
                                };
                            }
                        }
                    }
                }
            }
        })
```
``` html
     <div id="container" v-cloak>
        <h3>{{msg}}</h3>
        <my-hello></my-hello>
    </div>
    <!-- 父组件模板 -->
    <template id="hello">
        <div>
            <h3>我是hello，一个父组件</h3>
            <my-world></my-world>
        </div>
    </template>
    <!-- 子组件模板 -->
    <template id="world">
        <div>
            <h3>{{empire}}</h3>
        </div>
    </template>
```
默认情况下，子组件无法访问父组件中的数据，每一个组件的作用域（无论是什么关系）是独立的；
#### 13.5.2 组件间数据的通信；
#####13.5.2.1 子组件访问父组件中的数据；
1. 在调用子组件（使用子组件）的时候，绑定(`v-bind`)想要获取的父组件的数据
2. 在子组件中内部，使用`props`选项声明想要获取的数据（数组或对象），也就是来接受来自父组件上的数据；例如：
``` html
    <!-- 父组件模板 -->
    <template id="hello">
        <div>
            <h3>我是hello，一个父组件</h3>
            <h3>这些是父组件的数据：{{name}},{{address}}</h3>
            <!-- step1 :在调用自组建时候，绑定想要获取的父组件的数据 -->
            <!-- 在这个div内部所有的部分（包括子组件本身）都属于父组件，所以当然可以访问父组件数据 -->
             <my-world v-bind:name="name" :address = "address"></my-world>
        </div>
    </template>
    <!-- 子组件模板 -->
    <template id="world">
        <div>
            <h3>{{empire}}</h3>
            <!-- 拿到了父组件中的数据name -->
            <h1>{{name}}</h1>
        </div>
    </template>
```
``` javascript
    components: {
                        'my-world':{// 子组件
                            template:'#world',
                            data () {
                                return {
                                    empire:'唐'
                                };
                            },
                            //  step2 使用props选项 声明想要获取的数据,在这里是逍遥获取数据name和address
                            props:['name','address']
                        }
                    }
```
`props`也可以是对象，用来配置高级的设置，如类型的判断，数据校验，默认值等
``` javascript
    'my-computer':{// 子组件
        template:'#computer',
        data () {
            return {
                page:3
            };
        },
        props:{
            address:String, // 指定类型 必须是字符串
            ser:{
                type:Object,// 数据user的类型必须是对象,如果不是对象就会报错
                required:true, // 必须要有的参数
                default:function(){
                    return {
                        name:'张三',
                        age:3
                    }
                }
            }
        }
    }
```
``` html
     <my-computer v-bind:user="user" v-bind:address="address"></my-computer>
```
总结：
1. 父组件通过props向下传递数据给子组件，
2. 组件中的数据有三种形式，data，计算属性和props传递
##### 13.5.2.2 父组件访问子组件中的数据；
1. 在子组件中使用`vm.$emit(事件名,数据)`，触发一个自定义事件，事件名随意，这里的`vm`是当前的子组件
2. 父组件在使用子组件的地方（写子组件的地方）侦听子组件扔出来的自定义事件,侦听到之后,并在父组件中定义一个方法，来接收子组件传递过来的数据;
总之：首先子组件通过一个事件events给父组件发送消息，实际上就是子组件把自己的数据发送父组件;
例如:
``` javascript
    let app = new Vue({ // 根组件
            el: '#container',
            data: {
                msg: 'hehe',
                flag: true
            },
            components: {
                'my-hello':{// 父组件
                    template:'#hello',
                    data () {
                        return {
                            message:'你好，我是Vue',
                            send:'', //首先要预定义
                            user:''// 同上
                        };
                    },
                    methods: {
                        // 3. 并在父组件中定义一个方法，来接收子组件传递过来的数据
                        'getData':function(send,user){
                            this.send = send;
                            this.user = user;
                        }
                    },
                    components: {
                        'my-world':{ // 子组件
                            template:'#world',
                            data () {
                                return {
                                    send:'byIphone',
                                    user:{
                                        name:'张三',
                                        age:13,
                                        sex:'男'
                                    }
                                };
                            },
                            props:['message'],
                            methods: {
                                sendData:function(){
 // 1.在子组件中使用`vm.$emit(事件名,数据)`，触发一个自定义事件，事件名随意，这里的vm是当前的子组件
                                    // 在这里的this 指向的是当前子组件本身
                                    console.log(this);
                                    this.$emit('load',this.send,this.user)
                                }
                            }
                        }
                    }
                }
            }
        });
```
``` html

    <!-- 父组件my-hello模板 -->
    <template id="hello">
        <div>
            <h3>{{message}}</h3>
            <!-- 刚开始没有,当点击按钮后就有了 -->
            <h1>{{send}}</h1>
            <!-- 同上 -->
            <h1>{{user.name}}</h1>
            <!-- 子组件只能在父组件中使用 -->
            <!-- 在父组件中侦听子组件抛出的自定义事件,并定义一个getData方法来接收数据 -->
            <my-world v-bind:message="message" v-on:load="getData"></my-world>
        </div>
    </template>
    <!-- 子组件模板 -->
    <template id="world">
        <div>
            <h1>{{send}}</h1>
            <hr />
            <h3>{{message}}</h3>
            <button @click="sendData()">发送子组件中的数据给父组件my-hello</button>
        </div>
    </template>
```
### 15.5.2.3 单项数据流
`props`是单项绑定的，当父组件中的数据发生变化的时候将会传导给子组件，但不会反过来（子组件中直接改变从父组件中传递过来的prop数据是行不通的）；
解决办法：
    way1：如果子组件想把prop数据作为局部数据来使用，可以将数据存入子组件中另一个变量中再操作，这时该变量已经和父组件数据没有关系了；
    way2：如果子组件想修改prop数据并同步更新到父组件，两种方法：
        a).使用`.sync`(版本2.3以上支持),1.在父组件上将要绑定给子组件的数据添加修饰符`sync`,2.在子组件中通过一个事件使用`vm.$emit('update:prop数据'，'修改后的值')`；(不常用)
        b).可以将父组件中的数据（对象类型）传递给子组件，然后在子组件中修改对象的属性（因为对象是引用类型，父（子）组件拿到的数据指向的是同一个对象）
方法2：a)
``` html
            <template id="hello">
                <div>
                    <h2>人数：{{members}}</h2>
                    <input v-model="members" type="text" />
                    <!-- 结果是当父组件数据发生变化的时候，子组件中的数据也会发生改变 -->
                    <my-world v-bind:members.sync="members"></my-world>
                </div>
            </template>
```
``` javascript
            methods: {
                                changeMember:function(){
                                    this.$emit('update:members',500);
                                }
                            }
```
方法2：b)
``` javascript
    'my-hello':{ // 父组件
                    template:'#hello',
                    data () {
                        return {
                            // 父组件中的对象数据
                            book:{
                                name:'愿你迷路到我身旁',
                                author:'蕊希',
                                price:'💴20'
                            }
                        };
                    },
                    components: {
                        'my-world':{ // 子组件
                            template:'#world',
                            // step2：通过props获取父父组件上的数据
                            props: ['book'],// 拿到了父组件上数据book，
                            methods: {
                                // step3:该改变props数据的属性
                                changeMember:function(){
                                    this.book.name = '总要习惯一个人';
                                }
                            }
                        }
                    }
                }
```
``` html
     <!-- 父组件模板 -->
    <template id="hello">
        <div>
            <h1>我的书籍:{{book.name}}</h1>
            <!-- step1：将数据对象绑定给子组件 -->
            <my-world v-bind:book="book"></my-world>
        </div>
    </template>
    <!-- 子组件模板 -->
    <template id="world">
        <div>
            <h1>{{book.name}}</h1>
            <button @click="changeMember">改变数据</button>
        </div>
    </template>
```

Way1:
``` javascript
     let app = new Vue({ // 爷爷组件 （根组件）
            el:'#container',
            data:{
                company:'思安新能源股份有限公司'
            },
            components: {
                'my-hello':{ // 父组件
                    template:'#hello',
                    data () {
                        return {
                            members:200
                        };
                    },
                    components: {
                        'my-world':{ // 子组件
                            template:'#world',
                            data () {
                                return {
                                    industry:'煤炭和电力',
                                    companymember:this.members// 将props数据存入子组件中的另一个变量中
                                };
                            },
                            props: ['members'],// 拿到了父组件上数据，
                            methods: {
                                changeMember:function(){
                                    this.companymember = '300';
                                }
                            }
                        }
                    }
                }
            }
        });
```
``` html
    <!-- 父组件模板 -->
    <template id="hello">
        <div>
            <h2>人数：{{members}}</h2>
            <input v-model="members" type="text" />
            <!-- 结果是当父组件数据发生变化的时候，子组件中的数据也会发生改变 -->
            <my-world v-bind:members="members"></my-world>
        </div>
    </template>
    <!-- 子组件模板 -->
    <template id="world">
        <div>
            <h4>所属行业：{{industry}}</h4>
            <!-- 子组件的局部类变量companymember，已经和父组件上的变量没有关系了 -->
            <h2>公司人数：{{companymember}}</h2>
            <!-- 因为changemember方法是子组件上定义的，所以... -->
            <button @click="changeMember">改变数据</button>
        </div>
    </template>
```
####15.5.2.4 非父子组件间数据的通信
对于非父子组件间的通信：可以通过一个空的Vue实例作为中央事件总线（事件中心），用它来触发事件和侦听事件。
整个过程如下：
1. `var bus = new Vue()`:新建一个Vue实例作为中央事件总线；
2. `bus.$emit(自定义事件名,抛出的数据)`:在抛出数据的组件中，定义一个方法（methods中）通过`bus`来执行抛出事件和数据的操作`;
3. `bus.$on(自定义事件名,function(data){})`:在接受数据的组件中，一般在其生命周期的`mounted`阶段，通过`bus`侦听那个自定义事件，并接受数据；
> 简单的情况下是这样使用，但是在项目中一般要用到Vuex,来进行管理；
例如：
``` javascript
    // 定义一个空的Vue实例，作为中央事件总线
        let bus = new Vue();
        let app = new Vue({ // 根组件
            el:'#container',
            data:{
                task:'完成数据的展示',
                house:{
                    address:'陕西省西安市雁塔区锦业路一号',
                    price:'13000',
                    area:'124㎡'
                }
            },
            components: {
                'my-task':{// 父组件
                    template:'#tasks',
                    data () {
                        return {
                            timeLine:'明天'
                        };
                    },
                    components: {
                        'my-house':{ // 子组件1
                            template:'#house',
                            data () {
                                return {
                                    floor:28
                                };
                            }
                        },
                        'my-book':{ // 子组件2
                            template:'#book',
                            data () {
                                return {
                                    bookname:'愿你迷路到我身边'
                                };
                            },
                            // 定义一个放方法，通过中央事件总线bus触发一个自定义事件data-send,将数据bookname抛出去
                            methods: {
                                'sendData':function(){
                                    bus.$emit('data-send',this.bookname);
                                }
                            }
                        },
                        'my-computer':{
                            template:'#computer',
                            data () {
                                return {
                                    computer:'lenovo电脑',
                                    bookname:''
                                };
                            },
                            // 侦听自定义事件,当模板编译完成后执行
                            mounted:function(){
                                let _this = this;// 这个this才代表了组件 'my-computer'本身
                                //  通过中央事件总线bus，来监听跑出来的自定义事件
                                bus.$on('data-send',function(bookname){
                                    // 里面的this是bus实例，所以要在外部定义一个变量来保存外部的this
                                    _this.bookname = bookname;
                                });
                            }
                        }
                    }
                }
            }
        });
```
####15.5.2.5 slot内容分发
本意：位置，槽；
Vue：用于获取组件中的原内容（组件内部的内容），
方法：
1. 对于单`slot`组件，只需要在组件内部的合适地方写下`slot`标签即可（也就是原内容将来要呈现的位置），例如：
``` html
    <div id="container">
        <!-- 组件,其中的原内容就是"你好"两个字 -->
        <my-hello>你好</my-hello>
    </div>
    <template id="hello">
        <div>
            <h3>{{lesson}}</h3>
            <!-- 只需要在组件内部合适的地方插入组件slot组件，在slot的位置就会出现原内容 -->
            <slot>如果没有原内容就会显示这一段文字</slot>
        </div>
    </template>
```
2. 对于具名`slot`，如果原内容的结构比较复杂，那需要用到具名slot了：
  + 对于要分发的原内容用`slot`属性进行分组，例如：`slot = "bikc"`;
  + 在组件的模板内部的合适使用slot组件，为其指定name属性，例如:`slot = "bikc"`,
  + 渲染出来的效果就是，在模板中slot出现的位置显示对应的原内容；
``` html
    <!-- 具名slot -->
    <my-world>
        <!-- 原内容1 -->
        <div  slot="title">这是一本书 </div>
        <!-- 原内容2 -->
        <div slot="house">我最喜欢的一本书</div>
    </my-world>

     <template id="world">
        <div>
            <slot name = "title"></slot>
            <!-- 获取的内容将是属性slot值为title的原素，所代表的内容 -->
            <h2>{{book}}</h2>
            <slot name = "house"></slot>
            <!-- 同上 -->
        </div>
    </template>
```
##14、路由
### 14.1 路由的基本用法
常用来开发基于vue的SPA（单页面应用），根据不同的url地址，显示不同的内容，但始终是显示在一个界面上
基本的工作：简单使用的时候，需要引用`vue-router.js`文件；
基本的路由可以分为四步（js部分）：
1. 定义组件；
2. 配置路由；
3. 创建路由实例；
4. 创建根实例，并将路由实例挂载到Vue实例上
html部分：
1. 使用`router-link`组件定义导航，`to`属性指定连接的url；
2. 使用`router-view`组件定义路由的内容；
完整的例子：
``` html
    <div id="container">
        <!-- 使用router-link 定义导航，to属性指定连接url -->
        <div id="routerLink">
            <router-link to="/main">主页</router-link>
            <router-link to="/news">新闻</router-link>
        </div>
        <!-- router-view组件用来定义路由内容 -->
        <div id="content">
            <router-view></router-view>
        </div>
    </div>
```
``` javascript
    // 1. 定义组件，（只是定义了将来router-view中显示的内容)
        let home = {
            template:'<h2>我是主页</h2>'
        };
        let news = {
            template:'<h2>我是新闻</h2>'
        };
        // 2.配置路由(把相关的路由规则或者参数设置好)
        let routes = [
            {
                path:'/home',
                component:home
            },
            {
                path:'/news',
                component:news
            },
            { path: '*', redirect: '/home'} // 路由重定向,默认显示/home，连接到的内容
        ];
        // 3.创建路由实例；
        const router = new VueRouter({
            routes: routes,
            // mode:'history', // 定义路由模式,默认是hash;
            linkActiveClass:'active' // 定义连接激活时候的样式类
        })
        // 4.创建根实例，并将路由实例挂载到Vue实例上
        let app = new Vue({
            el:'#container',
            data:{
                book:'总要习惯一个人'
            },
            methods: {
                'change':function(){
                    console.log(this.book);
                }
            },
            router:router // 注入路由
        });
```
###14.2 路由的嵌套和传参
####14.2.1 路由的嵌套
一个路由下面可能有子路由，就像一个菜单下面可能有其二级菜单那样，那么路由的嵌套是怎么一回事呢？
``` javascript
     // 1. 定义组件
        let home = {
            template:'<h2>我是主页</h2>'
        };
        let user = {
            template:'#user'
        };
        // a. 子路由对应的内容模板
        let login = {
            template:'<h2>用户登录</h2>' // 当然内容过多和复杂可以使用 动态模板哦！ 😁
        };
        let regist = {
            template:'<h2>用户注册</h2>'
        };
        // 2.配置路由
        let routes = [
            {
                path:'/main',
                component:home
            },
            {
                path:'/user',
                component:user,
                // b. 在路由'/user'下配置子路由,一个路由下可能有多个子路由，所以children是一个数组
                children:[
                    {
                        path:'login',
                        component:login
                    },
                    {
                        path:'regist',
                        component:regist
                    },
                ]
            },
            { path: '*', redirect: '/main'} // 路由重定向,默认显示/home，连接到的内容
        ];
        // 3.创建路由实例；
        const router = new VueRouter({
            routes: routes,
            // mode:'history', // 定义路由模式,默认是hash;
            linkActiveClass:'active' // 定义连接激活时候的样式类
        });
        // 4.创建根实例，并将路由实例挂载到Vue实例上
        let app = new Vue({
            el:'#container',
            data:{
                book:'总要习惯一个人'
            },
            methods: {
                'change':function(){
                    console.log(this.book);
                }
            },
            router:router // 注入路由
        });
```
HTML部分：
``` html
    <!-- 路由 -->
    <div id="container">
        <!-- 使用router-link 定义导航，to属性指定连接url -->
        <div id="routerLink">
            <router-link to="/main">主页</router-link>
            <router-link to="/user">用户</router-link>
        </div>
        <!-- router-view组件用来定义路由内容 -->
        <div id="content">
            <router-view></router-view>
        </div>
    </div>
    <template id="user">
        <div>
            <h3>用户信息</h3>
            <ul>
                <!-- 嵌套的路由，由于是/user路由下的，所以前面要加上'/user'，这样才能体现出父子关系嘛！😄， -->
                <!-- 为什么要写在user的模板里呢？那是因为他们是user下面的子路由，当切换到user路由的时候才会出现，所以必须作为/user模板的一部分 -->
                <li><router-link to="/user/login">用户注册</router-link></li>
                <li><router-link to="/user/regist">用户登陆</router-link></li>

                <!-- 指定一个tag属性，将来在实际渲染的时候就会渲染成li  -->
                <!-- <router-link to="/user/login" tag="li">用户注册</router-link>
                <router-link to="/user/regist" tag="li">用户登陆</router-link> -->
            </ul>
            <!-- 子路由的内容显示的位置 -->
            <router-view></router-view>
        </div>
    </template>
```
> 像上面那样，就在路由user下建立了子路由；
#### 14.2.2 路由的传参
传参的两种方式：
1. 查询字符串，如‘login?name = zhangsan&id = 12’；
``` html
    <!-- 第一种传参方式 -->
    <li><router-link to="/user/login?name=zahnsgan&id=123">用户注册</router-link></li>
```
``` javascript
    // 通过`$route.query`返回一个包含参数的对象,也就是说$route.query是一个对象'
    let login = {
        template:'<h2>用户登录， 获取参数:{{$route.query}}</h2>'
    };
```
2.  rest风格url，例如‘regist/name/id’
``` html
     <!-- 第二种传参方式，这这里的alice和123就是要传的参数，那么怎么区分他们是参数呢（而不是各级子路由呢），下面有详细的解答-->
     <li><router-link to="/user/regist/alice/123">用户注册</router-link></li>
```
```javascript
    let regist = {
        // 如果说是第二种方式 通过 $route.params, {{$route.path}} 会获取路由的路径
         template:'<h2>用户注册 获取参数2 {{$route.params}},{{$route.path}}</h2>'
    };
    {
                path:'/user',
                component:user,
                // b. 在路由'/user'下配置子路由,一个路由下可能有多个子路由，所以children是一个数组
                children:[
                    {
                        path:'login',
                        component:login
                    },
                    {
                        // 指定上面的两个参数alice和123分别代表什么意思，名字和id
                        path:'regist/:name/:id',
                        component:regist
                    },
                ]
            },
```
###14.2.3 路由实例的方法
1. `router.push()`,添加路由(实际上就是切换路由)，功能上和`<router-link>`一样
2. `router.replace()`,替换路由（跟切换路由差不多），只不过不会产生历史记录(也就是不会回退)
例如：
``` html
    <button @click="addRouter()">添加路由</button>
    <button @click="changeRouter()">替换路由</button>
```
``` javascript
    let app = new Vue({
            el:'#container',
            data:{
                book:'总要习惯一个人'
            },
            methods: {
                'change':function(){
                    console.log(this.book);
                },
                // 添加路由（切换路由）
                'addRouter':function(){
                    // 路由实例.push
                    router2.push({path:'/main'}); // 其实就是切换路由，这里就是将路由切换到`/main`，效果和点击一下`主页`作用是一样的
                },
                // 替换路由
                'changeRouter':function(){
                    // 路由实例.replace()
                    router2.replace({path:'/user'}); // 效果是直接跳转到了`/user`的路由，和直接点击路由`/user`相比，这样做没有历记录（不能回退）
                }
            },
            router:router2 // 注入路由
        });7与咩咩咩咩咩咩咩咩咩咩咩咩咩咩咩咩模块，，，，，，
```
###14.2.4 路由结合动画；
略
### 14.3 单文件组件；
####14.3.1 .vue文件
`.vue`文件称为单文件组件，是`vue.js`自定义的一种文件格式，一个`.vue`文件就是一个组件，
在文件内部封装了组件相关的代码：html,css,js；
也就是说`.vue`文件由三部分组成：`template` ,`style`,`script`,标准的模板是：
``` html
    <template>
        html代码
    </template>

    <style>
        css代码
    </style>

    <script>
        js代码
    </script>
```
####14.3.2 vue-loader
但是浏览器并不认识`.vue`文件，所以必须对该文件进行加载和解析；此时需要`vue-loader`,
类似的loader还有很多，如：`html-loader`(加载并识别单文件组件中的html代码),`style-loader`（同理）,`babel-loader`(同理)等；
`vue-loader`是属于`webpack`的，所以你如果想要用webpack，就先要使用并安装webpack；
####14.3.3 webpack
一个前端资源模块化加载器和打包工具，它能够把前端的各种资源都作为模块来使用和处理，webpack也是通过不同的loader将资源进行打包和输出打包后的文件；
总而言之，webpack就是一个模块加载器，所有的资源都作为模块来加载<font color = red>【在webpack的眼中万物皆模块】</font>，最后打包输出；
[官网](http://www.webpack.io/)；
webpack有一个核心配置文件，webpack.config.js,必须放在项目的根目录下（跟文件夹的一级菜单）
####14.3.4 事例和步骤
1. 创建项目，目录结构如下:
webpack-demo
    |--index.html（s）
    |--package.json 工程文件（不用自己创建，系统会生成）
    |--webpack.config.js  webpack配置文件
    |--babel.lrc babel配置文件 （es6才有）
    |--.eslintignore 忽略eslint的对那些（类型）文件的规范检测；
    |--static 文件夹（静态资源文件夹）
    |--config 文件夹（配置信息文件夹）
    |--build文件夹（操作文件）
    |--src文件夹（主要编写代码的地方）
        |--main.js 入口文件
....创建以上文件，其中
> `package.json`文件一般是在根目录下使用 node命令`npm init --yes`来创建
1. 编写App.vue文件
   ......
2. 安装相关的模块（加载器,在根目录），用来识别`.vue`文件中的`html`,`js`和`css`;
   最好使用`cnpm`安装 在`npm`中安装`cnpm`的命令是`npm install -g cnpm --registry=https://registry.npm.taobao.org`
* `npm install vue -S`;  // vue的生产依赖(生产的时候需要存在的)【基本核心，引用vue.js的时候有用】
* `cnpm install webpack -D` // 基本开发依赖【基本】
* `cnpm install webpack-dev-server -D` webpack静态服务器【基本】
  <!-- loader部分 -->
* `cnpm install vue-loader -D`//【vue加载器】
* `cnpm install vue-html-loader -D`//【识别vue文件中html部分的加载器】
* `cnpm install css-loader -D`//【识别vue文件中css部分的加载器】
* `cnpm install vue-style-loader -D`//【识别vue文件中style部分的加载器】
* `cnpm install file-loader -D`//【文件资源，字体，图片等】
* `cnpm install vue-template-compiler -D` //【预编译template模板】
  <!-- ES6部分的loader（使用es6的时候要装） -->
* `cnpm install babel-loader -D`
* `cnpm install babel-core -D`
* `cnpm install babel-preset-env -D` //【根据配置的运行环境，自动启用需要的babel插件】
4. 编写入口文件main.js
...
5. 编写webpack.config.js
6. 编写.babelrc文件
7. 编写package.json文件
8. 运行测试
    在 node 的命令中来到项目的根目录下，执行`npm run dev`(并不一定是dev,这个`dev`来自于package.json)
<hr>

###14.4 Vue-cli脚手架（3.0）；
####14.4.1 简介
vue-cli是一个Vue脚手架，可以快速构造项目结构；
vue-cli本身集成了多种项目的模板：
####14.4.2 根据网上的一些教程初始化项目
1.  `npm install -g @vue/cli` 全局安装 vue-cli 3.0;
2.  `vue create <project-name>` 创建项目，包括一系列配置项，具体可以参考[vue-cli 3.0配置](https://juejin.im/entry/5ac1c540f265da237c690faf)和[vue-cli 3.0 配置](https://juejin.im/post/5ad862c95188252eb3237752)
3.  自己手动在项目的根目录创建一个`vue.config.js`,参考配置项文章[vue.config.js配置模板](https://juejin.im/post/5ad862c95188252eb323775
5. `npm run serve`运行项目
6. `(c)npm run build` 构建项目
###14.5 模块化开发；
####14.5.1 安装 vue-router路由，模块化（vue-cli 3.0 已经在`src/main.js`里面集成并且引用）;

####14.5.2路由在模块开发中的应用
> 1. 文件夹 `components`中创建和编辑所有的单文件组件；
> 2. 根目录下的`router.js`文件是一个路由配置文件，基础的配置工作已经做好了
> 3. 使用`import`导入文件（模块）的时候符号`./`表示在当前目录下;例如：`import abc from path文件`你可以理解为将path文件作为一个名为abc（名字可以自定义）的模块引用过来，以后就abc就代表path文件了，引用abc相当于引用该文件；注意引用过来只是拿过来了
1. 编辑`App.vue`组件，配置`router-link`路由；
2. 在`components`文件夹下创建（编辑）单文件组件
   每一个单文件组件分为三部分`template`,`style`,和`script`,其中`script`中一般要有`export default {...}`里面中的`...`表示的是当前组件的一些选项：data，事件，方法等
3. 在`router.js`文件中配置路由
####14.5.3 axios在模块化开发中的应用
1. 安装axios；
    cnpm install axios
    使用axios的两种方式：
        1. 在每一个使用axios的单文件组件中，引入axios；
            在组件中使用`import axios form axios`来引入axios模块；
            然后在正常那样使用axios；
            例如：
``` javascript
    import axios from 'axios';// 引入axios
    export default {
        methods: {
            sendAjax:function () {
                axios.get()
            }
        }
    };
```
2. 在全局引入axios
    在`main.js`文件中全局引入`axios`;并添加到Vue的原型中
    `import axios from axios`；
    `Vue.prototype.axios = axios`;此时axios是作为Vue对象的全局方法而出现的；
``` javascript
    export default {
        methods: {
            sendAjax:function () {
                //这里的this就是vue组件本身
                this.axios.get()
            }
        }
    };
```

####14.5.4 为自定义组件添加事件；
> <font color = red >component文件夹中的每一个`.vue`文件都是独立的组件,那么怎么将其中的一个组件作为另一个组件的子组件呢?
>其实很简单：首先在你指定的父组件文件中，引入该子组件：`import name form ‘子组件路径’`，这样做只是将该组件引过来了，若想作为子组件，那么必须将其注册为子组件（通过父组件中的components选项）注册，然后在父组件的template中使用该子组件；
> </font>
>  每一个单文件组件中的`export default {...}`就相当于该组件本身---在其内部存储着组件的数据，方法，子组件注册等等选项
例如：
``` javascript
    import button from './components/button'; //引入组件,路径要写对
    export default {
        //将引用过来的组件注册为本组件的子组件
        components: {
        'my-button':button
        }
    }
```
###14.6 Element UI
####14.6.1 简介
饿了么团队提供的一套基于Vue2.0的前端框架,PC端是Element，移动端是MintUI
####14.6.2 快速上手
1. 安装Element ui；
`cnpm install element-ui -S`
2. 在main.js文件中引如并使用组件；
``` javascript
    import elementUI from 'element-ui'; // 引入的是js文件
    import 'element-ui/lib/theme-chalk/index.css'; //css文件需要单独引用
    Vue.use(elementUI);
```
>在Vue-cli3.0中，初始化的时候只需要上述操作就可以完整引用element-ui的全部内容(css/js)了,不需要其他的配置，以后的工作就是使用element上的组件即可
### 14.7 全局组件；
全局组件（插件），就是可以在`main.js`中使用`Vue.use()`进行全局引入，然后其他组件中就都可以使用了，如`vue-router`;
import VueRouter from 'vue-router';
Vue.use(VueRouter);
普通组件（插件）：每次使用的时候都要引入，比如`axios`;
import axios form axios;
####14.7.1 定义全局组件并使用
1. 在`components`文件夹下，新建一个文件夹，然后在该文件夹下创建Vue组件,例如`user.vue`；
2. 在当前文件夹下新建一个`.js`文件；在该`js`文件中,如`user.js`
``` javascript
    // 引入组件,因为是当前文件夹下的user.vue组件
    import user from './user.vue';
    // 导出
    export default {
        install:function (Vue) {
            // 这里的user是上面引入的user组件；username是一个全局组件的组件名，可以随便定义
            Vue.component('username',user);
        }
    };
```
3. 在main.js中使用`import`引入当前自定义的全局组件,并使用之
`import username1 from './components/user/user.js'`;
`Vue.use(username1)`;
4. 以后就可以直接在任何一个组件中使用`username1`模块了
###14.8 Vuex；
####14.8.1 简介
简单来说就是用来集中管理数据，项目比较简单的时候没必要用，当项目比较大的时候，用起来比较方便，类似于react中的redux，都是基于Flux的前端状态管理框架
####14.8.2 基本用法
1. 安装Vuex，在vue-cli 3.0中在项目初始化的时候，Vuex已经安装了(在package.json中可以看到)
2. 创建`store.js`文件，并在入口文件`main.js`文件中导入`import`该文件，然后在根实例中配置store选项（vue-cli3.0已经做好了）,配置:
``` javascript
    new Vue({
        router,// 相当于 router：router
        store, // 同上,相当于：store：store，Vue会将store对象注入到所有的子组件当中，在子组件中通过this.$store来访问该对象
        ...
    })
```
3. 理解Vuex的工作原理
   ![Vuex原理图](img/vuex.png)
> 个人理解：`dispatch`派遣，首先是通过操作组件来抛出一个动作比如点击事件等，来触发一个定义在`actions`里面的方法（或动作），在该方法中的主要作用是提交`commit`一个变化（mutation）,然后由`mutation`选项中来改变数据，然后再次渲染组件；
4. 编辑`store.js`文件;
Vuex的核心是Store（仓库），相当于是一个容器，一个store实例中包含以下属性和方法：
* state    定义属性（状态，数据）,是一个对象，也就是定义和存储数据（状态）的地方
* getters 获取属性的
* actions 用来定义要执行的操作方法（动作）,流程的判断（if-else），ajax请求等，不能在这里直接操作数据。
* 都在这里定义通过commit 提交变化（修改数据的唯一方法就是显式提交 mutation（通过commit）），根据Vuex工作原理，该步骤会提交一个变化给mutations
* mutations ，处理（操作）状态（数据），具体要执行的动作
> 不能直接在actions中修改数据，必须显式的提交变化，目的是为了追踪数据的变化
> 其实在vue-cli 3.0 中 在项目初始化的时候已经配置好了该文件（只是模板配置，基本工作已经做好）
1. 在子组件中访问store对象的两种方法：
   方式一： 通过`this.$store`访问，这里的`this`指的是Vue组件实例本身；
   方式二：通过`mapGetters`,`mapActions`,vuex提供了两种方法：
            mapState：获取state；
            mapGetters：获取getters；
            mapActions:获取方法actions；
    怎么使用mapGetters？（其他相同）
    a. 首先在单文件组件中引入一个模块：`import { mapGetters } from "vuex"`;
    b. 在`store.js`中的输出中添加一个`getters`选项，
    c. 在单文件组件中的计算属性中引用
单文件组件中：
``` javascript
    // 数组中的num就是store.js中getters选项中的num函数
    computed:mapGetters([
      'num'
    ])
```
store.js中配置：
``` javascript
    state:{
        num:1
    },
     getters:{
        // 这里的state 就是上面的state对象
        num:function (state) {
            return state.num;
        }
    },
```
Vuex作为专门管理数据和状态的技术，自然操作数据的方法也是在Vuex管理的，所以---
``` javascript
    export default new Vuex.Store({
        state: {
            num:1
        },
        getters:{
            // 这里的state 就是上面的state对象
            num:function (state) {
            return state.num;
            }
        },
        actions: {
            add:function (params) {
                params.commit('increment');
            // 提交一个名为increment（名字随意）的变化，名称可以自定义，提交到了mutations
            }
        },
        // mutations处理数据的改变,具体要在执行什么动作
        mutations:{
            // 这里的increment来自于上面的自定义increment
            increment:function (state) {
                state.num++;
            }
        }
    });
```
在对应的单文件组件中：
``` javascript
    methods:mapActions([
        // 来源于store.js中actions选项中定义的add；
      'add'
    ]),
```
####14.8.3 更好的组织Vuex结构
|-src
    |-store
        |-index.js //公共模块
        |-getters.js
        |-actions.js
        |-mutations.js
        |-modules //根据业务，分为多个模块，每个模块都可以拥有自己的state，actions，actions，mutations
            |-user.js
            |-cart.js
            |-goods.js
            |-...
