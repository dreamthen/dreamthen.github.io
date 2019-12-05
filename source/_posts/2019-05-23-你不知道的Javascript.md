---
title: 你不知道的Javascript
date: 2019-05-23 14:22:45
tags: [Javascript]
categories: 你不知道的Javascript
---
# <上篇>整理: 词法作用域、this以及原型对象
## 一、词法作用域
> 浏览器执行JavaScript语言

 <p>在浏览器引擎执行JS之前,JS就已经经过了浏览器编译器的编译,也就是词法分析和语法分析,将关键字、保留字、自定义变量以及函数根据词法解释和抽象语法树进行解析,并且按照优先级和词法作用域放到应有的位置上,最后通过浏览器引擎执行</p>
 
> 词法分析

    词法分析分为: 分词和词法解释。
    分词就是将各个表达式根据空格分开,再根据关键字、保留字等词法进行匹配词法解释。

> 语法分析
    
    语法分析就是根据抽象语法树上面的语法解释,类型、强制类型转换、ToNumber、ToString和ToPrometive等泛泛含义对表达式解构。
    
> 引擎执行

    词法分析和语法分析之后,浏览器就会将已经编译好的JS代码,交给引擎执行。
    
> LHS、RHS

 <p>词法作用域限定了变量和函数产生效果的范围,分为三种: 全局作用域、函数作用域以及块级作用域(ES6引入),为了更好的理解这三种作用域,以及其中变量和函数的定义与赋值,从概念上引入了LHS和RHS,用来解释引擎执行时,变量的赋值目标以及赋值操作的源头</p>
 
    LHS: 赋值操作的目标是谁
    RHS: 谁才是赋值操作的源头
    
 <b>例子</b>
 
    //定义foo函数为LHS;获取变量a为RHS;var b = 为LHS;获取变量a和b为RHS
    function foo(a) {
        var b = a;
        return a + b;
    }
    //var c = 为LHS;foo(10)为RHS;将实参10赋值给虚参a为LHS
    var c = foo(10);
    //console.log为RHS;获取变量c为RHS
    console.log(c);
    //五个表达式中,共有四个LHS和五个RHS
    
> 词法作用域链

  <p>简单来说,作用域链使内部作用域内的变量和函数变成了私密且不可访问的,保证了内部变量不会污染到全局以及外部作用域,以免造成变量名冲突等不可预知的错误,外部作用域是访问不到以及操作不到的,而内部作用域的优先级却是越来越高,可以访问和操作到自己以及外部N层作用域的变量和函数</p>
  
<b>例子</b>

    var a = "hello";
    function foo() {
        var b = "world";
        //foo函数作用域,可以访问到和操作到a,这里打印"hello"
        console.log(a);
        function bar() {
            var c = "wenkai.yin";
            //bar函数作用域,可以访问到和操作到c,b,a,这里打印"wenkai.yin" "world" "hello"
            console.log(c, b, a);
        }
        bar();
        //这里报错ReferrenceError c is not defined
        //因为foo函数作用域中访问不到和操作不到优先级最高的bar函数作用域中的私密变量c,
        //且在本作用域下找不到变量c,由此向外部作用域,也就是全局作用域中查找变量c,发现c并没有定义,更别说给c赋值了,
        //所以这时候会报ReferrenceError c is not defined
        console.log(c);
    }
    foo();
    
> 变量提升

<p>综上所述,变量和函数的定义是在浏览器编译器编译时,具体应该是在词法分析的词法解释时,就已经定义好了变量和函数的位置,之后的引擎执行才是进行赋值,由此会出现变量提升的情况</p>

<b>例子一</b>

    console.log(a);
    var a = 14;
    //这里打印的值为undefined,这里不会报错,因为变量a已经在浏览器编译中就定义了,执行顺序应该是:
    //var a;
    //console.log(a);
    //a = 14;
    
<b>例子二</b>

    a = 14;
    var a;
    console.log(a);
    //这里打印的值为14,执行顺序应该是:
    //var a;
    //a = 14;
    //console.log(a);

<b>例子三</b>

    console.log(a);
    let a = 14;
    //这里会直接报错ReferrenceError a is not defined
    //因为在ES6中let和const不会出现变量提升,let和const并不只是为了进行区分变量和常量才产生的
    //其核心是为了产生块级作用域,块级作用域也遵从词法作用域的规则以及作用域链,所以才不会出现变量提升
    //实际执行结果应该是:
    //console.log(a);
    //{
    //  let a = 14;
    //}
    //这时候全局作用域中是没办法访问和操作块级作用域中的变量a的,由此判断a未定义,才会报错ReferrenceError a is not defined

<b>例子四</b>

    if(a in window) {
        var a = 10;
    }
    console.log(a);
    //这里会直接打印:10
    //这里是存在变量提升的概念的,变量a的定义是在浏览器编译的词法分析的词法解释时,就已经确定了a的位置,所以变量在window对象中是存在的
    //实际浏览器引擎执行结果应该是:
    //var a;
    //if(a in window) {
    //      a = 10;
    //}
    //console.log(a);
    
> eval和with

<p>eval通过将字符串转换为Javascript语句和表达式,来改变某个词法作用域;with通过创造词法作用域,使得某个对象属性获得with词法作用域中变量的值</p>

<b>例子一</b>
    
    var b = "bigger"; 
    function foo(sentence) {
        eval(sentence);
        console.log(b);
    }
    foo("var b = 'smaller'");
    //这里打印smaller,本来foo的词法作用域中是不存在变量b的,而eval改变了foo的词法作用域,使得foo词法作用域中出现了变量b
    
<b>例子二</b>

    var obj = {a: "foo", b: "bar"};
    with(obj) {
        a = "bar";
        b = "foos";
    }
    console.log(obj);
    //这里打印{a: "bar, b: "foos"},with创造了词法作用域,使得其中的变量赋值操作是私密的,不可访问且不可操作的
    console.log(a);
    console.log(b);
    //变量a和b在全局作用域中都没有定义,只有在with创造的作用域下,进行赋值,
    //所以这里会报错:ReferrenceError a is not defined;ReferrenceError b is not defined
    
<p>eval由于对字符串词法和语法分析比较复杂,字符串中的变量和表达式会永久的保留在内存中的,不会被浏览器垃圾回收机制回收,会造成网站的性能较差的原因,被官方不推荐使用;而with由于也会造成网站性能变差,并且没有必要使用with改变对象属性值的原因,被官方列为禁用表达式语句</p>

> 作用域与闭包

<p>闭包跟作用域有着千丝万缕的联系,有时候你会不经意间使用到,但是却不知是闭包,其实你平时使用的好多场景都有闭包</p>

    闭包简单来说,可以解释为:A函数里面定义了一个B函数,B函数在非A函数作用域下执行,在A函数释放的情况下,仍能访问和操作A函数作用域下的变量和函数
    
<p>这就是闭包,在业务开发过程中,我们会遇到很多此类示例</p>

<b>例子一</b>

    function foo() {
        var name = "wenkai.yin";
        setTimeout(function time() {
            console.log(name);
            name = "Gary";
            console.log(name);
        }, 1000);
    }    
    foo();
    //在这里打印: 
    //wenkai.yin
    //Gary
    //这就是一个闭包示例,名为time的函数在foo函数作用域下定义,在foo函数调用释放之后,在setTimeout这个函数作用域下执行,仍能访问和操作到foo函数作用域下的变量name,这就形成了一个闭包,变量name,明明应该随着foo函数的调用释放被销毁,但是却没有,在内存中获得保留,形成一块儿闭包区域
    
<b>例子二</b>

    function foo() {
        var name = "world";
        function bar() {
            console.log(name);
            name = "hello";
            console.log(name);
        }
        return bar;
    }
    foo()();
    //这里打印:
    //world
    //hello
    //在这里bar函数是在foo函数词法作用域下定义的,但是在foo函数调用释放之后,bar函数在全局作用域下还是能够访问和操作foo函数作用域下的本应被销毁掉的变量name,说明这时候变量name并没有在内存中显示,反而保留了下来,形成了一块儿闭包区域

