---
title: think of testing
date: 2022-05-29 12:32:35
tags: [testing]
categories: testing
---

# 测试(testing)

## 跨终端手动测试

### 平台

> <a href='https://www.lambdatest.com/'>lambdaTest</a>

- 手动测试

  - <a href='https://app.lambdatest.com/console/realtime'>Browser Testing</a>.

    可在线在不同的浏览器种类、版本、操作系统以及分辨率对website进行实时交互式测试,每次真实浏览器sessions可测试10分钟.

    - 结论.
    
      - 可切换配置浏览器种类、版本、操作系统以及分辨率;
      - 可在线录屏、截图(录屏、截图可下载);
      - 可在线标记bug(编辑bug截图、下载bug截图以及上传到lambdaTest合作的SLACK、JIRA和ASANA项目管理系统);

  - <a href='https://app.lambdatest.com/console/realtime'>App Testing</a>.

    可在线自由搭配不同的品牌手机、版本设备对App包或者App Url进行实时交互式测试,每次真机测试sessions可测试10分钟.

    - 结论.

      - 可切换配置品牌手机以及版本设备;
      - 可在线录屏、截图(录屏、截图可下载);
      - 可在线标记bug(编辑bug截图、下载bug截图以及上传到lambdaTest合作的SLACK、JIRA和ASANA项目管理系统);
      - 可下载新的上传的App、移除任意App.
      - 可在线查看网络日志、App日志以及设备日志;

  - Browser Testing开发环境在线测试.

    可配合lambdaTest桌面应用(LT_Windows or LT_Macs)配合在线网站进行开发环境在线测试.

    - 配置.

      <a href='https://www.lambdatest.com/support/docs/testing-locally-hosted-pages/'>Browser Testing开发环境在线测试视频</a>.

  - 结论.

    - 简洁、易用且容易理解;
    - 功能完备,在线随时切换终端设备配置、录屏下载、Debug标记应有尽有;
    - 测试过程流畅、无障碍性困难;
    - 其合作生态成熟且完备,例如其合作的一套项目管理系统SLACK、JIRA和ASANA;
    - 为测试人员大大提高了效率,节约了时间成本;
    - 开放的终端设备可重复使用;

  - 问题.

    - 大部分终端设备不开放.
    - 每个部分(Browser Testing or App Testing)体验时长不能超过30分钟.
    - 终端设备开放、永久使用需要付费.

> <a href='https://www.browserstack.com/'>browserstack</a>

  - <a href='https://live.browserstack.com/dashboard#os=android&os_version=10.0&device=OnePlus+7T&device_browser=chrome&zoom_to_fit=true&full_screen=true&url=https%3A%2F%2Fwww.google.com%2F%3Fgws_rd%3Dssl&speed=1'>Browser Testing</a>.

    可在线在不同的浏览器种类、版本、操作系统以及分辨率对website进行实时交互式测试,每次真实浏览器sessions可测试1分钟.

    - 结论.

      - 可切换配置浏览器种类、版本、操作系统以及分辨率;
      - 可在线标记bug(编辑bug截图、下载bug截图以及上传到Email、Github、browserstack合作的SLACK、JIRA和TRELLO项目管理系统);

  - <a href='https://app-live.browserstack.com/#os=iOS&os_version=14.0&zoom_to_fit=true&full_screen=true&speed=1'>App Testing</a>.

    可在线自由搭配不同的品牌手机、版本设备对App包或者App Url进行实时交互式测试,每次真机测试sessions可测试无限制.

    - 结论.

      - 可切换配置品牌手机以及版本设备;
      - 可在线录屏、截图(录屏、截图可下载);
      - 可在线标记bug(编辑bug截图、下载bug截图以及上传到Email、Github、browserstack合作的SLACK、JIRA和TRELLO项目管理系统);
      - 可下载新的上传的App、移除任意App.
      - 可切换手机语言配置.
      - 可在线查看网络日志、App日志以及设备日志;

  - Browser Testing开发环境在线测试.

    可配合browserstack桌面应用(BrowserStackLocal.exe or BrowserStackLocal.dmg)配合在线网站进行开发环境在线测试.

    - 配置.

      <a href='https://www.browserstack.com/docs/live/local-testing/test-using-local-testing'>Browser Testing开发环境在线测试视频</a>.

  - 结论.

    - 简洁、易用且容易理解;
    - 功能比较完备,在线随时切换终端设备配置、Debug标记;
    - 测试过程流畅、无障碍性困难;
    - 其合作生态成熟且完备,例如Email、Github和browserstack合作的SLACK、JIRA和TRELLO项目管理系统;
    - 为测试人员大大提高了效率,节约了时间成本;
    - 大部分浏览器设备开放,可进行体验.

  - 问题.

    - 体验时间过短,每次真实浏览器sessions只能测试1分钟.
    - App Testing体验时长不能超过30分钟.
    - 终端设备开放、永久使用需要付费.
    - 超过体验时间,不可重复体验开放的同一浏览器.


