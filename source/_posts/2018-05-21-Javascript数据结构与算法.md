---
title: 2018-05-21 Javascript数据结构与算法
date: 2018-05-21 18:51:24
tags: [Javascript, 数据结构, 算法]
categories: Javascript数据结构和算法
---
# 栈 Stack
> 栈是数据结构中比较简单的顺序数据结构,特点是: <b>后进先出</b>,新的元素或者你也可以理解为待删除的元素更接近与栈顶,而旧的元素更接近于栈底,生活中有很多栈的例子,比如说堆在一起的书,再比如说特别拥挤的地铁,你可以理解为任何只有一个出口的事物,都可以作为栈来使用,在Javascript中,我们可以使用数组来模拟栈的实现,首先是ES5版本
    
    //全局声明一个数组变量: stack_mock
    let stack_mock = [];
    //声明一个函数,这里当作栈Stack的类
    function Stack (){
        
    }
    
    //向栈内添加元素
    Stack.prototype.push = function(element) {
        return stack_mock.push(element);
    };
    
    //栈顶删除元素
    Stack.prototype.pop = function() {
        return stack_mock.pop();
    };
    
    //校验栈是否为空
    Stack.prototype.isEmpty = function() {
        return stack_mock.length === 0;
    };
    
    //获取栈顶的元素
    Stack.prototype.peek = function() {
        let len = stack_mock.length;
        return stack_mock[len - 1];  
    };
    
    //获取栈内元素的个数
    Stack.prototype.size = function() {
        return stack_mock.length;
    };
    
    //对栈内所有元素进行打印
    Stack.prototype.print = function() {
        return stack_mock.toString();
    };
    
    //对栈进行清空
    Stack.prototype.clear = function() {
        stack_mock = [];
    };

    