<b>例子三</b>

    function deep() {
        for(var i = 0; i < 10; i++) {
            setTimeout(function time() {
                console.log(i);
            }, i * 1000);
        }
    }
    deep();
    //在这里会打印: 10个10
    //由于延时器异步的关系,当浏览器引擎遇到异步代码时,会先把异步代码放到异步队列中,先执行同步代码,等待到同步代码执行完毕之后,再去轮询异步队列中的异步代码,而这时候for循环已经结束,i的值为10,所以打印了10个10
    //当然里面也存在闭包,例子一中已经说明
    
    //修复异步问题,使用闭包方法:
    function deep() {
        for(var i = 0; i < 10; i++) {
            setTimeout((function time(i) {
                var j = i;
                return function () {
                    console.log(j);
                }
            })(i), i * 1000);
        }
    }
    deep();
    //在这里会打印: 0-9十个数字
    //j是time函数词法作用域下的变量,而for循环中的变量i通过参数的方式传入time IIFE自执行函数表达式,
    //这时time函数词法作用域下返回一个匿名函数,且不在time函数词法作用域下而是在setTimeout函数作用域下执行,这时候形成了十个闭包,内存中保留了time函数释放之后的内部的i和j变量,形成了十个闭包区域
    
    //修复异步问题,使用let关键字:
    function deep() {
        for(let i = 0; i < 10; i++) {
            setTimeout(function time() {
                console.log(i);
            }, i * 1000);
        }
    }
    deep();
    //在这里会打印: 0-9十个数字
    //实际上在这里每一次循环都会形成一个块级作用域,块级作用域下定义的time函数,
    //而time函数在setTimeout函数词法作用域下执行,仍然可以获取到块级作用域下的变量i,这时的变量i是保留在内存当中的,形成了类似于闭包的十个块级作用域闭包区域
    
> IIFE自执行函数表达式

<p>IIFE自执行函数表达式的出现本质上是为了防止变量名称冲突,避免污染全局变量,利用函数词法作用域,做了一处自动执行的私密装置</p>

<b>例子</b>
    
    var name = "global";
    (function IIFE(global) {
        var name = "IIFE";
        console.log(name, global.name);
    })(window);
    console.log(name);
    //在这里打印: IIFE global
    //global
    //体现了全局作用域下的变量name和IIFE函数词法作用域下的变量name的不同含义,且IIFE函数词法作用域下的变量不会造成全局变量的污染,不会造成命名冲突,是私密的。
    
    //还有一种自执行函数表达式的写法
    var name = "global";
    (function IIFE(fn) {
        fn(window);
    })(function foo(global) {
        var name = "IIFE";
        console.log(name, global.name);
    });
    console.log(name);
    //在这里打印: IIFE global
    //global
    //同上含义,只不过传入的参数方式不同,一种是传递window参数,一种是直接传递函数
    
> try...catch...模拟块级作用域
 
 <p>早在ES6 let和const关键字出现之前,就已经有团队和公司在开始模拟块级作用域了,其中Google公司的Tracer解析编译工具在编译和模拟块级作用域时,编译出来的ES5代码,就是使用了try{} catch() {}这种方式</p>
 
<b>例子</b>

    try {
        throw undefined;
    } catch(a) {
        b = 12;
        console.log(b);
    }
    console.log(b);
    //在这里打印:
    //12
    //ReferrenceError:b is not defined
    //这种机制在ES3中就早已经出现了
    
## 二、this动态作用域

<p>this动态作用域是公认的js闭包之外的第二个难点,有很多人不明白this所指代的是什么,是对象?词法作用域?还是上下文?其实都不是,让我们来一起揭开this的面纱</p>

> this是什么

    this实际上是函数对象调用执行时所处的上下文对象(这里的上下文对象指的并不是作用域)
    
> this指向分类

    this指向的分类一共有四种: 
    1. 普通函数调用执行,默认指向window
    2. 使用对象调用执行,软绑定指向该对象
    3. 使用apply、call或者bind绑定在某个对象上执行,硬绑定指向该对象
    4. 使用new语法糖构造器调用执行,new绑定指向函数对象本身
    
<b>例子一</b>
    
    var a = 99;
    function foo() {
        console.log(this.a);
    }     
    foo();
    //在这里打印:
    //99
    //由于是普通调用在全局作用域下执行,此时的this指向的是window,
    //由此console.log(window.a),打印的是99
    
<b>例子二</b>

    var $a = 'world';
    var $obj = {
        $a: '9hello9',
        b() {
            console.log(this.$a);
        }
    };
    $obj.b();
    //在这里打印:
    //9hello9
    //由于是使用对象调用执行,软绑定this指向该对象
    //由此console.log($obj.a),打印的是9hello9
    
<b>例子三</b>

    var $a = '6world6';
    var $obj = {
        $a: '9hello9',
        b() {
            console.log(this.$a);
        }
    };
    var $_obj = {
        $a: '7fast7'
    };
    $obj.b.apply($_obj);
    $obj.b.call($_obj);
    //在这里打印:
    //7fast7
    //7fast7
    //由于是使用apply、call或者bind绑定在某个对象上调用执行,硬绑定this指向该对象
    //由此console.log($_obj.$a),打印的是7fast7
    
<b>例子四</b>

    var $a = '6world6';
    function Fo($a) {
        this.$a = $a;
    }
    var $fo = new Fo('9hello9');
    console.log($fo.$a);
    //在这里打印:
    //9hello9
    //由于是使用new语法糖构造器调用执行,new绑定指向函数对象本身
    //由此console.log($fo.$a),打印的是9hello9
    
> this指向优先级

    this默认绑定 < 对象软绑定 < apply、call和bind硬绑定 < new绑定
    
<b>对比对象软绑定和apply、call以及bind硬绑定的优先级</b>

    function bar() {
        console.log(this.$a);
    }
    var $obj = {
        $a: "5we5",
        bar: bar
    };
    var $_obj = {
        $a: "6happy6"
    };
    $obj.bar.apply($_obj);
    $obj.bar.call($_obj);
    //在这里打印:
    //6happy6
    //6happy6
    //由此可见,apply、call以及bind硬绑定的优先级大于对象软绑定
    
<b>对比对象软绑定和new绑定的优先级</b>

    function bar() {
        console.log(this.$a);
    }
    var $obj = {
        $a: "4snake4",
        bar: bar
    };
    var $result = new $obj.bar();
    //在这里打印:
    //undefined
    //由此可见,new绑定的优先级大于对象软绑定
    
<p>对比apply、call以及bind硬绑定和new绑定的优先级,由于apply/call和new不能同时使用,所以我们演示就使用bind硬绑定与new绑定进行优先级比较</p>

    function Fo($a) {
        this.$a = $a;
    }
    var bar = {
        $a: "8money8"
    };
    var fBind = Fo.bind(bar);
    var _bind = new fBind("3sheep3");
    console.log(_bind.$a);
    //在这里打印:
    //3sheep3
    //由此可见,new绑定的优先级大于apply、call以及bind硬绑定

> polyfill兼容模拟bind硬绑定
    
    if(!Function.prototype.bind) {
        Function.prototype.bind = function (context) {
            if(typeof this !== "function") {
                throw new TypeError("被绑定的对象并不是函数对象!");
            }
            let self = this,
                args = Array.from(arguments),
                fBind;
            args.shift();    
            function F() {}
            fBind = function () {
                let innerArgs = Array.from(arguments);
                return self.apply(this instanceof fBind ? this : context, [...args, ...innerArgs]);
            };
            F.prototype = self.prototype;
            fBind.prototype = new F();
            return fBind;
        };
    }
    //polyfill兼容模拟bind硬绑定大概上就是如此
    //测试硬绑定,非new绑定模式
    function Person(name, age) {
        this.name = name;
        this.age = age;
    }
    var $obj = {
        name: "Gary",
        age: 26
    };
    var $_obj = Person.bind($obj);
    var $obj_ano = {
        name: "Clay yin",
        age: 29,
        $_obj
    };
    var $obj_empty = {};
    $_obj("wenkai.yin", 27);
    console.log($obj.name, $obj.age);
    $obj_ano.$_obj("yin.wenkai", 25);
    console.log($obj.name, $obj.age);
    console.log($obj_ano.name, $obj_ano.age);
    $_obj.apply($obj_empty, ["Gary Yin", 24]);
    console.log($obj_empty.name, $obj_empty.age);
    console.log($obj.name, $obj.age);
    //在这里打印:
    //wenkai.yin 27
    //yin.wenkai 25
    //Clay yin 29
    //undefined undefined
    //Gary Yin 24
    
    //测试硬绑定,new绑定模式
    function Person(name, age) {
        this.name = name;
        this.age = age;
    }
    Person.prototype.introduce = function () {
        console.log(`hello, I'm ${this.name}, ${this.age} year's old`);
    };
    var obj = {
        name: "Gary Yin",
        age: 24
    };
    var fBind = Person.bind(obj);
    var person = new fBind("wenkai.yin", 26);
    console.log(person.name, person.age);
    person.introduce();
    console.log(obj.name, obj.age);
    //在这里打印:
    //wenkai.yin 26
    //hello, I'm wenkai.yin, 24 year's old
    //Gary Yin 24
    
