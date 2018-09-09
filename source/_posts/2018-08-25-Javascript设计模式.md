---
title: Javascript设计模式
date: 2018-08-25 11:37:47
tags: [Javascript, 设计模式]
categories: Javascript设计模式
---
# 单例模式
> 单例模式有两个特点: 全局性和唯一性.全局唯一性是指在全局环境中,只创建对象一次且保证对象在创建过后不被再次创建.下面我们就来演示一下Javascript语言的普通类单例模式和透明单例模式

## 普通类单例模式
    
    function GetSingleton(name) {
        this.name = name;
        this.instance = null;
    }
    
    GetSingleton.prototype.getName = function() {
        return this.name;
    };
    
    GetSingleton.prototype.Singleton = function(name) {
        return this.instance || (this.instance = new GetSingleton(name));  
    };
    
    let gary_one = GetSingleton.prototype.Singleton("gary_one");
    let gary_two = GetSingleton.prototype.Singleton("gary_two");
    //在这里打印:
    //true
    console.log(gary_one === gary_two);
    
## 普通类单例模式(闭包版本)

    function GetSingleton(name) {
        this.name = name;
    }
    
    GetSingleton.prototype.getName = function() {
        return this.name;
    };
    
    let Singleton = (function() {
        let instance;
        return function(name) {
            return instance || (instance = new GetSingleton(name));
        }
    })();
    
    let gary_one = Singleton("gary_one");
    let gary_two = Singleton("gary_two");
    //在这里打印:
    //true
    console.log(gary_one === gary_two);
    
## 透明单例模式

    let GetSingleton = (function() {
        let instance;
        return function(html) {
            if(instance) {
                return instance;
            }
            this.html = html;
            this.init();
            return instance = this;
        }
    })();
    
    GetSingleton.prototype.init = function() {
        let div = document.createElement("div");
        div.innerHTML = this.html;
        document.body.appendChild(div);
        return div;
    };
    
    let gary_one = new GetSingleton("gary_one");
    let gary_two = new GetSingleton("gary_two");
    //页面上只有创造了一个DIV DOM节点,内容是"gary_one"
    //在这里打印:
    //true
    console.log(gary_one === gary_two);
    
## 透明单例模式(代理模式版本)

    function GetSingleton(html) {
        this.html = html;
        this.init();
    }
    
    GetSingleton.prototype.init = function() {
        let div = document.createElement("div");
        div.innerHTML = this.html;
        document.body.appendChild(div);
    }
    
    let Singleton = (function() {
        let instance;
        return function(html) {
            return instance || (instance = new GetSingleton(html));
        }
    })();
    
    let gary_one = new Singleton("gary_one");
    let gary_two = new Singleton("gary_two");
    //页面上只有创造了一个DIV DOM节点,内容是"gary_one"
    //在这里打印:
    //true
    console.log(gary_one === gary_two);
    
## Javascript单例模式 ——— 单一对象

    let obj_only = {
        a() {
            console.log("a");
        },
        b() {
            console.log("b");
        }
    };
    //在这里打印:
    //a
    obj_only.a();
    //在这里打印:
    //b
    obj_only.b();
    
    //动态空间对象
    let MyApp = {};
    MyApp.namespace = function(model) {
        let parts = model.split("."),
            prototype = MyApp;
        for(let [key, value] of parts.entries()) {
            if(!prototype[value]) {
                prototype[value] = {};
            }
            prototype = prototype[value];
        }    
    };
    MyApp.namespace("model");
    MyApp.namespace("div.style");
    //在这里打印:
    //{model: {}, div: {style: {}}}
    console.log(MyApp);
    
    //闭包
    function Person() {
        let _name = "Gary",
            _age = 26;
         return function() {
            return `name: ${_name}, age: ${_age}`;
         }   
    }
    let Gary = Person();
    //在这里打印:
    //name: Gary, age: 26
    console.log(Gary());
    
