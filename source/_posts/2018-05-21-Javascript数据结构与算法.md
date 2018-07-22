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
    
    //声明一个栈Stack类的实例
    let stack = new Stack();
    //在这里打印栈是否为空
    //这里打印:
    //true
    console.log(stack.isEmpty());
    //向栈中添加元素
    stack.push("Gary");
    stack.push("Lily");
    stack.push("Frank");
    stack.push("Simon");
    //在这里打印添加元素之后的返回值
    //这里打印栈内的元素个数:
    //5
    console.log(stack.push("Aaron"));
    //在这里打印栈是否为空
    //这里打印:
    //false
    console.log(stack.isEmpty());
    //在这里打印栈内元素的个数
    //这里打印:
    //5
    console.log(stack.size());
    //在这里打印栈顶的元素
    //这里打印:
    //"Aaron"
    console.log(stack.peek());
    //在这里打印栈内所有的元素
    //这里打印:
    //Gary,Lily,Frank,Simon,Aaron
    console.log(stack.print());
    //在这里对栈内元素从栈顶进行删除
    //这里打印:
    //Aaron
    console.log(stack.pop());
    //在这里打印栈内元素的个数
    //这里打印:
    //4
    console.log(stack.size());
    //在这里打印栈顶的元素
    //这里打印:
    //"Simon"
    console.log(stack.peek());
    //对栈进行清空
    stack.clear();
    //在这里打印栈是否为空
    //这里打印:
    //true
    console.log(stack.isEmpty());
    //在这里打印栈内元素的个数
    //这里打印:
    //0
    console.log(stack.size());
    
> 这种方式stack_mock数组变量暴露在全局中,其他人可以随意修改,很不安全,且一个类的实例只能对应一个类似stack_mock的数组变量,很不方便,所以最好放在类的内部或者与类进行映射,下面是改进之后的ES6版本

    //声明一个类函数,这里当作栈Stack的类
    class Stack {
        constructor() {
            //在类函数内部定义stack_mock属性,并初始化为空数组
            this["stack_mock"] = [];
        }
        
        //向栈内添加元素
        push(element) {
            return this["stack_mock"].push(element);
        }
        
        //栈顶删除元素
        pop() {
            return this["stack_mock"].pop();
        }
        
        //校验栈是否为空
        isEmpty() {
            return this["stack_mock"].length === 0;
        }
        
        //获取栈顶元素
        peek() {
            let len = this["stack_mock"].length;
            return this["stack_mock"][len - 1];
        }
        
        //获取栈内元素的个数
        size() {
            return this["stack_mock"].length;
        }
        
        //对栈内所有元素进行打印
        print() {
            return this["stack_mock"].toString();
        }
        
        //对栈进行清空
        clear() {
            this["stack_mock"] = [];
        }
    }
    
    //声明一个栈Stack类的实例
    let stack = new Stack();
    //在这里打印栈是否为空
    //这里打印:
    //true
    console.log(stack.isEmpty());
    //向栈中添加元素
    stack.push("Gary");
    stack.push("Lily");
    stack.push("Frank");
    stack.push("Simon");
    //在这里打印添加元素之后的返回值
    //这里打印栈内的元素个数:
    //5
    console.log(stack.push("Aaron"));
    //在这里打印栈是否为空
    //这里打印:
    //false
    console.log(stack.isEmpty());
    //在这里打印栈内元素的个数
    //这里打印:
    //5
    console.log(stack.size());
    //在这里打印栈顶的元素
    //这里打印:
    //"Aaron"
    console.log(stack.peek());
    //在这里打印栈内所有的元素
    //这里打印:
    //Gary,Lily,Frank,Simon,Aaron
    console.log(stack.print());
    //在这里对栈内元素从栈顶进行删除
    //这里打印:
    //Aaron
    console.log(stack.pop());
    //在这里打印栈内元素的个数
    //这里打印:
    //4
    console.log(stack.size());
    //在这里打印栈顶的元素
    //这里打印:
    //"Simon"
    console.log(stack.peek());
    //对栈进行清空
    stack.clear();
    //在这里打印栈是否为空
    //这里打印:
    //true
    console.log(stack.isEmpty());
    //在这里打印栈内元素的个数
    //这里打印:
    //0
    console.log(stack.size());
    
> 这种方式不仅避免了数组变量暴露在全局被随意修改的风险,还避免了一个数组变量只能对应一个类的实例的窘境,但是在类函数内部的属性,通过实例是可以进行获取和修改的,所以内部属性被随意修改的问题又暴露了出来,类似于这样
    
    //声明一个栈Stack类的实例
    let stack = new Stack();
    //获取到类函数内部属性"stack_mock"
    let stack_mock = stack["stack_mock"];
    //在这里打印栈是否为空
    //这里打印:
    //true
    console.log(stack.isEmpty());
    //向栈中添加元素
    stack.push("Gary");
    stack.push("Lily");
    stack.push("Frank");
    stack.push("Simon");
    //在这里打印添加元素之后的返回值
    //这里打印栈内的元素个数:
    //5
    console.log(stack.push("Aaron"));
    //设置类函数内部属性"stack_mock"为空数组
    stack["stack_mock"] = [];
    //在这里打印栈是否为空
    //这里打印:
    //true
    console.log(stack.isEmpty());
    //在这里打印栈内元素的个数
    //这里打印:
    //0
    console.log(stack.size());
    //在这里打印栈顶的元素
    //这里打印:
    //undefined
    console.log(stack.peek());
    //在这里打印栈内所有的元素
    //这里打印:
    //""
    console.log(stack.print());
    //在这里对栈内元素从栈顶进行删除
    //这里打印:
    //undefined
    console.log(stack.pop());
    //在这里打印栈内元素的个数
    //这里打印:
    //0
    console.log(stack.size());
    //在这里打印栈顶的元素
    //这里打印:
    //undefined
    console.log(stack.peek());
    //对栈进行清空
    stack.clear();
    //在这里打印栈是否为空
    //这里打印:
    //true
    console.log(stack.isEmpty());
    //在这里打印栈内元素的个数
    //这里打印:
    //0
    console.log(stack.size());
    
> 明明已经添加到栈内的元素,直接被外部设置内部属性为空数组,给删除掉了,这岂不是很尴尬,所以想要利用Symbol ES6中这种枚举新语法进行改进
    
    //声明一个可公用的Symbol的枚举变量: stack_mock
    //为了避免此变量在全局中可以轻易拿到并进行随意修改,在外包一层自执行函数表达式,用函数作用域来保证它在全局中拿不到,且也修改不了
    let Stack = (function (){
        let stack_mock = Symbol();
        //声明一个类函数,这里当作栈Stack的类
        class Stack {
            constructor() {
                //在类函数内部定义stack_mock Symbol属性,并初始化为空数组
                this[stack_mock] = [];
            }
            
            //向栈内添加元素
            push(element) {
                return this[stack_mock].push(element);
            }
            
            //栈顶删除元素
            pop() {
                return this[stack_mock].pop();
            }
            
            //校验栈是否为空
            isEmpty() {
                return this[stack_mock].length === 0;
            }
            
            //获取栈顶元素
            peek() {
                let len = this[stack_mock].length;
                return this[stack_mock][len - 1];
            }
            
            //获取栈内元素的个数
            size() {
                return this[stack_mock].length;
            }
            
            //对栈内所有元素进行打印
            print() {
                return this[stack_mock].toString();
            }
            
            //对栈进行清空
            clear() {
                this[stack_mock] = [];
            }
        }
        //返回类函数Stack
        return Stack;
    })();
    
    //声明一个栈Stack类的实例
    let stack = new Stack();
    //在这里打印栈是否为空
    //这里打印:
    //true
    console.log(stack.isEmpty());
    //向栈中添加元素
    stack.push("Gary");
    stack.push("Lily");
    stack.push("Frank");
    stack.push("Simon");
    //在这里打印添加元素之后的返回值
    //这里打印栈内的元素个数:
    //5
    console.log(stack.push("Aaron"));
    //在这里打印栈是否为空
    //这里打印:
    //false
    console.log(stack.isEmpty());
    //在这里打印栈内元素的个数
    //这里打印:
    //5
    console.log(stack.size());
    //在这里打印栈顶的元素
    //这里打印:
    //"Aaron"
    console.log(stack.peek());
    //在这里打印栈内所有的元素
    //这里打印:
    //Gary,Lily,Frank,Simon,Aaron
    console.log(stack.print());
    //在这里对栈内元素从栈顶进行删除
    //这里打印:
    //Aaron
    console.log(stack.pop());
    //在这里打印栈内元素的个数
    //这里打印:
    //4
    console.log(stack.size());
    //在这里打印栈顶的元素
    //这里打印:
    //"Simon"
    console.log(stack.peek());
    //对栈进行清空
    stack.clear();
    //在这里打印栈是否为空
    //这里打印:
    //true
    console.log(stack.isEmpty());
    //在这里打印栈内元素的个数
    //这里打印:
    //0
    console.log(stack.size());
    
> 这时候外部类的实例,看样子好想完全拿不到内部的Symbol枚举属性,其实有两种方式可以完全拿到:getOwnPropertySymbols(仅可以拿到对象的Symbol枚举属性,包含继承)和Reflect.ownKeys(无论是Symbol枚举属性还是对象自身所拥有的属性都可以拿到,也包含继承),这时候去获取到Symbol枚举属性,并进行设置为空数组,依然可以在外部删除内部枚举属性数组的元素,类似于这样

    //声明一个栈Stack类的实例
    let stack = new Stack();
    //在这里打印栈是否为空
    //这里打印:
    //true
    console.log(stack.isEmpty());
    //向栈中添加元素
    stack.push("Gary");
    stack.push("Lily");
    stack.push("Frank");
    stack.push("Simon");
    //在这里打印添加元素之后的返回值
    //这里打印栈内的元素个数:
    //5
    console.log(stack.push("Aaron"));
    //获取内部的Symbol枚举属性
    //两种方式都可以
    //let stack_mock = Object.getOwnPropertySymbols(stack)[0];
    let stack_mock = Reflect.ownKeys(stack)[0];
    //设置内部的Symbol枚举属性值为空数组
    stack[stack_mock] = [];
    //在这里打印栈是否为空
    //这里打印:
    //true
    console.log(stack.isEmpty());
    //在这里打印栈内元素的个数
    //这里打印:
    //0
    console.log(stack.size());
    //在这里打印栈顶的元素
    //这里打印:
    //undefined
    console.log(stack.peek());
    //在这里打印栈内所有的元素
    //这里打印:
    //""
    console.log(stack.print());
    //在这里对栈内元素从栈顶进行删除
    //这里打印:
    //undefined
    console.log(stack.pop());
    //在这里打印栈内元素的个数
    //这里打印:
    //0
    console.log(stack.size());
    //在这里打印栈顶的元素
    //这里打印:
    //undefined
    console.log(stack.peek());
    //对栈进行清空
    stack.clear();
    //在这里打印栈是否为空
    //这里打印:
    //true
    console.log(stack.isEmpty());
    //在这里打印栈内元素的个数
    //这里打印:
    //0
    console.log(stack.size());
    
> 针对这种情况,尝试使用WeakMap集合来解决,WeakMap是Map的一种形式,它只能设置key为对象的属性,且在无法通过类实例的任何方法来获取并设置

    let Stack = (function (){
        //声明一个可公用的WeakMap的集合变量: stack_mock
        //为了避免此变量在全局中可以轻易拿到并进行随意修改,在外包一层自执行函数表达式,用函数作用域来保证它在全局中拿不到,且也修改不了
        let stack_mock = new WeakMap();
        //声明一个类函数,这里当作栈Stack的类
        class Stack {
            constructor() {
                //在类函数内部通过WeakMap集合变量设置本类,并初始化为空数组
                stack_mock.set(this, []);
            }
            
            //向栈内添加元素
            push(element) {
                let stack_arr = stack_mock.get(this);
                let stack_index = stack_arr.push(element);
                stack_mock.set(this, stack_arr);
                return stack_index;
            }
            
            //栈顶删除元素
            pop() {
                let stack_arr = stack_mock.get(this);
                let stack_item = stack_arr.pop();
                stack_mock.set(this, stack_arr);
                return stack_item;
            }
            
            //校验栈是否为空
            isEmpty() {
                let stack_arr = stack_mock.get(this);
                return stack_arr.length === 0;
            }
            
            //获取栈顶元素
            peek() {
                let stack_arr = stack_mock.get(this),
                    len = stack_arr.length;
                return stack_arr[len - 1];
            }
            
            //获取栈内元素的个数
            size() {
                let stack_arr = stack_mock.get(this);
                return stack_arr.length;
            }
            
            //对栈内所有元素进行打印
            print() {
                let stack_arr = stack_mock.get(this);
                return stack_arr.toString();
            }
            
            //对栈进行清空
            clear() {
                stack_mock.set(this, []);
            }
        }
        //返回类函数Stack
        return Stack;
    })();
    //声明一个栈Stack类的实例
    let stack = new Stack();
    //在这里打印栈是否为空
    //这里打印:
    //true
    console.log(stack.isEmpty());
    //向栈中添加元素
    stack.push("Gary");
    stack.push("Lily");
    stack.push("Frank");
    stack.push("Simon");
    //在这里打印添加元素之后的返回值
    //这里打印栈内的元素个数:
    //5
    console.log(stack.push("Aaron"));
    //在这里打印栈是否为空
    //这里打印:
    //false
    console.log(stack.isEmpty());
    //在这里打印栈内元素的个数
    //这里打印:
    //5
    console.log(stack.size());
    //在这里打印栈顶的元素
    //这里打印:
    //"Aaron"
    console.log(stack.peek());
    //在这里打印栈内所有的元素
    //这里打印:
    //Gary,Lily,Frank,Simon,Aaron
    console.log(stack.print());
    //在这里对栈内元素从栈顶进行删除
    //这里打印:
    //Aaron
    console.log(stack.pop());
    //在这里打印栈内元素的个数
    //这里打印:
    //4
    console.log(stack.size());
    //在这里打印栈顶的元素
    //这里打印:
    //"Simon"
    console.log(stack.peek());
    //对栈进行清空
    stack.clear();
    //在这里打印栈是否为空
    //这里打印:
    //true
    console.log(stack.isEmpty());
    //在这里打印栈内元素的个数
    //这里打印:
    //0
    console.log(stack.size());
    