> polyfill兼容模拟softBind软绑定
    
    Function.prototype.softBind = function (context) {
        if(typeof this !== "function") {
            throw new TypeError("被绑定的对象并不是函数对象!");
        }
        var self = this,
            args = Array.from(arguments),
            fBind;
        args.shift();    
        function F() {}
        fBind = function () {
            var innerArgs = Array.from(arguments);
            return self.apply((!this || this === window) ? context : this, [...args, ...innerArgs]);
        };
        F.prototype = self.prototype;
        fBind.prototype = new F();
        return fBind;
    };
    
    //polyfill兼容模拟softBind软绑定大概上就是如此
    //测试软绑定,非new绑定模式
    function Person(name, age) {
        this.name = name;
        this.age = age;
    }
    var $obj = {
        name: "Gary",
        age: 26
    };
    var $_obj = Person.softBind($obj);
    $_obj("wenkai.yin", 27);
    console.log($obj.name, $obj.age);
    var $obj_ano = {
        name: "Clay yin",
        age: 29,
        $_obj
    };
    var $obj_empty = {};
    $obj_ano.$_obj("Gary Yin", 28);
    console.log($obj_ano.name, $obj_ano.age);
    console.log($obj.name, $obj.age);
    $_obj.apply($obj_empty, ["yin.wenkai", 24]);
    console.log($obj_empty.name, $obj_empty.age);
    console.log($obj.name, $obj.age);
    //在这里打印:
    //wenkai.yin 27
    //Gary Yin 28
    //wenkai.yin 27
    //yin.wenkai 24
    //wenkai.yin 27
    
    //测试软绑定,new绑定模式
    function Person(name, age) {
        this.name = name;
        this.age = age;
    }
    Person.prototype.introduce = function () {
        console.log(`hello, I'm ${this.name}, ${this.age} year's old`);
    };
    var $obj = {
        name: "Clay yin",
        age: 29
    };
    var $_obj = Person.bind($obj);
    var person = new Person("Gary_yin", 22);
    console.log(person.name, person.age);
    person.introduce();
    console.log($obj.name, $obj.age);
    //在这里打印:
    //Gary_yin 22
    //hello, I'm Gary_yin, 22 year's old
    //Clay yin 29
    
> polyfill兼容模拟new绑定
    
    function _new() {
        var args = Array.from(arguments),
            Collapse = args.shift(),
            _obj = {};
        _obj.__proto__ = Collapse.prototype;
        var target = Collapse.apply(_obj, args);
        return typeof target === "object" ? target : _obj;
    }
    //测试模拟new绑定
    function Person(name, age) {
        this.name = name;
        this.age = age;
    }
    Person.prototype.introduce = function() {
        console.log(`hello, I'm ${this.name}, ${this.age} year's old`);
    };
    var person = _new(Person, "Gary", 26);
    console.log(person.name, person.age);
    person.introduce();
    console.log(Object.getPrototypeOf(person) === Person.prototype);
    console.log(Person.prototype.isPrototypeOf(person));
    //在这里打印:
    //Gary 26
    //hello, I'm Gary, 26 year's old
    //true
    //true
    
> 注意点

<p>this与函数调用执行的位置的上下文对象息息相关,有时候千万不要被一些障眼法蒙蔽</p>
    
<b>例子一</b>
    
    var name = "Gary Yin";
    function bar() {
        console.log(this.name);
    }
    var obj = {
        name: "wenkai.yin",
        bar
    };
    var _bar = obj.bar;
    _bar();
    //在这里打印:
    //Gary Yin
    //此时bar函数调用执行位置的上下文对象,并不是对象软绑定,而是全局对象window
    
<b>例子二</b>

    function say() {
        console.log(this.name);
    }
    var obj = {
        name: "obj_one"
    };
    var objTwo = {
        name: "obj_two"
    };
    var objThree = {
        name: "obj_three"
    };
    var foo = say.bind(obj).bind(objTwo).bind(objThree);
    foo();
    //在这里打印:
    //obj_one
    //此时say函数调用执行this只硬绑定指向了一层上下文对象,那就是obj,剩下的两层硬绑定,都是bind硬绑定内部返回的函数对象fBind进行的,与say函数没有任何关系
    
<b>例子三</b>

    function Person(name, age) {
        this.name = name;
        this.age = age;
    }
    Person.prototype.introduce = function() {
        console.log(`hello, I'm ${this.name}, ${this.age} year's old`);
    };
    var $obj = {
        name: "Gary",
        age: 26
    };
    var fBind = Person.bind($obj);
    var person = new fBind("wenkai.yin", 28);
    console.log(person.name, person.age);
    person.introduce();
    console.log($obj.name, $obj.age);
    //在这里打印:
    //wenkai.yn 28
    //hello, I'm wenkai.yin, 28 year's old
    //Gary 26
    //根据polyfill兼容模拟的bind,我们可以看出,当this指向其构造器fBind时,也就是new返回的函数,进行构造调用时,外部绑定的函数对象的this就不会指向绑定的对象,而是会指向构造器fBind,所以引用对象person委托关联指向fBind,并通过原型链指向Person。
    //于是,名称和年龄是外部参数wenkai.yin和28,可以调用执行原型链上面的函数introduce,而$obj对象上面的属性值并没有发生任何改变
    
## 三、原型链

<p>原型链,从本质上来讲,就是引用对象与普通对象、引用对象与函数对象之间委托关联,当建立起委托关联后,引用对象本身的隐式原型__proto__与构造函数的显式原型prototype就会形成引用关系,使得引用对象不仅可以调用本身被显式绑定的属性值,也可以追本溯源的通过原型链调用构造函数原型链上面的属性和函数方法。</p>

> 伪继承

<p>继承在传统面向对象的语言中是子类直接复制父类的属性和方法,复制后,子类上是直接存在其父类的属性和方法的,但是在JS中,继承并不是复制,而是委托关联,通过原型链向父级搜索查找,直至继承树的顶端Object.prototype也就是Object对象的显式原型。</p>

<b>例子一</b>

    function Person(name, age) {
        this.name = name;
        this.age = age;
    }
    Person.prototype.introduce = function () {
        console.log(`hello, I'm ${this.name}, ${this.age} year's old`);
    };
    function Gary(name, age, hobby) {
        Person.call(this, name, age);
        this.hobby = hobby;
    }
    //以下三行就是JS伪继承委托关联的精髓s
    //将子类的显式原型的隐式原型指向父类的显式原型
    function F() {}
    F.prototype = Person.prototype;
    Gary.prototype = new F();
    
    Gary.prototype.hobbyMine = function () {
        console.log(`${this.name}, I love ${this.hobby}`);
    };
    var gary = new Gary("wenkai.yin", 26, "program");
    console.log(gary.name, gary.age, gary.hobby);
    gary.introduce();
    gary.hobbyMine();
    //在这里打印:
    //wenkai.yin 26 program
    //hello, I'm wenkai.yin, 26 year's old
    //wenka.yin, I love program
    
<b>例子二</b>
    
    //还是同样剧情的例子,不过这一次我们要换一下继承方式
    //并且深究一下内部的委托关联原型链
    function Person(name, age) {
        this.name = name;
        this.age = age;
    }
    Person.prototype.introduce = function () {
        console.log(`hello, I'm ${this.name}, ${this.age} year's old`);
    };
    function Gary(name, age, hobby) {
        Person.call(this, name, age);
        this.hobby = hobby;
    }
    //以下三行就是JS伪继承委托关联的精髓
    //将子类的显式原型的隐式原型指向父类的显式原型
    Gary.prototype = Object.create(Person.prototype);
    
    Gary.prototype.hobbyMine = function () {
        console.log(`${this.name}, I love ${this.hobby}`);
    };
    var gary = new Gary("wenkai.yin", 26, "program");
    console.log(gary.name, gary.age, gary.hobby);
    gary.introduce();
    gary.hobbyMine();
    console.log(gary.__proto__ === Gary.prototype);
    console.log(Gary.prototype.__proto__ === Person.prototype);
    console.log(Object.getPrototypeOf(gary) === Gary.prototype);
    console.log(Object.getPrototypeOf(Object.getPrototypeOf(gary)) === Person.prototype);
    console.log(Gary.prototype.isPrototypeOf(gary));
    console.log(Person.prototype.isPrototypeOf(Gary.prototype));
    //在这里打印:
    //wenkai.yin 26 program
    //hello, I'm wenkai.yin, 26 year's old
    //wenkai.yin, I love program
    //true
    //true
    //true
    //true
    //true
    //true
    //这里使用了两个方法,isPrototypeOf和getPrototypeOf。
    //a.isPrototypeOf(b)是判断b是否是在a的原型链上,可以用于检查引用对象和其他任意对象之间的委托关联关系
    //Object.getPrototypeOf(b) === a与b.__proto__ === a的效果相同的,Object.getPrototypeOf(b)也只不过是提取了b对象中的隐式原型与a对象或者a函数对象的显式原型进行比对。
    
> polyfill兼容模拟Object.create方法

<p>从polyfill兼容模拟Object.create方法的源代码来看,利用的是原型链的机制,将子类与父类或者说是子对象与父对象委托关联起来。使用Object.create的优势,首先,不需要再去考虑委托关联构造调用时的参数问题,使用第三函数对象,也就是F函数中转承接;第二,适用于引用对象与任意对象(普通对象、函数对象)之间的委托关联。</p>

    if(!Object.create) {
        Object.create = function(o) {
            function F() {}
            F.prototype = o;
            return new F();
        };
    }
    
