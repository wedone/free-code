# GitHub Actions CI/CD 编译工作流 Spec

## Why
本机性能较差（i3-3220 CPU），编译速度慢且不支持 AVX2 指令集。需要通过 GitHub Actions 远程编译，同时输出 4 个版本覆盖不同平台和 CPU 架构：Windows/Linux × 有AVX2/无AVX2。

## What Changes
- 新增 `.github/workflows/build.yml` GitHub Actions 工作流文件
- 配置 4 个编译矩阵：Windows-x64、Linux-x64、Windows-baseline、Linux-baseline
- 自动安装 Bun（标准版和 baseline 版）
- 编译并打包二进制文件为 ZIP 格式
- 上传编译产物到 GitHub Releases

## Impact
- 受影响的能力：编译构建流程
- 受影响的文件：
  - `.github/workflows/build.yml` - 新增工作流文件
  - `scripts/build.ts` - 可能需要支持通过环境变量指定 Bun 路径

## ADDED Requirements

### Requirement: GitHub Actions 编译工作流
系统 SHALL 提供完整的 GitHub Actions 工作流，支持 4 个版本的并行编译。

#### Scenario: 手动触发编译
- **WHEN** 用户手动触发 workflow_dispatch
- **THEN** 系统并行编译 4 个版本

#### Scenario: Tag 触发编译
- **WHEN** 用户创建 v* 格式的 tag
- **THEN** 系统自动编译 4 个版本并发布到 GitHub Releases

### Requirement: 4 个编译版本
系统 SHALL 编译以下 4 个版本：
1. **Windows x64 (AVX2)** - 使用标准 Bun 编译，输出 `claude-windows-x64.exe`
2. **Linux x64 (AVX2)** - 使用标准 Bun 编译，输出 `claude-linux-x64`
3. **Windows x64 (Baseline)** - 使用 baseline Bun 编译，输出 `claude-windows-x64-baseline.exe`
4. **Linux x64 (Baseline)** - 使用 baseline Bun 编译，输出 `claude-linux-x64-baseline`

#### Scenario: Windows 版本编译
- **WHEN** 在 windows-latest runner 上编译
- **THEN** 使用对应版本的 Bun 编译
- **THEN** 输出 `.exe` 格式文件

#### Scenario: Linux 版本编译
- **WHEN** 在 ubuntu-latest runner 上编译
- **THEN** 使用对应版本的 Bun 编译
- **THEN** 输出 ELF 格式可执行文件

### Requirement: Bun 安装策略
系统 SHALL 根据不同矩阵配置安装对应版本的 Bun。

#### Scenario: 标准版 Bun
- **WHEN** matrix.baseline 为 false
- **THEN** 安装标准版 Bun（支持 AVX2 优化）

#### Scenario: Baseline 版 Bun
- **WHEN** matrix.baseline 为 true
- **THEN** 安装 baseline 版 Bun（无 AVX2，兼容老 CPU）

### Requirement: 产物打包
系统 SHALL 将编译好的二进制文件打包为 ZIP 格式并上传。

#### Scenario: 产物上传
- **WHEN** 编译成功
- **THEN** 将二进制文件和相关资源打包为 ZIP
- **THEN** 使用 actions/upload-artifact 上传编译产物

#### Scenario: Release 发布
- **WHEN** 由 tag 触发
- **THEN** 自动创建 GitHub Release 并附加所有编译产物

## MODIFIED Requirements
无

## REMOVED Requirements
无
