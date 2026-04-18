# Checklist

- [x] `.github/workflows/build.yml` 文件存在
- [x] workflow_dispatch 触发条件已配置（第4-9行）
- [x] v* tag 触发条件已配置（第10-12行）
- [x] 编译矩阵包含 4 个组合：Windows/Linux × AVX2/Baseline（第24-45行，matrix.include 配置）
- [x] Windows 版本使用 windows-latest runner（第27,37行）
- [x] Linux 版本使用 ubuntu-latest runner（第32,42行）
- [x] Baseline Bun 安装正确（通过 bun-download-url 下载 baseline 版本，第58-61行）
- [x] 标准 Bun 安装正确（通过 oven-sh/setup-bun@v2 action，第52-55行）
- [ ] bun install 步骤成功执行（需要在 GitHub Actions 运行时验证）
- [ ] bun run compile 步骤成功执行（需要在 GitHub Actions 运行时验证）
- [x] 编译产物打包为 ZIP 格式（第110-124行，release job 中使用 zip 打包）
- [ ] actions/upload-artifact 上传产物成功（需要在 GitHub Actions 运行时验证）
- [x] 由 tag 触发时自动创建 GitHub Release（第128-134行，使用 softprops/action-gh-release@v2）
- [ ] Release 包含所有 4 个版本的编译产物（需要在 GitHub Actions 运行时验证）
- [x] 产物命名格式正确：claude-<platform>-<arch>[-baseline].zip（第29,34,39,44行 artifact_name 配置）