## 惰性单例模式

    //首先演示的不是惰性单例模式,而是对于创造单个对象有哪几种方式
    let GetSingleton = (function (){
        let div = document.createElement("div");
        div.innerHTML = "Gary";
        div.style.display = "none";
        document.body.appendChild(div);
        return div;
    })();
    
    function Singleton() {
        document.getElementById("open").onclick = function(e) {
            let singletonDiv = GetSingleton;
            singletonDiv.style.display = "block";
            //取消冒泡事件
            e.stopImmediatePropagation();
        };
    }
    
    //这种情况下,无论调不调用Singleton方法,界面在最开始加载时,就已经进行了DOM操作,添加了一个DIV DOM节点,并把这个节点的内容设置为Gary,显示方式设置为none,这种方式的确时创造了单个对象且不可再次创造,但是缺点还是比较明显的,创造不创造单个对象跟绑定事件并没有关系,假如我在页面上并没有触发绑定的事件,页面上在一开始还是具有已经创造好的DIV DOM节点的
    Singleton();
    
    
    function GetSingleton() {
        let div = document.createElement("div");
        div.innerHTML = "Gary";
        div.style.display = "none";
        document.body.appendChild(div);
        return div;
    }
    
    function Singleton() {
        document.getElementById("open").onclick = function(e) {
            let singletonDiv = GetSingleton();
            singletonDiv.style.display = "block";
            //取消冒泡
            e.stopImmediatePropagation();
        };
    }
    
    //这种情况下,满足了调用时再创造单个对象的条件,但是并不满足创造了单个对象并不可再次创造的条件,在这种情况下,每点击一次id为open的按钮一次,就会创造一个对象,这显然是不符合单例模式的特点的
    Singleton();
    
    let GetSingleton = (function() {
        let res;
        return function() {
            if(!res) {
                res = document.createElement("div");
                res.innerHTML = "Gary";
                res.style.display = "none";
                document.body.appendChild(res);
            }
            return res;
        }
    })();
    
    function Singleton() {
        document.getElementById("open").onclick = function(e) {
            let singletonDiv = GetSingleton();
            singletonDiv.style.display = "block";
            //取消冒泡
            e.stopImmediatePropagation();
        };
    }
    
    //这种才是真正的惰性单例模式,在调用绑定事件时才创造单个对象,且也满足创造了单个对象并不可再次创造的条件,但是还是有优化的空间的
    Singleton();
    
## 惰性单例模式(优化版本)

    function GetSingleton(func) {
        let res;
        return function() {
            return res || (res = func.apply(this, arguments));
        }
    }
    
    let singleton = GetSingleton(function() {
        let div = document.createElement("div");
        div.innerHTML = "Gary";
        div.style.display = "none";
        document.body.appendChild(div);
        return div;
    });
    
    function Singleton() {
        document.getElementById("open").onclick = function(e) {
            let singletonDiv = singleton();
            singletonDiv.style.display = "block";
            //取消冒泡事件
            e.stopImmediatePropagation();
        };
    }
    
    //这是惰性单例模式的最终优化版本,最显著的特点时它的复用性,无论是创造任何的DOM节点,只用GetSingleton函数方法,外部传入一个func函数即可,立即满足创造单一对象之后不可再次创建的特点
    Singleton();
    
## 惰性单例模式的应用
> 还记得jQuery工具库的.one函数方法嘛,它就是最经典的单例模式例子,我们今天来模拟一下

    function GetSingleton(func) {
        let res;
        return function() {
            return res || (res = func.apply(this, arguments));
        }
    }
    
    let bindEvent = GetSingleton(function () {
        document.getElementById("open").onclick = function(e) {
            alert("Gary");
            //取消冒泡
            e.stopImmediatePropagation();
        };
        console.log("bind~");
        return true;
    });
    
    function render() {
        console.log("开始渲染~");
        bindEvent();
    }
    
    //切实的实现了单例模式"一朝绑定,终生收益"的特性
    //在这里打印:
    //开始渲染~
    //bind~
    //开始渲染~
    //开始渲染~
    render();
    render();
    render();
    
# 策略模式
> 策略模式的主要条件有三个: 可扩展、可复用和可替换,就让我们先演示一个非策略模式下的例子,我们要计算年终奖,首先要知晓月薪基数,然后再知道奖励倍数,就可以计算出最后的年终奖,一般我们会这么写

    function getPerformance(performance, salary) {
        if(performance === "S") {
            return salary * 4;
        }
        if(performance === "A") {
            return salary * 3;
        }
        if(performance === "B") {
            return salary * 2;
        }
    }
    
    //在这里打印:
    //80000
    console.log(getPerformance("S", 20000));
    //在这里打印:
    //120000
    console.log(getPerformance("A", 40000));
    
