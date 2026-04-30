# Bear Codex Plugin

This plugin connects Codex to Bear through Bear's first-party MCP server.

This is an unofficial Codex plugin. It is not affiliated with, endorsed by, or maintained by Shiny Frog or Bear. It uses Bear's official BearCLI and MCP server, which are currently in beta.

## Requirements

- Bear 2.8 or newer
- `bearcli` included with Bear

The plugin launches BearCLI through `scripts/bearcli-wrapper`, which checks common install locations and also supports:

```sh
BEARCLI=/path/to/bearcli
```

## MCP

The plugin registers one MCP server named `bear`:

```json
{
  "mcpServers": {
    "bear": {
      "command": "./scripts/bearcli-wrapper",
      "args": ["mcp-server"]
    }
  }
}
```
