# AngelScript Formatting Enhancement (as-clang-format)

This repository provides a customized version of `clang-format`, specifically optimized for **AngelScript (AS)**. It addresses the long-standing issue where handle symbols (`@`) are incorrectly spaced or attached, ensuring a professional and readable code style for game scripting.

## 🌟 Key Enhancements

* **Smart Handle Spacing**: Correctly formats handle declarations. Based on `PointerAlignment: Left`, it turns `xck::PersonInfo @p` into `xck::PersonInfo@ p`.
* **Generic/Template Support**: Fixes the trailing space issue inside templates. It ensures `cast<xck::PersonInfo@>` instead of `cast<xck::PersonInfo@ >`.
* **Scope/Namespace Awareness**: Accurately recognizes complex types across namespaces, such as `xck::UnitInfo@` or `abc::BuildingInfo@`.
* **Handle Anti-merging**: Prevents consecutive handle symbols from being merged, maintaining `@ @` for clear lexical parsing.

## 🔧 Technical Implementation

The modifications are integrated into the Clang Tooling layer, specifically within `clang/lib/Format/TokenAnnotator.cpp`. We have:
1.  Modified the `spaceRequiredBetween` function to recognize `@` as a pointer-like token (`TT_PointerOrReference`).
2.  Bypassed the default Objective-C rules that previously interfered with AngelScript's handle syntax.
3.  Synchronized handle positioning with the standard `PointerAlignment` configuration.

## 📦 Usage

1.  **Obtain Binary**: Download `as-clang-format.exe` from the GitHub Actions artifacts of this repository.
2.  **Configuration**: Place a `.clang-format` file in your project root.
3.  **Recommended Style Settings**:
    ```yaml
    Language: Cpp
    BasedOnStyle: LLVM
    PointerAlignment: Left  # Results in: Type@ var
    ```

---

# AngelScript 格式化增强版 (as-clang-format)

本仓库提供了一个专门针对 **AngelScript (AS)** 优化的定制版 `clang-format`。它解决了长期以来句柄符号（`@`）格式化不正确（如强制粘连或空格错误）的问题，为游戏脚本开发提供专业且易读的代码风格。

## 🌟 主要改进

* **智能句柄空格**: 完美处理句柄声明。在 `PointerAlignment: Left` 配置下，将 `xck::PersonInfo @p` 自动修正为 `xck::PersonInfo@ p`。
* **泛型与模板支持**: 修复了模板内部结尾处的空格问题。确保生成 `cast<xck::PersonInfo@>` 而非 `cast<xck::PersonInfo@ >`。
* **作用域与命名空间识别**: 准确识别跨命名空间的复杂类型，如 `xck::UnitInfo@` 或 `abc::BuildingInfo@`。
* **防止句柄粘连**: 确保连续的句柄符保持为 `@ @`，防止被错误合并为单一标记，确保语法解析正确。

## 🔧 技术实现

相关修改已集成至 Clang Tooling 层，主要位于 `clang/lib/Format/TokenAnnotator.cpp`：
1.  修改了 `spaceRequiredBetween` 函数，将 `@` 识别为类指针标记（`TT_PointerOrReference`）。
2.  绕过了原生 Objective-C 规则对 AngelScript 句柄语法的干扰。
3.  使句柄位置逻辑与标准的 `PointerAlignment` 样式配置保持同步。

## 📦 使用说明

1.  **获取程序**: 从本仓库 GitHub Actions 的构建产物中下载 `as-clang-format.exe`。
2.  **配置方法**: 在你的项目根目录创建 `.clang-format` 配置文件。
3.  **推荐配置**:
    ```yaml
    Language: Cpp
    BasedOnStyle: LLVM
    PointerAlignment: Left  # 实现效果: Type@ var
    ```
