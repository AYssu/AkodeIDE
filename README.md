# Akode - Android C++ IDE

<p align="center">
  <img src="https://img.shields.io/badge/Platform-Android-green.svg" alt="Platform">
  <img src="https://img.shields.io/badge/Language-C%2FC%2B%2B-blue.svg" alt="Language">
  <img src="https://img.shields.io/badge/Version-1.0.7-orange.svg" alt="Version">
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

### 🧠 LSP 智能支持
- 集成 Clangd LSP 服务
- 实时语法错误检测
- 智能代码补全
- 函数签名提示
- 代码诊断和错误标记
- 跳转到定义

### ❤️  编译运行
- 内置 Clang/Clang++ 编译器（首次启动自动安装）
- **OLLVM 代码混淆支持**（基于 Clang 18.1.8）
- 支持 C 语言（.c）和 C++ 语言（.cpp/.cc/.cxx）
- 自定义编译参数
- 自定义编译命令管理
- 支持 Root 权限运行程序
- 编译错误定位和标记
- 编译缓存（相同代码跳过编译）

### 🔐 OLLVM 代码混淆

内置 OLLVM 混淆器，支持多种代码保护方式，增强逆向难度：

| 参数 | 说明 |
|------|------|
| `-mllvm -fla` | 控制流平坦化（Control Flow Flattening） |
| `-mllvm -sub` | 指令替换（Instruction Substitution） |
| `-mllvm -bcf` | 虚假控制流（Bogus Control Flow） |
| `-mllvm -ibr` | 间接分支（Indirect Branching） |
| `-mllvm -sobf` | 字符串混淆（String Obfuscation） |
| `-mllvm -split` | 基本块分割（Basic Block Splitting） |
| `-mllvm -split_num=N` | 指定分割次数（N 为数字） |

使用方式：在「设置 → 编译设置」中开启对应的混淆选项即可。

### 📁 文件管理
- 侧边栏文件浏览器
- 支持新建文件/文件夹
- 文件重命名、删除、复制路径
- 快速定位当前文件
- 记住上次打开的文件和目录
- **Git 状态显示**（修改/新增/冲突等）

### 🔀 Git 集成
- Git 仓库克隆（支持 HTTPS）
- 私有仓库认证（用户名/密码/Token）
- Git 凭据加密存储
- 提交、推送、拉取操作
- 分支管理
- 远程仓库管理
- 文件状态实时显示

### 📦 项目管理
- 新建项目向导
- Git 初始化选项
- 最近项目列表
- 项目配置保存和恢复
- 自动保存功能（可配置间隔）

### 💻 终端模拟器
- 完整的终端环境
- 支持常用 Shell 命令
- 可调节字体大小和样式
- 底部快捷操作栏
- 屏幕常亮选项
- 自动加载插件环境变量

### 🧩 插件系统
- 支持安装第三方插件（ZIP格式）
- 插件 ABI 选择（arm64-v8a / x86_64）
- 插件启用/禁用管理
- 查看插件示例代码
- **插件安装脚本**（.install 文件）
- **插件 Hook 系统**（.hook 文件）
- 插件 PATH 环境变量自动注入

## 🔌 插件安装脚本

插件可以通过 `.install` 文件定义安装流程，支持交互式安装向导。

### 支持的节点类型

| 节点 | 说明 |
|------|------|
| `alert` | 弹窗提示 |
| `edit` | 单行输入框 |
| `select` | 单选/多选列表 |
| `if` | 条件判断分支 |
| `command` | 执行 Shell 命令 |
| `command_result` | 执行命令并获取结果（带 Loading） |
| `grep` | 正则表达式匹配 |
| `add_path` | 添加环境变量路径 |
| `create_value` | 创建变量 |
| `run_in_terminal` | 在终端运行可执行文件 |

### 内置变量

| 变量 | 说明 |
|------|------|
| `${plugin_path}` | 当前插件安装目录 |
| `${plugin_name}` | 插件目录名 |
| `${files_dir}` | 应用 files 目录 |
| `${cache_dir}` | 应用缓存目录 |
| `${current_file}` | 当前编辑器打开的文件路径（Hook 中可用） |
| `${current_dir}` | 当前文件所在目录（Hook 中可用） |

### 示例

```json
{
  "install_before": [
    {"node": "alert", "title": "欢迎", "message": "即将安装 NDK 插件"}
  ],
  "install_start": [
    {"node": "command", "sh": "tar -xzf ${plugin_path}/ndk.tar.gz"}
  ],
  "install_after": [
    {"node": "add_path", "export": "${plugin_path}/bin"}
  ]
}
```

## 🪝 插件 Hook 系统

插件可以通过 `.hook` 文件在特定事件时执行自定义操作。

