# PR Auto-Comments Integration Tests

This repository serves as an integration testing environment for the [auto-comments](https://github.com/RequestNetwork/auto-comments) reusable GitHub Actions workflow.

## Purpose

The `auto-comments` repository contains a reusable workflow that automatically posts comments on Pull Requests from external contributors. This test repository helps verify that the workflow functions correctly in real-world scenarios before changes are merged into the main workflow.

## Test Workflows

### 1. Automatic PR Testing

The repository includes an integration test workflow that runs automatically on Pull Requests:

- It's triggered by real PR events (opened, ready for review, closed/merged)
- It calls the reusable workflow from the main repository
- It uses test-specific comment messages that clearly indicate they're from a test

This allows testing the workflow by simply creating PRs in this repository.

### 2. Manual Testing

For testing specific branches or features, you can manually trigger the integration test:

1. Go to the Actions tab
2. Select the "Integration Test for PR Automated Comments" workflow
3. Click "Run workflow"
4. Choose:
   - Which branch/tag of the auto-comments repo to test
   - Which comment type to test (first PR, ready for review, merged)
5. The workflow will:
   - Create a test issue
   - Call the workflow with the specified parameters
   - Show results in the issue comments

## Contributing

When making changes to the `auto-comments` workflow:

1. Create a feature branch in the main repository
2. Test your changes using this repository
3. Once verified, merge your changes to the main branch

## Testing Strategies

### Testing a Feature Branch

To test changes before merging to main:

1. Push your changes to a feature branch in the auto-comments repository
2. Run the manual test workflow in this repository
3. Select your feature branch in the "workflow_ref" input
4. Verify the workflow behaves as expected

### Testing Edge Cases

You can test specific scenarios by:

1. Creating PRs with different characteristics in this repository
2. Transitioning PRs through different states (draft, ready, merged)
3. Using different authors (org members vs. external contributors)

## License

MIT
