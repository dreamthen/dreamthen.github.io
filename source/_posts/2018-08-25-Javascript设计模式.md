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

    

    

        
    
    
    
