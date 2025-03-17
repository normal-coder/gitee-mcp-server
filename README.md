# Gitee MCP Server

Let AI operate Gitee repositories/Issues/Pull Requests for you through MCP

[![Node Version](https://img.shields.io/badge/node-%3E%3D22.12.0-brightgreen.svg)](./package.json)
![NPM Version](https://img.shields.io/npm/v/gitee-mcp-server)
![Docker Pulls](https://img.shields.io/docker/pulls/normalcoder/gitee-mcp-server)
![Docker Image Version](https://img.shields.io/docker/v/normalcoder/gitee-mcp-server)
[![LICENSE](https://img.shields.io/badge/license-MIT-blue.svg)](./LICENSE)
[![smithery badge](https://smithery.ai/badge/@normal-coder/gitee-mcp-server)](https://smithery.ai/server/@normal-coder/gitee-mcp-server)

[<img width="380" height="200" src="https://glama.ai/mcp/servers/cck9xigm1d/badge" />](https://glama.ai/mcp/servers/Cck9XigM1d)

---

## Supported AI Operations

| Category | MCP Tool | Description |
|:----:|:----|:----|
| Repository Operations | `create_repository` | Create a Gitee repository | 
| | `fork_repository` | Fork a Gitee repository | 
| Branch Operations | `create_branch` | Create a new branch in a Gitee repository | 
| | `list_branches` | List branches in a Gitee repository | 
| | `get_branch` | Get details of a specific branch in a Gitee repository | 
| File Operations | `get_file_contents` | Get contents of a file or directory in a Gitee repository | 
| | `create_or_update_file` | Create or update a file in a Gitee repository | 
| | `push_files` | Push multiple files to a Gitee repository | 
| Issue Operations | `create_issue` | Create an Issue in a Gitee repository | 
| | `list_issues` | List Issues in a Gitee repository | 
| | `get_issue` | Get details of a specific Issue in a Gitee repository | 
| | `update_issue` | Update an Issue in a Gitee repository | 
| | `add_issue_comment` | Add a comment to an Issue in a Gitee repository | 
| Pull Request Operations | `create_pull_request` | Create a Pull Request in a Gitee repository | 
| | `list_pull_requests` | List Pull Requests in a Gitee repository | 
| | `get_pull_request` | Get details of a specific Pull Request in a Gitee repository | 
| | `update_pull_request` | Update a Pull Request in a Gitee repository | 
| | `merge_pull_request` | Merge a Pull Request in a Gitee repository | 
| User Operations | `get_user` | Get Gitee user information | 
| | `get_current_user` | Get authenticated Gitee user information | 

## Usage

### Installing via Smithery

To install Gitee MCP Server for Claude Desktop automatically via [Smithery](https://smithery.ai/server/@normal-coder/gitee-mcp-server):

```bash
npx -y @smithery/cli install @normal-coder/gitee-mcp-server --client claude
```

### Configuration

- `GITEE_API_BASE_URL`: Optional, Gitee OpenAPI Endpoint, default is `https://gitee.com/api/v5`
- `GITEE_PERSONAL_ACCESS_TOKEN`: Required, Gitee account personal access token (PAT), can be obtained from Gitee account settings [Personal Access Tokens](https://gitee.com/profile/personal_access_tokens)
- `DEBUG`: Optional, set to `true` to enable debug logging, default is disabled

### Run MCP Server via NPX

```json
{
  "mcpServers": {
    "Gitee": {
      "command": "npx",
      "args": [
        "-y",
        "gitee-mcp-server"
      ],
      "env": {
        "GITEE_PERSONAL_ACCESS_TOKEN": "<YOUR_TOKEN>"
      }
    }
  }
}
```

### Run MCP Server via Docker Container

1. Get Docker Image

```bash
# Get from DockerHub
docker pull normalcoder/gitee-mcp-server

# Build locally
docker build -t normalcoder/gitee-mcp-server .
```

2. Configure MCP Server

```json
{
  "mcpServers": {
    "Gitee": {
      "command": "docker",
      "args": [
        "run",
        "-i",
        "--rm",
        "-e",
        "GITEE_PERSONAL_ACCESS_TOKEN",
        "normalcoder/gitee-mcp-server"
      ],
      "env": {
        "GITEE_PERSONAL_ACCESS_TOKEN": "<YOUR_TOKEN>"
      }
    }
  }
}
```

## Development Guide

### Install Dependencies

```bash
npm install
```

### Build

```bash
npm run build
```

After successful build, `/dist` will contain the runnable MCP server.

### Run Server

```bash
npm start
```

The MCP server will run on stdio, allowing it to be used as a subprocess by MCP clients.

### Build Docker Image

You can also run the server using Docker:

```bash
docker build -t normalcoder/gitee-mcp-server .
```

Run MCP Server with Docker:

```bash
docker run -e GITEE_PERSONAL_ACCESS_TOKEN=<YOUR_TOKEN> normalcoder/gitee-mcp-server
```

### Debug MCP Server

You can use `@modelcontextprotocol/inspector` for debugging:

Create a `.env` file in the root directory for environment variables:

```.env
GITEE_API_BASE_URL=https://gitee.com/api/v5
GITEE_PERSONAL_ACCESS_TOKEN=<YOUR_TOKEN>
```

Run the debug tool to start the service and web debug interface:

```bash
npx @modelcontextprotocol/inspector npm run start --env-file=.env
```

The project includes a `debug()` function for printing debug information, usage:

```typescript
import { debug } from './common/utils.js';

debug('Message to log');
debug('Message with data:', { key: 'value' });
```

Debug logs are only printed when the `DEBUG` environment variable is set to `true`.

## Dependencies

- `@modelcontextprotocol/sdk`: MCP SDK for server implementation
- `universal-user-agent`: For generating user agent strings
- `zod`: For schema validation
- `zod-to-json-schema`: For converting Zod schemas to JSON schemas

## License

Licensed under MIT License. You are free to use, modify and distribute the software, subject to the terms and conditions of the MIT License. For more details, see the [LICENSE](./LICENSE) file in the project repository.

## Related Links

- [Model Context Protocol](https://modelcontextprotocol.io)
- [Gitee](https://gitee.com)