<b>例子一</b>

    var a = {
    };
    var b = {
        age: "b"
    };
    a = Object.create(b);
    console.log(a.age);
    //在这里打印:
    //b

<b>例子二</b>

    function Person(name, age) {
        this.name = name;
        this.age = age;
    }
    Person.prototype.introduce = function () {
        console.log(`hello, I'm ${this.name}, ${this.age} year's old`);
    };
    function Gary(name, age, hobby) {
        Person.call(this, name, age);
        this.hobby = hobby;
    }
    //以下三行就是JS伪继承委托关联的精髓
    //将子类的显式原型的隐式原型指向父类的显式原型
    Gary.prototype = Object.create(Person.prototype);
    
    Gary.prototype.hobbyMine = function () {
        console.log(`${this.name}, I love ${this.hobby}`);
    };
    var gary = new Gary("wenkai.yin", 26, "program");
    console.log(gary.name, gary.age, gary.hobby);
    gary.introduce();
    gary.hobbyMine();
    //在这里打印:
    //wenka.yin 26 program
    //hello, I'm wenkai.yin, 26 year's old
    //wenkai.yin, I love program
    
> 注意点
<p>instanceof通常是检查引用对象是否在某一个函数对象的原型链上,不过也只是作用于引用对象和函数对象之间,并不能检查引用对象和普通对象之间的委托关联关系</p>

<b>例子一</b>

    function Person(name, age) {
        this.name = name;
        this.age = age;
    }
    var gary = new Person("wenkai.yin", 26);
    console.log(gary instanceof Person);
    console.log(gary instanceof Object);
    //在这里打印:
    //true
    //true
    
<b>例子二</b>

    var a = {
        name: "Gary",
        age: 26
    };
    var b = {
        name: "wenkai.yin",
        age: 28
    };
    a = Object.create(b);
    console.log(Object.getPrototypeOf(a) === b);
    console.log(b.isPrototypeOf(a));
    //在这里打印:
    //true
    //true
    //当遇到检查引用对象和普通对象之间的委托关联,判断引用对象是否在普通对象的原型链上时,
    //就不能使用instanceof,我们这里使用的是isPrototypeOf,b.isPrototypeOf(a)
    
<p>原型链的顶部,也就是Object.prototype,Object对象的显式原型,那按照原型链的规则来看,原型链的顶部Object对象的显式原型的隐式原型指向哪儿呢? 答案是null</p>

    function Person(name, age) {
        this.name = name;
        this.age = age;
    }
    var gary = new Person("wenkai.yin", 26);
    console.log(Object.getPrototypeOf(gary) === Person.prototype);
    console.log(Object.getPrototypeOf(Person.prototype) === Object.prototype);
    console.log(Object.getPrototypeOf(Object.prototype) === null);
    console.log(Person.prototype.isPrototypeOf(gary));
    console.log(Object.prototype.isPrototypeOf(Person.prototype));
    //在这里打印:
    //true
    //true
    //true
    //true
    //true
    
## 四、对象
    
<p>定义对象有两种方式,一种是构造调用进行定义,还有一种是使用字面量语法糖的形式定义。</p>

<b>例子一</b>

    var obj = new Object();
    obj.name = "Gary";
    obj.age = 24;
    console.log(obj);
    //在这里打印:
    //Object {name: "Gary", age: 24}
    //使用构造调用定义,添加属性或者方法,必须使用.或者[字符串]的形式,一行一行添加,非常繁琐
    
<b>例子二</b>

    var obj = {
        name: "Gary Yin",
        age: 26
    };
    console.log(obj);
    //在这里打印:
    //Object {name: "Gary Yin", age: 26}
    //使用字面量语法糖定义,批量添加属性或者方法,一般定义对象,基本都这样使用
    
> 添加或者修改对象属性或者方法

<b>例子一</b>

    var obj = {
        name: "Gary Yin",
        age: 26
    }; 
    obj.name = "wenkai.yin";
    obj.hobby = "basketball";
    obj.sexy = "men";
    console.log(obj);
    //在这里打印:
    //Object {name: "wenkai.yin", age: 26, hobby: "basketball", sexy: "men"}
    //这种.形式添加或者修改对象属性或者方法,弊端在于属性名或者方法名,必须遵守定义变量名称的规则
    //也就是必须以字母、下划线或者$符号开头,且属性名称或者方法名称只允许使用数字、字母、下划线和$符号
    
<b>例子二</b>

    var obj = {
        name: "Gary Yin",
        age: 26
    }; 
    obj["name"] = "wenkai.yin";
    obj["1hobby"] = "basketball";
    obj["sexy"] = "men";
    obj["@#$%"] = "@#$%";
    console.log(obj);
    //在这里打印:
    //Object {name: "wenkai.yin", age: 26, 1hobby: "basketball", sexy: "men", @#$%: "@#$%"}
    //这种[字符串]形式添加或者修改对象属性或者方法,属性名或者方法名可以使用任意的字符串进行定义,没有任何的限制,兼容所有的字符串(包括汉字)
    
<b>例子三</b>

    var obj = {
    };
    Object.defineProperty(obj, "name", {
        value: "wenkai.yin",
        writable: true,
        enumerable: true,
        configurable: true
    });
    console.log(obj);
    //在这里打印:
    //Object {name: "wenkai.yin"}
    
    Object.defineProperties(obj, {
        age: {
            value: 26,
            writable: true,
            enumerable: true,
            configurable: true
        },
        hobby: {
            value: "program",
            writable: true,
            enumerable: true,
            configurable: true
        }
    });
    console.log(obj);
    //在这里打印:
    //Object {name: "wenkai.yin", age: 26, hobby: "program"}
    //defineProperty和defineProperties是添加和修改配置对象属性方法最细致的两种方式,defineProperty只能添加和修改一项属性和方法,而defineProperties可以批量添加和修改属性和方法
    
> 获取对象属性和方法的配置信息

<b>例子一</b>

    var obj = {
        name: "wenkai.yin",
        age: 26,
        hobby: "program"
    };
    console.log(Object.getOwnPropertyDescriptors(obj));
    //在这里打印:
    //{
    //      name: {
    //          configurable: true,
    //          enumerable: true,
    //          value: "wenkai.yin",
    //          writable: true
    //      },
    //      age: {
    //          configurable: true,
    //          enumerable: true,
    //          value: 26,
    //          writable: true
    //      },
    //      hobby: {
    //          configurable: true,
    //          enumerable: true,
    //          value: "program",
    //          writable: true
    //      }
    //}
    //批量获取对象属性和方法的配置信息
    
    console.log(Object.getOwnPropertyDescriptor(obj, "age"));
    //在这里打印:
    //{
    //      configurable: true,
    //      enumerable: true,
    //      value: 26,
    //      writable: true
    //}
    //获取对象单个属性或者方法的配置信息
    
<p>获取对象的属性和方法的配置信息后,将要解释一下这些配置信息的作用,value就是属性值,writable是用来控制属性或者方法是否可修改值的开关,configurable是用来控制属性或者方法是否可配置、可添加以及可删除,enumerable是用来控制属性或者方法是否可枚举</p>

<b>例子一</b>

    var obj = {
        name: "Gary"
    };
    Object.defineProperties(obj, {
        age: {
            value: 26,
            enumerable: false,
            writable: true,
            configurable: true
        },
        hobby: {
            value: "program",
            enumerable: true,
            writable: true,
            configurable: true
        }
    });
    for(var key in obj) {
        console.log(key);
    }
    //在这里打印:
    //name
    //program
    //属性的enumerable可枚举如果为false,遍历对象的属性名称,就不会出现
    for(let key of Object.keys(obj)) {
        console.log(key);
    }
    //在这里打印:
    //name
    //program
    //属性的enumerable可枚举如果为false,遍历对象的属性名称,就不会出现
    console.log(Object.getOwnPropertyNames(obj));
    //在这里打印:
    //["name", "age", program"]
    console.log(obj.hasOwnProperty("age"));
    //在这里打印:
    //true
    console.log(Reflect.ownKeys(obj));
    //在这里打印:
    //["name", "age", "program"]
    //由此可得出结论,除了for...in、Object.keys(obj)、Object.values(obj)和Object.entries(obj)受控制是否可枚举的属性enumerable影响之外,其他方式都可以获取到控制是否可枚举属性enumerable为false的属性名称
    //for...in、Object.keys(obj)、Object.values(obj)和Object.entries(obj)还是能获取原型链上的属性和方法的遍历方式
    
<b>例子二</b>

    var obj = {
        name: "Gary"
    };
    Object.defineProperties(obj, {
        age: {
            value: 26,
            enumerable: true,
            writable: true,
            configurable: true
        },
        hobby: {
            value: "program",
            enumerable: true,
            writable: false,
            configurable: true
        }
    });
    obj.name = "wenkai.yin";
    obj.hobby = "basketball";
    console.log(obj);
    //Object {name: "wenkai.yin", age: 26, hobby: "program"}
    //当设置了控制属性值是否可修改的writable为false时,属性值便不可被改变
    //且当writable设置为false时,不可被再次设置为true
    Object.defineProperty(obj, "hobby", {
        value: "program",
        writable: true,
        configurable: true,
        enumerable: true
    });
    //在这里打印:
    //直接报错,property can not redefine: hobby
    
