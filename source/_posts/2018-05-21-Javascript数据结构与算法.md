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
    
    let linkList = (function() {
        
        let head = null,
            length = 0;
        
        class Node {
            constructor(element) {
                this.element = element;
                this.next = null;
            }
        }
        
        class LinkList {
            constructor() {
                   
            }
            
            insert(element) {
                let current = head,
                    node = new Node(element);
                if(!head) {
                    head = node;
                } else {
                    while(current.next) {
                        current = current.next;
                    }
                    current.next = node;                        
                }
                length++;
                return length;
            }
            
            insertAt(element, index) {
                
            }
            
            remove(element) {
                
            }
            
            removeAt(element, index) {
                
            }
            
            indexOf(element) {
                
            }
        }
        
        return LinkList;
    })();

    
    
    
    
    
    
    
    
