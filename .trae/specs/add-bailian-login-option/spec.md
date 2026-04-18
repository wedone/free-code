# 阿里百炼登录选项 Spec

## Why
用户希望在 `/login` 命令中能够直接选择阿里百炼（Alibaba Bailian）作为登录方式，而不是只能通过配置环境变量来使用。当前登录界面提供了 Claude account、Anthropic Console、第三方平台（Bedrock/Vertex/Foundry）和 OpenAI Codex 选项，但缺少阿里百炼的直接入口。

## What Changes
- 在 `ConsoleOAuthFlow.tsx` 的登录方法选择界面添加"阿里百炼"选项
- 添加新的登录方法类型 `'bailian'` 到 `forceLoginMethod` 枚举
- 创建 Bailian API Key 输入界面（使用 `TextInput` 组件）
- 添加 Bailian 配置保存到 settings 的支持
- 在 Settings 配置面板中添加 Bailian 相关配置显示
- 扩展 `APIProvider` 类型以支持 `'bailian'`
- 添加 Bailian 模型配置到 `configs.ts`

## Impact
- Affected specs: `/login` 命令、OAuth 登录流程、Settings 配置面板
- Affected code: 
  - `src/components/ConsoleOAuthFlow.tsx` - 主要登录 UI
  - `src/utils/settings/types.ts` - settings schema
  - `src/utils/model/providers.ts` - API provider 类型
  - `src/utils/model/configs.ts` - 模型配置
  - `src/utils/auth.ts` - API key 处理
  - `src/utils/model/model.ts` - 模型解析

## ADDED Requirements

### Requirement: Bailian Login Option
系统 SHALL 在 `/login` 命令的登录方法选择界面提供"阿里百炼"选项。

#### Scenario: 用户选择阿里百炼登录
- **WHEN** 用户在登录方法选择界面选择"阿里百炼"
- **THEN** 系统显示 API Key 输入界面
- **AND** 用户输入有效的 API Key 后，系统保存配置
- **AND** 用户可以使用阿里百炼的大模型

### Requirement: Bailian API Key Input
系统 SHALL 提供一个安全的 API Key 输入界面，支持用户输入和保存阿里百炼的 API Key。

#### Scenario: 输入并保存 API Key
- **WHEN** 用户在 API Key 输入界面输入有效的 API Key
- **AND** 用户提交（按 Enter）
- **THEN** 系统保存 API Key 到 settings
- **AND** 系统显示登录成功消息
- **AND** 用户可以开始使用阿里百炼模型

### Requirement: Bailian Provider Configuration
系统 SHALL 支持将阿里百炼配置为 API 提供者，使用 Anthropic 兼容协议。

#### Scenario: 使用阿里百炼模型
- **WHEN** 用户已配置阿里百炼 API Key
- **AND** 用户运行 Claude Code
- **THEN** 系统使用阿里百炼的 API endpoint 进行请求
- **AND** 用户可以选择阿里百炼提供的模型（Qwen 系列等）

### Requirement: Settings Panel Bailian Config
系统 SHALL 在 Settings 配置面板中显示和管理阿里百炼相关配置。

#### Scenario: 查看和修改 Bailian 配置
- **WHEN** 用户打开 `/config` 设置面板
- **THEN** 系统显示阿里百炼 API Key 配置项（部分隐藏）
- **AND** 用户可以切换启用/禁用阿里百炼
- **AND** 用户可以修改 API Key

## MODIFIED Requirements

### Requirement: forceLoginMethod 枚举
**当前**: `forceLoginMethod` 支持 `'claudeai'` | `'console'`  
**修改为**: `forceLoginMethod` 支持 `'claudeai'` | `'console'` | `'bailian'`

### Requirement: APIProvider 类型
**当前**: `APIProvider` 包含 `'firstParty' | 'bedrock' | 'vertex' | 'foundry' | 'openai'`  
**修改为**: 添加 `'bailian'` 到 `APIProvider` 联合类型

## REMOVED Requirements
无
