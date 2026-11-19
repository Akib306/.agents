# Chrome DevTools MCP setup

Use the host's configured server when available. If the project needs a new managed test browser and authorizes setup, register `chrome-devtools-mcp` through the host's normal MCP configuration. For clients that accept a JSON MCP config, this is an example:

```json
{
  "mcpServers": {
    "chrome-devtools": {
      "command": "npx",
      "args": ["-y", "chrome-devtools-mcp", "--isolated"]
    }
  }
}
```

Use the project's approved package version where one is pinned. The isolated mode uses a temporary Chrome profile. Attaching to a running Chrome instance can expose all tabs and authenticated state in that profile. Prefer a separate test profile signed in only to the authorized service. Check whether the authorized test session already exists before asking for an additional login. Follow the installed server's documentation for the supported connection flags.