<b>例子三</b>

    var obj = {
        name: "Gary"
    };
    Object.defineProperties(obj, {
        age: {
            value: 26,
            enumerable: true,
            writable: true,
            configurable: true
        },
        hobby: {
            value: "program",
            enumerable: true,
            writable: true,
            configurable: false
        }
    });
    delete obj.age;
    delete obj.program;
    console.log(obj);
    //在这里打印:
    //Object {name: "Gary", hobby: "program"}
    Object.defineProperty(obj, "hobby", {
        value: "basketball",
        writable: true,
        enumerable: true,
        configurable: true
    });
    //在这里打印:
    //直接报错,property can not redefine: hobby
    
<b>例子四</b>

    var obj = {
        name: "Gary",
        age: 26,
        hobby: "basketball"
    };
    Object.preventExtensions(obj);
    obj.sexy = "men";
    obj.hobby = "program";
    console.log(obj);
    //在这里打印:
    //Object {name: "Gary", age: 26, hobby: "program"}
    //preventExtensions方法使得obj对象不可添加新的属性
    
<b>例子五</b>

    var obj = {
        name: "Gary",
        age: 26,
        hobby: "basketball"
    };
    Object.seal(obj);
    obj.sexy = "men";
    obj.hobby = "program"
    delete obj.age;
    delete obj.name;
    console.log(obj);
    //在这里打印:
    //Object {name: "Gary", age: 26, hobby: "program"}
    for(var key in obj) {
        console.log(key);
    }
    //在这里打印:
    //name
    //age
    //program
    Object.defineProperty(obj, "name", {
        value: "wenkai.yin",
        configurable: true,
        writable: true,
        enumerable: true
    });
    console.log(obj);
    //在这里打印:
    //直接报错: property can not redefine: name
    //由此可以得出结论: seal方法使得obj对象所有属性不可配置对象属性和方法信息、不可删除对象属性,且不可添加对象属性,但是属性名称还是可以枚举的,原属性值还是可以修改的,也就是说seal方法使得obj对象所有属性的configurable置为false,所有属性的writable和enumerable还是维持原来的状态
    
<b>例子六</b>

    var obj = {
        name: "Gary",
        age: 26,
        hobby: "basketball"
    };
    Object.freeze(obj);
    obj.sexy = "men";
    obj.hobby = "program"
    delete obj.age;
    delete obj.name;
    console.log(obj);
    //在这里打印:
    //Object {name: "Gary", age: 26, hobby: "basketball"}
    for(var key in obj) {
        console.log(key);
    }
    //在这里打印
    //name
    //age
    //hobby
    Object.defineProperty(obj, "name", {
        value: "wenkai.yin",
        configurable: true,
        writable: true,
        enumerable: true
    });
    console.log(obj);
    //在这里打印:
    //直接报错: property can not redefine: name
    //由此可以得出结论: freeze方法使得obj对象不可配置对象属性和方法信息、不可删除对象属性、不可添加对象属性,且不可修改对象属性值,但是属性名称还是可以枚举的,也就是说freeze方法使得obj对象所有属性的configurable和writable置为false,所有属性的enumerable还是维持原来的状态
    
> 对象遍历

<p>ES6语法中,新增了keys、values、entries和Reflect.OwnKeys遍历对象的函数方法,当然你也可以直接使用ES5语法中的for...in、getOwnPropertyNames等形式对对象进行遍历,还有一种使用迭代器(Symbol.iterator)的方式,这种方式需要开发者手写对象的Symbol.iterator迭代器方法,并不常见</p>

<b>例子一</b>

    var obj = {
        name: "wenkai.yin",
        age: 26,
        hobby: "basketball"
    };
    for(let key of Object.keys(obj)) {
        console.log(key);
    }
    //在这里打印:
    //name
    //age
    //hobby
    
    for(let value of Object.values(obj)) {
        console.log(value);
    }
    //在这里打印:
    //wenkai.yin
    //26
    //basketball
    
    for(let [key, value] of Object.entries(obj)) {
        console.log(key, value);
    }
    //在这里打印:
    //name wenkai.yin
    //age 26
    //hobby basketball
    
    for(let key in obj) {
        console.log(key);
    }
    //在这里打印:
    //name
    //age
    //hobby
    
<b>例子二</b>

    var obj = {
        name: "wenkai.yin",
        age: 26,
        hobby: "basketball"
    };
    var objNames = Object.getOwnPropertyNames(obj);
    for(let val of objNames) {
        console.log(val);
    }
    //在这里打印:
    //name
    //age
    //hobby
    var objOwnKeys = Reflect.ownKeys(obj);
    for(let val of objOwnKeys) {
        console.log(val);
    }
    //在这里打印:
    //name
    //age
    //hobby
    
<b>例子三</b>

    var obj = {
        name: "wenkai.yin",
        age: 26,
        hobby: "basketball",
        [Symbol.iterator]() {
            var self = this,
                index = 0,
                objArr = Object.keys(self),
                length = objArr.length;
            return {
                next() {
                    return {
                        value: self[objArr[index++]],
                        done: index > length
                    };
                }
            };
        }
    };
    for(let val of obj) {
        console.log(val);
    }
    //在这里打印:
    //wenkai.yin
    //26
    //basketball

## 笔试训练    
    
<p>自此你不知道的Javascript<上篇>整理: 词法作用域、this以及原型对象重点都已经划完了,下面我们会进入上篇的笔试训练阶段。</p>

<b><em>笔试一</em></b>

    var a = 20;
    var foo = {
        a: 10,
        getA: function () {
            return this.a;
        }
    };  
    var _getA = foo.getA;
    console.log(_getA());
    //在这里打印:
    //20
    
<b><em>笔试二</em></b>

    var timer1 = (cb, time) => {
        (function loop() {
            cb();
            setTimeout(loop, time);
        })();
    };
    var timer2 = (cb, time) => {
        cb();
        setInterval(cb, time);
    };
    //1.timer1和timer2实现了什么功能,执行结果上会有什么区别?
    //回答: timer1和timer2实现了隔时轮询的功能,从执行结果上来看并没有任何的区别
    //2.模拟requestAnimationFrame方法的话应该参照哪种实现?
    //回答: 应该参照第一种timer1的实现方法
    //3.timer1中调换cb()和setTimeout的先后顺序会有什么影响?
    //回答: 并不会有什么影响,由于JS语言是单线程语言,所以同一时间只能做同一件事,它会先执行同步代码,当遇到异步代码时,会先把异步代码放进异步队列中,等待同步代码执行完毕之后,再轮询异步队列中的异步代码,由此不会有任何的影响
    
<b><em>笔试三</em></b>

    var a = 1;
    function f() {
        console.log(a);
        var = 2;
    }
    f();
    //在这里打印:
    //undefined
    
<b><em>笔试四</em></b>

    f();
    g();
    function f() {
        console.log('f');
    }      
    var g = function() {
        console.log('g');
    };
    //在这里打印:
    //f
    //TypeError: g is not a function
    
<b><em>笔试五</em></b>

    var person = {
        name: "Messi"
    };
    console.log(person.hasOwnProperty("name"));
    console.log(person.hasOwnProperty("hasOwnProperty"));
    console.log(Object.prototype.hasOwnProperty("hasOwnProperty"));
    //在这里打印:
    //true
    //false
    //true
    
<b><em>笔试六</em></b>

    function person(pname, page) {
        this.name = pname;
        this.age = page;
    }
    person.prototype.profession = "football player";
    var person1 = new person("Messi", 29);
    var person2 = new person("Bale", 28);
    console.log(person1.hasOwnProperty("name"));
    console.log(person1.hasOwnProperty("hasOwnProperty"));
    console.log(person1.__proto__ === person.prototype);
    console.log(person.prototype.hasOwnProperty("hasOwnProperty"));
    console.log(person1.__proto__.__proto__ === person.prototype.__proto__);
    console.log(person.prototype.__proto__.hasOwnProperty("hasOwnProperty"));
    //在这里打印:
    //true
    //false
    //true
    //false
    //true
    //true
    
<b><em>笔试七</em></b>

    function shallowClone(o) {
        const obj = {};
        for(let i in o) {
            obj[i] = o[i];
        }
        return obj;
    }    
    const oldObj = {
        a: 1,
        b: ['e', 'f', 'g'],
        c: {h: {i: 2}}
    };
    const newObj = shallowClone(oldObj);
    console.log(newObj.c.h, oldObj.c.h);
    console.log(newObj.c.h === oldObj.c.h);
    newObj.c.h = "change";
    console.log(newObj.c.h, oldObj.c.h);
    //在这里打印:
    //{i: 2} {i: 2}
    //true
    //'change' 'change'
 
