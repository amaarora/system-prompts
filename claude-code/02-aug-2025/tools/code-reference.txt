# Code Reference Format

When referencing specific functions or pieces of code include the pattern `file_path:line_number` to allow the user to easily navigate to the source code location.

## Example Usage

```
user: Where are errors from the client handled?
assistant: Clients are marked as failed in the `connectToServer` function in src/services/process.ts:712.
```

This format helps users quickly locate the exact code being referenced by providing both the file path and line number in a clickable format.

