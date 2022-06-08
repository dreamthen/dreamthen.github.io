---
title: browserstack screenshots
date: 2022-06-07 22:58:37
tags: [testing, browserstack, screenshots]
categories: testing
---

# 实现browserstack screenshots

## browserstack screenshots api

   <a hef='https://www.browserstack.com/screenshots/api'>Screenshots API</a>，通过调用 Screenshots API 的例子<a href='https://github.com/scottgonzalez/node-browserstack/blob/master/lib/screenshot.js'>node-browserstack screenshots</a>就可以得知，通过 http 请求 https://www.browserstack.com/screenshots 接口:

  - url(需要测试截图的url);
  - os(测试环境: 操作系统);
  - os_version(测试环境: 操作系统版本);
  - browser(测试环境: 浏览器类型);
  - browser_version(测试环境: 浏览器版本);
  - device(测试环境: 若需要移动设备,设备类型);
  - orientation(测试环境: 设备的屏幕方向);
  - mac_res(测试环境: mac浏览器屏幕分辨率);
  - win_res(测试环境: windows浏览器屏幕分辨率);
  - quality(测试环境: 截图是否压缩);
  - local(测试环境: 是否建立本地测试连接);
  - wait_time(测试环境: 截图前等待的时间);
  - callback_url(测试环境: 回调网址);

选择性带入上述参数就可生成截图列表极其状态，并回调到对应的url页面上。类似的，lambdaTest 上面也是有一套 Screenshots API 实现逻辑，<a href="https://www.lambdatest.com/support/api-doc/">AUTOMATED SCREENSHOTS API</a>，其例子请求方式相同，都是通过 http 请求。

## browserstack Screenshots API背后所实现的原理

辗转反侧的通过 Google、询问平台技术支持人员，最后得到的结论是: Screenshots API背后使用了多个自动化测试脚本和不同的框架来捕获屏幕截图，其中包含了selenium webdriver，也就是说基本上为了捕获截图，browserstack 使用了 selenium webdriver 技术，但 selenium webdriver 只限于针对PC端/移动端的浏览器。

