---
layout: post
title: template page
categories: [cate1, cate2]
description: some word here
keywords: keyword1, keyword2
---

# GKCSHV100 PC SDK编译指南

# 编译指南

本指南详细介绍如何使用 build.sh 脚本编译本项目，包括环境准备、参数说明、常见用法、构建流程、输出目录及常见问题排查。

---

## 一、环境准备

1. **操作系统**

    Linux平台
2. **必备工具**

    - **GNU bash**（脚本强制要求，cmd/powershell 不支持）
    - **CMake 3.10+**
    - **MinGW 编译器**
    - **make、ctest、cpack**（随 CMake 一般自带）
3. **环境变量**
    确保 `cmake`、`make`等命令可在 shell 中直接调用。

---

## 二、脚本用法

在项目根目录下运行：

```bash
./build.sh [选项] 或 bash build.sh [选项]
```

### 参数说明

#### 构建类型

|参数|说明|
| -------------| ----------------------------------|
|-d, --debug|Debug 构建（带调试信息）|
|-r, --release|Release 构建（优化，去除调试信息）|
|默认|RelWithDebInfo（带调试信息的优化）|

#### 并行与清理

|参数|说明|
| ------------| ------------------------------|
|-c, --clean|清理构建目录|
|-j, --jobs N|并行编译任务数（默认自动检测）|

#### 组件选择

|参数|说明|
| ---------------| --------------|
|--no-apps|不构建应用程序|
|--no-foundation|不构建基础组件|
|--no-frameworks|不构建框架|
|--no-sdk|不构建 SDK|

#### 功能开关

|参数|说明|
| ----------------| -----------------------------|
|--with-tests|构建测试程序|
|--with-prebuilts|构建预编译文件|
|--with-coverage|启用代码覆盖率|
|--with-asan|启用地址消毒器（ASan）|
|--with-ubsan|启用未定义行为消毒器（UBSan）|
|--analyze|启用静态分析|
|--package|生成安装包（zip 格式）|
|--toolchain|使用交叉编译工具链|

#### 其他

|参数|说明|
| ----------| ------------|
|-h, --help|显示帮助信息|

---

## 三、常见用法举例

- **默认编译（RelWithDebInfo）**

  ```bash
  ./build.sh
  ```
- **Debug 模式编译**

  ```bash
  ./build.sh --debug
  ```
- **Release 模式编译**

  ```bash
  ./build.sh --release
  ```
- **清理构建目录后重新编译**

  ```bash
  ./build.sh --clean
  ```
- **编译测试程序**

  ```bash
  ./build.sh --with-tests
  ```
- **指定并行任务数为 8，未指定时默认使用所有可用核心**

  ```bash
  ./build.sh --jobs 8
  ```
- **不构建 SDK 和应用程序**

  ```bash
  bash ./build.sh --no-sdk --no-apps
  ```

---

## 四、构建流程详解

1. **环境检查**
    检查当前 shell 是否为 GNU bash。若不是，将提示切换 shell。
2. **参数解析**
    解析命令行参数，设置构建类型、并行数、功能开关等。
3. **打印构建配置**
    输出本次构建的详细参数，包括目录、类型、选项等。
4. **清理构建目录**
    若指定 `--clean`，则删除输出目录，重新创建。
5. **CMake 配置**
    进入构建目录，执行 CMake 配置，生成 Makefile 或 Ninja 文件。
6. **编译项目**
    调用 `cmake --build .`，并行编译所有目标。
7. **安装产物**
    调用 `cmake --install .`，将编译产物安装到指定目录。
8. **生成安装包**
    若启用 `--package`，调用 `cpack` 生成 zip 安装包。
9. **输出耗时统计**
    脚本会统计每一步耗时，并输出总用时。

---

## 五、输出目录结构

- 构建输出：GKCSHV100
- 安装目录：`out/GKCSHV100/install/`
- 安装包（如生成）：out/GKCSHV100 下的 zip 文件

---

## 六、常见问题与排查

1. **提示 shell 不是 bash**

    - 请确保在 Git Bash 或 WSL 下运行脚本。
    - 若在 Linux 下，确保 `/bin/sh` 链接到 `/bin/bash`。
2. **CMake 配置失败**

    - 检查 CMake 版本、编译器路径及依赖是否齐全。
    - 查看终端输出的详细错误信息。
3. **并行任务数报错**

    - `--jobs` 参数建议不超过本机 CPU 核心数。
4. **找不到命令**

    - 检查环境变量，确保 `cmake`、`make`可用。

---

## 七、查看帮助

运行以下命令查看完整帮助信息：

```
./build.sh --help
```