> 非策略模式的例子,存在很多缺点,首先,策略对象不可复用,策略对象逻辑全都写在一个函数对象里面,并不能拿出进行复用,其次,扩展很不方便,每一次扩展都必须去改变策略对象所处的逻辑函数对象,最后新的策略对象不可替换新的策略对象,接下来我们用传统的策略模式进行解决,首先将策略对象抽取到外面,形成一个抽象的对象

    function PerformanceS() {
        
    }
    
    PerformanceS.prototype.getSalary = function(salary) {
        return salary * 4;
    };
    
    function PerformanceA() {
        
    }
    
    PerformanceA.prototype.getSalary = function(salary) {
        return salary * 3;
    };
    
    function PerformanceB() {
    
    }
    
    PerformanceB.prototype.getSalary = function(salary) {
        return salary * 2;
    };
    
    function GetPerformanceSalary() {
        this.performance = null;
        this.salary = null;
    }
    
    GetPerformanceSalary.prototype.setPerformance = function(performance) {
        this.performance = performance;
    };
    
    GetPerformanceSalary.prototype.setSalary = function(salary) {
        this.salary = salary;
    };
    
    GetPerformanceSalary.prototype.getBonus = function() {
        return this.performance.getSalary(this.salary);  
    };
    
    let getPerformanceSalary = new GetPerformanceSalary();
    getPerformanceSalary.setSalary(20000);
    getPerformanceSalary.setPerformance(new PerformanceS());
    //在这里打印:
    //80000
    console.log(getPerformanceSalary.getBonus());
    getPerformanceSalary.setSalary(40000);
    getPerformanceSalary.setPerformance(new PerformanceA());
    //在这里打印:
    //120000
    console.log(getPerformanceSalary.getBonus());
    
> 策略模式下的策略对象,复用性、扩展性和替换性都很强,策略对象现在是以抽象函数的形式进行的定义,可以直接拿原有的抽象函数对象进行复用,也可以定义新的抽象函数对象进行扩展,在替换性方面,薪酬基数和策略对象模式都可根据set...方法的方式进行替换,并且得到不同的结果

## Javascript策略模式

    let categories = {
        S(salary) {
            return salary * 4;
        },
        A(salary) {
            return salary * 3;
        },
        B(salary) {
            return salary * 2;
        }
    };
    
    function getPerformance(performance, salary) {
        return categories[performance](salary);
    }
    
    //在这里打印:
    //80000
    console.log(getPerformance("S", 20000));
    //在这里打印:
    //120000
    console.log(getPerformance("A", 40000));
    
## 策略模式 —— 表单验证
> 使用策略模式来进行表单验证,也是一种很好的做法,首先我们先不使用策略模式来编写表单验证

    function validate() {
        let userAgent = document.getElementById("user-agent");
        if(userAgent.username.value === "") {
            return "用户名不可为空";
        }
        if(userAgent.password.value.length !== 6) {
            return "密码长度必须为6位";
        }
        if(!/^1(3|5|8)[\d]{9}$/.test(userAgent.phone.value)) {
            return "手机号码不符合规范";
        }
    }
    
    let userAgent = document.getElementById("user-agent");
    userAgent.onsubmit = function(e) {
        let errMsg = validate();
        if(errMsg) {
            console.log(errMsg);
        }
        //取消冒泡事件
        e.stopImmediatePropagation();
        //取消默认事件
        e.preventDefault();
    };
    
