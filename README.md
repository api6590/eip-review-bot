# EIP Review Bot

## Progress on Last-Call-Deadline Check

### Issue Identification
This work addresses issue #21, which relates to the implementation of a last-call-deadline check for Ethereum Improvement Proposals (EIPs).

### Implementation Details
- **Automatic Deadline Setting**: If an EIP is in "Last Call" status and does not have a `last-call-deadline`, it is automatically set to 14 days in the future.
- **Validation**: The implementation includes validation to ensure that the `last-call-deadline` is at least two weeks from the last commit date.

### Code Snippets
```javascript
if (frontmatter.status == "Last Call" && !frontmatter["last-call-deadline"]) {
    const fourteenDays = new Date(Date.now() + 12096e5); // 14 days in milliseconds
    frontmatter["last-call-deadline"] = new Date(
        `${fourteenDays.getUTCFullYear()}-${fourteenDays.getUTCMonth() + 1}-${fourteenDays.getUTCDate()}`
    );
    anyFilesChanged = true;
}
```
### Testing

I have tested the implementation locally to ensure that the deadline is set correctly and validated against the last commit date. However, I ran into issues that are stated in the [pull request](https://github.com/ethereum/eip-review-bot/pull/409).
