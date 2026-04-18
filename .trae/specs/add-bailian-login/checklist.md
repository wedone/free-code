# Checklist

- [ ] 阿里百炼选项出现在登录方法选择界面（在"3rd-party platform"和"OpenAI Codex account"之间）
- [ ] 选择阿里百炼后显示 API Key 输入提示
- [ ] API Key 输入界面支持 masked 输入（显示为星号）
- [ ] API Key 验证成功后保存到配置中
- [ ] ANTHROPIC_BASE_URL 自动设置为 `https://coding.dashscope.aliyuncs.com/apps/anthropic/v1`
- [ ] 登录成功后显示成功提示
- [ ] API Key 无效时显示错误提示并允许重新输入
- [ ] platform_setup 界面包含阿里百炼文档链接
- [ ] provider 检测逻辑正确识别阿里百炼配置
- [ ] 应用启动时使用阿里百炼端点进行 API 调用