> 这样就完美的写出了一个栈 Stack类函数,内部WeakMap集合属性设置类的数组,不可获取且修改,全局下也不可轻易的拿到且进行随意的修改,具有良好的封装性、安全性、扩展性以及可维护性

## 使用栈解决计算机科学中的经典算法问题
### 十进制转化为二进制
> 首先你要知道十进制转化二进制的原理,先从二进制转化为十进制说起,二进制中只有0和1,在相加时就是足2进1,比如说10这个十进制整数,转化为二进制就是1010,二进制分离转化十进制:1 \* 2^3 + 0 \* 2^2 + 1 \* 2^1 + 0 \* 2^0相加就是10这个十进制整数,所以十进制转化为二进制,就需要对2取余,取余之后再除以2到达下一位数,依次将余数添加进栈中,再依次从栈顶取出并删除栈顶元素,十进制转化为二进制是遵从栈<b>后进先出</b>的特点的

    let Stack = (function (){
        //声明一个可公用的WeakMap的集合变量: stack_mock
        //为了避免此变量在全局中可以轻易拿到并进行随意修改,在外包一层自执行函数表达式,用函数作用域来保证它在全局中拿不到,且也修改不了
        let stack_mock = new WeakMap();
        //声明一个类函数,这里当作栈Stack的类
        class Stack {
            constructor() {
                //在类函数内部通过WeakMap集合变量设置本类,并初始化为空数组
                stack_mock.set(this, []);
            }
            
            //向栈内添加元素
            push(element) {
                let stack_arr = stack_mock.get(this);
                let stack_index = stack_arr.push(element);
                stack_mock.set(this, stack_arr);
                return stack_index;
            }
            
            //栈顶删除元素
            pop() {
                let stack_arr = stack_mock.get(this);
                let stack_item = stack_arr.pop();
                stack_mock.set(this, stack_arr);
                return stack_item;
            }
            
            //校验栈是否为空
            isEmpty() {
                let stack_arr = stack_mock.get(this);
                return stack_arr.length === 0;
            }
            
            //获取栈顶元素
            peek() {
                let stack_arr = stack_mock.get(this),
                    len = stack_arr.length;
                return stack_arr[len - 1];
            }
            
            //获取栈内元素的个数
            size() {
                let stack_arr = stack_mock.get(this);
                return stack_arr.length;
            }
            
            //对栈内所有元素进行打印
            print() {
                let stack_arr = stack_mock.get(this);
                return stack_arr.toString();
            }
            
            //对栈进行清空
            clear() {
                stack_mock.set(this, []);
            }
        }
        //返回类函数Stack
        return Stack;
    })();
    
    /**进行十进制转化为二进制的函数
     * @params decimal 传进去的十进制参数
     */
    let DecimalConversionBinary = (decimal)=> {
        //声明一个栈Stack类的实例
        let stack = new Stack(),
            //声明一个承接%2之后的余数的变量
            decimal_remainder,
            //声明一个承接最终二进制的字符串变量,初始化为空字符串
            result_binary = "",
            //声明一个承接十进制的变量
            decimal_integer = decimal;
        //在十进制的变量除以2还不为0时,继续执行循环    
        while(decimal_integer / 2){
            //将十进制的变量对2进行取余,余数赋值给承接余数的变量
            decimal_remainder = decimal_integer % 2;
            //将余数添加进栈中
            stack.push(decimal_remainder);
            //十进制的变量取余后,再除以2向下取整,到达下一位数,复制给十进制的变量
            decimal_integer = Math.floor(decimal_integer / 2);
        }
        //检测栈是否为空,如果不为空,则继续执行循环
        while(!stack.isEmpty()){
            //承接二进制字符串的变量不断的拼接栈顶的元素,而栈顶元素也不断在被删除
            result_binary += stack.pop();
        }
        //待到栈顶元素彻底删除完毕,栈为空栈了,就返回最终的二进制变量
        return result_binary;
    };
    let binary = DecimalConversionBinary(10);
    //在这里打印:
    //1010
    console.log(binary);
    
### 十进制转化为任何进制

> 十进制转化为任何进制的原理跟二进制是一样的,只不过除以的数值变了,所以需要外部传入,这样做的比较通用

     let Stack = (function (){
         //声明一个可公用的WeakMap的集合变量: stack_mock
         //为了避免此变量在全局中可以轻易拿到并进行随意修改,在外包一层自执行函数表达式,用函数作用域来保证它在全局中拿不到,且也修改不了
         let stack_mock = new WeakMap();
         //声明一个类函数,这里当作栈Stack的类
         class Stack {
             constructor() {
                 //在类函数内部通过WeakMap集合变量设置本类,并初始化为空数组
                 stack_mock.set(this, []);
             }
             
             //向栈内添加元素
             push(element) {
                 let stack_arr = stack_mock.get(this);
                 let stack_index = stack_arr.push(element);
                 stack_mock.set(this, stack_arr);
                 return stack_index;
             }
             
             //栈顶删除元素
             pop() {
                 let stack_arr = stack_mock.get(this);
                 let stack_item = stack_arr.pop();
                 stack_mock.set(this, stack_arr);
                 return stack_item;
             }
             
             //校验栈是否为空
             isEmpty() {
                 let stack_arr = stack_mock.get(this);
                 return stack_arr.length === 0;
             }
             
             //获取栈顶元素
             peek() {
                 let stack_arr = stack_mock.get(this),
                     len = stack_arr.length;
                 return stack_arr[len - 1];
             }
             
             //获取栈内元素的个数
             size() {
                 let stack_arr = stack_mock.get(this);
                 return stack_arr.length;
             }
             
             //对栈内所有元素进行打印
             print() {
                 let stack_arr = stack_mock.get(this);
                 return stack_arr.toString();
             }
             
             //对栈进行清空
             clear() {
                 stack_mock.set(this, []);
             }
         }
         //返回类函数Stack
         return Stack;
     })();
     
     /**进行十进制转化为任何进制的函数
      * @params decimal 传进去的十进制参数
      * @params radix 表示十进制要转化的进制类型
      */
     let DecimalConversionRadix = (decimal, radix)=> {
         //声明一个栈Stack类的实例
         let stack = new Stack(),
             //声明一个承接%radix之后的余数的变量
             decimal_remainder,
             //声明一个承接最终外部传入进制的字符串变量,初始化为空字符串
             result_radix = "",
             //声明一个承接十进制的变量
             decimal_integer = decimal,
             //各个进制栈中的进制位数所对应的字符文本,最多十六进制,最少二进制
             radix_formatter = "0123456789ABCDEF";
         //在十进制的变量除以radix还不为0时,继续执行循环    
         while(decimal_integer / radix){
             //将十进制的变量对radix进行取余,余数赋值给承接余数的变量
             decimal_remainder = decimal_integer % radix;
             //将余数添加进栈中
             stack.push(decimal_remainder);
             //十进制的变量取余后,再除以radix向下取整,到达下一位数,复制给十进制的变量
             decimal_integer = Math.floor(decimal_integer / radix);
         }
         //检测栈是否为空,如果不为空,则继续执行循环
         while(!stack.isEmpty()){
             //承接外部传入进制字符串的变量不断的拼接栈顶的元素所对应的字符文本,而栈顶元素也不断在被删除
             result_radix += radix_formatter[stack.pop()];
         }
         //待到栈顶元素彻底删除完毕,栈为空栈了,就返回最终的外部传入进制变量
         return result_radix;
     };
     //这里传入的进制类型是二进制
     let radix = DecimalConversionRadix(10, 2);
     //在这里打印:
     //1010
     console.log(radix);
     //这里传入的进制类型是十六进制
     let radix_ano = DecimalConversionRadix(100, 16);
     //在这里打印:
     //64
     console.log(radix_ano);
    
# 队列 Queue
> 队列也是数据结构中比较简单的顺序数据结构,和栈相似,特点是: <b>先进先出</b>,新的元素都会添加到队列的末尾,等待队列中之前已经添加的元素删除掉,现实生活中也有好多队列的例子,排队就是很常见的例子,在医院排队挂号、在食堂排队打饭、在抢票软件中排队抢票等等一系列都是队列的表现,经过栈Stack一系列的对类函数Stack的优化改进,在和栈Stack相似的队列Queue这里就不再赘述,我们直接写最终的优化改进的ES6版本
    
        let Queue = (function() {
            //声明一个可公用的WeakMap的集合变量: queue_mock
            //为了避免此变量在全局中可以轻易拿到并进行随意修改,在外包一层自执行函数表达式,用函数作用域来保证它在全局中拿不到,且也修改不了
            let queue_mock = new WeakMap();
            //声明一个类函数,这里当作队列Queue的类
            class Queue {
                constructor(){
                    //在类函数内部通过WeakMap集合变量设置本类,并初始化为空数组
                    queue_mock.set(this, []);
                }
                
                //向队列末尾中添加新的元素
                enqueue(element) {
                    let queue_arr = queue_mock.get(this);
                    let queue_index = queue_arr.push(element);
                    queue_mock.set(this, queue_arr);
                    return queue_index;
                }
                
                //将队列列头的元素删除掉
                dequeue() {
                    let queue_arr = queue_mock.get(this);
                    let queue_item = queue_arr.shift();
                    queue_mock.set(this, queue_arr);
                    return queue_item;
                }
                
                //检测队列是否为空
                isEmpty() {
                    return queue_mock.get(this).length === 0;
                }
                
                //获取队列中元素的个数
                size() {
                    return queue_mock.get(this).length;
                }
                
                //将队列清空
                clear() {
                    queue_mock.set(this, []);
                }
                
                //将队列中所有的元素进行打印
                print() {
                    return queue_mock.get(this).toString();
                }
                
                //获取队列列头的元素
                front() {
                    return queue_mock.get(this)[0];
                }
            }
        })();
        
        //声明一个队列Queue类实例
        let queue = new Queue();
        //这里判断队列是否为空
        //在这里打印:
        //true
        console.log(queue.isEmpty());
        //向队列中添加元素
        queue.enqueue("Gary");
        queue.enqueue("Lily");
        queue.enqueue("Simon");
        queue.enqueue("Aaron");
        //这里打印队列添加元素的返回值
        //在这里打印队列中元素的个数:
        //5
        console.log(queue.enqueue("Frank"));
        //这里判断队列是否为空
        //在这里打印:
        //false
        console.log(queue.isEmpty());
        //这里打印队列中元素的个数
        //在这里打印:
        //5
        console.log(queue.size());
        //这里打印队列中列头的元素
        //在这里打印:
        //"Gary"
        console.log(queue.front());
        //这里打印队列中所有的元素
        //在这里打印:
        //Gary,Lily,Simon,Aaron,Frank
        console.log(queue.print());
        //这里将队列列头的元素删除
        //在这里打印列头的元素:
        //"Gary"
        console.log(queue.dequeue());
        queue.dequeue();
        queue.dequeue();
        //这里打印队列中元素的个数
        //在这里打印:
        //2
        console.log(queue.size());
        //这里打印队列中列头的元素
        //在这里打印:
        //"Aaron"
        console.log(queue.front());
        //将队列清空
        queue.clear();
        //这里判断队列是否为空
        //在这里打印:
        //true
        console.log(queue.isEmpty());
        //这里打印队列中元素的个数
        //在这里打印:
        //0
        console.log(queue.size());
        
