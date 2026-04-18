# Tasks
- [x] Task 1: 创建 GitHub Actions 工作流目录
  - [x] SubTask 1.1: 创建 .github/workflows 目录
  - [x] SubTask 1.2: 创建 build.yml 工作流文件
- [x] Task 2: 配置工作流基础结构
  - [x] SubTask 2.1: 设置 workflow_dispatch 和 tag 触发条件
  - [x] SubTask 2.2: 配置 4 个矩阵组合（Windows/Linux × AVX2/Baseline）
  - [x] SubTask 2.3: 设置并发编译策略
- [x] Task 3: 配置 Bun 安装步骤
  - [x] SubTask 3.1: 标准版 Bun 安装（windows-latest 和 ubuntu-latest）
  - [x] SubTask 3.2: Baseline 版 Bun 安装（通过 URL 下载）
  - [x] SubTask 3.3: 验证 Bun 版本 >= 1.3.11
- [x] Task 4: 配置编译和产物上传步骤
  - [x] SubTask 4.1: 安装依赖（bun install）
  - [x] SubTask 4.2: 执行编译（bun run compile）
  - [x] SubTask 4.3: 打包编译产物为 ZIP
  - [x] SubTask 4.4: 上传到 GitHub Artifacts
  - [x] SubTask 4.5: 如果由 tag 触发，创建 Release 并附加产物

# Task Dependencies
- [Task 2] depends on [Task 1]
- [Task 3] depends on [Task 2]
- [Task 4] depends on [Task 3]
