# Akode - Android C++ IDE

<p align="center">
  <img src="https://img.shields.io/badge/Platform-Android-green.svg" alt="Platform">
  <img src="https://img.shields.io/badge/Language-C%2FC%2B%2B-blue.svg" alt="Language">
  <img src="https://img.shields.io/badge/Version-1.0.1-orange.svg" alt="Version">
</p>

Akode 是一款专为 Android 平台设计的 C/C++ 集成开发环境（IDE），让你可以在手机上编写、编译和运行 C/C++ 代码。无需电脑，随时随地进行 C/C++ 开发。

## ✨ 功能特性

### 🖥️ 代码编辑器
- 基于 Sora Editor 的专业代码编辑器
- C/C++ 语法高亮（TextMate 语法支持）
- 智能代码补全
- 括号匹配高亮
- 行号显示
- 当前行高亮
- 多文件标签页管理（最多10个）
- 符号快捷输入栏
- 支持多种编辑器主题

### 🔧 编译运行
- 内置 GCC/G++ 编译器（首次启动自动安装）
- 支持 C 语言（.c）和 C++ 语言（.cpp/.cc/.cxx）
- 自定义编译参数
- 自定义编译命令管理
- 支持 Root 权限运行程序
- 编译错误定位和标记

### 📁 文件管理
- 侧边栏文件浏览器
- 支持新建文件/文件夹
- 文件重命名、删除、复制路径
- 快速定位当前文件
- 记住上次打开的文件和目录

### 💻 终端模拟器
- 完整的终端环境
- 支持常用 Shell 命令
- 可调节字体大小和样式
- 底部快捷操作栏
- 屏幕常亮选项

### 🧩 插件系统
- 支持安装第三方插件（ZIP格式）
- 插件 ABI 选择（arm64-v8a / x86_64）
- 插件启用/禁用管理
- 查看插件示例代码

## 📱 系统要求

- Android 5.0 (API 21) 及以上
- 支持架构：arm64-v8a、x86_64
- 存储空间：约 100MB（含 GCC 工具链）
- 需要存储权限（访问文件系统）

## 🚀 快速开始

### 安装
1. 下载 `Akode_x.x.x_release.apk`
2. 安装 APK（可能需要允许安装未知来源应用）
3. 首次启动会自动安装 GCC 工具链，请耐心等待

### 编写第一个程序
1. 点击主页的「代码编辑器」进入编辑器
2. 编写你的 C/C++ 代码，例如：
```cpp
#include <stdio.h>

int main() {
    printf("Hello, Akode!\n");
    return 0;
}
```
3. 点击工具栏的运行按钮（▶）编译并运行

## 📖 使用指南

### 编辑器操作

| 操作 | 说明 |
|------|------|
| 左滑屏幕边缘 | 打开文件浏览器 |
| 点击标题栏文件名 | 切换已打开的文件 |
| 长按标题栏文件名 | 查看完整文件路径 |
| 长按保存按钮 | 另存为 |
| 底部符号栏 | 快速输入常用符号 |

### 文件浏览器

| 操作 | 说明 |
|------|------|
| 点击文件夹 | 进入目录 |
| 点击文件 | 打开文件 |
| 长按文件/文件夹 | 显示操作菜单（重命名、删除、复制路径等） |
| 点击路径栏 | 手动输入路径跳转 |
| 长按路径栏 | 复制当前路径 |
| 📍 按钮 | 定位到当前文件所在目录 |
| ➕ 按钮 | 新建文件 |
| 📁 按钮 | 新建文件夹 |

### 编译运行

| 操作 | 说明 |
|------|------|
| ▶ 运行按钮 | 编译并运行当前文件 |
| 长按运行按钮 | 设置运行参数 |
| 编译模式切换 | 单文件模式 / 多文件模式 |

### 终端操作

| 操作 | 说明 |
|------|------|
| 底部工具栏 | 常用快捷键（Tab、Ctrl、Alt 等） |
| 双指缩放 | 调整字体大小 |
| 长按屏幕 | 粘贴文本 |

### 插件管理

| 操作 | 说明 |
|------|------|
| ➕ 按钮 | 安装插件（选择 ZIP 文件） |
| 点击插件 | 查看插件示例代码 |
| 长按插件 | 删除插件 |
| 点击 ABI 标签 | 切换插件 ABI |
| 开关按钮 | 启用/禁用插件 |

## ⚙️ 设置选项

### 编辑器设置
- **记住上次打开的文件**：下次启动时恢复上次的文件和目录
- **编辑器字体大小**：12-24sp 可选
- **编辑器主题**：Darcula（暗色）等主题

### 终端设置
- **终端字体大小**：10-24sp 可选
- **终端字体**：Monospace、Sans Serif、Serif
- **显示底部操作栏**：控制快捷键栏显示

### 编译设置
- **编译命令管理**：自定义编译和运行命令
- **GCC 编译参数**：C 语言编译参数（默认：`-lm -ldl -llog -lz -std=c99 -Wfatal-errors -Os -s -pie`）
- **G++ 编译参数**：C++ 编译参数（默认：`-lm -ldl -llog -lz -std=c++14 -Wfatal-errors -Os -s -pie`）

### 功能设置
- **启用 Root 运行**：使用 su 以 root 权限执行程序
- **自定义 SU 命令**：Root 运行时使用的 su 命令（默认：`su -c`）
- **启用日志**：开启终端操作日志记录
- **保持屏幕常亮**：终端运行时保持屏幕不熄灭

### 高级设置
- **清除缓存**：清除应用缓存和临时文件
- **导出日志**：导出终端操作日志文件

## 🔌 插件开发

### 插件结构
```
plugin.zip
├── .config          # 插件配置文件（JSON格式，必需）
├── lib/
│   ├── arm64-v8a/   # arm64 架构的 .so 文件
│   └── x86_64/      # x86_64 架构的 .so 文件
├── include/         # 头文件
└── example/         # 示例代码
```

### 配置文件格式（.config）
```json
{
  "pluginCode": "my_plugin",
  "pluginName": "我的插件",
  "pluginVersion": "1.0.0",
  "pluginDescribe": "插件描述",
  "supportABI": ["arm64-v8a", "x86_64"]
}
```

## 🙏 致谢

Akode 的开发离不开以下开源项目：

- [Sora Editor](https://github.com/Rosemoe/sora-editor) - 代码编辑器组件
- [Termux](https://github.com/termux/termux-app) - 终端模拟器
- [libsu](https://github.com/topjohnwu/libsu) - Root 权限访问库
- [Material Components](https://github.com/material-components/material-components-android) - Material Design 组件库
- [C4droid](https://baike.baidu.com/item/c4droid/8215130) - Android 平台 C/C++ 编程工具
- [simpleC](https://github.com/luoyesiqiu/simpleC) - Android 平台 C/C++ 编程工具

## 👨‍💻 开发者

**阿夜** - [GitHub](https://github.com/AYssu)

---

如有问题或建议，欢迎反馈！
