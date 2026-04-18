# Tasks

- [x] Task 1: Add Bailian to forceLoginMethod enum in settings schema
  - [x] SubTask 1.1: Update `forceLoginMethod` enum in `src/utils/settings/types.ts` to include `'bailian'`
  - [x] SubTask 1.2: Add `'bailian'` to `forceLoginMethod` type in `ConsoleOAuthFlow.tsx`

- [x] Task 2: Add Bailian login option to login method selection
  - [x] SubTask 2.1: Add new option to Select options in OAuthStatusMessage's idle state
  - [x] SubTask 2.2: Handle 'bailian' selection to show API key input state
  - [x] SubTask 2.3: Add new OAuthStatus state `'bailian_api_key_input'`

- [x] Task 3: Create Bailian API Key input UI
  - [x] SubTask 3.1: Add TextInput component for API key entry
  - [x] SubTask 3.2: Handle API key submission and validation
  - [x] SubTask 3.3: Save API key to ANTHROPIC_API_KEY environment variable or settings

- [x] Task 4: Add Bailian API Provider support
  - [x] SubTask 4.1: Add `'bailian'` to APIProvider type in `src/utils/model/providers.ts`
  - [x] SubTask 4.2: Add `getBailianBaseUrl()` helper function
  - [x] SubTask 4.3: Update provider detection logic

- [x] Task 5: Add Bailian model configurations
  - [x] SubTask 5.1: Add model configs for Qwen and other Bailian models to `src/utils/model/configs.ts`
  - [x] SubTask 5.2: Register new configs in `ALL_MODEL_CONFIGS`

- [x] Task 6: Update Settings panel for Bailian
  - [x] SubTask 6.1: Add Bailian API key display to Config.tsx settings items
  - [x] SubTask 6.2: Add toggle to enable/disable Bailian provider
  - [x] SubTask 6.3: Handle Bailian config changes and persistence

- [x] Task 7: Test and verify the implementation
  - [x] SubTask 7.1: Verify login flow shows Bailian option
  - [x] SubTask 7.2: Verify API key input and save works
  - [x] SubTask 7.3: Verify Settings panel shows Bailian config
  - [x] SubTask 7.4: Run build to ensure no compilation errors

# Task Dependencies
- [Task 2] depends on [Task 1]
- [Task 3] depends on [Task 2]
- [Task 4] depends on [Task 3]
- [Task 5] depends on [Task 4]
- [Task 6] depends on [Task 5]
- [Task 7] depends on [Task 6]
