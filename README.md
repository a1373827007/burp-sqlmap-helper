# Sqlmap Burp Suite 插件

一个用于 **Burp Suite** 的 Sqlmap 辅助插件，帮助快速生成 **Sqlmap** 命令并集成到渗透测试工作流程中，简化 SQL 注入检测流程。

## 功能特点

- 一键抓取 Burp 中的 HTTP 请求
- 自动提取请求中的参数（待优化）
- 可视化配置 Sqlmap 参数（注入点、测试级别、风险等级等）
- 自动生成请求文件和完整的 Sqlmap 命令
- 支持打开独立 CMD 窗口执行命令，输出避免问题
- 自动处理路径空格和特殊字符，确保命令兼容性

## 环境要求

- **Burp Suite**（专业版 / 社区版）
- **Jython 2.7.2**（Burp 插件运行环境）
- **Python 3.x**（用于执行 Sqlmap）
- **Sqlmap**（最新版本）
- **Windows**（针对 Windows CMD 优化的系统插件）

## 安装步骤

### 1. 配置 Jython 环境

1. 打开 Burp Suite → Extender → 选项 → Python 环境
2. 点击选择文件，选择 Jython 安装包（如 jython-standalone-2.7.2.jar）
3. 等待 Burp 加载 Jython 环境

### 2. 安装插件

1. 进入 Burp Suite 的 Extender → Extensions
2. 点击 **添加扩展**，扩展类型选择 **Python**
3. 选择插件脚本文件（burp_sqlmap_plugin.py）
4. 点击下一步，插件加载成功后会在 Burp 标签栏显示 Sqlmap 助手

## 使用教程

### 1. 提取目标请求

在 Burp 的代理或目标模块中找到需要测试的 HTTP 请求：

- 右键请求 → 发送到 Sqlmap 助手
- 或在插件的 **1. 提取请求** 标签页手动选择

### 2. 配置 Sqlmap 参数

切换到插件的 **2. sqlmap参数** 标签页，进行以下配置：

- **必填配置**：
  - Python 解释器路径：选择本地 python.exe（如 `C:\Python310\python.exe`）
  - Sqlmap.py 路径：选择 Sqlmap 安装目录下的 `sqlmap.py`（如 `C:\sqlmap\sqlmap.py`）

- **可选配置**：
  - 填充参数（-p）：自动识别请求中的参数，可手动修改
  - 测试级别（--level）：1-5（默认 1）
  - 风险等级（--risk）：1-3（默认 1）
  - 其他参数（代理、线程数等）：根据需求配置

### 3. 生成命令并执行

切换到 **3. 执行命令** 标签页：

- 点击 **生成请求文件**：插件会在临时目录创建请求文件（如 `C:\Users\用户名\AppData\Local\Temp\burp_sqlmap\req_xxx.txt`）
- 点击 **打开 CMD 窗口**：自动打开 CMD 并切换到 Sqlmap 目录
- 点击 **复制命令**：将生成的 Sqlmap 命令复制到 CMD 窗口，粘贴命令并回车执行

## 常见问题

### Q：CMD 窗口未弹出？
A：检查 Sqlmap 配置是否正确。

### Q：“生成的命令为空”？
A：确保 Python 和 Sqlmap 路径配置正确且文件存在，路径中避免特殊情况。

### Q：Sqlmap 执行无响应？
A：检查代理配置（默认 http://127.0.0.1:8080 需与 Burp 代理一致），或关闭代理重试。

### Q：中文乱码？
A：CMD 默认编码为 GBK，插件已改装，若仍乱码可在 CMD 中执行 `chcp 65001` 切换为 UTF-8。

## 许可证

本项目基于 MIT 许可证开源，详情见 LICENSE 文件。欢迎提交问题或 PR 改进插件功能，使用过程中遇到问题请提问题反馈。