> 自此你不知道的Javascript<上篇>整理: 词法作用域、this以及原型对象整理结束

# <花絮>整理polyfill兼容模拟的函数方法以及元素视图盒模型

## polyfill兼容模拟的函数方法

> polyfill兼容模拟new绑定

    function _new() {
        var obj = {},
            args = Array.from(arguments),
            Collapse = args.shift();
        obj.__proto__ = Collapse.prototype;
        var target = Collapse.apply(obj, args);
        return typeof target === "object" ? target : obj;
    }
    function Person(name, age) {
        this.name = name;
        this.age = age;
    }    
    Person.prototype.introduce = function() {
        console.log(`I'm ${this.name}, ${this.age} year's old`);
    };
    var person = _new(Person, "wenkai.yin", 26);
    console.log(person.name, person.age);
    person.introduce();
    //在这里打印:
    //wenkai.yin 26
    //I'm wenkai.yin, 26 year's old
    
> polyfill兼容模拟bind硬绑定
    
    if(!Function.prototype.bind) {
        Function.prototype.bind = function(context) {
            if(typeof this !== "function") {
                throw new TypeError("被绑定的对象类型并不是函数~");
            }
            var self = this,
                args = Array.from(arguments)
                fBind;
            args.shift();
            function F() {}
            fBind = function() {
                var innerArgs = Array.from(arguments);
                return self.apply(this instanceof fBind ? this : context, [...args, ...innerArgs]);
            }
            F.prototype = self.prototype;
            fBind.prototype = new F();
            return fBind;
        } 
    }
    function Person(name, age) {
        this.name = name;
        this.age = age;
    }    
    Person.prototype.introduce = function() {
        console.log(`I'm ${this.name}, ${this.age} year's old`);
    };
    var obj = {
        name: "Gary Yin",
        age: 26
    };
    var fBind = Person.bind(obj);
    var obj_ano = {
        name: "wenkai.yin",
        age: 27,
        fBind
    };
    obj_ano.fBind("one piece", 12);
    console.log(obj, obj_ano);
    //在这里打印:
    //Object {name: "one piece", age: 12}
    //Object {name: "wenkai.yin", age: 27, fBind: f}
    var obj_empty = {};
    fBind.apply(obj_empty, ["Gary wenkai", 22]);
    console.log(obj, obj_empty);
    //在这里打印:
    //Object {name: "Gary wenkai", age: 22}
    //Object {}
    
> polyfill兼容模拟Object.create

    if(!Object.create) {
        Object.create = function(o) {
            function F() {}
            F.prototype = o;
            return new F();
        };
    }
    var gary = {
        name: "Gary Yin",
        age: 24
    };
    var gary_ = Object.create(gary);
    console.log(gary_.name, gary_.age);
    console.log(gary.isPrototypeOf(gary_));
    console.log(Object.getPrototypeOf(gary_) === gary);
    //在这里打印:
    //Gary Yin 24
    //true
    //true
    
> polyfill兼容模拟函数截流以及函数防抖

    //函数截流
    var throttle = (function () {
        var firstTime = true,
            timer = null;
        return function(func, speed) {
            if(firstTime) {
                func();
                firstTime = false;
                return false;
            }
            if(timer) {
                return false;
            }
            timer = setTimeout(function time() {
                clearTimeout(timer);
                timer = null;
                func();
            }, speed);
        };    
    })();
    window.onresize = function (event) {
        throttle(function () {
            console.log(event);
        }, 1000);
    };
    //快速缩小或者放大浏览器长宽最多会打印两条数据,输出的数据会很慢:
    //Event {isTrusted: true, type: "resize", target: Window, currentTarget: Window, eventPhase: 2, …}
    //Event {isTrusted: true, type: "resize", target: Window, currentTarget: Window, eventPhase: 2, …}
    
    //函数防抖
    var debounce = (function () {
        var timer = null;
        return function (func, speed) {
            if(timer) {
                clearTimeout(timer);
                timer = null;
            }
            timer = setTimeout(function time() {
                func();
            }, speed);
        }
    })();
    window.onresize = function(event) {
        debounce(function() {
            console.log(event);
        }, 1000);
    };
    //持续快速缩小或者放大浏览器长宽1s之后,只会打印一条数据:
    //Event {isTrusted: true, type: "resize", target: Window, currentTarget: Window, eventPhase: 2, …}
    
>  polyfill兼容模拟softBind软绑定

    if(!Function.prototype.softBind) {
        Function.prototype.softBind = function(context) {
            if(typeof this !== "function") {
                throw new TypeError("被绑定的对象类型并不是函数~");
            }
            var self = this,
                args = Array.from(arguments),
                fSoftBind;
            args.shift();
            function F() {}
            fBind = function() {
                var innerArgs = Array.from(arguments);
                return self.apply((!this || this === window) ? context : this, [...args, ...innerArgs]);
            };
            F.prototype = self.prototype;
            fBind.prototype = new F();
            return fBind;
        };
    }
    function Person(name, age) {
        this.name = name;
        this.age = age;
    }    
    Person.prototype.introduce = function() {
        console.log(`I'm ${this.name}, ${this.age} year's old`);
    };
    var obj = {
        name: "Gary Yin",
        age: 26
    };
    var fBind = Person.softBind(obj);
    var obj_ano = {
        name: "wenkai.yin",
        age: 27,
        fBind
    };
    obj_ano.fBind("one piece", 12);
    console.log(obj, obj_ano);
    //在这里打印:
    //Object {name: "Gary Yin", age: 26}
    //Object {name: "one piece", age: 12, fBind: f}
    var obj_empty = {};
    fBind.apply(obj_empty, ["Gary wenkai", 22]);
    console.log(obj, obj_empty);
    //在这里打印:
    //Object {name: "Gary Yin", age: 26}
    //Object {name: "Gary wenkai", age: 22}
    
> polyfill兼容模拟isInteger是否为整数

    if(!Number.isInteger) {
        Number.isInteger = function(num) {
            return typeof num === "number" && (num % 1 === 0);
        };
    }
    
    console.log(Number.isInteger(44.6));
    console.log(Number.isInteger(Number.MAX_SAFE_INTEGER));
    console.log(Number.isInteger(Infinity));
    console.log(Number.isInteger(NaN));
    console.log(Number.isInteger(99));
    //在这里打印:
    //false
    //true
    //false
    //false
    //true
    
> polyfill兼容模拟isNaN是否为NaN

    if(!Number.isNaN) {
        Number.isNaN = function(num) {
            return typeof num === "number" && (num !== num);
        };
    }
    
    console.log(Number.isNaN({}));
    console.log(Number.isNaN([]));
    console.log(Number.isNaN(NaN));
    console.log(Number.isNaN(0 * Infinity));
    console.log(Number.isNaN(1 / 0));
    console.log(Number.isNaN(1 / Infinity));
    console.log(Number.isNaN(Infinity / Infinity));
    //在这里打印:
    //false
    //false
    //true 
    //true
    //false
    //false
    //true
    
> polyfill兼容模拟isNagetiveZero是否为负零,负号一般代指方向

    if(!Number.isNagetiveZero) {
        Number.isNagetiveZero = function(num) {
            return typeof num === "number" && (1 / num === -Infinity);
        };
    }
    
    console.log(Number.isNagetiveZero(-0));
    console.log(Number.isNagetiveZero(0));
    console.log(Number.isNagetiveZero(1 / Infinity));
    console.log(Number.isNagetiveZero(99 / -Infinity));
    //在这里打印:
    //true
    //false
    //false
    //true
    
> polyfill兼容模拟isEpsilon来判断0.1 + 0.2 === 0.3

    if(!Number.isEpsilon) {
        Number.isEpsilon = function(num) {
            return num < Number.EPSILON;
        };
    }
    
    console.log(Number.isEpsilon(0.1 + 0.2 - 0.3));
    //在这里打印:
    //true
        
    
## 元素视图盒模型

    //获取浏览器屏幕的可视宽度以及高度
    console.log(window.innerWidth, window.innerHeight);
    //获取页面元素的无边框宽度以及高度
    var box = document.getElementById("box");
    console.log(box.clientWidth, box.clientHeight);
    //获取页面元素的有边框宽度以及高度
    console.log(box.offsetWidth, box.offsetHeight);
    //获取页面文档的高度
    console.log(document.body.clientHeight || document.documentElement.clientHeight);
    //获取滑块滑动后距离顶部的高度
    console.log(document.body.scrollTop || document.documentElement.scrollTop);
    //获取元素在页面的相对位置
    var position = box.getBoundingClientRect();
    console.log(position.top, position.left, position.right, position.bottom);
    //获取元素在页面的绝对位置
    var scrollTop = document.body.scrollTop || document.documentElement.scrollTop;
    var absoluteTop = position.top + scrollTop,
        absoluteBottom = position.bottom + scrollTop;
    console.log(absoluteTop, absoluteBottom);
    //获取元素的滑块滑动高度
    console.log(box.scrollHeight);
    
