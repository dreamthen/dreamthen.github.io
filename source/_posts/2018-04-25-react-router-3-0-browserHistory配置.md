---
title: 2018-04-25 react-router 3.0 browserHistory配置
date: 2018-04-25 13:01:53
tags: [react-router, browserHistory]
categories: react-router
---
# 为什么推荐使用browserHistory,舍弃hashHistory

> 1. 首先browserHistory从表现来看,比较舒服和语义化,更易读。
> 2. browserHistory使用的是HTML5的History API,根据路由路径的变化引起浏览器历史记录的变化;hashHistory则是依靠hash的改变,来使得浏览器的历史记录发生改变。hashHistory的hash部分不会请求到服务端,服务端获取不到URL的细节部分,而browserHistory使用的History API需要服务端的支持,服务端可以完全的掌握URL中的细节部分。
> 3. 有一些浏览器会把hashHistory URL当中的hash部分删除掉,记起之前进行分享的时候,URL传到微信中,hash部分遭到丢失。

# browserHistory配置

> 路由上面除了引入不同,基本上和hashHistory配置相同

    import {Router, browserHistory} from "react-router";
    <Router history={browserHistory}>
    </Router>
    
> 配置路径为空时,callback的处理,使用webpack-dev-server时,在配置文件内部添加

    historyApiFallback: true
    
> 使用nginx时,在配置文件内部添加
    
    location / {
        root ...
        index index.html index.htm
        try_files $uri /index.html
    }
            