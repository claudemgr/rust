# TODO.AI.md

## Broken hook matcher syntax in "Example Project Configuration" (SERVER.md, API.md)

Both `SERVER.md` and `API.md` document a `hooks.PreToolUse` example using
`"matcher": "Write(**)"` and `"matcher": "Write(*.rs)"`. Two bugs:

1. Hook matchers only match tool names (`"Write"`, `"Write|Edit"`) — they
   are not glob patterns and do not support `(...)` syntax. `Write(**)` /
   `Write(*.rs)` will not match anything correctly.
2. The hook commands reference `$file` as a shell environment variable
   (`grep -qi ... "$file"`, `rustfmt --check "$file"`). Hook input arrives
   as JSON on stdin, not an env var — the command needs to extract the
   path itself, e.g. `jq -r '.tool_input.file_path'`.

Fix: change matchers to bare `"Write"` and rewrite each command to read
`tool_input.file_path` from stdin via `jq`, guarding the `.rs`-specific
check by file extension inside the command instead of via the matcher.