> 策略对象不可复用,全都处在validate函数作用域下,且不可扩展,扩展必须去更改validate源代码,不符合开放封闭原则,更不能替换在任何的表单校验上面,只能针对特定的表单(name为username,password,phone的表单)进行校验,所以不使用策略模式,效果极差,下面我们就使用策略模式来进行表单校验

    let categories = {
        isNonUsername(value, errMsg) {
            if(value === "") {
                return errMsg;
            }
        },
        minLength(value, length, errMsg) {
            if(value.length !== parseInt(length)) {
                return errMsg;
            }
        },
        isMobile(value, errMsg) {
            if(!/^1(3|5|8)[\d]{9}$/.test(value)) {
                return errMsg;
            }
        }
    };
    
    function Validate() {
        this.cache = [];
    }
    
    Validate.prototype.add = function(dom, condition, errMsg) {
        this.cache.push(function() {
            let parts = condition.split(":");
            let categories_condition = parts.shift();
            parts.unshift(dom.value);
            parts = [...parts, errMsg];
            return categories[categories_condition].apply(dom, parts);
        });
    };
    
    Validate.prototype.start = function() {
        for(let [key, value] of this.cache.entries()) {
            let validateFunc = value;
            let errMsg = validateFunc();
            if(errMsg) {
                return errMsg;
            }
        }  
    };
    
    function validate() {
        let userAgent = document.getElementById("user-agent"),
            new_validate = new Validate();
        new_validate.add(userAgent.username, "isNonUsername", "用户名不可为空");
        new_validate.add(userAgent.password, "minLength:6", "密码长度必须为6位");
        new_validate.add(userAgent.phone, "isMobile", "手机号码不符合规范");
        let errMsg = new_validate.start();
        if(errMsg) {
            return errMsg;
        }    
    }
    
    let userAgent = document.getElementById("user-agent");
    userAgent.onsubmit = function(e) {
        let errMsg = validate();
        if(errMsg) {
            console.log(errMsg);
        }
        //取消冒泡事件
        e.stopImmediatePropagation();
        //取消默认事件
        e.preventDefault();
    };
    
> 这样就利用策略模式的复用性、扩展性以及替换性完美的解决了表单验证,你这时可能会有疑问,假如表单里面一个表单项有多个验证条件怎么办,这套策略模式的方式不就不好使了嘛,别急,只要修改一下Validate.prototype.add函数方法,就可以既兼容一个还兼容多个验证条件

    let categories = {
        isNonUsername(value, errMsg) {
            if(value === "") {
                return errMsg;
            }
        },
        minLength(value, length, errMsg) {
            if(value.length !== parseInt(length)) {
                return errMsg;
            }
        },
        isMobile(value, errMsg) {
            if(!/^1(3|5|8)[\d]{9}$/.test(value)) {
                return errMsg;
            }
        }
    };
    
    function Validate() {
        this.cache = [];
    }
    
    Validate.prototype.add = function(dom, rules) {
        for(let [key, value] of rules.entries()) {
            this.cache.push((function() {
                let condition = value["condition"],
                    errMsg = value["errMsg"];
                return function() {
                    let parts = condition.split(":");
                    let categories_condition = parts.shift();
                    parts.unshift(dom.value);
                    parts = [...parts, errMsg];
                    return categories[categories_condition].apply(dom, parts);
                }    
            })());
        }
    };
    
    Validate.prototype.start = function() {
        for(let [key, value] of this.cache.entries()) {
            let validateFunc = value;
            let errMsg = validateFunc();
            if(errMsg) {
                return errMsg;
            }
        }
    };
    
    function validate() {
        let userAgent = document.getElementById("user-agent"),
            new_validate = new Validate();
         new_validate.add(userAgent.username, [{
            condition: "isNonUsername",
            errMsg: "用户名不可为空"
         }, {
            condition: "minLength:10",
            errMsg: "用户名长度必须为10位"
         }]);
         new_validate.add(userAgent.password, [{
            condition: "minLength:6",
            errMsg: "密码长度必须为6位"
         }]);
         new_validate.add(userAgent.phone, [{
            condition: "isMobile",
            errMsg: "手机号码不和规范"
         }]);
         
         let errMsg = new_validate.start();
         if(errMsg) {
            return errMsg;
         }
    }
    
    let userAgent = document.getElementById("user-agent");
    userAgent.onsubmit = function(e) {
        let errMsg = validate();
        if(errMsg) {
            console.log(errMsg);
        }
        //取消冒泡事件
        e.stopImmediatePropagation();
        //取消默认事件
        e.preventDefault();
    };
    
> 这样就完美解决了多个验证条件的问题,这种策略模式可复用,可扩展,可替换,十分完美

