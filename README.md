README

```markdown
# fix-claude-vscode-windows

A PowerShell patch for the recurring Claude Code VS Code extension activation bug on Windows.

## The Problem

The Claude Code VS Code extension (Anthropic) periodically ships with hardcoded Linux CI build paths baked into `extension.js`. On Windows, this causes the extension to fail activation entirely, resulting in:

```
command 'claude-vscode.editor.openLast' not found
```

```
Activating extension 'Anthropic.claude-code' failed: The argument 'filename' must be a 
file URL object, file URL string, or absolute path string. Received 
'file:///home/runner/work/claude-cli-internal/claude-cli-internal/build-agent-sdk/sdk.mjs'
```

Reinstalling the extension does **not** fix it — the bad paths are baked into the distributed bundle.

Affected versions include: 2.1.51, 2.1.53, 2.1.55, 2.1.129, and likely others.

## The Fix

Run `fix-claude-vscode.ps1` in PowerShell:

```powershell
.\fix-claude-vscode.ps1
```

Then in VS Code: `Ctrl+Shift+P` → **Developer: Reload Window**

The script uses regex to patch all hardcoded Linux paths in `extension.js` regardless of the exact path string, so it should work across affected versions.

## ⚠️ After Extension Updates

This patch will be overwritten every time the extension auto-updates. To prevent that:

- Right-click **Claude Code** in the VS Code Extensions panel
- Select **Disable Auto Update**

Or just re-run the script after each update.

## References

- [GitHub Issue #28051](https://github.com/anthropics/claude-code/issues/28051)
- [GitHub Issue #28081](https://github.com/anthropics/claude-code/issues/28081)
- [GitHub Issue #28416](https://github.com/anthropics/claude-code/issues/28416)
```

