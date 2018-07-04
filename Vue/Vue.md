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
