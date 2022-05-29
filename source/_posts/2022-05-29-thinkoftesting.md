---
title: think of testing
date: 2022-05-29 12:32:35
tags: [testing]
categories: testing
---

# 测试(testing)

## 跨终端自动化测试

### 平台

> <a href='https://www.lambdatest.com/'>lambdaTest</a>

- 手动测试

  - Browser Testing.

    可在线在不同的浏览器种类、版本、操作系统以及分辨率对website进行实时交互式测试,每次真实浏览器sessions可测试10分钟.

    - 可切换配置浏览器种类、版本、操作系统以及分辨率;
    - 可录屏(录屏可下载);
    - 可标记bug(编辑bug截图、下载bug截图以及上传到lambdaTest衍生的SLACK、JIRA和ASANA项目管理系统);

  - App Testing.

    可在线自由搭配不同的品牌手机、版本设备对App包或者App Url进行实时交互式测试,每次真机测试sessions可测试10分钟.

    - 可切换配置品牌手机以及版本设备;
    - 可录屏(录屏可下载);
    - 可标记bug(编辑bug截图、下载bug截图以及上传到lambdaTest衍生的SLACK、JIRA和ASANA项目管理系统);

  - Browser Testing开发环境在线测试.

    可配合lambdaTest桌面应用(LT_Windows or LT_Macs)配合在线网站进行开发环境在线测试.

    - 配置.

      <a href='https://www.lambdatest.com/support/docs/testing-locally-hosted-pages/'>Browser Testing开发环境在线测试</a>. PS:注意看视频中的介绍步骤.

  - 结论.
  
    - 简洁、易用且容易理解;
    - 功能完备,在线随时切换终端设备配置、录屏下载、Debug标记应有尽有;
    - 测试过程流畅、无障碍性困难;
    - 其衍生生态成熟且完备,例如其衍生的一套项目管理系统SLACK、JIRA和ASANA;
    - 为测试人员大大提高了效率,节约了时间成本;

  - 问题.

    - 大部分终端设备不开放.
    - 终端设备开放需要付费.

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

      Selenium IDE能够以插件的形式被安装到测试者的浏览器中,从而方便地实现Web界面的测试.
    
    - lambdaTest配合Selenium IDE.

      <a href='https://www.lambdatest.com/support/docs/run-selenium-ide-tests-on-lambdatest-selenium-cloud-grid/'>Run Selenium IDE Tests with LambdaTest Selenium Grid</a>.

      - 可根据selenium-webdriver事件步骤分帧在录屏中在线查看测试套件自动化测试的情况;
      - 可在线查看在自动化测试过程当中网络资源接口的加载情况;
      - 可下载自动化测试的录屏;
      - 可将标记bug(将有问题的selenium事件步骤分帧上传到lambdaTest衍生的SLACK、JIRA和ASANA项目管理系统);

      - 结论.

        - Selenium IDE是最为流行的一种可视化、自动化测试工具;
        - 无需编辑一行代码,凭借录制操作就可实现编辑测试用例,进而实现可视化、自动化测试;
        - 可视化编辑测试用例流畅并且效果顶级;
        - 与lambdaTest配合相得益彰,做到了跨浏览器自动化可视化测试完备且成熟的流程.

      - 问题

        - 定制性、精确性不足,不如使用Jest配合selenium-webdriver编辑测试用例.

    - selenium-webdriver.

      浏览器自动化库,提供了许多浏览器自动化接口,用于测试web应用.
      
      - api.
      
        <a href='https://www.selenium.dev/selenium/docs/api/javascript/'>selenium-webdriver</a>.

  - App自动化测试工具.

    - Appium.

      Appium是一个开源的,适用于原生或混合移动应用(hybrid mobile apps)的自动化测试工具.
    - Appium支持多App平台(Android、iOS等);
    - Appium支持多语言(python、java、ruby、js、c#等),Appium选择了Client/Server的设计模式,只要client能够发送http请求给server,那么client用什么语言来实现都是可以的,这就是如何做到支持多语言的原因;
    - Appium是跨平台的,可以用在OSX，Windows以及Linux桌面系统上运行;
    - Appium扩展了WebDriver的协议,这样的好处是以前的WebDriver API能够直接被继承过来,以前的WebDriver各种语言的binding都可以拿来就用,省去了为浏览器、App端各开发一个client的工作量;
    - Appium开源免费;

    - lambdaTest配合Appium.

      <a href='https://www.lambdatest.com/support/docs/appium-nodejs-webdriverio/'>WebDriverIO With Appium in lambdaTest</a>.
    
      - 结论.
      
        - 支持多语言编写测试用例(python、java、ruby、js、PHP、c#等).

      - 问题.
    
        - 真机跨终端自动化测试需要付费,无法深层次体验产品.
        - 只有API,没有产品文档,无法了解产品.
    
    - 阿里云移动测试配合Appium.

      <a href='https://help.aliyun.com/document_detail/175761.html'>阿里云移动测试</a>.
    
      - 结论.
        
        - 集成Appium IDE于阿里云平台内部,做到可视化、自动化测试.
        - 录制、编写测试用例二合一,做到了跨浏览器自动化可视化测试完备且成熟的流程.
        - 产品文档完备,可直观了解产品.
        - 测试报告:截图、录屏、测试用例日志、Appium日志、移动设备日志、错误日志以及性能报告一应俱全.
      
      - 问题.
      
        - 只支持Python编写测试用例.
        - 测试报告中有一些不完整,如网络日志.
      
    - browserstack
    
      <a href='https://www.browserstack.com/docs/app-automate/appium/getting-started/nodejs/webdriverio'>WebDriverIO With Appium in browserstack</a>.

      - 结论.

        - API配置有可视化的介绍引导.
        - 支持多语言编写测试用例(python、java、ruby、js、PHP、c#等).
        - 做到了跨浏览器自动化测试比较完备且成熟的流程.
        - 测试报告: 截图、录屏、网络日志、Appium日志、移动设备日志以及性能报告应有尽有.

      - 问题.
        
        - 只有API,没有产品文档,无法了解产品.
        - 在线平台不保存测试用例,也不集成测试套件,只能进行线下编辑测试用例,没有做到完全自动化可视化测试.
        - 测试报告中有一些不完整,如测试用例日志,需要在命令行中查看.

    - saucelabs

      <a href='https://github.com/saucelabs-training/demo-js/tree/main/webdriverio/appium-app/examples/simple-example'>WebDriverIO With Appium in saucelabs</a>.

       - 结论.
      
         - 支持多语言编写测试用例(python、java、ruby、js、PHP、c#等).
         - 做到了跨浏览器自动化测试比较完备且成熟的流程.
         - 测试报告: 截图、录屏、网络日志、Appium日志、移动设备日志以及性能报告应有尽有.

       - 问题.

         - API无任何引导,且比较简陋.
         - 只有API,没有产品文档,无法了解产品.
         - 在线平台不保存测试用例,也不集成测试套件,只能进行线下编辑测试用例,自动化可视化测试能力不足.
         - 测试报告中有一些不完整,如测试用例日志,需要在命令行中查看.