# 代理模式
> 下面我们要介绍的是代理模式,顾名思义,代理模式就是通过代理层去替代实体对象处理一些信息,其实就是在保护实体对象,减少实体对象的职责,在过滤、处理、整合信息之后再交给实体对象,这样会使得实体对象很轻便,对于实体对象的扩展性、维护性以及替换性有很大的帮助

    function Flower() {
    }
    
    let xiaoming = {
        sendFlower(target) {
            let flower = new Flower();
            target.receiveFlower(flower);
        }
    };
    
    let A = {
        receiveFlower(flower) {
            console.log("已收到花朵: " + flower);
        }
    };
    
    let B = {
        receiveFlower(flower) {
            A.receiveFlower(flower);
        }
    };
    
    //在这里打印:
    //已收到花朵: [object Object]
    xiaoming.sendFlower(B);

> 这样就形成了一个小明送给女神A花朵表达想和她恋爱的心意,又不太好意思亲自送,只好让他跟A共同的好友B来进行代理送,这就是一个典型的代理模式的例子,你可能会问,这样做有什么意义呢,只不过多了一层罢了,的确这样只是多添加了一层而已,但是假如我们再改编一下剧情,你就会感觉很有意义

    function Flower() {
    }
    
    let xiaoming = {
        sendFlower(target) {
            let flower = new Flower();
            target.receiveFlower(flower);
        }
    };
    
    let A = {
        receiveFlower(flower) {
            console.log("已收到花朵: " + flower);
        },
        listenerBeHappy(func) {
            let self = this;
            setTimeout(function() {
                func.apply(self);
            }, 1000);
        }
    };
    
    let B = {
        receiveFlower(flower) {
            A.listenerBeHappy(function () {
                this.receiveFlower(flower);
            });
        }
    };
    
    //在这里打印:
    //已收到花朵: [object Object]
    xiaoming.sendFlower(B);
    
> 故事的剧情转变成了这样,小明送给女神A花朵表达想和她恋爱的心意,又不太好意思亲自送,只好让他跟A共同的好友B来进行代理送,B清楚A什么时间心情最好,什么时间可以接受别人对她的表白,所以B在A心情很好的时候将小明的花朵转交给女神A,虽然也不见得小明的追求会成功,但是B的代理工作充分表明了代理模式

## 虚拟代理
> 我们使用虚拟代理来写一个懒加载图片的例子,通常我们使用Js写加载图片时,一般会这么做

    let loadImage = (function () {
        let Image = document.createElement("img");
        document.body.appendChild(Image);
        return {
            setSrc(src) {
                Image.src = src;
            }
        }
    })();
    
    loadImage.setSrc("https://www.google.com/images/branding/googlelogo/2x/googlelogo_color_272x92dp.png");
    
> 但是这样做有一个用户体验的交互问题,图片还没有完全渲染的时候,图片区域是空白的,这时候我们需要使用代理来虚拟在图片还没有完全渲染完毕的时候,先在所在区域展示loading加载图,当图片完全渲染完毕之后,再将所在区域替换成图片

    let loadImage = (function () {
        let Image = document.createElement("img");
        document.body.appendChild(Image);
        return {
            setSrc(src) {
                Image.src = src;
            }
        }
    })();
    
    let proxyLoadImage = (function () {
        let img = new Image();
        img.onload = function() {
            loadImage.setSrc(this.src);
        };
        
        return {
            setSrc(src) {
                loadImage.setSrc("../img/zy.jpeg");
                img.src = src;
            }
        }
    })();
    
    proxyLoadImage.setSrc("https://www.google.com/images/branding/googlelogo/2x/googlelogo_color_272x92dp.png");
    
> 虚拟代理模式对于用户是无感的,用户不会知道你使用的是实体对象接口还是虚拟代理对象接口,且虚拟代理对象的复用性、扩展性以及可替换性都是很完美的,完全不会破坏原有的实体对象的代码结构,下面我们来写一个使用虚拟代理模式实现批量提交文件,节省浏览器和后台服务器资源的例子

    function syncReadFile(id) {
        console.log("开始上传文件: " + id);
    }
    
    let checkbox = document.getElementsByName("checkbox");
    for(let i = 0; i < checkbox.length; i ++) {
        checkbox[i].onclick = function(e) {
            if(this.checked) {
                syncReadFile(this.id);
            }
            //取消冒泡事件
            e.stopImmediatePropagation();
        };
    }
    
