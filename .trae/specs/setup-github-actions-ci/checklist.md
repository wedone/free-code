# GitHub Actions 多平台编译 Checklist

- [ ] GitHub Actions Workflow 配置文件已创建（.github/workflows/build.yml）
- [ ] 编译矩阵包含 4 个组合（Windows/Linux × AVX2/无AVX2）
- [ ] Windows + AVX2 版本编译成功
- [ ] Windows + 无AVX2 版本编译成功
- [ ] Linux + AVX2 版本编译成功
- [ ] Linux + 无AVX2 版本编译成功
- [ ] 编译产物正确上传为 GitHub Release assets
- [ ] 版本命名清晰（如 claude-windows-avx2.exe）
- [ ] Push 到 main 分支触发编译
- [ ] 创建 tag 时自动生成 Release 并上传产物
- [ ] 缓存策略配置正确以加速编译
- [ ] 所有任务并行执行以节省时间
- [ ] Workflow 配置通过 GitHub Actions lint 验证