# <中篇>整理: 类型、语法
## 类型
> 基本类型

<p>Javascript中基本类型分为: number、string、boolean、undefined和null,null类型由于JS最初时的一个bug导致它的typeof类型为object</p>
    
> 引用类型

<p>Javascript中引用类型分为: object以及function</p>
    
> 内置函数和内置对象

<p>Javascript中存在内置函数和内置对象,它们分别是: String、Number、Boolean、Object、Array、Function、RegExp、Math、JSON、Symbol和Error,当你去构造调用一个内置函数时,你就可以使用这些内置函数所拥有的属性或者方法,譬如说toString,valueOf,toFixed等等,但是你可能会问,为什么那些常量,比如说var string = "string";string.toString();也可以调用构造调用的引用对象才能调用的属性或者方法呢?<br/>回答: 这些常量本身并没有这些属性和方法,而是它们在调用属性或者方法的时候,浏览器引擎会将它们封装成理应匹配的构造调用内置函数或者内置方法,这样这些常量就可以调用了</p>

<b>例子</b>

    var string_obj = new String("I'm Gary"),
        string = "I'm Seven";
    console.log(string_obj.slice(0, 5));
    console.log(string.slice(0, 6));
    //在这里打印:
    //I'm G
    //I'm Se
    var number_obj = new Number(10),
        number = 22;
    console.log(number_obj.toFixed(2));
    console.log(number.toFixed(2));
    //使用数字常量去调用数字构造调用的属性或者方法时,必须使用两个点调用,第一个点浏览器会认为是数字常量浮点类型的第一个点,第二点才是调用数字构造调用的属性或者方法的点
    console.log(40..toFixed(2));
    //在这里打印:
    //10.00
    //22.00
    //40.00
        
> 0.1 + 0.2 !== 0.3

<p>大家都清楚,在JS里,0.1+0.2!==0.3,而是等于0.30000000000000004,原因:浮点数十进制在底层转化为二进制机器码进行运算,由于JS的浮点数并不是很精确,所以运算之后,转化为十进制之后,并不是0.3,而是0.30000000000000004<br/>那该怎么解决这个问题,使得0.1+0.2===0.3呢? ES6在Number内置函数上提供了一个属性EPSILON,它可以进行甄别0.1+0.2相加运算之后的值是否是在这个范围之内,如果是,就返回true,如果不是,就返回false</p>

<b>例子</b>
    
    function isEpsilon(num) {
        return num < Number.EPSILON
    }
    console.log(isEpsilon(0.1 + 0.2 - 0.3));
    //在这里打印:
    //true
    //说明0.1 + 0.2 - 0.3是在这个区间之内的,说明0.1 + 0.2 === 0.3
    //而这个Number.EPSILON的区间范围是:2.220446049250313e-16
    
> 内置数字函数Number处理

<p>下面是Number内置数字函数对各个类型的常量或者变量处理的结果,当处理基本类型的常量或者变量时,遇到null、false、0、""、"      "和"0"时,会处理成0;遇到true,会处理成1;遇到undefined、NaN、字符串中含有字母时,会处理成NaN;当处理引用类型的常量或者变量时,会根据对象的ToNumber、ToString和ToPremitive进行处理,当遇到Number内置数字函数进行处理时,会直接调用对象的ToNumber也就是valueOf,遇到空数组时,会处理成0;遇到有一个数组元素的数组时,会处理成这一个数组元素产生的结果;遇到有两个数组的数组时,会处理成NaN;遇到对象时,会处理成NaN</p>

<b>例子</b>

    console.log(Number(undefined));
    console.log(Number(null));
    console.log(Number(NaN));
    console.log(Number(0));
    console.log(Number("0"));
    console.log(Number("0n0"));
    console.log(Number(""));
    console.log(Number("     "));
    console.log(Number({}));        
    console.log(Number([]));
    console.log(Number([44]));
    console.log(Number(["4N4"]));
    console.log(Number([44, 99]));
    console.log(Number(true));
    console.log(Number(false));
    //在这里打印:
    //NaN
    //0
    //NaN
    //0
    //0
    //NaN
    //0
    //0
    //NaN
    //0
    //44
    //NaN
    //NaN
    //1
    //0
    
> 内置字符串函数String处理
<p>下面是String内置字符串函数对各个类型的常量或者变量处理的结果,当处理基本类型的常量或者变量时,遇到undefined、null、NaN、true、false、1、0时,会处理成"undefined","null","NaN","true","false","true","false","1","0";当处理引用类型的常量或者变量时,会根据对象的ToNumber、ToString和ToPremitive进行处理,当遇到String内置字符串函数进行处理时,会直接调用对象的ToString也就是toString,遇到空数组时,会处理成"";遇到有一个数组元素的数组时,会处理成这个数组元素的字符串形式;遇到有多个数组的数组时,会处理成每个数组元素的字符串形式并在中间加上逗号;遇到对象时,会处理成其原型链上toString后显示的结果[object Object]</p>

<b>例子</b>

    console.log(String(undefined));
    console.log(String(null));
    console.log(String(0));
    console.log(String(NaN));
    console.log(String(true));
    console.log(String(false));
    console.log(String([]));
    console.log(String({}));
    console.log(String([44]));
    console.log(String([66, 99]));
    console.log(String("      "));
    //在这里打印:
    //"undefined"
    //"null"
    //"0"
    //"NaN"
    //"true"
    //"false"
    //""
    //[object Object]
    //"44"
    //"66,99"
    //"      "

> 字符串toString方法处理

<p>下面是toString字符串方法对各个类型的常量或者变量处理的结果,当处理基本类型的常量或者变量时,遇到undefined、null时,会直接报TypeError错误,表明undefined和null并不存在toString方法;当遇到NaN、true、false、1、0时,会直接处理成"NaN","true","false","1","0";当处理引用类型的常量或者变量时,会根据对象的ToNumber、ToString和ToPremitive进行处理,当遇到toString字符串方法进行处理时,遇到空数组时,会处理成"";遇到有一个数组元素的数组时,会处理成这个数组元素的字符串形式;遇到有多个数组的数组时,会处理成每个数组元素的字符串形式并在中间加上逗号;遇到对象时,会处理成其原型链上toString后显示的结果[object Object]</p>

<b>例子</b>

    console.log(undefined.toString());
    console.log(null.toString());
    console.log(0..toString());
    console.log(1..toString());
    console.log(true.toString());
    console.log(false.toString());
    console.log(NaN.toString());
    console.log([].toString());
    console.log({}.toString());
    console.log([44].toString());
    console.log(["4n4"].toString());
    console.log([44, 89].toString());
    console.log("      ".toString());
    //在这里打印:
    //TypeError: Cannot read property 'toString' of undefined
    //TypeError: Cannot read property 'toString' of null
    //"0"
    //"1"
    //"true"
    //"false"
    //"NaN"
    //""
    //[object Object]
    //"44"
    //"4n4"
    //"44, 89"
    //"      "
    
> polyfill兼容模拟判断一个常量或者一个变量是否为NaN

<p>通常我们使用内置数字函数Number上的isNaN静态方法来判断一个常量或者一个变量是否为NaN,当然当遇到不兼容Number.isNaN方法的浏览器时,我们可以手写一个polyfill兼容版的静态方法,利用NaN的特性:NaN自己不等于其本身</p>

<b>例子</b>

    console.log(Number.isNaN(NaN));
    //在这里打印:
    //true
    
    if(!Number.isNaN) {
        Number.isNaN = function(num) {
            return num !== num;
        };
    }
    console.log(Number.isNaN(NaN));
    console.log(Number.isNaN(0));
    console.log(Number.isNaN({}));
    console.log(Number.isNaN([]));
    console.log(Number.isNaN([44]));
    //在这里打印:
    //true
    //false
    //false
    //false
    //false
    
> 内置数字函数Number上的属性或者方法

<p>Number内置数字函数的MAX_VALUE和MIN_VALUE属性代表的是JS里所能表示的最大数值和最小数值;而MAX_SAFE_INTEGER和MIN_SAFE_INTEGER代表的是JS里面最大的和最小的安全整数;isInteger是判断一个常量或者一个变量是否是整数;而isSafeInteger则是判断一个常量或者一个变量是否是安全整数;当然我们也可以polyfill兼容模拟判断一个常量或者一个变量是否为整数isInteger</p>