## 跨终端自动化测试

- 自动化测试

  - WebDriver.

    WebDriver是W3C的一个标准,是一个远程控制协议,提供操纵浏览器的方式,提供访问操作DOM的API.

    - 工作过程.

      <a href='https://blog.csdn.net/ant_ren/article/details/7970793'>WebDriver的工作过程</a>.

    - 衍生.

      Selenium、Appium都是基于WebDriver协议并进行了扩展,属于WebDriver的衍生品.

  - 浏览器自动化测试工具.

    - Selenium.

      Selenium是浏览器自动化测试工具领域最为流行的一种测试套件.

      - Selenium支持多浏览器平台(Chrome、Firefox、IE、Opera、Safari等);
      - Selenium开发支持多语言(python、java、ruby、js、c#等);
      - Selenium的Remote Control可以通过录制用户的操作,来简化Web测试人员的各项重复作业;
      - Selenium的Grid具有编写、运行和并行处理测试的功能;
      - Selenium的Core则是基于JsUnit,完全由JavaScript所编写,因此可以被运行在各种支持JavaScript的主流浏览器之上;
      - Selenium开源免费;

    - Selenium IDE.

      Selenium IDE能够以插件的形式被安装到测试者的浏览器中,从而方便地实现Web界面的测试,是最为流行的一种可视化、自动化测试工具.

    - selenium-webdriver.

      浏览器自动化库,提供了许多浏览器自动化接口,用于测试web应用.

      - api.

        <a href='https://www.selenium.dev/selenium/docs/api/javascript/'>selenium-webdriver</a>.

  - App自动化测试工具.

    - Appium.

      Appium是一个开源的,适用于原生或混合移动应用(hybrid mobile apps)的自动化测试工具.

    - Appium特性.    

      - Appium支持多App平台(Android、iOS等);
      - Appium支持多语言(python、java、ruby、js、c#等),Appium选择了Client/Server的设计模式,只要client能够发送http请求给server,那么client用什么语言来实现都是可以的,这就是如何做到支持多语言的原因;
      - Appium是跨平台的,可以用在OSX，Windows以及Linux桌面系统上运行;
      - Appium扩展了WebDriver的协议,这样的好处是以前的WebDriver API能够直接被继承过来,以前的WebDriver各种语言的binding都可以拿来就用,省去了为浏览器、App端各开发一个client的工作量;
      - Appium开源免费;
    
    - Appium框架组成.
    
      ![](https://image.white-than-wood.zone/appium/content.png)
    
    - Appium通信原理.

      Client端运行Webdriver协议的机器发送自动化指令给Appium server,Appium Server接收到client发送的指令后,转换为移动端能够识别的指令,然后发送给移动端设备,并对移动端设备进行操作.
    
    - Appium整体流程.

      ![](https://image.white-than-wood.zone/appium/tenet.png)

### 平台

> <a href='https://www.lambdatest.com/'>lambdaTest</a>
    
- lambdaTest配合Selenium IDE.
  
  <a href='https://www.lambdatest.com/support/docs/run-selenium-ide-tests-on-lambdatest-selenium-cloud-grid/'>Run Selenium IDE Tests with LambdaTest Selenium Grid</a>.

  - 结论.

    - API、技术文档完备,引导配置成熟.
    - 可视化编辑测试用例流畅并且效果顶级;
    - 支持多语言编写测试用例(python、java、ruby、js、PHP、c#等).
    - 与lambdaTest配合相得益彰,做到了跨浏览器自动化可视化测试完备且成熟的流程.
    - 录制操作、编写测试用例二合一,既考虑了定制性、精确性,也考虑了自动化、可视化和灵活性.
    - 测试报告: 截图、录屏、网络日志、Selenium日志、浏览器日志、浏览器参数以及终端日志俱有.
  
  - 问题.

    - 无产品文档,无法直观具体了解产品.
    - 测试报告中有一些不完整,如性能报告.
    
- selenium-webdriver、jest配合lambdaTest.
    
  <a href='https://www.lambdatest.com/support/docs/automation-testing-with-selenium-and-jest/'>Jest with Selenium: Tutorial to Run Your First Test on LambdaTest</a>.

  - 结论.
  
    - API、技术文档完备,引导配置成熟.
    - 支持多语言编写测试用例(python、java、ruby、js、PHP、c#等).
    - 测试报告: 截图、录屏、网络日志、Selenium日志、浏览器日志、浏览器参数以及终端日志俱有.

  - 问题.

    - 在线平台不保存测试用例,也不集成测试套件,只能进行线下编辑测试用例,没有做到完全自动化可视化测试.
    - 无产品文档,无法直观具体了解产品.
    - 测试报告中有一些不完整,如性能报告.

- lambdaTest配合Appium.

  <a href='https://www.lambdatest.com/support/docs/appium-nodejs-webdriverio/'>WebDriverIO With Appium in lambdaTest</a>.
    
  - 结论.

    - API、技术文档完备,引导配置成熟.
    - 支持多语言编写测试用例(python、java、ruby、js、PHP、c#等).

  - 问题.
    
    - 真机跨终端自动化测试需要付费,无法体验产品.
    - 无产品文档,无法直观具体了解产品.

- Visual UI Testing.

  <a href='https://app.lambdatest.com/console/screenshot'>Visual UI Testing Screenshot</a>.

    - 结论.

      - 可实行多终端UI截图,并可实现对比.
      - 可下载、分享截图或者截图列表压缩包.
      - 可配置各终端的分辨率.
      - 可预定日程(每天、每个周、每个月)进行截图.
      - 根据账号保存每次截图列表历史.
    
    - 问题.
  
      - 不可实行本地终端UI截图.

> <a href='https://www.aliyun.com/product/mqc'>阿里云移动测试</a>

- 阿里云移动测试配合Appium.

  <a href='https://help.aliyun.com/document_detail/175761.html'>阿里云移动测试产品文档</a>.
    
  - 结论.

    - API、技术文档完备,引导配置成熟.
    - 集成Appium IDE于阿里云平台内部,做到可视化、自动化测试.
    - 录制、编写测试用例二合一,做到了跨浏览器自动化可视化测试完备且成熟的流程.
    - 产品文档完备,可直观了解产品.
    - 测试报告:截图、录屏、测试用例日志、Appium日志、移动设备日志、错误日志以及性能报告一应俱全.
      
  - 问题.
      
    - 只支持Python编写测试用例.
    - 测试报告中有一些不完整,如网络日志.

- Visual UI Testing.

  无Visual UI Testing功能.

> <a href='https://www.browserstack.com/'>browserstack</a>    

- browserstack配合Appium.
    
  <a href='https://www.browserstack.com/docs/app-automate/appium/getting-started/nodejs/webdriverio'>WebDriverIO With Appium in browserstack</a>.

  - 结论.

    - API、技术文档完备,引导配置成熟.
    - 支持多语言编写测试用例(python、java、ruby、js、PHP、c#等).
    - 做到了跨浏览器自动化测试比较完备且成熟的流程.
    - 测试报告: 截图、录屏、网络日志、Appium日志、移动设备日志以及性能报告应有尽有.

  - 问题.

    - 在线平台不保存测试用例,也不集成测试套件,只能进行线下编辑测试用例,没有做到完全自动化可视化测试.
    - 测试报告中有一些不完整,如测试用例日志,需要在命令行中查看.
    - 产品文档有欠缺,急需补足.

- Visual UI Testing.

  <a href='https://www.browserstack.com/screenshots'>Visual UI Testing Screenshot</a>.

    - 结论.

      - 可进行多终端UI截图,进行对比.
      - 可下载、分享截图或者截图列表压缩包.
      - 根据账号保存每次截图列表历史.
      - 可配置各终端的分辨率.
      - 可实行本地终端UI截图
    
    - 问题.

      - 配置各终端的分辨率需付费.
      - 不可预定日程(每天、每个周、每个月)进行截图.

> <a href='https://saucelabs.com/'>sauceLabs</a>

- sauceLabs配合Appium.

  <a href='https://github.com/saucelabs-training/demo-js/tree/main/webdriverio/appium-app/examples/simple-example'>WebDriverIO With Appium in sauceLabs</a>.

   - 结论.
      
     - 支持多语言编写测试用例(python、java、ruby、js、PHP、c#等).
     - 做到了跨浏览器自动化测试比较完备且成熟的流程.
     - 测试报告: 截图、录屏、网络日志、Appium日志以及移动设备日志俱有.

   - 问题.

     - Simple Demo冗杂耦合在一起,下载很慢,且很乱.
     - API、技术文档无任何引导,且比较简陋.
     - 无产品文档,无法直观具体了解产品.
     - 在线平台不保存测试用例,也不集成测试套件,只能进行线下编辑测试用例,自动化可视化测试能力不足.
     - 测试报告中有一些不完整,如测试用例日志,需要在命令行中查看.
   
- Visual UI Testing.

  <a href='https://screener.io/'>Visual UI Testing Screenshot</a>.

    - 结论.

      - 可进行多终端UI截图,进行对比.
      - 可下载、分享截图或者截图列表压缩包.
      - 根据账号保存每次截图列表历史.
      - 可配置各终端的分辨率.

    - 问题.

      - 需要合作公司的有资质的账号进行注册才可实行多终端UI截图.
      - 不可预定日程(每天、每个周、每个月)进行截图.
      - 不可实行本地终端UI截图.

> <a href='https://crossbrowsertesting.com'>CrossBrowserTesting</a>

- CrossBrowserTesting配合Appium.

  <a href='https://crossbrowsertesting.com/automated-testing/appium'>NodeJS With Appium in CrossBrowserTesting</a>.

  - 结论.

    - 支持多语言编写测试用例(python、java、ruby、js、PHP、c#等).
    - 做到了跨浏览器自动化测试比较完备且成熟的流程.
    - 测试报告: 截图、录屏、网络日志、Appium日志以及移动设备日志俱有.

  - 问题.

    - API、技术文档无任何引导,且比较简陋.
    - 无产品文档,无法直观具体了解产品.
    - 在线平台不保存测试用例,也不集成测试套件,只能进行线下编辑测试用例,没有做到完全自动化可视化测试.
    - 测试报告中有一些不完整,如测试用例日志,需要在命令行中查看.

- Visual UI Testing.

  <a href='https://support.smartbear.com/crossbrowsertesting/docs/visual-testing/visual-testing.html'>Visual UI Testing Screenshot</a>.

    - 结论.

        - 可进行多终端UI截图,进行对比.
        - 可下载、分享截图或者截图列表压缩包.
        - 根据账号保存每次截图列表历史.

    - 问题.

        - 需要合作公司的有资质的账号进行注册才可实行多终端UI截图.
        - 不可预定日程(每天、每个周、每个月)进行截图.
        - 不可实行本地终端UI截图.
        - 不可配置各终端的分辨率.

> <a href='https://www.aznfz.com/'>冰狐智能辅助</a>

  不使用Appium,有自己开发的一套移动端自动化测试工具.

  <a href='https://www.aznfz.com/mobile-terminal/about'>冰狐智能辅助 - 移动端</a>.

  - 问题.

    - 只适用Android自动化测试.
    - 需要开发者自己准备设备,无在线真机调试,没有做到在线跨终端测试.
    - 只支持Javascript编写测试用例.
    - 在线平台不保存测试用例,也不集成测试套件,只能进行线下编辑测试用例,自动化可视化测试能力非常欠缺.
    - 无产品概念,无测试报告,只是单一的一种工具.


  - Visual UI Testing.

    无Visual UI Testing功能.