# 添加阿里百炼登录选项 Spec

## Why
当前 `/login` 命令的登录方法选择界面中，虽然有"3rd-party platform"选项，但该选项仅显示配置文档说明，并不支持直接配置和认证。用户希望能够直接在登录界面选择阿里百炼（Ali Bailian），输入 API Key 后即可使用对应的阿里百炼大模型，而无需手动配置环境变量。

## What Changes
- 在登录方法选择界面新增"阿里百炼（Ali Bailian）"选项
- 实现阿里百炼 API Key 输入和验证流程
- 将 API Key 和 Anthropic 兼容 base URL 保存到配置中
- 在 `platform_setup` 界面添加阿里百炼的文档链接
- 修改应用启动逻辑以支持阿里百炼 provider

## Impact
- 受影响的能力：登录流程、API Key 配置、模型 provider 选择
- 受影响的核心文件：
  - `src/commands/login/login.tsx` - 登录入口
  - `src/components/ConsoleOAuthFlow.tsx` - OAuth 流程和登录方法选择
  - `src/utils/model/providers.ts` - Provider 检测逻辑
  - `src/utils/auth.ts` - 认证相关工具函数

## ADDED Requirements

### Requirement: 阿里百炼登录选项
系统 SHALL 在 `/login` 命令的登录方法选择界面提供"阿里百炼（Ali Bailian）"选项。

#### Scenario: 用户选择阿里百炼
- **WHEN** 用户在登录方法选择界面选择"阿里百炼"
- **THEN** 系统显示 API Key 输入提示

#### Scenario: 用户输入 API Key
- **WHEN** 用户输入有效的阿里百炼 API Key
- **THEN** 系统保存 API Key 到配置文件
- **THEN** 系统设置 `ANTHROPIC_BASE_URL` 为 `https://coding.dashscope.aliyuncs.com/apps/anthropic/v1`
- **THEN** 系统显示登录成功提示

#### Scenario: API Key 验证失败
- **WHEN** 用户输入的 API Key 无效或验证失败
- **THEN** 系统显示错误提示信息
- **THEN** 系统允许用户重新输入 API Key

### Requirement: 阿里百炼平台设置文档
系统 SHALL 在"3rd-party platform"设置界面添加阿里百炼的文档链接。

#### Scenario: 查看平台设置文档
- **WHEN** 用户选择"3rd-party platform"选项
- **THEN** 系统在文档列表中显示"阿里百炼"链接
- **THEN** 链接指向阿里百炼配置文档

### Requirement: 阿里百炼 Provider 支持
系统 SHALL 在应用启动时识别并使用阿里百炼作为有效的 API provider。

#### Scenario: 使用阿里百炼 Provider
- **WHEN** 配置文件包含有效的阿里百炼 API Key 和 base URL
- **THEN** 系统在调用模型 API 时使用阿里百炼端点
- **THEN** 用户可以使用阿里百炼提供的大模型（如 qwen3.6-plus、qwen3-coder-plus 等）

## MODIFIED Requirements

### Requirement: 登录方法选择界面
系统 SHALL 扩展现有的登录方法选择界面，添加阿里百炼作为新的登录方法选项。

**现有选项：**
- Claude account with subscription
- Anthropic Console account
- 3rd-party platform
- OpenAI Codex account

**新增选项：**
- 阿里百炼（Ali Bailian）

### Requirement: 平台设置文档列表
系统 SHALL 在"3rd-party platform"设置界面添加阿里百炼文档链接到现有的平台文档列表（Bedrock、Foundry、Vertex AI）。

## REMOVED Requirements
无
