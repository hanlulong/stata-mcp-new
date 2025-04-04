# Stata MCP Extension for VS Code and Cursor

[![VS Code Marketplace](https://img.shields.io/badge/VS%20Code-Marketplace-blue)](https://marketplace.visualstudio.com/items?itemName=DeepEcon.stata-mcp)
[![GitHub license](https://img.shields.io/github/license/hanlulong/stata-mcp)](https://github.com/hanlulong/stata-mcp/blob/main/LICENSE)

This extension provides Stata integration for Visual Studio Code and Cursor IDE using the Model Context Protocol (MCP). It allows you to:

- Run Stata commands directly from VS Code or Cursor
- Execute selections or entire .do files
- View Stata output in the editor in real-time
- Get AI assistant integration through the MCP protocol
- Experience enhanced AI coding in Cursor IDE with Stata context

## Features

- **Run Stata Commands**: Execute selections or entire .do files directly from your editor
- **Syntax Highlighting**: Full syntax support for Stata .do, .ado, .mata, and .doh files
- **AI Assistant Integration**: Contextual help and code suggestions via MCP
- **Cross-platform**: Works on Windows, macOS, and Linux
- **Automatic Stata Detection**: Automatically finds your Stata installation
- **Real-time Output**: See Stata results instantly in your editor

## Installation Options

### Option 1: VS Code Marketplace

Install this extension directly from the [VS Code Marketplace](https://marketplace.visualstudio.com/items?itemName=DeepEcon.stata-mcp).

```bash
code --install-extension DeepEcon.stata-mcp
```

Or:
1. Open VS Code
2. Go to Extensions view (Ctrl+Shift+X)
3. Search for "Stata MCP"
4. Click "Install"

### Option 2: Cursor Extension Store

For Cursor users:
```bash
cursor --install-extension DeepEcon.stata-mcp
```

Or:
1. Open Cursor
2. Go to Settings > Extensions > Browse Extensions
3. Search for "Stata MCP"
4. Click "Install"

### Option 3: Manual Installation

If you prefer to install manually:

1. Download the latest `.vsix` file from the [GitHub releases page](https://github.com/hanlulong/stata-mcp/releases)
2. For VS Code:
   - Open VS Code
   - Go to Extensions view
   - Click on "..." menu in the top-right
   - Select "Install from VSIX..."
   - Navigate to and select the downloaded .vsix file
3. For Cursor:
   - Run this command in a terminal: `cursor --install-extension path/to/stata-mcp-0.1.3.vsix`

> **Note:** The first time the extension is installed or run may take some time as dependencies need to be added. Please be patient and wait for it to finish. This process should normally take less than 2 minutes.

## Extension Settings

You can customize the extension behavior through VS Code settings:

- `stata-vscode.stataPath`: Path to Stata installation directory
- `stata-vscode.pythonPath`: Path to Python interpreter. If not set, the extension will try to use the system Python or Anaconda base environment
- `stata-vscode.mcpServerHost`: Host for MCP server (default: localhost)
- `stata-vscode.mcpServerPort`: Port for the MCP server (default: 4000)
- `stata-vscode.autoStartServer`: Automatically start MCP server when extension activates (default: true)
- `stata-vscode.debugMode`: Show detailed debug information in output panel (default: false)
- `stata-vscode.forcePort`: Force the MCP server to use the specified port even if it's already in use (default: false)
- `stata-vscode.useUvForPython`: Use uv for Python environment management which is faster and more reliable (default: true)

## Cursor MCP Configuration

To enable AI integration with Stata in Cursor, you need to configure the MCP connection:

1. Create or edit the MCP configuration file:
   - On macOS/Linux: `~/.cursor/mcp.json`
   - On Windows: `%USERPROFILE%\.cursor\mcp.json`

2. Add the following configuration to your `mcp.json` file:

```json
{
  "mcpServers": {
    "stata-mcp": {
      "url": "http://localhost:4000/mcp",
      "transport": "sse"
    }
  }
}
```

3. If you already have other MCP configurations in the file, just add the "stata-mcp" section to your existing "mcpServers" object.

4. Save the file and restart Cursor

This configuration allows Cursor's AI to communicate with the Stata MCP server that starts automatically when you use the extension. When properly configured, the AI assistant can:
- Interact with your Stata sessions
- Execute Stata commands
- Understand your datasets and variables
- Provide more context-aware coding assistance
- Help with data analysis and visualizations

## Requirements

- Stata installed on your machine (Stata 14 or higher recommended)
- Python 3.11 or higher (automatically installed locally if your existing Python version is < 3.11)

## Python Environment Management

The extension now includes advanced Python environment management:

- **Version Check**: Checks if Python 3.11+ is available on your system
- **Smart Installation**: Installs Python 3.11 locally only when your existing Python version is < 3.11
- **Isolated Environment**: Uses a local installation that won't conflict with any existing Python installations
- **Dependency Management**: Sets up a virtual environment with all required packages
- **Cross-Platform Support**: Works on Windows, macOS, and Linux with platform-specific optimizations
- **Fast Package Installation**: Uses [uv](https://github.com/astral-sh/uv), a Python packaging tool built in Rust that's much faster than pip

This ensures the extension works reliably regardless of your existing Python setup and prevents version conflicts.

### About uv Integration

Starting with version 0.1.3, this extension integrates [uv](https://github.com/astral-sh/uv), a fast Python package installer built in Rust that significantly improves dependency installation speed.

How uv is used:
- **When Python is Missing**: If no Python installation is found, the extension uses uv to create a virtual environment and install dependencies
- **When Python < 3.11**: If your system Python is older than 3.11, uv is used to manage a local Python installation
- **For Dependency Management**: All Python package installations use uv for faster installation times

You can control uv usage with the `stata-vscode.useUvForPython` setting (default: true).

**No Action Required**: Everything is handled automatically - the extension will download and use uv as needed without any manual steps from you.

**Performance Improvement**: Package installation with uv can be 10-100x faster than with pip, reducing the initial setup time significantly.

## Usage

1. Open a Stata .do file
2. Run commands using:
   - **Run Selection**: Select Stata code and press `Ctrl+Shift+Enter` (or `Cmd+Shift+Enter` on Mac)
   - **Run File**: Press `Ctrl+Shift+D` (or `Cmd+Shift+D` on Mac) to run the entire .do file
3. View output in the editor panel

## How It Works

The extension creates a local MCP server that connects your editor to Stata, enabling:

1. **Command Execution**: Run Stata commands and see results instantly
2. **Context Awareness**: AI assistants understand your Stata data and commands
3. **Enhanced Productivity**: Get intelligent code suggestions and documentation

## License

MIT

## Credits

Created by Lu Han
Published by DeepEcon 