## 优先队列
> 队列有时需要根据某些参数进行优先级处理,比如我们乘坐飞机,购买飞机票,分为头等舱、商务舱和经济舱,头等舱的优先级最高,经济舱的优先级最低,所以在进行队列处理时,需要根据优先级进行排列
    
    let Queue = (function () {
        //声明一个可公用的WeakMap的集合变量: queue_mock
        //为了避免此变量在全局中可以轻易拿到并进行随意修改,在外包一层自执行函数表达式,用函数作用域来保证它在全局中拿不到,且也修改不了
        let queue_mock = new WeakMap();
        //声明一个队列优先级类函数
        //生成队列元素优先级实例
        class Queue_Prior {
            constructor(element, prior) {
                this.element = element;
                this.prior = prior;
            }
        }
        //声明一个类函数,这里当作队列Queue的类
        class Queue {
            constructor() {
                //在类函数内部通过WeakMap集合变量设置本类,并初始化为空数组
                queue_mock.set(this, []);
            }
            //根据优先级向队列中添加优先级实例元素
            enqueue(element, prior) {
                //生成队列优先级实例元素
                let queue_prior = new Queue_Prior(element, prior),
                    //获取现状态的队列
                    queue_arr = queue_mock.get(this),
                    len = queue_arr.length,
                    index = 0;
                //循环现状态的队列,假如队列中存在元素优先级比实例优先级小的,就插入到小优先级队列元素之前
                while(index < len) {
                    if(queue_arr[index]["prior"] > queue_prior["prior"]) {
                        queue_arr.splice(index, 0, queue_prior);
                        queue_mock.set(this, queue_arr);
                        return index + 1;
                    }
                    index++;
                }
                //假如不存在,就直接添加到队列列尾
                index = queue_arr.push(queue_prior);
                queue_mock.set(this, queue_arr);
                return index;   
            }
            
            //对队列列头的元素进行删除
            dequeue() {
                let queue_arr = queue_mock.get(this);
                let queue_index = queue_arr.shift();
                queue_mock.set(this, queue_arr);
                return queue_index;
            }
            
            //判断队列是否为空
            isEmpty() {
                return queue_mock.get(this).length === 0;
            }
            
            //获取队列中的元素个数
            size() {
                return queue_mock.get(this).length;
            }
            
            //对队列进行清空
            clear() {
                queue_mock.set(this, []);
            }
            
            //获取队列列头的元素
            front() {
                return queue_mock.get(this)[0];
            }
            
            //对队列中的所有的元素进行打印
            print() {
                let queue_arr = queue_mock.get(this);
                let len = queue_arr.length;
                let queue_toString_arr = [];
                for(let i = 0; i < len; i++) {
                    queue_toString_arr.push(queue_arr[i]["element"]);
                }
                return queue_toString_arr.toString();
            }
        }
        //返回队列Queue队列
        return Queue;   
    })();
    
    //声明一个优先队列Queue类实例
    let queue = new Queue();
    //这里判断优先队列是否为空
    //在这里打印:
    //true
    console.log(queue.isEmpty());
    //向优先队列中添加元素
    queue.enqueue("Gary", 1);
    queue.enqueue("Lily", 2);
    queue.enqueue("Simon", 1);
    queue.enqueue("Aaron", 3);
    //这里打印优先队列添加元素的返回值
    //在这里打印优先队列添加元素的位置:
    //4
    console.log(queue.enqueue("Frank", 2));
    //这里判断优先队列是否为空
    //在这里打印:
    //false
    console.log(queue.isEmpty());
    //这里打印优先队列中元素的个数
    //在这里打印:
    //5
    console.log(queue.size());
    //这里打印优先队列中列头的元素
    //在这里打印:
    //{element: "Gary", prior: 1}
    console.log(queue.front());
    //这里打印优先队列中所有的元素
    //在这里打印:
    //Gary,Simon,Lily,Frank,Aaron
    console.log(queue.print());
    //这里将优先队列列头的元素删除
    //在这里打印列头的元素:
    //{element: "Gary", prior: 1}
    console.log(queue.dequeue());
    queue.dequeue();
    queue.dequeue();
    //这里打印优先队列中元素的个数
    //在这里打印:
    //2
    console.log(queue.size());
    //这里打印优先队列中列头的元素
    //在这里打印:
    //{element: "Frank", prior: 2}
    console.log(queue.front());
    //将优先队列清空
    queue.clear();
    //这里判断优先队列是否为空
    //在这里打印:
    //true
    console.log(queue.isEmpty());
    //这里打印优先队列中元素的个数
    //在这里打印:
    //0
    console.log(queue.size());

## 循环队列
### 使用循环队列解决计算机经典算法 - 击鼓传花
> 用队列来实现击鼓传花,再合适不过了,给定一个数组以及传递的次数作为函数的参数
    
    let Queue = (function () {
        //声明一个可公用的WeakMap的集合变量: queue_mock
        //为了避免此变量在全局中可以轻易拿到并进行随意修改,在外包一层自执行函数表达式,用函数作用域来保证它在全局中拿不到,且也修改不了
        let queue_mock = new WeakMap();
        //声明一个类函数,这里当作队列Queue的类
        class Queue {
            constructor() {
                //在类函数内部通过WeakMap集合变量设置本类,并初始化为空数组
                queue_mock.set(this, []);
            }
            
            //向队列末尾中添加新的元素
            enqueue(element) {
                let queue_arr = queue_mock.get(this);
                let queue_index = queue_arr.push(element);
                queue_mock.set(this, queue_arr);
                return queue_index;
            }
            
            //将队列列头的元素删除掉
            dequeue() {
                let queue_arr = queue_mock.get(this);
                let queue_item = queue_arr.shift();
                queue_mock.set(this, queue_arr);
                return queue_item;
            }
            
            //检测队列是否为空
            isEmpty() {
                return queue_mock.get(this).length === 0;
            }
            
            //获取队列中的元素个数
            size() {
                return queue_mock.get(this).length;
            }
            
            //对队列进行清空
            clear() {
                queue_mock.set(this, []);
            }
            
            //对队列中的所有的元素进行打印
            print() {
                return queue_mock.get(this).toString();
            }
            
            //对队列中的所有的元素进行打印
            front() {
                return queue_mock.get(this)[0];
            }
        }
        return Queue;
    })();
    
    //击鼓传花函数
    //@params queueList 数组
    //@params count 传递的次数
    function passThePaperFlower(queueList, count) {
        //声明一个循环队列Queue类的实例
        let queue = new Queue();
        //遍历数组,将数组元素添加到队列中
        for(let i = 0; i < queueList.length; i++) {
            queue.enqueue(queueList[i]);
        }
        //只要队列中的元素大于1,就继续循环
        while(queue.size() > 1) {
            //遍历传递的次数,将队列列头的元素(就是击鼓传花中要淘汰的人)删除掉,再添加到队列的列尾
            for(let j = 0; j < count; j++) {
                queue.enqueue(queue.dequeue());
            }
            //获取到传递完之后,队列列头的元素
            let queueItem = queue.dequeue();
            console.log(`${queueItem}被淘汰~`);
        }
        //返回队列中仅剩的最后的击鼓传花大赢家
        return queue.front();
    }
    //给定的进行击鼓传花的人
    let paperFlowerParticipant = ["Gary", "Lily", "Aaron", "Alice", "Simon", "Frank"];
    //队列中仅剩的最后的击鼓传花大赢家
    let finallyGet = passThePaperFlower(paperFlowerParticipant, 10);
    //对最后的击鼓传花大赢家进行打印
    console.log("最后的赢家是:" + finallyGet);
    
# 链表 LinkList

> 前面说了栈和队列简单的顺序数据结构,下面介绍一下最后的顺序数据结构: 链表 LinkList,链表相比于栈和队列的优点在于: 栈和队列会直接对内部元素进行添加、修改以及删除的操作,使得其他内存元素的位置发生改变(其他元素前移或者后移),大量的消耗内存,而链表不会破坏内存元素的位置,假如进行添加、修改以及删除的操作,直接断开中间的一个环节,将这个环节的前一个环节以及后一个环节重连就可以了,生活中也有很多链表的例子: 比如说火车,火车的车厢都是一环连着一环的,和链表差不多
    
    let LinkList = (function() {
        //定义链表头部的链表元素,并在初始化时设置为null
        //定义链表的长度,并在初始化时设置为0
        let head = new WeakMap(),
            length = new WeakMap();
        
        //声明链表元素Node对象的类函数
        //初始化有两个参数
        //@param node 现链表元素的值
        //@param next 用来链接下一个链表元素
        class Node {
            constructor(node) {
                this.node = node;
                this.next = null;
            }
        }
        
        //声明链表LinkList对象的类函数
        class LinkList {
            constructor() {
                head.set(this, null);
                length.set(this, 0);
            }

            //向链表中添加链表元素
            insert(element) {
                let headElement = head.get(this),
                    lengths = length.get(this),
                    current = headElement,
                    node = new Node(element);
                if(!headElement) {
                    headElement = node;
                } else {
                    while(current.next) {
                        current = current.next;
                    }
                    current.next = node;
                }
                lengths++;
                head.set(this, headElement);
                length.set(this, lengths);
                return lengths;
            }
            //向链表的指定位置添加链表元素
            insertAt(element, position) {
                let headElement = head.get(this),
                    lengths = length.get(this),
                    current = headElement,
                    index = 0,
                    previous,
                    node = new Node(element);
                if(position >=0 && position < lengths) {
                    if(!headElement) {
                        headElement = node;
                    } else {
                        if(position === 0) {
                            node.next = current;
                            headElement = node;
                        } else {
                            while(index++ < position) {
                                previous = current;
                                current = current.next;
                            }
                            previous.next = node;
                            node.next = current;
                        }
                    }
                    lengths++;
                    head.set(this, headElement);
                    length.set(this, lengths);
                    return position;
                }
                return false;
            }
            //删除链表中的指定链表元素
            remove(element) {
                const {indexOf, removeAt} = this;
                let index = indexOf.bind(this)(element);
                return typeof index === "number" ? removeAt.bind(this)(index) : index;
            }

            //获取指定链表元素的位置
            indexOf(element) {
                let headElement = head.get(this),
                    lengths = length.get(this),
                    current = headElement,
                    index = 0;

                while(index++ < lengths) {
                    if(element === current.node) {
                        return index - 1;
                    }
                    current = current.next;
                }
                return false;
            }

            //删除链表中指定位置的链表元素
            removeAt(position) {
                let headElement = head.get(this),
                    lengths = length.get(this),
                    index = 0,
                    previous,
                    current = headElement;
                if(position >=0 && position < lengths) {
                    if(!head) {
                        return false;
                    } else {
                        if(lengths === 1) {
                            headElement = null;
                        } else {
                            if(position === 0) {
                                headElement = current.next;
                            } else {
                                while(index++ < position) {
                                    previous = current;
                                    current = current.next;
                                }
                                previous.next = current.next;
                            }
                        }
                    }
                    lengths--;
                    head.set(this, headElement);
                    length.set(this, lengths);
                    return position;
                }
                return false;
            }

            //获取链表中所有的链表结构
            toString() {
                let headElement = head.get(this),
                    lengths = length.get(this),
                    current = headElement,
                    index = 0,
                    result = ``;
                while(index++ < lengths) {
                    result = `${result}${current.node}|~`;
                    current = current.next;
                }
                return result;
            }

            //获取链表的头部链表元素
            headElement() {
                return head.get(this).node;
            }

            //获取链表的长度
            size() {
                return length.get(this);
            }

            //判断链表是否为空
            isEmpty() {
                return length.get(this) === 0;
            }

            //获取链表的真实结构
            valueOf() {
                return head.get(this);
            }
            
            //将链表清空
            clear() {
                head.set(this, null);
                length.set(this, 0);
            }
        }
        
        //返回链表LinkList类函数
        return LinkList;
    })();
    
    //声明链表类函数的实例
    let link_list = new LinkList();
    //这里判断链表是否是空链表
    //在这里打印:
    //true
    console.log(link_list.isEmpty());
    //这里获取链表的长度
    //在这里打印:
    //0
    console.log(link_list.size());
    //这里打印链表元素的数量:
    //在这里打印:
    //1
    console.log(link_list.insert(104));
    link_list.insert(99);
    link_list.insert(155);
    link_list.insert(34);
    link_list.insert(16);
    //这里判断链表是否是空链表
    //在这里打印:
    //false
    console.log(link_list.isEmpty());
    //这里获取链表的长度
    //在这里打印:
    //5
    console.log(link_list.size());
    //这里打印链表中所有的链表元素
    //在这里打印:
    //104
    //99
    //155
    //34
    //16
    console.log(link_list.toString());
    //这里获取链表的头部链表元素
    //在这里打印:
    //104
    console.log(link_list.headElement());
    //这里在链表下标为2处插入链表元素
    //在这里打印:
    //2
    console.log(link_list.insertAt(88, 2));
    //这里打印链表中所有的链表元素
    //在这里打印:
    //104
    //99
    //88
    //155
    //34
    //16
    console.log(link_list.toString());
    //这里打印链表中所有的链表结构
    //在这里打印:
    //{element: 104, next: {element: 99, next: {element: 88, next: {element: 155, next: {element: 34, next: {element: 16, next: null}}}}}}
    console.log(link_list.valueOf());
    //这里删除链表下标为3处的链表元素
    //在这里打印:
    //3
    console.log(link_list.removeAt(3));
    link_list.removeAt(4);
    //这里打印链表中所有的链表元素
    //在这里打印:
    //104
    //99
    //88
    //34
    console.log(link_list.toString());
    //这里删除链表中链表元素为88的链表元素
    //在这里打印:
    //2
    console.log(link_list.remove(88));
    //这里打印链表中所有的链表元素
    //在这里打印:
    //104
    //99
    //34
    link_list.toString();
    //这里打印链表中的头部链表元素
    //在这里打印:
    //104
    console.log(link_list.headElement());
    link_list.clear();
    //这里判断链表是否是空链表
    //在这里打印:
    //true
    console.log(link_list.isEmpty());
    //这里获取链表的长度
    //在这里打印:
    //0
    console.log(link_list.size());
    
## 双向链表 DoublyLinkList