## 哪些方式可以实现跨终端自动化截图？

  - Selenium WebDriver

    - Selenium 是什么?

      Selenium 是一套基于浏览器的自动化工具，它提供了一种跨平台、跨浏览器的端到端的 web 自动化解决方案。
    
      Selenium 主要包括三部分:
  
       - Selenium IDE：它可以进行录制回放用户操作，并且可以把录制的操作以多种语言（如JAVA、Python、C#等）的形式导出成测试用例。
       - Selenium WebDriver：提供 Web 自动化所需的 API，主要用作浏览器控制、页面元素选择和调试，通常也被成为WebDriver。不同的浏览器需要不同的 WebDriver，例如针对Chrome使用的chromedriver。
       - Selenium Grid：提供了在不同机器的不同浏览器上运行 selenium 测试的能力，一个分布式运行用例时的工具。
    
    - Selenium WebDriver 的工作原理

      简单来说: 自动化 Selenium WebDriver API 测试脚本发送请求给浏览器的驱动，驱动将测试脚本解析后的结果发送给浏览器，浏览器执行驱动发来的指令，并最终完成想要的操作。
  
    - Selenium WebDriver 的结构

      典型的 C/S 结构，Selenium WebDriver API 相当于是客户端，而浏览器驱动才是服务器端。
    
    - 浏览器的驱动兼容多个测试脚本的原因

      WebDriver基于的协议：JSON Wire protocol，这个协议规范在WebDriver中数据都是以JSON的形式存在并进行传送的，所以在 client 和 server 之间，只要是基于JSON Wire Protocol来传递数据，与具体的脚本语言无关。
    
    - WebDriver协议 - JSON Wire protocol

      <a href='https://www.selenium.dev/documentation/legacy/json_wire_protocol/'>JSON Wire protocol 官方文档</a>，是<a href='https://w3c.github.io/webdriver/'>W3C WebDriver协议</a>的前身，是在http协议基础上，对http请求及响应的body部分的数据的进一步规范，必须以JSON的形式存在并进行传送，提供了操作浏览器<a href='https://w3c.github.io/webdriver/#endpoints'>命令的方法以及所对应的 URI 模板。<a>

    - 深析 Selenium WebDriver 的工作原理

        1. 对于每一条转换为 JSON 之后的 Selenium WebDriver API 测试脚本,会通过 CommandExecutor 发送 http 请求给浏览器的驱动。
        2. 浏览器驱动中包含了一个 WebDriver remote server，通过监听端口用来接收 http 请求。
        3. WebDriver remote server 接收到请求后根据请求来具体操控对应的浏览器。
        4. 浏览器执行具体的测试脚本步骤。
        5. 浏览器将执行结果返回给 WebDriver remote server。
        6. WebDriver remote server 又将结果返回给 Selenium WebDriver API client 端。

      ![](/images/basic_comms.png)
    
    - 自动化截图

      可以通过 Selenium WebDriver API 用于捕获当前浏览上下文的屏幕截图，会返回以 Base64 格式编码的屏幕截图。
    
      <a href='https://www.selenium.dev/documentation/webdriver/browser/windows/#takescreenshot'>TakeScreenshot(屏幕截图)</a>

      也可以通过 Selenium WebDriver API 用于捕获当前浏览上下文的元素内的屏幕截图，会返回以 Base64 格式编码的屏幕截图。

      <a href='https://www.selenium.dev/documentation/webdriver/browser/windows/#takeelementscreenshot'>TakeElementScreenshot(元素内屏幕截图)</a>
    

  - Appium

    - Appium 是什么?

      Appium 是一个开源的移动端自动化测试工具，用于自动化 iOS设备、 Android设备 和 Windows 桌面系统上的原生、移动 Web 和混合应用。
    
      - [原生应用]指那些用 iOS、 Android 或者 Windows SDKs 编写的应用。
      - [移动 Web 应用]是用移动端浏览器访问的应用(Appium 支持 iOS 上的 Safari、Chrome 和 Android 上的内置浏览器）。
      - [混合应用]带有一个[ webview ]的包装器——用来和 Web 内容交互的原生控件。
    
    - 安装

      可以通过 NPM 安装。

          npm install -g appium

      也可以通过 <a href='https://github.com/appium/appium-desktop/releases'>Appium Desktop</a> 桌面应用程序安装。
  
      PS: 安装的 Appium 实际上只是用于启动 Appium HTTP Server 的。要想建立连接，还需要<a href='https://appium.io/docs/en/about-appium/appium-clients/index.html'> Appium 服务器的客户端程序库</a>，它负责与Appium服务器建立连接，并将测试脚本的指令发送到Appium HTTP Server。

    - 深析 Appium 的工作原理

      1. 测试人员执行测试脚本（java,python等脚本）通过 Appium client(基于 WebDriver 协议: JSON Wire protocol 扩展实现了 <a href='https://github.com/SeleniumHQ/mobile-spec/blob/master/spec-draft.md'>Mobile JSON Wire Protocol</a> 协议) 转换为 JSON 数据，通过CommandExecutor 发送 http 请求传递给 Appium server，Appium server默认监听4723端口，这和 Selenium WebDriver 工作原理的前两步是一致的。
      2. 之后，Appium server 需要与移动端设备自带的自动化测试框架进行通信。
         
         ![](/images/automate_test.png)
      
         Appium server 会通过 TCP/IP 协议转发请求并转化成移动设备可以识别的命令（command）给不同设备的中间件，在转发请求的同时，会在PC端开启一个监听端口4724，来接收设备返回的结果。
      3. Appium server with Android
      
         以 UIAutomator 的自动化测试框架为例。

         ![](/images/appium_android.png)

         命令（command）由中间件 bootstrap.jar 通过监听设备的4724端口来获得，经过其解释，将它们转换为 Android 设备可理解的 UIAutomator 格式，Android 设备通过 UIAutomator 命令调用其提供的 API 去做一些实际的操作；接着，Android 设备通过 bootstrap.jar 将执行命令的结果返回到 Appium server；最后，Appium server 将此结果响应给 Appium client。
      4. Appium server with IOS

         以 XCUITest 的自动化测试框架为例。

         ![](/images/appium_ios.png)

         命令（command）由中间件 WebDriverAgent.app 通过监听设备的4724端口来获得，经过其解释，通过调用 Apple 的 XCUITest API 将它们转换为 Apple 设备可理解的格式，Apple 设备通过转换后的命令去做一些实际的操作；接着，Apple 设备通过 WebDriverAgent.app 将执行命令的结果返回到 Appium server；最后，Appium server 将此结果响应给 Appium client。