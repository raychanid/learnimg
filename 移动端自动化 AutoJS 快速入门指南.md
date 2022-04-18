之前写过很多 App 端自动化的文章，大都基于 Appium、Airtest、无障碍服务等技术来实现的

其中，Appium 和 Airtest 编写的自动化脚本都依赖于 PC 端运行，没有办法直接运行在移动端；无障碍服务需要单独创建一个 Android 项目，没有完整的使用文档，使用起来有一定的门槛

从本篇文章开始，介绍一款可以直接运行在移动端的自动化工具：AutoJS

2. AutoJS 介绍
AutoJS 类似于按键精灵，它是 Android 平台上的一款自动化工具，它通过编写 JavaScript 脚本，结合系统的「 无障碍服务 」对 App 进行自动化操作

官方文档：https://pro.autojs.org/docs/#/zh-cn/

它的优势包含：

使用 JS 编写脚本，代码可读性强
脚本文件体积小，可以打包成 APK 直接安装
拥有丰富的 UI 组件用于构建 GUI 界面
非 Root 设备也能完成自动化操作，可以摆脱 PC 直接运行
提供多种元素定位方式，可以适配各种机型
官方文档非常详细，学习成本低
3. 准备
AutoJS 拥有多个版本，其中最常用的两个版本分别是：Auto.js Pro、Auto.js 4.1.1 Beta

PS：由于某些原因，AutoJS 作者现在只对 Auto.js Pro 版本进行维护，并且 Auto.js Pro 对部分主流 App 进行了限制

原因：https://pro.autojs.org/faq

后面的文章都是以 Auto.js 4.1.1 Beta 为例进行讲解（ 文末有提供下载方式 ）

首先，下载 VS Code 软件和 2 个插件

2 个插件包含：

Auto.js-VSCodeExt
Auto.js-VSCodeExt-Fixed
其中，Auto.js-VSCodeExt-Fixed 对插件 Auto.js-VSCodeExt 进行了部分优化，更加方便我们调试脚本

然后，使用 VS Code 快捷键「 Ctrl/Command + Shift + P 」，选择「 Auto.js:Start Server 」开启 AutoJS 服务

接着，在真机或模拟器安装 AutoJS 应用及 AutoJS 打包工具应用

PS：如果使用模拟器，推荐使用网易 MuMu 或雷电模拟器

打开 AutoJS 应用，首次进入应用关闭更新提示对话框，并按照指引开启「 无障碍服务 」


在软件主界面，点击左上角滑出侧边栏，依次打开无障碍服务、前台服务、悬浮窗

前台服务用于提升服务的存活率，防止服务被回收掉


悬浮窗会悬浮在任意界面之上，提供一些快捷功能操作，具体包含：

文件项目列表
会展示示例代码及自己编写的脚本、文件夹，可以快速完成脚本编辑、运行、定时任务、打包等操作
脚本录制
录制脚本，仅适用于 Root 后的设备，由于它基于坐标点，适配性不强，所以很少使用
元素控件定位
针对当前界面进行布局控件分析、布局层次分析
关闭正在执行的脚本
一键停止所有正在执行的脚本任务
更多设置
可以快速进入到「无障碍服务」页面、查看当前应用包名及 Activity 名称等
最后，选中软件侧边栏中的「 连接电脑 」这一项，在对话框中输入 PC 的 ip 地址

PS：AutoJS 连接电脑时如果没有报错，VS Code 通知栏和 OUTPUT 会展示设备连接成功的消息


4. 实战一下
在完成上面的准备工作后，我们就可以在 VS Code 中使用 JS 编写自动化脚本了

这里以自动刷抖音短视频为例

首先，使用「 auto.waitFor() 」确保无障碍服务开启成功

然后，使用 launchApp + 应用名称，快速启动抖音 App

接着使用界面元素内容 + waitFor() 方法等待元素出现，代表界面加载完成

最后，使用 Root + Swipe + 坐标点模拟界面滑动

PS：这里为了方便，直接使用 Root 设备的 API 方法，如果是非 Root 设备，可以采用官方提供的滑动 API 或控件中心坐标点击事件来实现

完整代码如下：

auto.waitFor()

//打开抖音App
var appName = "抖音";
(appName);

//等待进入主界面成功
text("首页").waitFor();

toast("准备开始滑动")

//滑动（Root+坐标点）
while (true) {
    Swipe(200, 1000, 210, 400, 500);
    //休息5s钟
    sleep(5000);
    toast("继续滑动。。。")
}
5. 最后
本篇文章介绍了 AutoJS 最基础的使用步骤，并通过一个简单的实例讲解其用法
