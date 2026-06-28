# n8n MCP Server Setup

This repository contains configuration and documentation for setting up the n8n MCP (Model Context Protocol) server with Claude Desktop.

## Overview

The n8n MCP server allows Claude to interact with your n8n workflows, enabling automation and integration capabilities directly from Claude conversations.

## Prerequisites

- Node.js (v16 or higher)
- npm or npx
- An n8n instance (cloud or self-hosted)
- n8n API key

## Getting Your n8n API Key

1. Log in to your n8n instance
2. Navigate to **Settings** → **API**
3. Click **Create API Key**
4. Copy the generated API key
5. Store it securely

## Installation

### 1. Install the n8n MCP Server

The n8n MCP server can be run directly via npx without installation:

```bash
npx n8n-mcp
```

### 2. Configure Claude Desktop

To use the n8n MCP server with Claude Desktop, you need to add the configuration to your Claude Desktop config file.

**Configuration File Location:**

- **macOS**: `~/Library/Application Support/Claude/claude_desktop_config.json`
- **Linux**: `~/.config/Claude/claude_desktop_config.json`
- **Windows**: `%APPDATA%\Claude\claude_desktop_config.json`

**Add the following configuration:**

```json
{
  "mcpServers": {
    "n8n-mcp": {
      "command": "npx",
      "args": ["n8n-mcp"],
      "env": {
        "MCP_MODE": "stdio",
        "LOG_LEVEL": "error",
        "DISABLE_CONSOLE_OUTPUT": "true",
        "N8N_API_URL": "YOUR_N8N_INSTANCE_URL",
        "N8N_API_KEY": "YOUR_N8N_API_KEY"
      }
    }
  }
}
```

**Replace the placeholders:**

- `YOUR_N8N_INSTANCE_URL`: Your n8n instance URL (e.g., `https://your-instance.app.n8n.cloud`)
- `YOUR_N8N_API_KEY`: Your n8n API key

### 3. Restart Claude Desktop

After updating the configuration file, restart Claude Desktop to load the n8n MCP server.

## Configuration Options

### Environment Variables

| Variable | Description | Default | Required |
|----------|-------------|---------|----------|
| `MCP_MODE` | Communication mode for MCP | `stdio` | Yes |
| `LOG_LEVEL` | Logging level (error, warn, info, debug) | `info` | No |
| `DISABLE_CONSOLE_OUTPUT` | Disable console output | `false` | No |
| `N8N_API_URL` | Your n8n instance URL | - | Yes |
| `N8N_API_KEY` | Your n8n API key | - | Yes |

## Example Configuration

See the `config/mcp-config.example.json` file for a complete example configuration.

## Verification

To verify the setup is working:

1. Open Claude Desktop
2. Start a new conversation
3. Ask Claude to list available n8n workflows
4. Claude should be able to interact with your n8n instance

## Security Considerations

**IMPORTANT**: Never commit your actual API keys to version control!

- Use environment variables for sensitive data
- Add `claude_desktop_config.json` to your `.gitignore` if storing locally
- Rotate API keys regularly
- Use read-only API keys when possible
- Limit API key permissions to necessary scopes

## Troubleshooting

### Server Not Loading

1. Check that the configuration file is valid JSON
2. Verify the file location is correct for your OS
3. Check Claude Desktop logs for errors
4. Ensure `npx` is available in your PATH

### API Connection Issues

1. Verify your n8n instance is accessible
2. Check that the API key is valid and not expired
3. Ensure the API URL includes the protocol (https://)
4. Check firewall/network settings

### Permission Errors

1. Ensure the API key has necessary permissions
2. Check n8n instance settings for API access
3. Verify your n8n plan includes API access

## Features

With the n8n MCP server, Claude can:

- List available workflows
- Execute workflows
- Check workflow execution status
- Retrieve workflow results
- Manage workflow parameters

## Contributing

Contributions are welcome! Please feel free to submit issues or pull requests.

## Resources

- [n8n Documentation](https://docs.n8n.io/)
- [n8n MCP Server](https://github.com/n8n-io/n8n-mcp)
- [Model Context Protocol Specification](https://modelcontextprotocol.io/)
- [Claude Desktop Documentation](https://docs.claude.com/)

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Support

For issues related to:
- **n8n MCP Server**: Open an issue in the n8n-mcp repository
- **Claude Desktop**: Contact Anthropic support
- **n8n Platform**: Visit n8n community forum or support channels