> 双向链表和单向链表的模式,唯一的区别: 双向链表多出了一个尾部链表元素,且链表元素类实例不仅仅有next属性,还有prev属性,next指向下一个链表元素,prev指向上一个链表元素

    let DoublyLinkList = (function() {
        //定义链表头部的链表元素,并在初始化时设置为null
        //定义链表尾部的链表元素,并在初始化时设置为null
        //定义链表的长度,并在初始化时设置为0
        let head = new WeakMap(),
            tail = new WeakMap(),
            length = new WeakMap();
        
        //声明链表元素Node对象的类函数
        //初始化有三个参数
        //@param node 现链表元素的值
        //@param next 用来链接下一个链表元素
        //@param prev 用来链接上一个链表元素
        class Node {
            constructor(node) {
                this.node = node;
                this.next = null;
                this.prev = null;
            }
        }
        
        //声明双向链表DoublyLinkList对象的类函数
        class DoublyLinkList {
            constructor() {
                head.set(this, null);
                tail.set(this, null);
                length.set(this, 0);
            }

            //向链表中添加链表元素
            insert(element) {
                let headElement = head.get(this),
                    tailElement = tail.get(this),
                    lengths = length.get(this),
                    current = headElement,
                    node = new Node(element);
                if(!headElement) {
                    headElement = node;
                    tailElement = node;
                } else {
                    while(current.next) {
                        current = current.next;
                    }
                    current.next = node;
                    node.prev = current;
                    tailElement = node;
                }
                lengths++;
                head.set(this, headElement);
                tail.set(this, tailElement);
                length.set(this, lengths);
                return lengths;
            }
            
            //向链表的指定位置添加链表元素
            insertAt(element, position) {
                let headElement = head.get(this),
                    tailElement = tail.get(this),
                    current = headElement,
                    lengths = length.get(this),
                    node = new Node(element),
                    previous,
                    index = 0;
                if(position >=0 && position < lengths) {
                    if(!headElement) {
                        headElement = node;
                        tailElement = node;
                    } else {
                        if(position === 0) {
                            node.next = current;
                            current.prev = node;
                            headElement = node;
                        } else if(position === lengths - 1) {
                            node.prev = tailElement;
                            tailElement.next = node;
                            tailElement = node;
                        } else {
                            while(index++ < position) {
                                previous = current;
                                current = current.next;
                            }
                            previous.next = node;
                            node.prev = previous;
                            node.next = current;
                            current.prev = node;
                        }
                    }
                    lengths++;
                    head.set(this, headElement);
                    tail.set(this, tailElement);
                    length.set(this, lengths);
                    return position;
                }
                return false;
            }
            
            //删除链表中指定位置的链表元素
            removeAt(position) {
                let headElement = head.get(this),
                    tailElement = tail.get(this),
                    lengths = length.get(this),
                    current = headElement,
                    index = 0,
                    previous;
                if(position >=0 && position < lengths) {
                    if(!headElement) {
                        return false;
                    } else {
                        if(lengths === 1) {
                            headElement = null;
                            tailElement = null;
                        } else {
                            if(position === 0) {
                                headElement = current.next;
                                headElement.prev = null;
                            } else if (position === lengths - 1) {
                                tailElement = tailElement.prev;
                                tailElement.next = null;
                            } else {
                                while(index++ < position) {
                                    previous = current;
                                    current = current.next;
                                }
                                previous.next = current.next;
                                current.next.prev = previous;
                            }
                        }
                        lengths--;
                        head.set(this, headElement);
                        tail.set(this, tailElement);
                        length.set(this, lengths);
                        return position;
                    }
                }
                return false;
            }

            //获取链表指定的元素位置
            indexOf(element) {
                let headElement = head.get(this),
                    lengths = length.get(this),
                    current = headElement,
                    index = 0;
                while(index++ < lengths) {
                    if(current.node === element) {
                        return index - 1;
                    }
                    current = current.next;
                }
                return false;  
            }

            //删除链表中的指定链表元素
            remove(element) {
                const {indexOf, removeAt} = this;
                let index = indexOf.bind(this)(element);
                return typeof index === "number" ? removeAt.bind(this)(index) : false;
            }

            //获取链表的长度
            size() {
                return length.get(this);
            }
            
            //判断链表是否为空数组
            isEmpty() {
                return length.get(this) === 0;
            }
            
            //打印链表中所有的链表元素
            toString() {
                let headElement = head.get(this),
                    lengths = length.get(this),
                    current = headElement,
                    index = 0,
                    result = ``;
                while(index++ < lengths) {
                    result = `${result}${current.node}~|~`;
                    current = current.next;
                }   
                return result; 
            }
            
            //获取链表中所有的链表结构
            valueOf() {
                return head.get(this);
            }
            
            //将链表清空
            clear() {
                head.set(this, null);
                tail.set(this, null);
                length.set(this, 0);
            }
            
            //获取链表的头部链表元素
            headElement() {
                return head.get(this).node;
            }
            
            //获取链表的尾部链表元素
            tailElement() {
                return tail.get(this).node;
            }
        }
        
        //返回双向链表DoublyLinkList类函数
        return DoublyLinkList;
    })();    
    
    let doubly_link = new DoublyLinkList();
    //这里打印链表是否为空链表
    //在这里打印:
    //true
    console.log(doubly_link.isEmpty());
    //这里打印链表的长度
    //在这里打印:
    //0
    console.log(doubly_link.size());
    //这里打印插入新的链表元素后链表的长度
    //在这里打印:
    //1
    console.log(doubly_link.insert(111));
    doubly_link.insert(88);
    doubly_link.insert(99);
    doubly_link.insert(77);
    doubly_link.insert(222);
    //这里打印链表是否为空链表
    //在这里打印:
    //false
    console.log(doubly_link.isEmpty());
    //这里打印链表的长度
    //在这里打印:
    //5
    console.log(doubly_link.size());
    //这里打印链表的头部链表元素
    //在这里打印:
    //111
    console.log(doubly_link.headElement());
    //这里打印链表的尾部链表元素
    //在这里打印:
    //222
    console.log(doubly_link.tailElement());
    //这里打印链表的所有链表元素
    //在这里打印:
    //111~|88~|99~|77~|222~|
    console.log(doubly_link.toString());
    //这里打印链表的所有链表结构
    //在这里打印:
    //{prev: null, element: 111, next: {prev: {//上一个链表元素 ...}, element: 88, next: {prev: {//上一个链表元素 ...}, element: 99, next: {prev: {//上一个链表元素 ...}, element: 77, next: {//上一个链表元素 ...}, element: 222, next: null}}}}}
    console.log(doubly_link.valueOf());
    //这里打印插入到3号位置的新的链表元素的下标位置
    //在这里打印:
    //3
    console.log(doubly_link.insertAt(66, 3));
    //这里打印链表的所有链表元素
    //在这里打印:
    //111~|88~|99~|66~|77~|222~|
    console.log(doubly_link.toString());
    //这里打印链表的所有链表结构
    //在这里打印:
    //{prev: null, element: 111, next: {prev: {//上一个链表元素 ...}, element: 88, next: {prev: {//上一个链表元素 ...}, element: 99, next: {prev: {//上一个链表元素 ...}, element: 66, next: {prev: {//上一个链表元素 ...}, element: 77, next: {//上一个链表元素 ...}, element: 222, next: null}}}}}}
    console.log(doubly_link.valueOf());
    //这里打印删除4号位置的链表元素的下标位置
    //在这里打印:
    //4
    console.log(doubly_link.removeAt(4));
    doubly_link.removeAt(0);
    //这里打印删除指定的链表元素的下标位置
    //在这里打印:
    //2
    doubly_link.remove(66);
    //这里打印链表的所有链表元素
    //在这里打印:
    //88~|99~|222~|
    console.log(doubly_link.toString());
    //这里打印链表的所有链表结构
    //在这里打印:
    //{prev: null, element: 88, next: {prev: {//上一个链表元素 ...}, element: 99, next: {prev: {//上一个链表元素 ...}, element: 222, next: null}}}
    console.log(doubly_link.valueOf());
    //这里打印链表的头部链表元素
    //在这里打印:
    //88
    console.log(doubly_link.headElement());
    //这里打印链表的尾部链表元素
    //在这里打印:
    //222
    console.log(doubly_link.tailElement());
    doubly_link.clear();
    //这里打印链表是否为空链表
    //在这里打印:
    //true
    console.log(doubly_link.isEmpty());
    //这里打印链表的长度
    //在这里打印:
    //0
    console.log(doubly_link.size());

# 集合
## 自己封装Set集合
> 接下来学习下一种非顺序线性数据结构,那就是集合。在实义上指的是具有某种特定性质的事物的总体,俗话讲的好,"物以类聚,人以群分",这是对集合相当恰当的写照,在ES6中,新语法对象Set也是用来实现集合的,下面我们也来封装一下Set集合,并封装一些ES6 Set语法中不存在的方法,比如:交集、并集、差集和子集

    let Set = (function () {
        //设置集合的容器,并在初始化时设置为空对象{}
        let set = new WeakMap();

        //设置集合类
        class Set {
            constructor() {
                set.set(this, {});
            }

            //在集合中添加集合项
            add(value) {
                let set_add = set.get(this);
                set_add[value] = value;
                set.set(this, set_add);
                return true;
            }

            //判断集合中是否存在此集合项
            has(value) {
                let set_has = set.get(this);
                return set_has.hasOwnProperty(value);
            }

            //删除集合中的指定集合项
            delete(value) {
                let set_delete = set.get(this);
                if(set_delete.hasOwnProperty(value)) {
                    delete set_delete[value];
                    set.set(this, set_delete);
                    return true;
                }
                return false;
            }

            //获取集合的长度
            size() {
                let set_size = set.get(this),
                    index = 0;
                for(let [key, value] of Object.entries(set_size)) {
                    index++;
                }
                return index;
            }

            //判断集合是否为空
            isEmpty() {
                let set_isEmpty = set.get(this);
                for(let [key, value] of Object.entries(set_isEmpty)) {
                    if(set_isEmpty.hasOwnProperty(key)) {
                        return false;
                    }
                }
                return true;
            }

            //获取集合的属性值数组
            values() {
                let set_values = set.get(this);
                return Object.values(set_values);
            }
            
            //清空集合
            clear() {
                set.set(this, {});
                return true;
            }

            //并集
            union(union_ano) {
                let union_this = this,
                    union_new = new Set();
                for(let [key_this, value_this] of union_this.values().entries()) {
                    union_new.add(value_this);
                }
                for(let [key_ano, value_ano] of union_ano.values().entries()) {
                    union_new.add(value_ano);
                }
                return union_new.values();
            }

            //交集
            intersection(intersection_ano) {
                let intersection_this = this,
                    intersection_new = new Set();
                for(let [key_this, value_this] of intersection_this.values().entries()) {
                    if(intersection_ano.has(value_this)) {
                        intersection_new.add(value_this);
                    }
                }
                return intersection_new.values();
            }

            //差集
            differenceSet(differenceSet_ano) {
                let differenceSet_this = this,
                    differenceSet_new = new Set();
                for(let [key, value] of differenceSet_this.values().entries()) {
                    if(!differenceSet_ano.has(value)) {
                        differenceSet_new.add(value);
                    }
                }
                return differenceSet_new.values();
            }

            //子集
            subset(subset_ano) {
                let subset_this = this;
                for(let [key, value] of subset_this.values().entries()) {
                    if(!subset_ano.has(value)) {
                        return false;
                    }
                }
                return true;
            }
        }

        //返回集合类
        return Set;
    })();

    let set = new Set();
    //这里判断集合是否为空
    //在这里打印:
    //true
    console.log(set.isEmpty());
    //这里查看集合的长度
    //在这里打印:
    //0
    console.log(set.size());
    //这里在集合中添加集合项,并返回true
    //在这里打印:
    //true
    console.log(set.add("Gary"));
    set.add("Simon");
    set.add("Frank");
    set.add("Lily");
    set.add("Alice");
    set.add("Tom");
    set.add("Tommy");
    //这里判断集合是否为空
    //在这里打印:
    //false
    console.log(set.isEmpty());
    //这里查看集合的长度
    //在这里打印:
    //7
    console.log(set.size());
    //这里判断集合中是否存在此集合项"Gary"
    //在这里打印:
    //true
    console.log(set.has("Gary"));
    //这里判断集合中是否存在此集合项"Alice"
    //在这里打印:
    //true
    console.log(set.has("Alice"));
    //这里判断集合中是否存在此集合项"Clay"
    //在这里打印:
    //false
    console.log(set.has("Clay"));
    //这里获取集合的属性值数组
    //在这里打印:
    //["Gary", "Simon", "Frank", "Lily", "Alice", "Tom", "Tommy"]
    console.log(set.values());
    //这里删除集合中的指定集合项
    //在这里打印:
    //true
    console.log(set.delete("Simon"));
    set.delete("Alice");
    //这里查看集合的长度
    //在这里打印:
    //5
    console.log(set.size());
    //这里获取集合的属性值数组
    //在这里打印:
    //["Gary", "Frank", "Lily", "Tom", "Tommy"]
    console.log(set.values());
    set.clear();
    //这里判断集合是否为空
    //在这里打印:
    //true
    console.log(set.isEmpty());
    //这里打印集合的长度
    //在这里打印:
    //0
    console.log(set.size());
    let _set = new Set();
    let _set_ano = new Set();
    _set.add(45);
    _set.add(66);
    _set.add(100);
    _set.add(52);
    _set.add(28);
    _set.add(89);
    _set_ano.add(28);
    _set_ano.add(52);
    _set_ano.add(111);
    _set_ano.add(120);
    _set_ano.add(18);
    //这里查询两个集合属于_set集合或者属于_set_ano集合的并集
    //在这里打印:
    //[45, 66, 100, 52, 28, 89, 111, 120, 18]
    console.log(_set.union(_set_ano));
    //这里查询两个集合既属于_set集合又属于_set_ano集合的交集
    //在这里打印:
    //[28, 52]
    console.log(_set.intersection(_set_ano));
    //这里查询两个集合属于_set集合但不属于_set_ano集合的差集
    //在这里打印:
    //[45, 66, 100, 89]
    console.log(_set.differenceSet(_set_ano));
    //这里查询_set集合是否是_set_ano的子集
    //在这里打印:
    //false
    console.log(_set.subset(_set_ano));
    
