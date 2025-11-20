---
title: Gemini Cli
date: 2025-11-20 10:50:00 +0800
categories: [ai]
tags: [ai, vibe coding]
description: "Google Gemini Cli"
---

## 一、什么是 Gemini Cli

Gemini Cli 是围绕 Google 的 Gemini 大语言模型开发的命令行工具（Command-Line Interface），允许用户通过终端直接与 Gemini 模型交互，无需依赖图形界面。它支持文本生成、对话交互、文档处理等功能，适合开发者或习惯终端操作的用户快速调用 Gemini 的能力，例如生成代码、撰写文档、回答问题等。

优势：

+ 支持 1M token上下文内容
+ 占用CPU、内存较低（相对trae）
+ 支持学生认证
+ Gemini API标准套餐，每分钟限制2次频率，Gemni-2-Pro限制每日50次回复；Gemin-3-Pro。

## 二、创建 API Token

可以找我借一个用，就不用自己申请了。

获取 Gemini API 密钥**，**首先需要在 [<font style="color:rgb(36,91,219);">Google AI Studio</font>](https://makersuite.google.com/) 注册并创建 API 密钥，用于调用 Gemini 模型。

## 三、安装 Gemini Cli

官方地址：https://github.com/google-gemini/gemini-cli?tab=readme-ov-file

### 3.1 配置代理

#### 3.1.1、方式一：端口代理

确认端口，Clash代理（其他vpn同理）：

![](https://cdn.nlark.com/yuque/0/2025/png/40359153/1759134007112-6b57a8dd-c20a-4e74-988f-7e48b8a742b9.png)

进入PowerShell，配置代理端口

```plain
# 建议先开代理，配置代理端口
$env:http_proxy="http://127.0.0.1:7898"
```

#### 3.1.2、方式二：tun模式

全局生效，cmd窗口不需要配置代理。缺点是微信收不到消息或很慢，慎用。

### 3.2 安装

注意：需要nodejs环境

#### 3.2.1、npm（推荐）

```plain
# npm安装打印进度
npm install -g @google/gemini-cli --verbose

# 检查gemini版本号，确认安装完毕
gemini --version
```

#### 3.2.2、npx

```plain
# Using npx (no installation required)
npx https://github.com/google-gemini/gemini-cli

# 会自动打开gemini cli
```

### 3.3 配置 API KEY

推荐使用PowerShell窗口运行

```plain
# 记得使用“端口代理”或“tun模式”

# 设置 API 密钥
$env:GEMINI_API_KEY=""

# 启动1 npm全局安装模式，注意需要环境变量到node目录
gemini

# 启动2 Gemini Cli，注意先cd到工程目录，再启动
npx https://github.com/google-gemini/gemini-cli
```

+ 配置代理、API KEY 截图：

![](https://cdn.nlark.com/yuque/0/2025/png/40359153/1759134007132-5cdc1542-904b-42fe-9676-5177e9b76ddb.png)

+ 选择Use Gemini API Key

![](https://cdn.nlark.com/yuque/0/2025/png/40359153/1759134007134-cf5271b1-bc36-4752-ab8c-ccf7a0af7707.png)

+ 启动成功截图

![](https://cdn.nlark.com/yuque/0/2025/png/40359153/1759134007146-a6787ef0-e677-48b6-ac8e-0bc4df42ffa6.png)

## 四、使用 Gemini Cli 

### 4.1、输入指令

![](https://cdn.nlark.com/yuque/0/2025/png/40359153/1759134007166-c7349e29-a447-4b0e-8b75-a2c604ff86f9.png)

+ 不建议输入&&或者其他符号到命令行，可能触发下文5.3的"Command exited with code 1. "报错

### 4.2、切换模型（限额说明）

+ gemini（默认gemini pro）：每日限额50次回复
+ gemini -m gemini-3-pro-preview：免费层级用户没权限，第一层级每天1k次
+ gemini -m gemini-2.5-flash：基本无限制

### 4.2、统计Token

每次退出Gemni后，自动统计

![](https://cdn.nlark.com/yuque/0/2025/png/40359153/1759134007805-372cb429-b782-44b6-bb35-459cda59ca1b.png)

## 五、注意事项 & 问题

### 5.1、支持历史对话吗？

不支持，每次运行 npx gemini cli 都会启动一个新的会话，之前的对话历史不会被自动记忆。

推荐使用标准技术文档方式，用文档记录重要内容，比如日常使用如下：

① 编写技术规范md文件：GEMINI.md（放项目根目录下）

② 启动Gemini Cli后，输入交互指令（系统会自动读取GEMINI.md）：
迁移xxx接口，实现xxx

### 5.2、fetch failed sending request

[API Error: exception TypeError: fetch failed sending request]

网络波动，VPN换个好的

### 5.3、Command exited with code 1. 

![](https://cdn.nlark.com/yuque/0/2025/png/40359153/1759134008009-a43563fe-26eb-4262-8ab6-8d968ae6adf1.png)

Ctrl+C退出，重新进入

### 5.4、code 429. Limit: 50

Gemini Pro每日限额50次回复，这时候需要切换到`gemini-2.5-flash`模型使用：

```plain
gemini -m gemini-2.5-flash
```

![](https://cdn.nlark.com/yuque/0/2025/png/40359153/1759134007820-c894a378-2d6c-40ec-bf95-124c76637f0d.png)