### 支持的 Hook 类型

| Hook | 说明 | 版本 |
|------|------|------|
| `menu` | 添加编辑器右上角菜单项 | v1.0.2+ |
| `run_menu` | 添加运行按钮下拉菜单项 | v1.0.3+ |
| `toolbar` | 添加工具栏按钮 | v1.0.4+ |
| `on_compile_before` | 编译前执行 | v1.0.2+ |
| `on_compile_success` | 编译成功后执行 | v1.0.2+ |
| `on_compile_error` | 编译失败后执行 | v1.0.2+ |
| `on_run_before` | 运行前执行 | v1.0.2+ |
| `on_app_init` | 应用启动时执行 | v1.0.4+ |

### 菜单 Hook 示例

```json
{
  "menu": [
    {
      "title": "NDK编译",
      "position": "start",
      "onClick": [
        {
          "node": "command_result",
          "sh": "ndk-build",
          "dir": "${current_dir}",
          "loading": "正在编译...",
          "success": [
            {"node": "alert", "title": "成功", "message": "${cmd_output}"}
          ],
          "error": [
            {"node": "alert", "title": "失败", "message": "${cmd_error}"}
          ]
        }
      ]
    }
  ]
}
```

### 事件 Hook 示例

```json
{
  "events": {
    "on_compile_success": [
      {"node": "command", "sh": "echo '编译成功' >> ${plugin_path}/log.txt"}
    ]
  }
}
```

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

## � 使用指南

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
| 卸载按钮 | 删除插件 |
| 点击 ABI 标签 | 切换插件 ABI（多 ABI 时显示） |
| 开关按钮 | 启用/禁用插件 |

## ⚙️ 设置选项

### 编辑器设置
- **记住上次打开的文件**：下次启动时恢复上次的文件和目录
- **编辑器字体大小**：12-24sp 可选
- **编辑器主题**：Darcula（暗色）等主题
- **启用 Clangd LSP**：开启智能代码分析（需要安装 Clangd 插件）

### 终端设置
- **终端字体大小**：10-24sp 可选
- **终端字体**：Monospace、Sans Serif、Serif
- **显示底部操作栏**：控制快捷键栏显示