## ES6 Set集合
> 之前说过ES6中使用Set来表现集合,ES6的Set也有add、has、delete和clear等方法,当然size是以属性来存储集合的长度,而也拥有keys、values和entries等遍历的方式来返回属性数组、属性值数组以及[属性, 属性值]数组,但是Set并没有封装union(并集)、intersection(交集)、differenceSet(差集)和subset(子集)等方法,我们可以利用它现有的属性和方法来封装一下

    //封装ES6 Set集合union并集方法
    Set.prototype.union = function(set_ano) {
        let set_this = this,
            set_new = new Set(),
            set_union = [];
        for(let [key, value] of set_this.entries()) {
            set_new.add(key);
        }

        for(let [key, value] of set_ano.entries()) {
            set_new.add(key);
        }

        for(let [key, value] of set_new.entries()) {
            set_union = [...set_union, key];
        }

        return set_union;
    };

    //封装ES6 Set集合intersection交集方法
    Set.prototype.intersection = function(set_ano) {
        let set_this = this,
            set_new = new Set(),
            set_intersection = [];
        for(let [key, value] of set_this.entries()) {
            if(set_ano.has(key)) {
                set_new.add(key);
            }
        }

        for(let [key, value] of set_new.entries()) {
            set_intersection = [...set_intersection, key];
        }

        return set_intersection;
    };
    
    //封装ES6 Set集合differenceSet差集方法
    Set.prototype.differenceSet = function(set_ano) {
        let set_this = this,
            set_new = new Set(),
            set_differenceSet = [];
        for(let [key, value] of set_this.entries()) {
            if(!set_ano.has(key)) {
                set_new.add(key);
            }
        }

        for(let [key, value] of set_new.entries()) {
            set_differenceSet = [...set_differenceSet, key];
        }

        return set_differenceSet;
    };

    //封装ES6 Set集合subset子集方法
    Set.prototype.subset = function(set_ano) {
        let set_this = this;
        for(let [key, value] of set_this.entries()) {
            if(!set_ano.has(key)) {
                return false;
            }
        }
        return true;
    };

    let set = new Set(),
        set_ano = new Set();
    set.add(45);
    set.add(66);
    set.add(100);
    set.add(52);
    set.add(28);
    set.add(89);
    set_ano.add(28);
    set_ano.add(52);
    set_ano.add(111);
    set_ano.add(120);
    set_ano.add(18);
    //这里查询属于set集合或者属于set_ano集合的并集
    //在这里打印:
    //[45, 66, 100, 52, 28, 89, 111, 120, 18]
    console.log(set.union(set_ano));
    //这里查询既属于set集合又属于set_ano集合的交集
    //在这里打印:
    //[52, 28]
    console.log(set.intersection(set_ano));
    //这里查询属于set集合但不属于set_ano集合的差集
    //在这里打印:
    //[45, 66, 100, 89]
    console.log(set.differenceSet(set_ano));
    //这里查询set集合是否是set_ano集合的子集
    //在这里打印:
    //false
    console.log(set.subset(set_ano));

# 字典
> 除了集合这种线性的非顺序结构以外,还有两种线性的非顺序结构: 字典和散列表,如果说集合是具有某种特征性质事物的总量的话,那字典就是具有某种特征性质事物的分集(分类集合),ES6中用Map来表现字典,下面我们就来介绍一下字典

    let Map = (function () {
        //设置字典的容器,并在初始化时设置为空对象{}
        let map = new WeakMap();
        
        //定义Map字典类
        class Map {
            constructor() {
                map.set(this, {});
            }

            //在字典中添加字典项
            set(key, value) {
                let map_set = map.get(this);
                map_set[key] = value;
                map.set(this, map_set);
                return true;
            }

            //获取字典指定的字典项
            get(key) {
                let map_get = map.get(this);
                if(map_get.hasOwnProperty(key)) {
                    return map_get[key];
                }
                return false;
            }

            //判断字典是否存在指定的字典项
            has(key) {
                let map_has = map.get(this);
                return map_has.hasOwnProperty(key);
            }

            //删除字典指定的字典项
            delete(key) {
                let map_delete = map.get(this);
                if(map_delete.hasOwnProperty(key)){
                    delete map_delete[key];
                    map.set(this, map_delete);
                    return true;
                }
                return false;
            }

            //清空字典
            clear() {
                map.set(this, {});
                return true;
            }

            //获取字典的属性数组
            keys() {
                let map_keys = map.get(this);
                return Object.keys(map_keys);
            }

            //获取字典的属性值数组
            values() {
                let map_values = map.get(this);
                return Object.values(map_values);
            }

            //获取字典的长度
            size() {
                let map_size = map.get(this);
                return Object.keys(map_size).length;
            }

            //判断字典是否为空
            isEmpty() {
                let map_isEmpty = map.get(this);
                return Object.keys(map_isEmpty).length === 0;
            }
        }

        //返回Map字典类
        return Map;
    })();

    let map = new Map();
    //这里判断字典是否为空
    //在这里打印:
    //true
    console.log(map.isEmpty());
    //这里获取字典的长度
    //在这里打印:
    //0
    console.log(map.size());
    //这里在字典中添加制定的字典项
    //在这里打印:
    //true
    console.log(map.set("Gary", "gary@gmail.com"));
    map.set("Simon", "simon@gmail.com");
    map.set("Lily", "lily@gmail.com");
    map.set("Alice", "alice@gmail.com");
    map.set("Aaron", "aaron@gmail.com");
    //这里判断字典是否为空
    //在这里打印:
    //false
    console.log(map.isEmpty());
    //这里获取字典的长度
    //在这里打印:
    //5
    console.log(map.size());
    //这里获取字典指定的字典项
    //在这里打印:
    //gary@gmail.com
    console.log(map.get("Gary"));
    //这里获取字典指定的字典项
    //在这里打印:
    //lily@gmail.com
    console.log(map.get("Alice"));
    //这里判断是否存在指定的字典项
    //在这里打印:
    //true
    console.log(map.has("Lily"));
    //这里获取字典的属性数组
    //在这里打印:
    //["Gary", "Simon", "Lily", "Alice", "Aaron"]
    console.log(map.keys());
    //这里获取字典的属性值数组
    //在这里打印:
    //["gary@gmail.com", "simon@gmail.com", "lily@gmail.com", "alice@gmail.com", "aaron@gmail.com"]
    console.log(map.values());
    //这里删除字典的执行字典项
    //在这里打印:
    //true
    console.log(map.delete("Alice"));
    //这里判断是否存在指定的字典项
    //在这里打印:
    //false
    console.log(map.has("Alice"));
    //这里清空字典
    //在这里打印:
    //true
    console.log(map.clear());
    //这里获取字典指定的字典项
    //在这里打印:
    //false
    console.log(map.get("Gary"));
    //这里判断字典是否为空
    //在这里打印:
    //true
    console.log(map.isEmpty());
    //这里获取字典的长度
    //在这里打印:
    //0
    console.log(map.size());

# 散列表
> 另外一种线性非顺序数据结构就是散列表了,也就是我们在Java中常用的HashTable,当然单纯的用HashTable会出现很多问题,最显著的一点就是容易一个值被另外一个值所覆盖,下面我们来介绍一下HashTable散列表

    let HashTable = (function () {
        //设置散列表的容器,并初始化为空数组[]
        let hash_table = new WeakMap();
        
        //定义散列表类
        class HashTable {
            constructor() {
                hash_table.set(this, []);
            }

            //定义设计散列表的算法为loseLose算法
            //loseLose算法就是将HashTable中的key的每一个字符所对应的ASCII码值加上所处位置乘以任何一个质数
            //然后对任何一个质数取余
            //最后进行返回
            loseLoseHashTable(key) {
                let hash_key = 13,
                    result_index = 0;
                for(let i = 0; i < key.length; i++) {
                    result_index += i * hash_key + key.charCodeAt(i);
                }
                return result_index % 37;
            }
            
            //在散列表中添加散列表项
            put(key, value) {
                let hashTable = hash_table.get(this);
                const {loseLoseHashTable} = this;
                let index = loseLoseHashTable.bind(this)(key);
                hashTable[index] = value;
                hash_table.set(this, hashTable);
                return true;
            }

            //获取散列表指定的散列表项
            get(key) {
                let hashTable = hash_table.get(this);
                const {loseLoseHashTable} = this;
                let index = loseLoseHashTable.bind(this)(key);
                if(hashTable[index] !== undefined) {
                    return hashTable[index];
                }
                return false;
            }

            //删除散列表中指定的散列表项
            remove(key) {
                let hashTable = hash_table.get(this);
                const {loseLoseHashTable} = this;
                let index = loseLoseHashTable.bind(this)(key);
                if(hashTable[index] !== undefined) {
                    hashTable[index] = undefined;
                    hash_table.set(this, hashTable);
                    return true;
                }
                return false;
            }

            //获取散列表拥有值的字符串项
            toString() {
                let hashTable = hash_table.get(this),
                    result_str = ``;
                for(let [key, value] of hashTable.entries()) {
                    if(value !== undefined) {
                        result_str = `${result_str}${value} -> `;
                    }
                }
                return result_str;
            }

            //获取散列表的具体结构
            valueOf() {
                let hashTable = hash_table.get(this);
                return hashTable;
            }
        }

        //返回散列表类
        return HashTable;
    })();

    let hash_table = new HashTable();
    //这里在散列表中添加散列表项
    //在这里打印:
    //true
    console.log(hash_table.put("Gary", "gary@gmail.com"));
    hash_table.put("Helen", "helen@gmail.com");
    hash_table.put("Lily", "lily@gmail.com");
    hash_table.put("Alice", "alice@gmail.com");
    hash_table.put("Simon", "simon@gmail.com");
    hash_table.put("Aaron", "aaron@gmail.com");
    hash_table.put("Tom", "tom@gmail.com");
    hash_table.put("Tommy", "tommy@gmail.com");
    hash_table.put("Betty", "betty@gmail.com");
    hash_table.put("Frank", "frank@gmail.com");
    hash_table.put("Martin", "martin@gmail.com");
    //这里获取散列表指定的散列表项
    //在这里打印:
    //tommy@gmail.com
    console.log(hash_table.get("Aaron"));
    //这里获取散列表指定的散列表项
    //在这里打印:
    //tom@gmail.com
    console.log(hash_table.get("Tom"));
    //这里获取散列表拥有值的字符串项
    //在这里打印:
    //martin@gmail.com -> lily@gmail.com -> tom@gmail.com -> alice@gmail.com -> simon@gmail.com -> betty@gmail.com -> helen@gmail.com -> tommy@gmail.com -> frank@gmail.com -> 
    console.log(hash_table.toString());
    //这里获取散列表的具体结构
    //在这里打印:
    //["martin@gmail.com", empty × 6, "lily@gmail.com", empty × 2, "tom@gmail.com", empty × 5, "alice@gmail.com", empty × 2, "simon@gmail.com", empty, "betty@gmail.com", empty × 8, "helen@gmail.com", empty × 4, "tommy@gmail.com", "frank@gmail.com"]
    console.log(hash_table.valueOf());
    //这里删除散列表中指定的散列表项
    //在这里打印:
    //true
    console.log(hash_table.remove("Aaron"));
    hash_table.remove("Tom");
    //这里获取散列表中指定的散列表项
    //在这里打印:
    //false
    console.log(hash_table.get("Tom"));
    //这里获取散列表拥有值的字符串项
    //在这里打印:
    //martin@gmail.com -> lily@gmail.com -> alice@gmail.com -> simon@gmail.com -> betty@gmail.com -> helen@gmail.com -> frank@gmail.com -> 
    console.log(hash_table.toString());
    //这里获取散列表的具体结构
    //在这里打印:
    //["martin@gmail.com", empty × 6, "lily@gmail.com", empty × 2, undefined, empty × 5, "alice@gmail.com", empty × 2, "simon@gmail.com", empty, "betty@gmail.com", empty × 8, "helen@gmail.com", empty × 4, undefined, "frank@gmail.com"]
    console.log(hash_table.valueOf());

> 不知道你们注意到了没,有一些散列表项被覆盖了,比如说key属性为Aaron的散列表项的value属性值竟然是tommy@gmail.com,再比如说我将key属性为Aaron的散列表项删除掉,key属性为Tommy的散列表项也消失了,变为了undefined,说明key属性为Tommy和key属性为Aaron的散列表项经过loseLose算法解析散列表项后是同一个散列表项,所以散列表项被覆盖了,所以用单纯的用HashTable是不适当的,要解决这个比较显著的问题,有两种解决方式:链表查询以及散列表巡航迭代