> 这个例子,我每点一次复选框,且复选框选中,就会上传文件,在短时间内选中多个复选框,会造成大量的上传请求发出,频繁的调用上传接口,会大量浪费浏览器和后台服务器资源,所以我们设置一个函数节流函数来模拟syncReadFile函数,相当于是一个虚拟代理模式的函数,节省浏览器和后台服务器资源

    function syncReadFile(id) {
        console.log("开始上传文件: " + id);
    }
    
    let proxySyncReadFile = (function() {
        let cache = [],
            timer = null;
        return function (id) {
            let self = this;
            cache = [...cache, id];
            if(timer) {
                return false;
            }
            timer = setTimeout(function () {
                let id_transform = cache.join(",");
                syncReadFile.call(self, id_transform);
                clearTimeout(timer);
                timer = null;
                cache.length = 0;
            }, 2000);
        }    
    })();
    
    let checkbox = document.getElementsByName("checkbox");
    for(let i = 0; i < checkbox.length; i ++) {
        checkbox[i].onclick = function (e) {
            if(this.checked) {
                proxySyncReadFile(this.id);
            }
            //取消冒泡事件
            e.stopImmediatePropagation();
        };
    }
    
## 缓存代理
> 我们先来写一个缓存代理计算乘积的例子,当传入的参数与上一次传入的参数相同时,就使用缓存中的乘积结果,不需要再次进行计算

    function getMultiple() {
        let cache = {};
        function multiple() {
            let a = 1;
            for(let i = 0; i < arguments.length; i ++) {
                a *= arguments[i];
            }
            return a;
        }
        return function() {
            let cache_prototype = Array.prototype.join.call(arguments, "_");
            if(cache[cache_prototype]) {
                return cache[cache_prototype];
            }
            console.log("again");
            return cache[cache_prototype] = multiple.apply(this, arguments);
        }
    }
    
    let multipleForReal = getMultiple();
    //在这里打印:
    //again
    //168
    console.log(multipleForReal(4, 6, 7));
    //在这里打印:
    //168
    console.log(multipleForReal(4, 6, 7));
    
> 让我们将事情变得更有趣一些

    function plus() {
        let a = 0;
        for(let i = 0; i < arguments.length; i ++) {
            a += arguments[i];
        }
        return a;
    }
    
    function multiple() {
        let a = 1;
        for(let i = 0; i < arguments.length; i ++) {
            a *= arguments[i];
        }
        return a;
    }
    
    function getMethod(func) {
        let cache = {};
        return function () {
            let cache_prototype = Array.prototype.join.call(arguments, "_");
            if(cache[cache_prototype]) {
                return cache[cache_prototype];
            }
            console.log("again");
            return cache[cache_prototype] = func.apply(this, arguments);
        }
    }
    
    let getMethodResult = getMethod(plus);
    //在这里打印:
    //again
    //20
    console.log(getMethodResult(4, 8, 8));
    //在这里打印:
    //20
    console.log(getMethodResult(4, 8, 8));
    let getMethodResult_multiple = getMethod(multiple);
    //在这里打印:
    //again
    //256
    console.log(getMethodResult_multiple(4, 8, 8));
    //在这里打印:
    //256
    console.log(getMethodResult_multiple(4, 8, 8));
    
# 迭代器模式
> 除了某一些古代的语言,现代的程序语言都实现了内置迭代器,迭代器模式或许从来都没有被人所听说过,我们今天就用JavaScript来模拟迭代器模式

    function each(arr, func) {
        for(let [key, value] of arr.entries()) {
            func.call(this, key, value);
        }
    }
    
    //在这里打印:
    //0 2
    //1 6
    //2 8
    each([2, 6, 8], function (index, item) {
        console.log(index, item);
    });
    
> 这只是内部迭代器模式,将迭代逻辑放在内部实现,但是这样做很不灵活,比如我要实现一个俩数组是否相等的函数compare,你会发现compare的实现方式并不美观,且很不灵活

    function each(arr, func) {
        for(let [key, value] of arr.entries()) {
            func.call(this, key, value);
        }
    }
    
    function compare(arr, arrAno) {
        if(arr.length !== arrAno.length) {
            throw new Error("两个数组不相同");
        }
        each(arr, function (index, item) {
            if(item !== arrAno[index]) {
                throw new Error("两个数组不相同");
            }
        });
        console.log("两个数组是相同的");
    }
    
    //在这里打印:
    //两个数组是相同的
    compare([1, 2, 5], [1, 2, 5]);
    //在这里报错:
    //两个数组不相同
    compare([1, 2, 8], [1, 3, 6]);
    
