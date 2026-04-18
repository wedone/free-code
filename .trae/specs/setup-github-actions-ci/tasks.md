# Tasks

- [x] Task 1: 分析编译脚本和 CPU 指令集支持
  - [x] SubTask 1.1: 检查 `scripts/build.ts` 了解编译流程
  - [x] SubTask 1.2: 确认 Bun 支持 `bun-baseline` 目标（无 AVX2）
  - [x] SubTask 1.3: 确定使用 `--target bun-baseline` 禁用 AVX2

- [x] Task 2: 创建 GitHub Actions Workflow
  - [x] SubTask 2.1: 创建 `.github/workflows/build.yml` 配置文件
  - [x] SubTask 2.2: 配置编译矩阵：4 个组合（Windows/Linux × AVX2/无AVX2）
  - [x] SubTask 2.3: 设置触发条件：push 到 main、tag 创建、手动触发
  - [x] SubTask 2.4: 配置缓存策略加速编译

- [x] Task 3: 配置 Windows 编译
  - [x] SubTask 3.1: 使用 `windows-latest` runner
  - [x] SubTask 3.2: 安装 Bun 和依赖
  - [x] SubTask 3.3: 编译 AVX2 版本（`--target bun`）
  - [x] SubTask 3.4: 编译无 AVX2 版本（`--target bun-baseline`）
  - [x] SubTask 3.5: 上传编译产物（.exe 文件）

- [x] Task 4: 配置 Linux 编译
  - [x] SubTask 4.1: 使用 `ubuntu-latest` runner
  - [x] SubTask 4.2: 安装 Bun 和依赖
  - [x] SubTask 4.3: 编译 AVX2 版本
  - [x] SubTask 4.4: 编译无 AVX2 版本
  - [x] SubTask 4.5: 上传编译产物

- [x] Task 5: 配置 Release 自动化
  - [x] SubTask 5.1: 创建 tag 时自动生成 GitHub Release
  - [x] SubTask 5.2: 上传所有编译产物到 Release
  - [x] SubTask 5.3: 为每个版本添加清晰的命名（如 `claude-windows-avx2.exe`）

- [x] Task 6: 验证和优化
  - [x] SubTask 6.1: 验证 Workflow 配置语法
  - [x] SubTask 6.2: 确认编译矩阵正确运行
  - [x] SubTask 6.3: 优化编译时间（缓存、并行）

# Task Dependencies
- [Task 2] depends on [Task 1]
- [Task 3] depends on [Task 2]
- [Task 4] depends on [Task 2]
- [Task 5] depends on [Task 3] and [Task 4]
- [Task 6] depends on [Task 5]