## 链表查询
> 链表查询就是用链表来作为散列表项,假如已经存在loseLose算法解析散列表项后的散列表项,就添加到此位置链表的最后,这样的话就不会发生覆盖的事情了,下面我们就用链表查询来解决散列表项覆盖的问题吧

    let LinkList = (function () {
        //定义链表头部的链表元素,并在初始化时设置为null
        //定义链表的长度,并在初始化时设置为0
        let head = new WeakMap(),
            length = new WeakMap();

        //声明链表元素Node对象的类函数
        //初始化有两个参数
        //@param node 现链表元素的值
        //@param next 用来链接下一个链表元素
        class Node {
            constructor(node) {
                this.node = node;
                this.next = null;
            }
        }

        //定义链表类
        class LinkList {
            constructor() {
                head.set(this, null);
                length.set(this, 0);
            }

            //向链表中添加链表元素
            insert(element) {
                let headElement = head.get(this),
                    lengths = length.get(this),
                    current = headElement,
                    node = new Node(element);
                if(!headElement) {
                    headElement = node;
                } else {
                    while(current.next) {
                        current = current.next;
                    }
                    current.next = node;
                }
                lengths++;
                head.set(this, headElement);
                length.set(this, lengths);
                return lengths;
            }

            //向链表的指定位置添加链表元素
            insertAt(element, position) {
                let headElement = head.get(this),
                    lengths = length.get(this),
                    current = headElement,
                    index = 0,
                    previous,
                    node = new Node(element);
                if(position >= 0 && position < lengths) {
                    if(!headElement) {
                        headElement = node;
                    } else {
                        if(position === 0) {
                            node.next = current;
                            headElement = node;
                        } else {
                            while(index++ < position) {
                                previous = current;
                                current = current.next;
                            }
                            previous.next = node;
                            node.next = current;
                        }
                    }
                    lengths++;
                    head.set(this, headElement);
                    length.set(this, lengths);
                    return position;   
                }
                return false; 
            }

            //删除链表中指定位置的链表元素
            removeAt(position) {
                let headElement = head.get(this),
                    lengths = length.get(this),
                    index = 0,
                    current = headElement,
                    previous;
                if(position >= 0 && position < lengths) {
                    if(!headElement) {
                        return false;
                    } else {
                        if(lengths === 1) {
                            headElement = null;
                        } else {
                            if(position === 0) {
                                headElement = current.next;
                            } else {
                                while(index++ < position) {
                                    previous = current;
                                    current = current.next;
                                }
                                previous.next = current.next;
                            }
                        }
                        lengths--;
                        head.set(this, headElement);
                        length.set(this, lengths);
                        return position;
                    }
                }
                return false;
            }

            //删除链表中的指定链表元素
            remove(element) {
                const {indexOf, removeAt} = this;
                let index = indexOf.bind(this)(element);
                return typeof index === "number" ? removeAt.bind(this)(index) : false;
            }

            //删除链表中散列表链表查询中的链表项
            removeKey(key) {
                const {indexOfKeyPosition, removeAt} = this;
                let index = indexOfKeyPosition.bind(this)(key);
                return typeof index === "number" ? removeAt.bind(this)(index) : index;
            }

            //获取链表指定的元素位置
            indexOf(element) {
                let headElement = head.get(this),
                    lengths = length.get(this),
                    current = headElement,
                    index = 0;
                while(index++ < lengths) {
                    if(current.node === element) {
                        return index - 1;
                    }
                    current = current.next;
                }
                return false;
            }
            
            //判断链表中是否存在散列表链表查询中的key
            indexOfKey(key) {
                let headElement = head.get(this),
                    lengths = length.get(this),
                    current = headElement,
                    index = 0;
                while(index++ < lengths) {
                    if(key === current.node.key) {
                        return true;
                    }
                    current = current.next;
                }
                return false;   
            }

            //获取链表指定的散列表链表查询中的链表项位置
            indexOfKeyPosition(key) {
                let headElement = head.get(this),
                    lengths = length.get(this),
                    current = headElement,
                    index = 0;
                while(index++ < lengths) {
                    if(key === current.node.key) {
                        return index - 1;
                    }
                    current = current.next;
                }
                return false;
            }

            //获取链表中散列表链表查询中的链表项
            indexOfNode(key) {
                let headElement = head.get(this),
                    lengths = length.get(this),
                    current = headElement,
                    index = 0;
                while(index++ < lengths) {
                    if(key === current.node.key) {
                        return current.node;
                    }
                    current = current.next;
                }
                return false; 
            }

            //获取链表的长度
            size() {
                return length.get(this);
            }

            //判断链表是否为空
            isEmpty() {
                return length.get(this) === 0;
            }

            //获取链表的头部链表元素
            headElement() {
                return head.get(this).node;
            }

            //获取链表中所有的链表结构
            toString() {
                let headElement = head.get(this),
                    lengths = length.get(this),
                    current = headElement,
                    index = 0,
                    result_str = ``;
                while(index++ < lengths) {
                    result_str = `${result_str}${current.node} => `;
                    current = current.next;
                }
                return result_str;   
            }

            //获取链表中所有散列表查询的链表结构
            toStringKey() {
                let headElement = head.get(this),
                    lengths = length.get(this),
                    current = headElement,
                    index = 0,
                    result_str = ``;
                while(index++ < lengths) {
                    result_str = `${result_str}{key: ${current.node.key}, value: ${current.node.value}} => `;
                    current = current.next;
                }
                return result_str;
            }

            //获取链表的真实结构
            valueOf() {
                return head.get(this);
            }

            //将链表清空
            clear() {
                head.set(this, null);
                length.set(this, 0);
            }
        }

        //返回链表类
        return LinkList;
    })();

    let HashTable = (function (){
        //设置散列表的容器,并初始化为空数组[]
        let hash_table = new WeakMap();
        
        //设置散列表中的链表类
        //@params key
        //@params value
        class Node {
            constructor(key, value) {
                this.key = key;
                this.value = value;
            }
        }

        //设置散列表类
        class HashTable {
            constructor() {
                hash_table.set(this, []);
            }

            //定义设计散列表的算法为loseLose算法
            //loseLose算法就是将HashTable中的key的每一个字符所对应的ASCII码值加上所处位置乘以任何一个质数
            //然后对任何一个质数取余
            //最后进行返回
            loseLoseHashTable(key) {
                let hash_key = 13,
                    index = 0;
                for(let i = 0; i < key.length; i++) {
                    index += i * hash_key + key.charCodeAt(i);
                }
                return index % 37;
            }

            //在散列表中添加散列表链表查询项
            put(key, value) {
                const {loseLoseHashTable} = this;
                let hashTable = hash_table.get(this),
                    index = loseLoseHashTable.bind(this)(key),
                    node = new Node(key, value),
                    linkList;
                if(hashTable[index] === undefined) {
                    linkList = new LinkList();
                    linkList.insert(node);
                    hashTable[index] = linkList;
                } else {
                    linkList = hashTable[index];
                    if(linkList.indexOfKey(key)) {
                        return false;
                    } else {
                        linkList = hashTable[index];
                        linkList.insert(node);
                        hashTable[index] = linkList;
                    }
                }
                hash_table.set(this, hashTable);
                return true;
            }

            //获取散列表指定的散列表链表查询项
            get(key) {
                const {loseLoseHashTable} = this;
                let hashTable = hash_table.get(this),
                    index = loseLoseHashTable.bind(this)(key),
                    linkList,
                    node;
                if(hashTable[index] !== undefined) {
                    linkList = hashTable[index];
                    if(linkList.indexOfKey(key)) {
                        node = linkList.indexOfNode(key);
                        return node.value;
                    } else {
                        return false;
                    }
                }
                return false;
            }

            //删除散列表中指定的散列表链表查询项
            remove(key) {
                const {loseLoseHashTable} = this;
                let hashTable = hash_table.get(this),
                    index = loseLoseHashTable.bind(this)(key),
                    linkList;
                if(hashTable[index] !== undefined) {
                    linkList = hashTable[index];
                    if(linkList.indexOfKey(key)) {
                        linkList.removeKey(key);
                        if(linkList.isEmpty()){
                            hashTable[index] = undefined;
                        } else {
                            hashTable[index] = linkList;
                        }
                        return true;
                    } else {
                        return false;
                    }
                }
                return false;
            }

            //获取散列表链表查询拥有值的字符串项
            toString() {
                let hashTable = hash_table.get(this),
                    result_str = ``;
                for(let [key, value] of hashTable.entries()) {
                    if(value !== undefined) {
                        result_str = `${result_str}${value.toStringKey()} -> `;
                    }
                }
                return result_str;
            }

            //获取散列表链表查询的具体结构
            valueOf() {
                return hash_table.get(this);
            }
        }

        //返回散列表类
        return HashTable;
    })();

    let hash_table = new HashTable();
    //这里在散列表中添加散列表链表查询项
    //在这里打印:
    //true
    console.log(hash_table.put("Gary", "gary@gmail.com"));
    hash_table.put("Helen", "helen@gmail.com");
    hash_table.put("Lily", "lily@gmail.com");
    hash_table.put("Alice", "alice@gmail.com");
    hash_table.put("Simon", "simon@gmail.com");
    hash_table.put("Aaron", "aaron@gmail.com");
    hash_table.put("Tom", "tom@gmail.com");
    hash_table.put("Tommy", "tommy@gmail.com");
    hash_table.put("Betty", "betty@gmail.com");
    hash_table.put("Frank", "frank@gmail.com");
    hash_table.put("Martin", "martin@gmail.com");
    //这里在散列表中获取散列表链表查询项
    //在这里打印:
    //aaron@gmail.com
    console.log(hash_table.get("Aaron"));
    //这里在散列表中获取散列表链表查询项
    //在这里打印:
    //tom@gmail.com
    console.log(hash_table.get("Tom"));
    //这里获取散列表链表查询拥有值的字符串项
    //在这里打印:
    //{key: Gary, value: gary@gmail.com} => {key: Martin, value: martin@gmail.com} =>  -> {key: Lily, value: lily@gmail.com} =>  -> {key: Tom, value: tom@gmail.com} =>  -> {key: Alice, value: alice@gmail.com} =>  -> {key: Simon, value: simon@gmail.com} =>  -> {key: Betty, value: betty@gmail.com} =>  -> {key: Helen, value: helen@gmail.com} =>  -> {key: Aaron, value: aaron@gmail.com} => {key: Tommy, value: tommy@gmail.com} =>  -> {key: Frank, value: frank@gmail.com} =>  -> 
    console.log(hash_table.toString());
    //这里获取散列表链表查询的具体结构
    //在这里打印:
    //[LinkList, empty × 6, LinkList, empty × 2, LinkList, empty × 5, LinkList, empty × 2, LinkList, empty, LinkList, empty × 8, LinkList, empty × 4, LinkList, LinkList]
    console.log(hash_table.valueOf());
    //这里删除散列表中指定的散列表链表查询项
    //在这里打印:
    //true
    console.log(hash_table.remove("Aaron"));
    hash_table.remove("Tom");
    hash_table.remove("Tommy");
    //这里在散列表中获取散列表链表查询项
    //在这里打印:
    //false
    console.log(hash_table.get("Tom"));
    //这里获取散列表链表查询拥有值的字符串项
    //在这里打印:
    //{key: Gary, value: gary@gmail.com} => {key: Martin, value: martin@gmail.com} =>  -> {key: Lily, value: lily@gmail.com} =>  -> {key: Alice, value: alice@gmail.com} =>  -> {key: Simon, value: simon@gmail.com} =>  -> {key: Betty, value: betty@gmail.com} =>  -> {key: Helen, value: helen@gmail.com} =>  -> {key: Frank, value: frank@gmail.com} =>  ->
    console.log(hash_table.toString());
    //这里获取散列表链表查询的具体结构
    //在这里打印:
    //[LinkList, empty × 6, LinkList, empty × 2, undefined, empty × 5, LinkList, empty × 2, LinkList, empty, LinkList, empty × 8, LinkList, empty × 4, undefined, LinkList]
    console.log(hash_table.valueOf());

