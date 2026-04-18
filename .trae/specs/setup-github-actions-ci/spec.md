# 使用 GitHub Actions 编译多平台多 CPU 版本 Spec

## Why
本机性能较差（CPU i3-320 不支持 AVX2 指令集），无法在本地高效完成编译任务。需要利用 GitHub Actions 的云端算力来编译项目，并生成 4 个不同版本以覆盖不同平台和 CPU 指令集需求。

## What Changes
- 创建 GitHub Actions Workflow 配置文件
- 配置 4 个编译矩阵：
  1. **Windows + AVX2** - 正常版本，适用于支持 AVX2 的现代 CPU
  2. **Windows + 无 AVX2** - 兼容版本，适用于 i3-320 等老旧 CPU
  3. **Linux (Debian) + AVX2** - 正常版本，适用于支持 AVX2 的现代 CPU
  4. **Linux (Debian) + 无 AVX2** - 兼容版本，适用于老 CPU
- 编译产物自动上传为 GitHub Release assets

## Impact
- Affected specs: CI/CD、多平台编译、Release 自动化
- Affected code: 
  - `.github/workflows/build.yml` - 新增 CI 工作流配置
  - `scripts/build.ts` - 可能需要添加 CPU 指令集选项支持

## ADDED Requirements

### Requirement: GitHub Actions 多平台编译
系统 SHALL 提供 GitHub Actions Workflow，自动在云端编译 4 个版本。

#### Scenario: Push 到 main 分支触发编译
- **WHEN** 代码推送到 main 分支或创建 tag
- **THEN** GitHub Actions 触发编译流程
- **AND** 并行编译 4 个版本（Windows/Linux × AVX2/无AVX2）
- **AND** 所有编译产物上传为 Release assets

### Requirement: AVX2 指令集控制
系统 SHALL 支持通过编译标志控制是否启用 AVX2 指令集优化。

#### Scenario: 编译无 AVX2 版本
- **WHEN** 编译标志设置为无 AVX2
- **THEN** Bun/编译器不使用 AVX2 指令集优化
- **AND** 生成的二进制文件可以在 i3-320 等老 CPU 上运行

#### Scenario: 编译 AVX2 版本
- **WHEN** 编译标志启用 AVX2
- **THEN** 编译器使用 AVX2 指令集优化
- **AND** 生成的二进制文件在现代 CPU 上性能更好

### Requirement: 多平台支持
系统 SHALL 支持在 Windows 和 Linux (Debian) 两个平台上编译。

#### Scenario: Windows 编译
- **WHEN** GitHub Actions 在 `windows-latest` runner 上运行
- **THEN** 生成 Windows 可执行文件（.exe）

#### Scenario: Linux 编译
- **WHEN** GitHub Actions 在 `ubuntu-latest` runner 上运行
- **THEN** 生成 Linux 可执行文件

## MODIFIED Requirements

### Requirement: Build Script
**当前**: 编译脚本可能不支持 CPU 指令集控制  
**修改为**: 编译脚本支持通过参数控制 AVX2 启用/禁用

## REMOVED Requirements
无
