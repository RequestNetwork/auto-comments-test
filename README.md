# PR Auto-Comments Integration Tests

This repository serves as an integration testing environment for the [auto-comments](https://github.com/RequestNetwork/auto-comments) reusable GitHub Actions workflow.

## Purpose

The `auto-comments` repository contains a reusable workflow that automatically posts comments on Pull Requests from external contributors. This test repository helps verify that the workflow functions correctly in real-world scenarios before changes are merged into the main workflow.

## Proper Testing Methodology

The core functionality of the auto-comments workflow can only be properly tested with real user accounts, as it relies on checking organization membership status. For comprehensive testing, you should:

### Create a Testing Matrix

| Test Case | User Type | PR Action | Expected Result |
|-----------|-----------|-----------|-----------------|
| 1 | Internal (org member) | Open PR | No comments |
| 2 | External (non-member) | Open first PR | First PR comment appears |
| 3 | External (non-member) | Open second PR | No first PR comment |
| 4 | External (non-member) | Mark PR ready for review | Ready for review comment appears |
| 5 | External (non-member) | Merge PR | Merged PR comment appears |

### Test with a Real External Account

1. Create or use a GitHub account that is **not** a member of the RequestNetwork organization
2. Have this account create a PR to the auto-comments-test repository
3. Check that the first PR comment appears
4. Have the same account create a second PR
5. Verify that the first PR comment doesn't appear this time
6. Mark the PR as ready for review (after creating as draft)
7. Verify the ready for review comment appears
8. Merge the PR
9. Verify the merged PR comment appears

### Verify Variable Substitution

In all comments, verify that:
- `{{username}}` correctly shows the PR author's username
- `{{repository}}` correctly shows "auto-comments-test"
- `{{org}}` correctly shows "RequestNetwork"

## How This Repository Works

This repository includes a simplified integration-test.yml workflow that:

1. Is triggered by actual pull request events (opened, ready for review, closed)
2. Calls the reusable workflow from the auto-comments repository
3. Provides test-specific comment messages clearly marked with "[TEST]"

By using real pull requests, we can accurately test the workflow's core functionality:
- Organization membership detection
- First PR detection
- Event-specific comments
- Variable substitution

## Best Practices for Testing Changes

1. **Local Validation**: First validate workflow syntax locally
2. **Real User Testing**: Have a non-org member create a PR to verify the full functionality
3. **Review Results**: Check that comments appear correctly and variables are substituted properly

Remember: The most crucial aspects (first-PR detection, org membership detection) can only be properly verified with actual GitHub accounts that are not members of your organization.

## Creating a Test Account

For thorough testing, consider:
1. Creating a dedicated testing GitHub account
2. Keeping it outside your organization
3. Using it exclusively for testing external contributor experiences
4. Documenting test results with screenshots

## License

MIT