### 编译设置
- **编译命令管理**：自定义编译和运行命令
- **Clang 编译参数**：C 语言编译参数（默认：`-lm -ldl -llog -lz -std=c99 -Wfatal-errors -Os -s -pie`）
- **Clang++ 编译参数**：C++ 编译参数（默认：`-lm -ldl -llog -lz -std=c++17 -Wfatal-errors -Os -s -pie`）
- **Android API Level**：目标 Android API 版本（21-35，默认 21）

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
├── .install         # 安装脚本（JSON格式，可选）
├── .hook            # Hook 配置（JSON格式，可选）
├── .path            # 环境变量路径（安装后自动生成）
├── lib/
│   ├── arm64-v8a/   # arm64 架构的 .so 文件
│   └── x86_64/      # x86_64 架构的 .so 文件
├── include/         # 头文件
└── example/         # 示例代码
```

### 配置文件格式（.config）
```json
{
  "plugin_code": "my_plugin",
  "plugin_name": "我的插件",
  "plugin_version": "1.0.0",
  "plugin_describe": "插件描述",
  "author": "作者名称",
  "github": "https://github.com/xxx/xxx",
  "support_ABI": ["arm64-v8a", "x86_64"]
}
```

### 安装脚本格式（.install）

详见 [插件安装脚本文档](docs/插件安装脚本文档.md)

### Hook 配置格式（.hook）

详见 [插件安装脚本文档](docs/插件安装脚本文档.md)（Hook 系统部分）

## 📝 更新日志

### v1.0.7
- **新增 OLLVM 混淆 Clang 工具链**
  - 基于 Clang 18.1.8 + OLLVM 混淆器
  - 支持代码混淆保护，增强逆向难度
  - 自动检测工具链版本，版本不匹配时提示重新安装
- **支持的混淆参数**
  - `-mllvm -fla`：控制流平坦化（Control Flow Flattening）
  - `-mllvm -sub`：指令替换（Instruction Substitution）
  - `-mllvm -bcf`：虚假控制流（Bogus Control Flow）
  - `-mllvm -ibr`：间接分支（Indirect Branching）
  - `-mllvm -sobf`：字符串混淆（String Obfuscation）
  - `-mllvm -split`：基本块分割（Basic Block Splitting）
  - `-mllvm -split_num=3`：指定分割次数
- **编辑器优化**
  - 更优秀的代码补全策略，提升补全准确性和响应速度
  - 支持快捷键拆解多行（选中代码后快速拆分）
  - 支持快速格式化代码（基于 clang-format）
- **UI 优化**
  - 优化对话框输入框样式，更符合 M3 设计规范
  - 对话框按钮颜色统一为 M3 紫色
  - 新建项目页面自动聚焦到项目名称输入框
  - 项目名称支持中文命名

### v1.0.6
- **修复大屏设备输入法焦点问题**
  - 添加 onWindowFocusChanged 回调方法
  - 修复 iPad 等大屏设备点击唤起输入法后焦点丢失的问题
- **编译进度对话框深色主题适配**
  - 根据当前编辑器主题动态设置对话框背景色
  - 动态调整进度指示器颜色和轨道颜色
  - 文本颜色随主题自动切换
  - 编译错误信息对话框主题颜色适配
- **更新修复
  - 修复更新弹窗主题

### v1.0.5
- **新增 Git 集成功能**
  - 支持 Git 仓库克隆（支持私有仓库认证）
  - Git 凭据管理（加密存储）
  - Git 提交、推送、拉取操作
  - 分支管理功能
  - 文件列表显示 Git 状态标识（M/A/U/C 等）
- **新增项目管理功能**
  - 新建项目向导（支持 Git 初始化选项）
  - 最近项目列表
  - 项目配置保存和恢复
- **新增 Android API Level 配置**
  - 支持 API 21 到 API 35 版本选择
  - 编译器目标参数可配置
- **新增应用内版本更新**
  - 自动检查 GitHub releases 版本
  - 支持 APK 下载和安装
  - Markdown 格式发布说明渲染
- **新增自动保存功能**
  - 支持定时静默保存文件
  - 可配置保存间隔
- **优化编译器参数处理**
  - 区分 C 和 C++ 文件编译参数
  - 自动过滤 C++ 专用参数
- **UI 优化**
  - 工具栏响应式布局（窄屏适配）
  - 暗色主题对话框样式统一
  - 远程仓库添加对话框

### v1.0.4
- **重大升级：将编译链从 GCC 升级为 Clang**，提供更好的编译性能和错误提示
- **新增 C++17 标准支持**，可在编译参数中选择 `-std=c++17`
- 优化 Makefile 文件读取，修复 mk 文件解析问题
- 新增 `toolbar` Hook，支持在工具栏添加自定义按钮
- 新增 `on_app_init` Hook，支持应用启动时执行初始化操作
- 优化编译缓存机制，提升编译速度
- 改进错误提示和日志输出
- 优化内存使用，减少应用占用空间

### v1.0.3
- 新增插件 `author` 字段支持，显示插件作者信息
- 新增 `run_menu` Hook，支持在运行按钮下拉菜单添加自定义项
- 优化插件列表 UI，新增卸载按钮
- 修复保存按钮点击无反应的问题
- 修复首次启动状态栏显示紫色的问题
- 修复首次打开编辑器显示白色主题的问题

### v1.0.2
- 新增 Clangd LSP 智能代码分析支持
- 新增插件安装脚本系统（.install 文件）
- 新增插件 Hook 系统（.hook 文件）
- 新增插件 PATH 环境变量自动注入
- 新增编辑器菜单 Hook 支持
- 新增编译事件 Hook（编译前/成功/失败）
- 新增运行事件 Hook（运行前）
- 新增 `command_result` 节点（带 Loading 和结果分支）
- 新增 `grep` 节点（正则表达式匹配）
- 新增 `run_in_terminal` 节点（在终端运行文件）
- 优化编译流程，支持编译缓存
- 修复多项已知问题

### v1.0.1
- 初始版本发布
- 基础代码编辑器功能
- GCC/G++ 编译支持
- 终端模拟器
- 插件系统基础功能

## 🙏 致谢

Akode 的开发离不开以下开源项目：

- [Sora Editor](https://github.com/Rosemoe/sora-editor) - 代码编辑器组件
- [Termux](https://github.com/termux/termux-app) - 终端模拟器
- [Clang/LLVM](https://clang.llvm.org/) - C/C++ 编译器工具链
- [libsu](https://github.com/topjohnwu/libsu) - Root 权限访问库
- [Material Components](https://github.com/material-components/material-components-android) - Material Design 组件库
- [JGit](https://www.eclipse.org/jgit/) - Java Git 实现库
- [OkHttp](https://square.github.io/okhttp/) - HTTP 客户端
- [Markwon](https://github.com/noties/Markwon) - Markdown 渲染库
- [C4droid](https://baike.baidu.com/item/c4droid/8215130) - Android 平台 C/C++ 编程工具
- [simpleC](https://github.com/luoyesiqiu/simpleC) - Android 平台 C/C++ 编程工具

## 👨‍💻 开发者

**阿夜** - [GitHub](https://github.com/AYssu)

---

如有问题或建议，欢迎反馈！