<b>例子</b>

    console.log(Number.MAX_VALUE);
    console.log(Number.MIN_VALUE);
    console.log(Number.MAX_SAFE_INTEGER); 
    console.log(Number.MIN_SAFE_INTEGER);
    console.log(Number.isInteger(Number.MAX_VALUE));
    console.log(Number.isInteger(Infinity));
    console.log(Number.isInteger(44.7));
    console.log(Number.isInteger(1.7976931348623157e+308));
    console.log(Number.isSafeInteger(1.7976931348623157e+308));
    console.log(Number.isSafeInteger(9007199254740991));
    console.log(Number.isSafeInteger(Number.MAX_SAFE_INTEGER + 1));
    //在这里打印:
    //1.7976931348623157e+308
    //5e-324
    //9007199254740991
    //-9007199254740991
    //true
    //false
    //false
    //true
    //false
    //true
    //false
    
    //polyfill模拟判断一个常量或者一个变量是否为整数isInteger
    if(!Number.isInteger) {
        Number.isInteger = function (num) {
            return typeof num === "number" && (num % 1 === 0);
        };
    }
    console.log(Number.isInteger(Number.MAX_VALUE));
    console.log(Number.isInteger(Infinity));
    console.log(Number.isInteger(44.7));
    console.log(Number.isInteger(1.7976931348623157e+308));
    console.log(Number.isInteger(44));
    //在这里打印:
    //true
    //false
    //false
    //true
    //true
    
> Infinity、-Infinity、0与-0

<p>除了0与-0之外,任何与Infinity进行运算(除了除法运算)的数值结果全都为Infinity或者-Infinity,任何与-Infinity进行运算(除了除法运算)的数值结果全都为Infinity或者-Infinity,任何与Infinity或者-Infinity进行运算的非数值结果根据隐式类型转换(valueOf)后决定;0与Infinity进行乘法运算的结果为NaN,进行加减运算的结果为Infinity或者-Infinity;-0与Infinity进行乘法运算的结果为NaN,进行加减运算的结果为Infinity或者-Infinity;任何与Infinity进行除法运算的数值结果全都为0或者-0;任何与-Infinity进行除法运算的数值结果全都为0或者-0;除了0与-0之外,任何与0进行除法运算的数值结果全都为Infinity或者-Infinity;任何与-0进行除法运算的数值结果全都为Infinity或者-Infinity;0, -0与0, -0进行除法运算的结果为NaN;</p>

<b>例子</b>

    console.log(1 * Infinity);
    console.log(-1 * Infinity);
    console.log(1 / Infinity);
    console.log(-1 / Infinity);
    console.log(199 * Infinity);
    console.log(-199 * Infinity);
    console.log("1ab" * Infinity);
    console.log(Infinity * Infinity);
    console.log(-Infinity * Infinity);
    console.log(-Infinity * -Infinity);
    console.log([44] * Infinity);
    console.log(["4n4"] * Infinity);
    console.log([99, 77, 29] * Infinity);
    console.log({} * Infinity);
    console.log([] * Infinity);
    console.log(NaN + Infinity);
    console.log(0 * Infinity);
    console.log(-0 * Infinity);
    console.log(0 - Infinity);
    console.log(-0 - Infinity);
    console.log(0 / Infinity);
    console.log(-0 / Infinity);
    console.log(Infinity / Infinity);
    console.log(-Infinity / Infinity);
    console.log(1 / 0);
    console.log(-1 / 0);
    console.log(0 / 0);
    console.log(-0 / 0);
    console.log(-0 / -0);
    
    //在这里打印:
    //Infinity
    //-Infinity
    //0
    //-0
    //Infinity
    //-Infinity
    //NaN
    //Infinity
    //-Infinity
    //Infinity
    //Infinity
    //NaN
    //NaN
    //NaN
    //NaN
    //NaN
    //NaN
    //NaN
    //-Infinity
    //-Infinity
    //0
    //-0
    //NaN
    //NaN
    //Infinity
    //-Infinity
    //NaN
    //NaN
    //NaN
    
> polyfill兼容模拟判断一个数值是-0

<b>例子</b>

    if(!Number.isNagetiveZero) {
        Number.isNagetiveZero = function(num) {
            return typeof num === "number" && (1 / num === -Infinity);
        };
    }
    console.log(Number.isNagetiveZero(0));
    console.log(Number.isNagetiveZero(-0));
    console.log(Number.isNagetiveZero(1 / Infinity));
    console.log(Number.isNagetiveZero(-99 / Infinity));
    console.log(Number.isNagetiveZero(Infinity / Infinity));
    //在这里打印:
    //false
    //true
    //false
    //true
    //false
    
> parseInt是从字符串首部开始截取字符为数值并转化为数值的函数方法

<p>parseInt函数方法的第一个参数是要进行首部开始截取字符为数值并转化为数值的字符串,而第二个参数则是转化的进制数;parseInt函数方法当遇到并不是字符串的常量或者变量时,它会先将其隐式类型转换为字符串,再进行首部开始截取字符为数值并转化为数值</p>

<b>例子</b>

    console.log(parseInt("468Gary743"));
    console.log(parseInt("Gary468743"));
    console.log(parseFloat("48.6Gary733.4"));
    console.log(parseFloat("Gary48.6733.4"));
    console.log(["1", "2", "3"].map((item, index) => parseInt(item, index)));
    console.log(parseInt([]));
    console.log(parseInt([44]));
    console.log(parseInt([89, 96, 44]));
    console.log(parseInt(function() {}));
    console.log(parseInt({}));
    console.log(parseInt(function() {}, 16));
    console.log(parseInt(true));
    console.log(parseInt(false, 16));
    console.log(parseInt(true, 16));
    console.log(parseInt(1/0, 19));
    console.log(parseInt(function() {}, 8));
    console.log(parseInt(1/-0, 19));
    console.log(parseInt([1/0, "68", false, true], 19));
    
    //在这里打印:
    //468
    //NaN
    //48.6
    //NaN
    //[1, NaN, NaN]
    //NaN
    //44
    //89
    //NaN
    //NaN
    //15
    //NaN
    //250
    //NaN
    //18
    //NaN
    //NaN
    //18
    
> try {} catch(err) {} finally {}

<p>在ES6的let、const块级作用域之前,Google的Tracer团队就是使用try {} catch(a) {}这种方式来模拟块级作用域,浏览器编译后基本上是以下表达式形式:</p>

<b>例子</b>

    function foo() {
        try {
            throw undefined;
        } catch(a) {
            a = 2;
            console.log(a);
        }
        console.log(a);
    }
    foo();
    //在这里打印:
    //2
    //ReferrenceError: a is not defined
    
<p>使用try...catch()...finally了之后,try表达式中的return返回表达式语句不会被执行,会直接跳过,执行finally中的返回表达式语句:</p>

<b>例子</b>

    function foo(num) {
        try {
            console.log(668);
            console.log(num + 1);
            return 100;
        } catch(error) {
            console.log(error);
        } finally {
            return num;
        }
    }    
    console.log(foo(999));
    //在这里打印:
    //668
    //1000
    //999
    
> == 与 === 的区别

<p>在初学者阶段,被问到 == 与 === 的区别,我一般都会回答==不校验类型,只校验值,===既校验类型,还校验值;而现在的理解是,==进行隐式强制类型转换,而===不进行强制类型转换。</p>

<b>例子</b>

    console.log(1 == "1");
    console.log(22 === "22");
    console.log(true == 1);
    console.log(false === 0);
    //在这里打印:
    //true
    //false
    //true
    //false
    
> && 与 ||的优先级

<p>&&与||是有优先级区分的,&&的优先级是大于||的。</p>

<b>例子</b>
    
    var a = true,
        b = false,
        c = true;
    console.log(b && a || c);
    //在这里打印:
    //true   
    //说明表达式是执行(b && a) || c,而不是b && (a || c),如果是后者,那返回就应该是false
    
> JSON.stringify将JS对象转化为JSON字符串

<p>JSON.stringify进行转化时,遇到非JSON语法的表达式语句,会转化成undefined或者null,当遇到undefined或者function() {}时,会转化为undefined;当遇到NaN时,会转化为null;当遇到在数组对象中的非JSON语法的表达式语句,会全部转化为null;当遇到对象中的非JSON语法的表达式语句时,会删除掉非法的属性或者属性值</p>

<b>例子</b>

    console.log(JSON.stringify(undefined));
    console.log(JSON.stringify(null));
    console.log(JSON.stringify(function() {}));
    console.log(JSON.stringify(NaN));
    console.log(JSON.stringify([]));
    console.log(JSON.stringify([function() {}, NaN, null, true, {}, 66, undefined]));
    console.log(JSON.stringify({}));
    console.log(JSON.stringify({a: function() {}, b: NaN, c: null, d: true, e: 88, f: undefined, g: [], h: [undefined, NaN, function() {}]}));
    //在这里打印:
    //undefined
    //null
    //undefined
    //null
    //[]
    //[null, null, null, true, {}, 66, null]
    //{b: null, c: null, d: true, e: 88, g: [], h: [null, null, null]}
        
    
   

      
    
    
    
      
    
    
    
           
    
    
    
    
    

    

    
    
        
    
    
    
    
        
    
    
    
    
    
    
    

        
    
        
    
    
    
    
    
    
    
    
        
    
    
    
    
    
    
    
    

        
    
    
    
    
        
 
    

    
 
    
    
        

    