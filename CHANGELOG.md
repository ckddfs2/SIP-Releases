# 变更记录

## 1.3 — 2026-10-29

### 修复

- **Web UI 导出详设 PDF 报 `No module named 'PIL'`**：打包配置误把 Pillow 排除，而内置 reportlab 5.0.1 在 `reportlab/lib/utils.py` 顶层无条件 `from PIL import Image`，导致冻结版 exe 的所有 PDF 导出在导入阶段失败（Markdown 仍能保存）。现已在 exe 中带上 Pillow，详设 PDF（含 PlantUML 图）恢复生成。

### 分发

- `SIP.exe` 体积由 105,501,559 B 增至 111,764,377 B（约 +6.0 MB），SHA-256 `681ea0e1a12284544a9de7402e3dfb4c151773cdf45eb300878cb4be523c4124`。

## 1.2 — 2026-10-28

首个公开发布版本。

### 工具接入

- **TESSY 宿主测试**：使用 TESSY 自带的 x86 GNU GCC 在主机上运行，不依赖 Keil / IAR / 调试器；自动生成 `tessy_compat.h`，把固件通过绝对地址访问的 SFR 映射到 `VirtualAlloc` 内存，并自动为驱动写入 `-include`。
- **Polyspace 预检与自动 shim**：分析前先做 `-to compile` 纯编译预检，失败即中止，避免“静默跳过编译失败文件”的假成功；IAR 工程自动生成 `ps_compat` 影子头并注入关键字空宏，只影响分析侧，不改 `01_Sources`。
- **需求页三页签**：SRS 拆分 → 单元需求 → 绑定与追溯（函数绑定、用例链接、XLSX / PDF 导出）。

### 日常开发入口

- 生成的工程自带 `02_Build\setup_dev_env.bat` v2.0.3：17 项交互菜单、21 种非交互模式，覆盖 discover / modules / toolchain / gen / build / clean / Eclipse / TESSY / Polyspace 等。

### 修复

- TESSY 宿主测试全部 `notexecuted`、`TC/C=0`、无覆盖率：修复 SFR 绝对地址访问崩溃与驱动 `-include` 缺失。
- Polyspace 静默漏分析：改为预检不通过即中止。

### 文档

- 中英文档、PDF 与介绍 PPT 刷新到 1.2；架构与流程示意图改用 PlantUML 绘制。

### 分发

- `SIP.exe`（约 100.6 MB）超出仓库单文件限制，改由 GitHub Releases 分发。