## 外部迭代模式
> 后来出现了外部迭代模式,代码如下,这种迭代模式,灵活的解决了外部传入迭代器时,一些比较复杂的需求,维护性、扩展性、灵活性都很高,且针对对象和数组,只要拥有length属性的对象都可以进行迭代

    function Iterator(obj) {
        let index = 0,
            length = obj.length;
        function next() {
            index++;
        }    
        function isDone() {
            return index < length;
        }
        function getCurrentItem() {
            return obj[index];
        }
        return {
            length,
            next,
            isDone,
            getCurrentItem
        }
    }
    let iterator_arr = Iterator([55, 66, 99, 10, 1, 11, 28, 32]);
    //在这里打印:
    //55
    //66
    //99
    //10
    //1
    //11
    //28
    //32
    while(iterator_arr.isDone()) {
        console.log(iterator_arr.getCurrentItem());
        iterator_arr.next();
    }
    
> 这样的话,我们来编写compare函数进行两个函数比对时,就会灵活,更可维护的多

    function Iterator(obj) {
        let index = 0,
            length = obj.length;
        
        function next() {
            index++;
        }
        
        function getCurrentItem() {
            return obj[index];
        }
        
        function isDone() {
            return index >= length;
        }
        
        return {
            length,
            isDone,
            getCurrentItem,
            next
        }; 
    }
    
    function compare(arr, arrAno) {
        if(arr.length !== arrAno.length) {
            throw new Error("两个数组不相同");
        }
        while(!arr.isDone() && !arrAno.isDone()) {
            if(arr.getCurrentItem() !== arrAno.getCurrentItem()) {
                throw new Error("两个数组不相同");
            }
            arr.next();
            arrAno.next();
        }
        console.log("两个数组是相同的");
    }
    
    let iterator = Iterator([1, 6, 8, 10, 55, 25, 36, 96]);
    let iterator_ano = Iterator([1, 6, 8, 10, 55, 25, 36, 96]);
    let iterator_diff = Iterator([1, 6, 8, 10, 55, 25, 36, 96]);
    let iterator_diff_ano = Iterator([1, 6, 8, 10, 55, 28, 36, 96]);
    //在这里打印:
    //两个数组是相同的
    compare(iterator, iterator_ano);
    //在这里报错:
    //两个数组不相同
    compare(iterator_diff, iterator_diff_ano);

> jQuery中的each方法,就提供了迭代的功能,但是each方法不仅可以迭代数组,还可以迭代对象,我们来看一下each方法的源代码实现方式

    $.each = function (obj, func) {
        let value,
            i = 0,
            length = obj.length;
        if(Object.prototype.toString.call(obj) === "[object Array]") {
            for(; i < length; i++) {
                value = func.call(this, i, obj[i]);
                if(value === false) {
                    break;
                }
            }
        } else {
            for(i in obj) {
                value = func.call(this, i, obj[i]);
                if(value === false) {
                    break;
                }
            }
        }
    }
    
    //在这里打印:
    //0 5
    //1 8
    //2 10
    $.each([5, 8, 10, 3, 66], function (index, item) {
        if(item === 3) {
            return false;
        }
        console.log(index, item);
    });
    
> 这期间还使用了中断迭代器模式的判断语句 if(value === false) break;当函数返回false的时候,就将迭代器终止掉,直接break出for循环,下面我们来介绍反向迭代函数,我们分分钟搞定

    function reverseEach(obj, func) {
        let value;
        for(let l = obj.length - 1; l >=0; l--) {
            value = func.call(this, l, obj[l]);
            if(value === false) {
                break;
            }
        }
    }
    
    //在这里打印:
    //4 101
    //3 99
    //2 66
    reverseEach([10, 88, 66, 99, 101], function (index, item) {
        if(item === 88) {
            return false;
        }
        console.log(index, item);
    });

    

        
    
    
    
    
    
    
    

    

    
    

    

        
    
    
    
