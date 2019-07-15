## 简介

Tencent Serverless Toolkit for VSCode 是腾讯云 Serverless 产品的 VSCode (Visual Studio Code) IDE 的插件，该插件可以让客户更好的在本地进行 Serverless 项目开发和代码调试，并且轻松将项目部署到云端。

## 功能特性

通过该VSCode插件，你可以：
* 拉取云端的云函数列表，并触发云函数
* 在本地快速创建云函数项目
* 在本地开发、调试及测试你的云函数代码
* 使用模拟的 COS、CMQ、CKafka、API 网关等触发器事件来触发函数运行
* 上传函数代码到云端，更新函数配置

## 安装与配置

### 前置依赖

Tencent Serverless可以在Windows，Linux和MacOS中安装。在安装Tencent Serverless之前，需要确保系统中已有以下组件/信息：

- VS Code ：在[VSCode下载页面](https://code.visualstudio.com/)下载对应的IDE并安装 ；**版本要求 ：v1.33.0 +** 
- Python 2.7+ 或 Python 3.6+，以及pip
- SCF CLI ：VSCode插件借助于SCF 命令行工具进行本地函数的创建，触发和调试，可以通过`pip install scf` 进行组件的安装，可前往查看[CLI 详细安装教程](<https://cloud.tencent.com/document/product/583/33449>)
- 对应的开发语言环境：当前主要支持 Node.js 和 Python 的开发环境
- 腾讯云账户

### 安装插件

1. 打开VS Code IDE
2. 在IDE左侧栏选择扩展选项，打开VS Code插件市场

![Alt text](https://main.qcloudimg.com/raw/a7e6bf1febac343694ed571bffcda587.png)

3. 在插件市场中搜索"Tencent Serverless 插件"，查看详情并点击【安装】
4. 安装完毕后，左侧栏中会展示已安装完毕的Tencent Serverless 插件。

### 配置插件
1. 打开左侧的VS Code插件，点击创建一个腾讯云用户凭证。从腾讯云控制台获取到账号的 APPID，SecretId及 SecretKey 信息，作为插件调用云API 时的认证信息。之后选择希望部署函数的地域，依次填写到VS Code插件中。

![Alt text](https://main.qcloudimg.com/raw/fca11ef6e54287f2ad400d34123872c9.png)

> 注：如你已经在SCF CLI中配置了账户信息，则不需要再次配置，即可自动获取本机存储的账户信息。

各个配置信息的获取位置如下：

- 地域：产品期望所属的地域。地域列表及对应的英文写法可 [点此](https://cloud.tencent.com/document/product/213/6091#.E4.B8.AD.E5.9B.BD.E5.A4.A7.E9.99.86.E5.8C.BA.E5.9F.9F) 参阅。
- 账号 ID：即 APPID。通过访问控制台中的【账号中心】>【[账号信息](https://console.cloud.tencent.com/developer)】，可以查询到您的账号 ID。
- SecretID 及 SecretKey：指云 API 的密钥 ID 和密钥 Key。您可以通过登录【[访问管理控制台](https://console.cloud.tencent.com/cam/overview)】，选择【云 API 密钥】>【[API 密钥管理](https://console.cloud.tencent.com/cam/capi)】，获取相关密钥或创建相关密钥。

### 初始化函数项目

配置插件完毕后，可以看到对应地域的云端函数列表。点击创建一个函数，可以在本地初始化新的函数项目。

![Alt text](https://main.qcloudimg.com/raw/ff066429770ebeb8eeaca0e104a1839a.png)

依次选取函数所在的命名空间，运行时 runtime，和函数名等信息。填写完毕后，列表页中会展示新建的本地函数。

【注意】**当前暂不支持不同的命名空间（无论是否在同一区域）下创建同名的本地函数**。

### 本地触发函数项目

点击左侧列表页中的本地函数，点击【本地调用】按钮，即可对函数进行本次地测试（当前仅支持 Python 及Node.js 函数的本地触发能力。）

![Alt text](https://main.qcloudimg.com/raw/f9d01294c4fb00b30d0ff14cd244f7fc.png)

### 本地调试函数项目

针对Node.js函数，可以利用SCF CLI的本地调试能力，结合VS Code插件进行本地调试。首先在本地编辑页面，给函数打断点。

​![Alt text](https://main.qcloudimg.com/raw/a625eb3c81f4eb23e414ef14cfdb1533.png)

之后点击左侧列表页中本地函数，点击【开启调试模式】，并且点击【本地调用】。
![Alt text](https://main.qcloudimg.com/raw/c0d91380867a84e864df7054d6b6f96e.png)

在VS Code IDE左侧点击调试页（或 ctrl+shift+D），新建调试的配置文件，并且**选择`SCF LocalFuncDebugger`本地调试的模板**。点击执行按钮，即可看到调试信息。

**注意：不同的 runtime 须选择对应的调试模板，即根据当前的调试文件类型，区分选择 Python 和 Node**
![Alt text](https://main.qcloudimg.com/raw/d6539c72d90042a57fc3fa9ba866200e.png)

![Alt text](https://main.qcloudimg.com/raw/338fee7416572046cec6df6adf006561.png)

### 函数部署

本次开发、调试完毕后，可以通过插件能力将函数一键部署到云端。
在VS Code插件中，点击左侧目录树中的函数名称，在右侧页面中点击【上传函数】按钮，等待函数上传完毕。即可在云控制台列表页中查看到函数的相关信息。
![Alt text](https://main.qcloudimg.com/raw/37c46e1985e94cefaf200c9b3f61d40d.png)

### 远端函数操作

#### 远端调用

针对远端的函数，可以通过VS Code插件进行云端的触发，更改事件模板等操作。在VS Code插件中，点击左侧目录树中的云端函数名称，在右侧页面中点击【云端调用】按钮，即可在页面中查看到函数在云端运行的相关信息。
![Alt text](https://main.qcloudimg.com/raw/6bdaa2ad38e04ce6c16c51992e72aeeb.png)



#### 导入本地

如果您已经在[腾讯云云函数控制台](<https://console.cloud.tencent.com/scf/list?rid=1&ns=default>)创建了函数，则可以在 vscode 插件里直接导入到本地。  

在目标函数上**点击右键**，选择**导入到本地**，右下角弹框选择 ’yes‘  即可：

![Alt text](https://main.qcloudimg.com/raw/adfa4b5b72da09b69478274feaad142a.png)

点击左侧列表右上角【刷新】按钮，即可看到导入到本地的函数。在目标函数**点击右键**，选择**编辑代码**，即可打开对于函数代码编辑视图：  

![Alt text](https://main.qcloudimg.com/raw/90a0facf61d0a8867d9040f2aa512f59.png)

### 测试模板

本地调用时，可以根据函数功能选择不同的测试模板，也可以自定义模板：

![Alt text](https://main.qcloudimg.com/raw/7c4ae9b49a457663a626ccf4ae893772.png)

您可以[前往此处](<https://cloud.tencent.com/document/product/583/9705>)了解更多测试模板相关内容。  

## 欢迎交流

如果您对 Tencent Serverless 感兴趣，您可以加入QQ群（537539545）与我们交流。

![Alt text](https://main.qcloudimg.com/raw/bc881547d1cd2043ecf1b286c70f7319.png)