## 散列表巡航迭代
> 散列表巡航迭代其实就是利用位置迭代解决问题,假如根据loseLose算法解析散列表项后的散列表项,所在位置已经存在散列表项,就去查询所在位置的下一个位置,依次迭代下去,直到查询到位置的散列表项为没有定义的值为止,下面我们就用散列表巡航迭代来解决散列表项覆盖的问题吧

    let HashTable = (function () {
        //设置散列表的容器,并初始化为空数组[]
        let hash_table = new WeakMap();

        //设置散列表中的对象类
        //@params key
        //@params value
        class Node {
            constructor(key, value) {
                this.key = key;
                this.value = value;
            }
        }

        //设置散列表类
        class HashTable {
            constructor() {
                hash_table.set(this, []);
            }

            //定义设计散列表的算法为loseLose算法
            //loseLose算法就是将HashTable中的key的每一个字符所对应的ASCII码值加上所处位置乘以任何一个质数
            //然后对任何一个质数取余
            //最后进行返回
            loseLoseHashTable(key) {
                let hash_key = 13,
                    index = 0;
                for(let i = 0; i < key.length; i++) {
                    index += i * hash_key + key.charCodeAt(i);
                }
                return index % 37;
            }

            //在散列表中添加散列表巡航迭代项
            put(key, value) {
                const {loseLoseHashTable} = this;
                let hash_key = loseLoseHashTable.bind(this)(key),
                    hashTable = hash_table.get(this),
                    node = new Node(key, value);
                if(hashTable[hash_key] === undefined) {
                    hashTable[hash_key] = node;
                } else {
                    while(hashTable[hash_key] !== undefined) {
                        if(hashTable[hash_key].key === key) {
                            return false;
                        }
                        hash_key++;
                    }
                    if(hashTable[hash_key] === undefined) {
                        hashTable[hash_key] = node;
                    }
                }
                hash_table.set(this, hashTable);
                return true;
            }

            //获取散列表指定的散列表巡航迭代项
            get(key) {
                const {loseLoseHashTable} = this;
                let hash_key = loseLoseHashTable.bind(this)(key),
                    hashTable = hash_table.get(this);
                if(hashTable[hash_key] === undefined) {
                    return false;
                } else {
                    while(hashTable[hash_key] !== undefined) {
                        if(hashTable[hash_key].key === key) {
                            return hashTable[hash_key].value;
                        }
                        hash_key++;
                    }
                }
                return false;
            }

            //删除散列表中指定的散列表巡航迭代项
            remove(key) {
                const {loseLoseHashTable} = this;
                let hash_key = loseLoseHashTable.bind(this)(key),
                    hashTable = hash_table.get(this);
                if(hashTable[hash_key] === undefined) {
                    return false;
                } else {
                    while(hashTable[hash_key] !== undefined) {
                        if(hashTable[hash_key].key === key) {
                            hashTable[hash_key] = undefined;
                            hash_table.set(this, hashTable);
                            return true;
                        }
                        hash_key++;
                    }
                }
                return false;
            }

            //获取散列表巡航迭代拥有值的字符串项
            toString() {
                let hashTable = hash_table.get(this),
                    result_str = ``;
                for(let [key, value] of hashTable.entries()) {
                    if(value !== undefined) {
                        result_str = `${result_str}{key: ${value["key"]}, value: ${value["value"]}} -> `;
                    }
                }
                return result_str;
            }

            //获取散列表巡航迭代的具体结构
            valueOf() {
                return hash_table.get(this);
            }
        }
        
        //返回散列表类
        return HashTable;
    })();

    let hash_table = new HashTable();
    //这里在散列表中添加散列表巡航迭代项
    //在这里打印:
    //true
    console.log(hash_table.put("Gary", "gary@gmail.com"));
    hash_table.put("Helen", "helen@gmail.com");
    hash_table.put("Lily", "lily@gmail.com");
    hash_table.put("Alice", "alice@gmail.com");
    hash_table.put("Simon", "simon@gmail.com");
    hash_table.put("Aaron", "aaron@gmail.com");
    hash_table.put("Tom", "tom@gmail.com");
    hash_table.put("Tommy", "tommy@gmail.com");
    hash_table.put("Betty", "betty@gmail.com");
    hash_table.put("Frank", "frank@gmail.com");
    hash_table.put("Martin", "martin@gmail.com");
    //这里在散列表中获取散列表巡航迭代项
    //在这里打印:
    //aaron@gmail.com
    console.log(hash_table.get("Aaron"));
    //这里在散列表中获取散列表巡航迭代项
    //在这里打印:
    //tom@gmail.com
    console.log(hash_table.get("Tom"));
    //这里获取散列表巡航迭代拥有值的字符串项
    //在这里打印:
    //{key: Gary, value: gary@gmail.com} -> {key: Martin, value: martin@gmail.com} -> {key: Lily, value: lily@gmail.com} -> {key: Tom, value: tom@gmail.com} -> {key: Alice, value: alice@gmail.com} -> {key: Simon, value: simon@gmail.com} -> {key: Betty, value: betty@gmail.com} -> {key: Helen, value: helen@gmail.com} -> {key: Aaron, value: aaron@gmail.com} -> {key: Tommy, value: tommy@gmail.com} -> {key: Frank, value: frank@gmail.com} -> 
    console.log(hash_table.toString());
    //这里获取散列表巡航迭代的具体结构
    //在这里打印:
    //[Node, Node, empty × 5, Node, empty × 2, Node, empty × 5, Node, empty × 2, Node, empty, Node, empty × 8, Node, empty × 4, Node, Node, Node]
    console.log(hash_table.valueOf());
    //这里删除散列表中指定的散列表巡航迭代项
    //在这里打印:
    //true
    console.log(hash_table.remove("Aaron"));
    hash_table.remove("Tom");
    //这里在散列表中获取散列表巡航迭代项
    //在这里打印:
    //false
    console.log(hash_table.get("Tom"));
    //这里获取散列表巡航迭代拥有值的字符串项
    //在这里打印:
    //{key: Gary, value: gary@gmail.com} -> {key: Martin, value: martin@gmail.com} -> {key: Lily, value: lily@gmail.com} -> {key: Alice, value: alice@gmail.com} -> {key: Simon, value: simon@gmail.com} -> {key: Betty, value: betty@gmail.com} -> {key: Helen, value: helen@gmail.com} -> {key: Tommy, value: tommy@gmail.com} -> {key: Frank, value: frank@gmail.com} -> 
    console.log(hash_table.toString());
    //这里获取散列表巡航迭代的具体结构
    //在这里打印:
    //[Node, Node, empty × 5, Node, empty × 2, undefined, empty × 5, Node, empty × 2, Node, empty, Node, empty × 8, Node, empty × 4, undefined, Node, Node]
    console.log(hash_table.valueOf());

 ## djb2算法解决一切问题
 > 还有一种既不使用链表查询,也不使用巡航迭代的方法,那就是展示散列表更广的djb2算法,使用djb2算法就可以直接解决loseLose算法解析后散列表项覆盖的问题,下面我们就用djb2算法来解决散列表项覆盖的问题吧

    let HashTable = (function() {
        //设置散列表的容器,并初始化为空数组[]
        let hash_table = new WeakMap();

        //设置散列表类
        class HashTable {
            constructor() {
                hash_table.set(this, []);
            }

            //定义设计散列表的算法为djb2算法
            //djb2算法和loseLose算法相近,都是定义一个质数(数值比较大的质数)乘以属性的每一个字符所在的位置,再加上属性每一个字符所对应的ASCII码值
            //然后对任何一个质数(数值比较大的质数)取余
            //最后再返回
            djb2HashTable(key) {
                let hash_key = 5381,
                    index = 0;
                for(let i = 0; i < key.length; i++) {
                    index += i * hash_key + key.charCodeAt(i);
                }
                return index % 1013;    
            }

            //在散列表中添加散列表项
            put(key, value) {
                const {djb2HashTable} = this;
                let hashTable = hash_table.get(this),
                    hash_key = djb2HashTable.bind(this)(key);
                if(hashTable[hash_key] !== undefined) {
                    return false;
                }
                hashTable[hash_key] = value;
                return true;
            }

            //获取散列表指定的散列表项
            get(key) {
                const {djb2HashTable} = this;
                let hashTable = hash_table.get(this),
                    hash_key = djb2HashTable.bind(this)(key);
                if(hashTable[hash_key] === undefined) {
                    return false;
                }    
                return hashTable[hash_key];
            }

            //删除散列表中指定的散列表项
            remove(key) {
                const {djb2HashTable} = this;
                let hashTable = hash_table.get(this),
                    hash_key = djb2HashTable.bind(this)(key);
                if(hashTable[hash_key] === undefined) {
                    return false;
                }
                hashTable[hash_key] = undefined;
                return true;
            }

            //获取散列表拥有值的字符串项
            toString() {
                let hashTable = hash_table.get(this),
                    result_str = ``;
                for(let [key, value] of hashTable.entries()) {
                    if(value !== undefined) {
                        result_str = `${result_str}${value} -> `;
                    }
                }
                return result_str;
            }

            //获取散列表的具体结构
            valueOf() {
                return hash_table.get(this);
            }
        }

        //返回散列表类
        return HashTable;
    })();

    let hash_table = new HashTable();
    //这里在散列表中添加散列表项
    //在这里打印:
    //true
    console.log(hash_table.put("Gary", "gary@gmail.com"));
    hash_table.put("Helen", "helen@gmail.com");
    hash_table.put("Lily", "lily@gmail.com");
    hash_table.put("Alice", "alice@gmail.com");
    hash_table.put("Simon", "simon@gmail.com");
    hash_table.put("Aaron", "aaron@gmail.com");
    hash_table.put("Tom", "tom@gmail.com");
    hash_table.put("Tommy", "tommy@gmail.com");
    hash_table.put("Betty", "betty@gmail.com");
    hash_table.put("Frank", "frank@gmail.com");
    hash_table.put("Martin", "martin@gmail.com");
    //这里获取散列表中指定的散列表项
    //在这里打印:
    //aaron@gmail.com
    console.log(hash_table.get("Aaron"));
    //这里获取散列表中指定的散列表项
    //在这里打印:
    //tom@gmail.com
    console.log(hash_table.get("Tom"));
    //这里获取散列表拥有值的字符串项
    //在这里打印:
    //tom@gmail.com -> gary@gmail.com -> lily@gmail.com -> martin@gmail.com -> alice@gmail.com -> helen@gmail.com -> aaron@gmail.com -> frank@gmail.com -> simon@gmail.com -> betty@gmail.com -> tommy@gmail.com -> 
    console.log(hash_table.toString());
    //这里获取散列表的具体结构
    //在这里打印:
    //[empty × 239, "tom@gmail.com", empty × 33, "gary@gmail.com", empty × 6, "lily@gmail.com", empty × 13, "martin@gmail.com", empty × 304, "alice@gmail.com", empty × 13, "helen@gmail.com", empty × 4, "aaron@gmail.com", "frank@gmail.com", empty × 19, "simon@gmail.com", empty, "betty@gmail.com", empty × 13, "tommy@gmail.com"]
    console.log(hash_table.valueOf());
    //这里删除散列表中指定的散列表项
    //在这里打印:
    //true
    console.log(hash_table.remove("Aaron"));
    hash_table.remove("Tom");
    //这里获取散列表中指定的散列表项
    //在这里打印:
    //false
    console.log(hash_table.get("Tom"));
    //这里获取散列表拥有值的字符串项
    //在这里打印:
    //gary@gmail.com -> lily@gmail.com -> martin@gmail.com -> alice@gmail.com -> helen@gmail.com -> frank@gmail.com -> simon@gmail.com -> betty@gmail.com -> tommy@gmail.com -> 
    console.log(hash_table.toString());
    //这里获取散列表的具体结构
    //在这里打印:
    //[empty × 239, undefined, empty × 33, "gary@gmail.com", empty × 6, "lily@gmail.com", empty × 13, "martin@gmail.com", empty × 304, "alice@gmail.com", empty × 13, "helen@gmail.com", empty × 4, undefined, "frank@gmail.com", empty × 19, "simon@gmail.com", empty, "betty@gmail.com", empty × 13, "tommy@gmail.com"]
    console.log(hash_table.valueOf());

# 二叉树
> 这是我们学习的第一种非线性非顺序的数据结构 —— <b>树</b>,后面还会学到更多,比如说<b>图</b>。树只有一个根节点,每一个节点都可能有一个或者多个子节点 —— <b>子叶</b>,今天我们实现的二叉树,每个节点最多只能有两个子叶,left的子叶比其父节点数值小,right的子叶比其父节点数值大,下面我们来介绍一下二叉树

    let Tree = (function () {
        //设置二叉树的容器,并初始化为null
        let head = new WeakMap();

        //定义二叉树子叶节点类
        //@params node
        //@params left
        //@params right
        class Node {
            constructor(node) {
                this.node = node;
                this.left = null;
                this.right = null;
            }
        }

        //定义二叉树类
        class Tree {
            constructor() {
                head.set(this, null);
            }

            //在二叉树中添加子叶节点
            insert(node) {
                const {insertNode} = this;
                let head_tree = head.get(this);
                head_tree = insertNode.bind(this)(head_tree, node);
                head.set(this, head_tree);
                return true;
            }

            //二叉树中添加子叶节点执行方法
            //利用当前的子叶节点和添加的子叶节点数值进行比较
            //假如小于添加的子叶节点数值,就查询当前子叶节点的右子叶节点
            //假如大于添加的子叶节点数值,就查询当前子叶节点的左子叶节点
            //直到查询到节点为null为止,然后添加新的子叶节点
            insertNode(node, node_key) {
                const {insertNode} = this;
                if(!node) {
                    node = new Node(node_key);
                } else if(node.node > node_key) {
                    node.left = insertNode.bind(this)(node.left, node_key);
                } else {
                    node.right = insertNode.bind(this)(node.right, node_key);
                }
                return node;
            }

            //在二叉树中删除指定的子叶节点
            remove(node) {
                const {removeNode} = this;
                let head_tree = head.get(this);
                if(!head_tree) {
                    return false;
                }
                head_tree = removeNode.bind(this)(head_tree, node);
                head.set(this, head_tree);
                return true;
            }

            //二叉树中删除指定的子叶节点执行方法
            //利用当前的子叶节点和删除的子叶节点数值进行比较
            //假如小于删除的子叶节点,就查询当前子叶节点的右子叶节点
            //假如大于删除的子叶节点,就查询当前子叶节点的左子叶节点
            //直到等于删除的子叶节点数值,分为三种情况
            //第一种,删除的子叶节点底下没有其左右子叶节点,就直接将删除的子叶节点置为null
            //第二种,删除的子叶节点底下的左右子叶节点有一边为null,就直接将删除的子叶节点置为左右子叶节点不为null的一边
            //第三种,删除的子叶节点底下其左右子叶节点都不为null,就直接去查询删除的子叶节点其右子叶节点底下的最小的子叶节点,并将删除的子叶节点的数值置为这个最小的子叶节点的数值,再将删除的子叶节点其右子叶节点底下的最小的子叶节点删除
            removeNode(node, node_key) {
                const {removeNode, findTheLeftNode} = this;
                if(node.node > node_key) {
                    node.left = removeNode.bind(this)(node.left, node_key);
                } else if(node.node < node_key){
                    node.right = removeNode.bind(this)(node.right, node_key);
                } else {
                    if(!node.left && !node.right) {
                        node = null;
                    } else if (!node.left) {
                        node = node.right;
                    } else if (!node.right) {
                        node = node.left;
                    } else {
                        let aux = findTheLeftNode.bind(this)(node.right);
                        node.node = aux.node;
                        node.right = removeNode.bind(this)(node.right, aux.node);
                    }
                }
                return node;
            }
            
            //查询子叶节点底下的最小的(最左边的)子叶节点
            findTheLeftNode(node) {
                const {findTheLeftNode} = this;
                if(node.left) {
                    return findTheLeftNode.bind(this)(node.left);
                }
                return node;
            }

            //在二叉树中获取最小的(最左边的)子叶节点数值
            min() {
                const {minNode} = this;
                let head_tree = head.get(this);
                console.log("最小的子叶:");
                return minNode.bind(this)(head_tree).node;
            }

            //二叉树中获取最小的(最左边的)子叶节点执行方法
            minNode(node) {
                const {minNode} = this;
                if(node.left) {
                    return minNode.bind(this)(node.left);
                }
                return node;
            }

            //在二叉树中获取最大的(最右边的)子叶节点数值
            max() {
                const {maxNode} = this;
                let head_tree = head.get(this);
                console.log("最大的子叶:");
                return maxNode.bind(this)(head_tree).node;
            }

            //二叉树中获取最大的(最右边的)子叶节点执行方法
            maxNode(node) {
                const {maxNode} = this;
                if(node.right) {
                    return maxNode.bind(this)(node.right);
                }
                return node;
            }

            //在二叉树获取先序遍历
            preorderTraversal(method) {
                const {preorderTraversalNode} = this;
                let head_tree = head.get(this);
                console.log("先序遍历:");
                preorderTraversalNode.bind(this)(head_tree, method);
            }

            //二叉树先序遍历执行方法
            preorderTraversalNode(node, method) {
                const {preorderTraversalNode} = this;
                if(node) {
                    method.bind(this)(node);
                    preorderTraversalNode.bind(this)(node.left, method);
                    preorderTraversalNode.bind(this)(node.right, method);
                }
            }

            //在二叉树中获取中序遍历
            inorderTraversal(method) {
                const {inorderTraversalNode} = this;
                let head_tree = head.get(this);
                console.log("中序遍历:");
                inorderTraversalNode.bind(this)(head_tree, method);
            }

            //二叉树中序遍历执行方法
            inorderTraversalNode(node, method) {
                const {inorderTraversalNode} = this;
                if(node) {
                    inorderTraversalNode.bind(this)(node.left, method);
                    method.bind(this)(node);
                    inorderTraversalNode.bind(this)(node.right, method);
                }
            }

            //在二叉树中获取后序遍历
            postorderTraversal(method) {
                const {postorderTraversalNode} = this;
                let head_tree = head.get(this);
                console.log("后序遍历:");
                postorderTraversalNode.bind(this)(head_tree, method);
            }

            //二叉树后序遍历执行方法
            postorderTraversalNode(node, method) {
                const {postorderTraversalNode} = this;
                if(node) {
                    postorderTraversalNode.bind(this)(node.left, method);
                    postorderTraversalNode.bind(this)(node.right, method);
                    method.bind(this)(node);
                }
            }

            //在二叉树中获取二叉树的具体结构
            valueOf() {
                let head_tree = head.get(this);
                return head_tree;
            }
        }

        //返回二叉树类
        return Tree;
    })();

    let tree = new Tree();
    //这里在二叉树中添加子节点
    //在这里打印:
    //true
    console.log(tree.insert(15));
    tree.insert(10);
    tree.insert(18);
    tree.insert(20);
    tree.insert(17);
    tree.insert(16);
    tree.insert(25);
    tree.insert(5);
    tree.insert(8);
    tree.insert(55);
    tree.insert(30);
    tree.insert(35);
    tree.insert(40);
    tree.insert(45);
    tree.insert(50);
    //这里在二叉树中获取最小的(最左边的)子叶节点数值
    //在这里打印:
    //最小的子叶:
    //5
    console.log(tree.min());
    //这里在二叉树中获取最大的(最右边的)子叶节点数值
    //在这里打印:
    //最大的子叶:
    //55
    console.log(tree.max());
    //这里在二叉树中获取中序遍历
    //在这里打印:
    //中序遍历:
    //5
    //8
    //10
    //15
    //16
    //17
    //18
    //20
    //25
    //30
    //35
    //40
    //45
    //50
    //55
    tree.inorderTraversal((node)=>{
        console.log(node.node);
    });
    //这里在二叉树中获取先序遍历
    //在这里打印:
    //先序遍历:
    //15
    //10
    //5
    //8
    //18
    //17
    //16
    //20
    //25
    //55
    //30
    //35
    //40
    //45
    //50
    tree.preorderTraversal((node)=>{
        console.log(node.node);
    });
    //这里在二叉树中获取后序遍历
    //在这里打印:
    //后序遍历:
    //8
    //5
    //10
    //16
    //17
    //50
    //45
    //40
    //35
    //30
    //55
    //25
    //20
    //18
    //15
    tree.postorderTraversal((node)=>{
        console.log(node.node);
    });
    //这里在二叉树中获取二叉树的具体结构
    //在这里打印:
    //Node {node: 15, left: Node, right: Node}
    console.log(tree.valueOf());
    //这里在二叉树中删除指定的子叶节点
    //在这里打印:
    //true
    console.log(tree.remove(50));
    tree.remove(40);
    tree.remove(15);
    //这里在二叉树中获取二叉树的具体结构
    //在这里打印:
    //Node {node: 16, left: Node, right: Node}
    console.log(tree.valueOf());

