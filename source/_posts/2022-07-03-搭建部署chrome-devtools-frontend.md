---
title: 搭建部署devtools-frontend
date: 2022-07-03 01:50:28
tags: [devtools-frontend,chrome]
categories: chrome-devtools-frontend
---
# devtools-frontend

> 原理分析

原理在<a href='https://www.cnblogs.com/vivotech/p/15735242.html'>《DevTools 实现原理与性能分析实战》</a>和<a href='https://zhaomenghuan.js.org/blog/chrome-devtools-frontend-analysis-of-principle.html'>《Chrome DevTools Frontend 运行原理浅析》</a>这两篇文章中实际上已经说得很清楚了,整个 Devtools 实现 PC 端: chrome浏览器,Android客户端: chrome 浏览器、App webview中调试都是完全依赖了 Chromium 浏览器内核,其高性能的Blink(之前是Webkit)渲染引擎使得这一套生态得以实现.

> 源码下载及编译

DevTools Frontend 属于 Chromium 完全独立的一部分,代码托管在 Google 开源仓库上,代码开源可以从这里下载(但是不推荐,因为源代码不全,无法进行检出和编译): <a href='https://chromium.googlesource.com/devtools/devtools-frontend/'>Chromium DevTools Frontend</a> 或 <a href='https://www.npmjs.com/package/chrome-devtools-frontend'>GitHub DevTools Frontend 镜像</a>.DevTools Frontend 基于 GN 构建.

  - 构建系统

    构建系统实际上就是一套编译规则,将无数的源代码文件根据一定的顺序和策略来进行编译,模块划分、编译成动静态库,最后链接成可执行代码通过构建系统的编译可以大大提升开发人员的工作效率.比如很常见的 GNU Makefile,但编写 GNU Makefile 是一件繁琐和乏味的事情,而且极容易出错.这时就出现了生成 GNU Makefile 的工具,比如 cmake、AutoMake 等等,这种构建系统称作元构建系统（meta build system）,如在Linux上软件仓库的概念还没有普及的时候,通常我们安装软件的步骤是:

        ./configure
        make
        make install

  - Chromium 中的构建系统

    几年前的chromium开源项目采用的是 GYP (Generate Your Projects）构建系统,这也是一种元构建系统.软件工程师根据 GYP 规则编写构建工程文件（通常以 gyp, gypi 为后缀）,GYP 工具根据 gyp 文件生成 GNU Makefile.接着chromium 项目又搞出了 Ninja 构建系统,但 Ninja 并不是用来取代 GYP 的,而是取代 GNU Makefile 的,据 Google 官方的说法是速度有了好几倍的提升.但对于开发者而言, 不需要去深入了解 GYP 或 GN 这样的元构建系统，因为这只是一种中间输出，所以 ninja 的出现，与开发者关系不大，原来怎么写 gyp，现在还是怎么写，只是构建命令稍微做了改变。GN 文件相当于 gyp 文件的下一代，和 GYP 差别不大，但是总体上比原来的 GYP 文件更清晰.

  - GN 元构建系统

    GN 是一种元构建系统,生成 Ninja 构建文件（Ninja build files）,相较 GYP 而言,有很大的优点:

       1. 可读性更好，更容易编写和维护.
       2. 速度更快，Google 官方给的数据是 20 倍的速度提升.
       3. 修改 GN 文件后,执行 ninja 构建时会自动更新 Ninja 构建文件.
       4. 更简单的模块依赖,提供了 public_deps, data_deps 等,在 GYP 中,只有一种目标依赖,导致依赖关系错综复杂,容易引入不必要的模块依赖.
       5. 提供了更好的工具查询模块依赖图谱: 这在 GYP 构建系统中是一个噩梦,要查一个目标依赖哪些模块或者一个模块被哪些目标依赖几乎是不可能的.
       6. 更好的调试支持: 在 GN 中，只需要一条 print 语句就可以解决.


  - depot_tools

    depot_tools是一个工具集,里面包含了gclient、gcl、gn和ninja等工具,用来下载、编译、运行 和调试 Chromium 中的独立的项目,所以为了学习 Chromium 代码,下载安装 depot_tools 是前提.

        git clone https://chromium.googlesource.com/chromium/tools/depot_tools.git

    Tips: 这里使用终端下载 depot_tools 需要将终端或者 git 设置 VPN,否则会超时导致不能下载.

        # 终端临时设置 VPN
        export http_proxy=http://127.0.0.1:7890/
        export https_proxy=$http_proxy

        # 全局 git 设置 VPN
        git config --global http.proxy http://127.0.0.1:7890/
        git config --global https.proxy http://127.0.0.1:7890/

    打开 ~/.bash_profile 文件，将 depot_tools 添加到环境变量中,这样 depot_tools 里的工具命令就添加到了全局变量中(/path/to/depot_tools 为你 depot_tools 本地的路径).

        vim ~/.bash_profile
        export PATH=$PATH:/path/to/depot_tools

    更新环境变量,立即生效命令.

        source ~/.bash_profile

    这样所有的下载、编译、运行 和调试 Chromium 中的独立的项目的工具命令就全存在在全局变量中了,包括 GN 元构建系统.

  - 源码下载

        # fetch 也是 depot_tools 中的工具命令.
        fetch devtools_frontend

    Tips: 这里使用终端下载 devtools_frontend 需要将终端或者 git 设置 VPN,否则会超时导致不能下载.

        # 终端临时设置 VPN
        export http_proxy=http://127.0.0.1:7890/
        export https_proxy=$http_proxy

        # 全局 git 设置 VPN
        git config --global http.proxy http://127.0.0.1:7890/
        git config --global https.proxy http://127.0.0.1:7890/

    PS: 如果电脑上装的是 python 3.x 的话,会出现证书验证失败的错误,需要手动验证激活,点击 Install Certificates.command 即可手动验证激活.

        urllib.error.URLError: <urlopen error [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed: unable to get local issuer certificate (_ssl.c:1108)

    ![](https://image.white-than-wood.zone/devtools_frontend/urlError.png)

    若出现以下内容:

    ![](https://image.white-than-wood.zone/devtools_frontend/glicent.png)

    说明资源发生了更新,运行以下命令来下载代码.

        gclient sync

    - gclient

      gclient 是由 Google 用 Python 开发的一套跨平台的 git 仓库管理工具,它的作用类似 git 的 submodule，用来将多个 git 仓库组成一个 solution 进行管理，比如 chromium 项目是由80多个独立的 git 仓库构成的.gclient sync 就是同步更新最新的代码资源.

  - 编译

        cd devtools-frontend
        # GN 构建系统新生成一个编译目录,并产出 Ninja 构建文件
        gn gen out/Default
        # 运行 Ninja 构建文件进行根据编译规则实行编译
        autoninja -C out/Default

    编译生成的文件可以在 out/Default/gen/front_end 中找到.

> 基于Chrome运行

  根据<a href='https://chromium.googlesource.com/devtools/devtools-frontend/+/HEAD/docs/workflows.md#Integrated-checkout'> Devtools Frontend Workflows </a>以及<a href='https://docs.google.com/document/d/1COgCBWWuTh2o-Zbp6h_z0h0LtlJaimaEDsION4RZPxc/edit#heading=h.406e03aq0xjm'> DevTools debugging workflow -> Existing workflows </a>可知,原有的基于 DevServer 运行 DevTools 方式(npm start)已经移除,Chromium 79版本之后统一使用 --custom-devtools-frontend 方式.

  - Chrome Canary

      众所周知,Chrome = Chromium + Google产品集,那么Chrome Canary是什么呢? Chrome Canary 是更新速度最快的 Chrome 版本,几乎每天更新且支持自动更新,也是功能、代码最先进的 Chrome 版本,可独立安装、与其他版本的 Chrome 程序共存,适合进阶用户或开发者人员安装备用,尝鲜最新功能,由于是每日更新的 Chrome Dev 版本,极其不稳定.

      Chrome Dev 是 Chrome 的开发者版本,每个周更新 1-2 次,虽然该版本已经过测试,但仍可能存在一些问题,但比 Chrome Canary 更稳定.

      Chrome Beta 是 Chrome 的测试版本,每周更新一次,而每 4 周会进行一次重大的可纳入到稳定版本的更新.

  - 通过文件系统运行

        <path-to-devtools-frontend>/third_party/chrome/chrome-<platform>/chrome --custom-devtools-frontend=file://$(realpath out/Default/gen/front_end)

    Tips: file://...在 Mac 和 Linux 上,文件 url 必须以三个斜杠开头,$(realpath out/Default/gen/front_end)扩展的 Devtools Frontend 目录路径必须为绝对路径.
    PS: 为了避免代价昂贵的 Chromium 构建,可以在预构建的 Chromium 中运行 DevTools Frontend.例如,可以使用最新版本的 Chrome Canary,或者使用 third_party/chrome 中下载的二进制文件.

    - 实际演示

      运行以下命令:

            ./third_party/chrome/chrome-mac/Chromium.app/Contents/MacOS/Chromium --custom-devtools-frontend=file:///Users/yinwk/keryi/devtools-frontend/out/Default/gen/front_end/

      <video muted controls="controls" autoplay="autoplay" loop="loop" style="width:100%;">
        <source src="https://image.white-than-wood.zone/devtools_frontend/fileSystem.mp4" type="video/mp4" />
      </video>

      终端显示:

      ![](https://image.white-than-wood.zone/devtools_frontend/fileSystem.png)
    
  - 通过Server运行

    将 out/Default/gen/front_end 的内容放入本地服务器,比如运行:

        python -m http.server

    这里用的是http-server.

        cd out/Default/gen/front_end
        http-server -p 8000

    ![](https://image.white-than-wood.zone/devtools_frontend/remoteUrl.png)

    - 实际演示

      运行以下命令:

            ./third_party/chrome/chrome-mac/Chromium.app/Contents/MacOS/Chromium --custom-devtools-frontend=http://localhost:8000/

      <video muted controls="controls" autoplay="autoplay" loop="loop" style="width:100%;">
        <source src="https://image.white-than-wood.zone/devtools_frontend/remoteUrl.mp4" type="video/mp4" />
      </video>

      终端显示:

      ![](https://image.white-than-wood.zone/devtools_frontend/remoteUrlShow.png)

  - 通过远程连接运行

    将 out/Default/gen/front_end 的内容放入本地服务器,比如运行:

        python -m http.server

    这里用的是http-server.

        cd out/Default/gen/front_end
        http-server -p 8000
        
    ![](https://image.white-than-wood.zone/devtools_frontend/remoteUrl.png)

    - 实际演示

      运行以下命令:

            # 设置远程调试接口为 9222
            ./third_party/chrome/chrome-mac/Chromium.app/Contents/MacOS/Chromium --custom-devtools-frontend=http://localhost:8000/ --remote-debugging-port=9222