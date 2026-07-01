# Gboard-Key-Customizer

# Gboard 按键自定义模块 (Gboard Key Customizer)

一个基于 LSPosed API 101 的 Xposed 模块，用于自定义 Gboard 字母键的下滑手势动作。可以为 26 个字母键中的任意一个绑定单动作或组合动作（例如「全选 → 删除选中」实现一键清空输入框），并可突破 Gboard 内置的剪贴板字符上限。

- 模块包名：`com.sidesand.gboardhook`
- 目标包：`com.google.android.inputmethod.latin` (Gboard)
- 适配 LSPosed API 101（`io.github.libxposed:api:101.0.1`）
- **适配 Gboard 版本：17.3.3.902587967-beta-(175776222)**

## 功能特性

### 1. 字母键下滑动作绑定

为 QWERTY 键盘上 26 个字母键（a–z）单独配置下滑手势触发的动作。支持组合动作按顺序执行。

| 分类 | 动作 |
|------|------|
| 选择操作 | 全选 / 剪切 / 复制 / 粘贴 |
| 光标移动 | 左移 / 右移 / 上移 / 下移 |
| 编辑操作 | 删除前一字符 / 删除选中 / 撤销 |
| 读取文本 | 获取选中文本 / 光标前文本 / 光标后文本 |
| 输出文本 | 输出自定义文本 |

**组合动作示例：**
- `t` 键 → 全选 → 删除选中：一键清空输入框
- `e` 键 → 复制：快速复制全部
- `a` 键 → 输出文本 "admin@example.com"：快速输入常用账号

### 2. 突破 Gboard 剪贴板字符上限

Gboard 内部对剪贴板条目有字符长度限制（默认 20000 字符），超过会被截断。本模块通过 Hook 把上限替换为用户可配置的值（默认 100 万，可在面板中调整）。

### 3. 配置即时生效

UI 侧修改配置后，实时感知，**无需重启 Gboard**，下一次下滑即读取最新配置。Xposed 日志会单行输出变化项，例如：

```
clipboard limit: 20000 -> 1000000
'q' → 全选 → 删除选中
'e' → 复制
```

## 安装

### 前置条件

- 已 Root 且已安装 [LSPosed](https://github.com/LSPosed/LSPosed)（支持 API 101 的版本）
- **Gboard 版本：17.3.3.902587967-beta-(175776222)**

### 步骤

1. 在 LSPosed Manager 中安装本模块 APK
2. 启用模块，并在作用域中勾选 `com.google.android.inputmethod.latin` (Gboard)
3. 强制停止 Gboard 一次，使其重新加载并注入 Hook
4. 打开本模块的配置面板，为字母键设置下滑动作
5. 在任意输入框中唤起 Gboard，下滑已绑定的字母键即可触发动作

> 配置面板修改后无需再次重启 Gboard，下一次下滑即生效。

## 使用须知

**必须在 Gboard 设置中开启下滑手势识别**：

打开 Gboard 设置 → 偏好设置 → 开启「快速滑动按键即可输入符号」

未开启此选项时，Gboard 不会触发下滑手势事件，模块无法识别下滑动作。

## 配置面板说明

打开模块启动器进入配置面板：

- **状态卡片**：总开关（开启后才会拦截 Gboard 下滑事件）
- **全局参数**：剪贴板字符上限（输入新值后点「确定」生效，下方显示当前生效值）
- **按键下滑绑定**：按 QWERTY 布局列出 26 个字母键，点击按键进入编辑弹窗
  - 编辑弹窗中可勾选多个动作组成组合，按勾选顺序执行
  - 勾选「输出自定义文本」后可填写要插入的字符串
  - 长按删除图标可清除该按键绑定
- **动作说明卡片**：列出全部动作分类
- **右上角重置按钮**：清除所有按键绑定并恢复默认全局参数
- **获取更新卡片**：点击访问 `https://github.com/sidesand/Gboard-Key-Customizer` 获取最新版本
- **支持作者卡片**：扫描二维码捐赠支持

## 构建

### 关键依赖

| 依赖 | 版本 | 用途 |
|------|------|------|
| `io.github.libxposed:api` | 101.0.1 | LSPosed 模块 API |



## 已知限制

- 下滑动作 Hook 依赖 Gboard 内部混淆类，Gboard 大版本升级后类名可能变化，需要重新定位
- 仅支持英文字母键（a–z）的下滑手势，不支持数字键和符号键

## 获取更新

访问 [https://github.com/sidesand/Gboard-Key-Customizer](https://github.com/sidesand/Gboard-Key-Customizer) 获取最新版本与更新信息。

## 支持作者

如果这个模块对你有用，欢迎扫描下方二维码请作者喝杯咖啡 ☕
<img width="1193" height="1789" alt="2wm" src="https://github.com/user-attachments/assets/3eb9bd9e-41f3-4a1e-9f8c-2caf2f5dcfdf" />

## 许可证

本项目仅供学习交流使用。