## 平衡二叉树
> 介绍并封装完了二叉树之后,我们来介绍一下平衡二叉树,其实平衡二叉树就是每一个二叉树上面的节点的平衡因子的绝对值不可以超过1,也就是说-1 <= 平衡因子 <= 1,所谓的平衡因子就是二叉树节点子树节点级数,-1 <= 左子树级数 - 右子树级数 <= 1,下面就让我们来介绍一下平衡二叉树吧

    let AVLTree = (function () {
        //设置平衡二叉树的容器,并初始化为null
        let head = new WeakMap();

        //定义平衡二叉树子叶节点类
        //@params node
        //@params left
        //@params right
        class Node {
            constructor(node) {
                this.node = node;
                this.left = null;
                this.right = null;
            }
        }

        //定义平衡二叉树类
        class AVLTree {
            constructor() {
                head.set(this, null);
            }

            //在平衡二叉树中添加子叶节点
            insert(node) {
                const {insertNode} = this;
                let head_tree = head.get(this);
                head_tree = insertNode.bind(this)(head_tree, node);
                head.set(this, head_tree);
                return true;
            }

            //平衡二叉树中添加子叶节点执行方法
            //利用当前的子叶节点和添加的子叶节点数值进行比较
            //假如小于添加的子叶节点数值,就查询当前子叶节点的右子叶节点
            //假如大于添加的子叶节点数值,就查询当前子叶节点的左子叶节点
            //直到查询到节点为null为止,然后添加新的子叶节点
            insertNode(node, node_key) {
                const {insertNode, findBalanceFactor, LLBalanceNode, LRBalanceNode, RRBalanceNode, RLBalanceNode} = this;
                if(!node) {
                    node = new Node(node_key);
                } else if(node.node > node_key) {
                    node.left = insertNode.bind(this)(node.left, node_key);
                    if(findBalanceFactor.bind(this)(node.left) - findBalanceFactor.bind(this)(node.right) > 1) {
                        if(node_key < node.left.node) {
                            node = LLBalanceNode.bind(this)(node);
                        } else {
                            node = LRBalanceNode.bind(this)(node);
                        }
                    }
                } else {
                    node.right = insertNode.bind(this)(node.right, node_key);
                    if(findBalanceFactor.bind(this)(node.right) - findBalanceFactor.bind(this)(node.left) > 1) {
                        if(node_key > node.right.node) {
                            node = RRBalanceNode.bind(this)(node);
                        } else {
                            node = RLBalanceNode.bind(this)(node);
                        }
                    }
                }
                return node;
            }

            //平衡二叉树使用LL算法来解决添加的新的子叶节点数值小于其父子叶节点(左边父子叶节点)的数值的平衡问题
            LLBalanceNode(node) {
                let target = node.left;
                node.left = target.right;
                target.right = node;
                return target;
            }

            //平衡二叉树使用LL算法来解决添加的新的子叶节点数值大于其父子叶节点(左边父子叶节点)的数值的平衡问题
            LRBalanceNode(node) {
                const {RRBalanceNode, LLBalanceNode} = this;
                node.left = RRBalanceNode.bind(this)(node.left);
                return LLBalanceNode.bind(this)(node);
            }

            //平衡二叉树使用RR算法来解决添加的新的子叶节点数值大于其父子叶节点(右边父子叶节点)的数值的平衡问题
            RRBalanceNode(node) {
                let target = node.right;
                node.right = target.left;
                target.left = node;
                return target;
            }

            //平衡二叉树使用RR算法来解决添加的新的子叶节点数值小于其父子叶节点(右边父子叶节点)的数值的平衡问题
            RLBalanceNode(node) {
                const {RRBalanceNode, LLBalanceNode} = this;
                node.right = LLBalanceNode.bind(this)(node.right);
                return RRBalanceNode.bind(this)(node);
            }
            
            //获取每个平衡二叉树节点的平衡因子
            findBalanceFactor(node) {
                const {findBalanceFactor} = this;
                if(!node) {
                    return -1;
                } else {
                    return Math.max(findBalanceFactor.bind(this)(node.left), findBalanceFactor.bind(this)(node.right)) + 1;
                }
            }

            //在平衡二叉树中删除指定的子叶节点
            remove(node) {
                const {removeNode} = this;
                let head_tree = head.get(this);
                if(!head_tree) {
                    return false;
                }
                head_tree = removeNode.bind(this)(head_tree, node);
                head.set(this, head_tree);
                return true;
            }

            //平衡二叉树中删除指定的子叶节点执行方法
            //利用当前的子叶节点和删除的子叶节点数值进行比较
            //假如小于删除的子叶节点,就查询当前子叶节点的右子叶节点
            //假如大于删除的子叶节点,就查询当前子叶节点的左子叶节点
            //直到等于删除的子叶节点数值,分为三种情况
            //第一种,删除的子叶节点底下没有其左右子叶节点,就直接将删除的子叶节点置为null
            //第二种,删除的子叶节点底下的左右子叶节点有一边为null,就直接将删除的子叶节点置为左右子叶节点不为null的一边
            //第三种,删除的子叶节点底下其左右子叶节点都不为null,就直接去查询删除的子叶节点其右子叶节点底下的最小的子叶节点,并将删除的子叶节点的数值置为这个最小的子叶节点的数值,再将删除的子叶节点其右子叶节点底下的最小的子叶节点删除
            removeNode(node, node_key) {
                const {removeNode, findTheLeftNode} = this;
                if(node.node > node_key) {
                    node.left = removeNode.bind(this)(node.left, node_key);
                } else if(node.node < node_key){
                    node.right = removeNode.bind(this)(node.right, node_key);
                } else {
                    if(!node.left && !node.right) {
                        node = null;
                    } else if (!node.left) {
                        node = node.right;
                    } else if (!node.right) {
                        node = node.left;
                    } else {
                        let aux = findTheLeftNode.bind(this)(node.right);
                        node.node = aux.node;
                        node.right = removeNode.bind(this)(node.right, aux.node);
                    }
                }
                return node;
            }
            
            //查询子叶节点底下的最小的(最左边的)子叶节点
            findTheLeftNode(node) {
                const {findTheLeftNode} = this;
                if(node.left) {
                    return findTheLeftNode.bind(this)(node.left);
                }
                return node;
            }

            //在平衡二叉树中获取最小的(最左边的)子叶节点数值
            min() {
                const {minNode} = this;
                let head_tree = head.get(this);
                console.log("最小的子叶:");
                return minNode.bind(this)(head_tree).node;
            }

            //平衡二叉树中获取最小的(最左边的)子叶节点执行方法
            minNode(node) {
                const {minNode} = this;
                if(node.left) {
                    return minNode.bind(this)(node.left);
                }
                return node;
            }

            //在平衡二叉树中获取最大的(最右边的)子叶节点数值
            max() {
                const {maxNode} = this;
                let head_tree = head.get(this);
                console.log("最大的子叶:");
                return maxNode.bind(this)(head_tree).node;
            }

            //平衡二叉树中获取最大的(最右边的)子叶节点执行方法
            maxNode(node) {
                const {maxNode} = this;
                if(node.right) {
                    return maxNode.bind(this)(node.right);
                }
                return node;
            }

            //在平衡二叉树获取先序遍历
            preorderTraversal(method) {
                const {preorderTraversalNode} = this;
                let head_tree = head.get(this);
                console.log("先序遍历:");
                preorderTraversalNode.bind(this)(head_tree, method);
            }

            //平衡二叉树先序遍历执行方法
            preorderTraversalNode(node, method) {
                const {preorderTraversalNode} = this;
                if(node) {
                    method.bind(this)(node);
                    preorderTraversalNode.bind(this)(node.left, method);
                    preorderTraversalNode.bind(this)(node.right, method);
                }
            }

            //在平衡二叉树中获取中序遍历
            inorderTraversal(method) {
                const {inorderTraversalNode} = this;
                let head_tree = head.get(this);
                console.log("中序遍历:");
                inorderTraversalNode.bind(this)(head_tree, method);
            }

            //平衡二叉树中序遍历执行方法
            inorderTraversalNode(node, method) {
                const {inorderTraversalNode} = this;
                if(node) {
                    inorderTraversalNode.bind(this)(node.left, method);
                    method.bind(this)(node);
                    inorderTraversalNode.bind(this)(node.right, method);
                }
            }

            //在平衡二叉树中获取后序遍历
            postorderTraversal(method) {
                const {postorderTraversalNode} = this;
                let head_tree = head.get(this);
                console.log("后序遍历:");
                postorderTraversalNode.bind(this)(head_tree, method);
            }

            //平衡二叉树后序遍历执行方法
            postorderTraversalNode(node, method) {
                const {postorderTraversalNode} = this;
                if(node) {
                    postorderTraversalNode.bind(this)(node.left, method);
                    postorderTraversalNode.bind(this)(node.right, method);
                    method.bind(this)(node);
                }
            }

            //在平衡二叉树中获取二叉树的具体结构
            valueOf() {
                let head_tree = head.get(this);
                return head_tree;
            }
        }

        //返回平衡二叉树类
        return AVLTree;
    })();

    let tree = new AVLTree();
    //这里在平衡二叉树中添加子节点
    //在这里打印:
    //true
    console.log(tree.insert(15));
    tree.insert(10);
    tree.insert(18);
    tree.insert(20);
    tree.insert(17);
    tree.insert(16);
    tree.insert(25);
    tree.insert(5);
    tree.insert(8);
    tree.insert(55);
    tree.insert(30);
    tree.insert(35);
    tree.insert(40);
    tree.insert(45);
    tree.insert(50);
    //这里在平衡二叉树中获取最小的(最左边的)子叶节点数值
    //在这里打印:
    //最小的子叶:
    //5
    console.log(tree.min());
    //这里在平衡二叉树中获取最大的(最右边的)子叶节点数值
    //在这里打印:
    //最大的子叶:
    //55
    console.log(tree.max());
    //这里在平衡二叉树中获取中序遍历
    //在这里打印:
    //中序遍历:
    //5
    //8
    //10
    //15
    //16
    //17
    //18
    //20
    //25
    //30
    //35
    //40
    //45
    //50
    //55
    tree.inorderTraversal((node)=>{
        console.log(node.node);
    });
    //这里在平衡二叉树中获取先序遍历
    //在这里打印:
    //先序遍历:
    //17
    //15
    //8
    //5
    //10
    //16
    //30
    //20
    //18
    //25
    //40
    //35
    //50
    //45
    //55
    tree.preorderTraversal((node)=>{
        console.log(node.node);
    });
    //这里在平衡二叉树中获取后序遍历
    //在这里打印:
    //后序遍历:
    //5
    //10
    //8
    //16
    //15
    //18
    //25
    //20
    //35
    //45
    //55
    //50
    //40
    //30
    //17
    tree.postorderTraversal((node)=>{
        console.log(node.node);
    });
    //这里在平衡二叉树中获取二叉树的具体结构
    //在这里打印:
    //Node {node: 17, left: Node, right: Node}
    console.log(tree.valueOf());
    //这里在平衡二叉树中删除指定的子叶节点
    //在这里打印:
    //true
    console.log(tree.remove(50));
    tree.remove(40);
    tree.remove(15);
    //这里在平衡二叉树中获取二叉树的具体结构
    //在这里打印:
    //Node {node: 17, left: Node, right: Node}
    console.log(tree.valueOf());







    
    
    
    
    
    
