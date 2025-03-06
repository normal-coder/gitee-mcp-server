<div align="center">
<h2>Gitee MCP Server</h2>
<p align="center">通过 MCP，让 AI 代你操作 Gitee 上的仓库/Issue/Pull Request</p>

[![LICENSE](https://img.shields.io/badge/license-MIT-blue.svg)](./LICENSE)

[![Node Version](https://img.shields.io/badge/node-%3E%3D22.12.0-brightgreen.svg)](./package.json)
![NPM Version](https://img.shields.io/npm/v/gitee-mcp-server)

![Docker Pulls](https://img.shields.io/docker/pulls/normalcoder/gitee-mcp-server)
![Docker Image Version](https://img.shields.io/docker/v/normalcoder/gitee-mcp-server)
</div>

---

## 当前支持 AI 调度的能力

| 工具分类 | MCP Tool 工具名称 | 能力描述 |
|:----:|:----|:----|
| 仓库操作 | `create_repository` | 创建一个 Gitee 仓库 | 
| | `fork_repository` | Fork Gitee 仓库 | 
| 分支操作 | `create_branch` | 在 Gitee 仓库中创建一个新分支 | 
| | `list_branches` | 列出 Gitee 仓库中的分支 | 
| | `get_branch` | 获取 Gitee 仓库中的特定分支信息 | 
| 文件操作 | `get_file_contents` | 获取 Gitee 仓库中文件或目录的内容 | 
| | `create_or_update_file` | 在 Gitee 仓库中创建或更新文件 | 
| | `push_files` | 向 Gitee 仓库提交多个文件 | 
| Issue 操作 | `create_issue` | 在 Gitee 仓库中创建 Issue | 
| | `list_issues` | 列出 Gitee 仓库中的 Issues | 
| | `get_issue` | 获取 Gitee 仓库中的特定 Issue | 
| | `update_issue` | 更新 Gitee 仓库中的 Issue | 
| | `add_issue_comment` | 向 Gitee 仓库中的 Issue 添加评论 | 
| Pull Request 操作 | `create_pull_request` | 在 Gitee 仓库中创建 Pull Request | 
| | `list_pull_requests` | 列出 Gitee 仓库中的 Pull Requests | 
| | `get_pull_request` | 获取 Gitee 仓库中的特定 Pull Request | 
| | `update_pull_request` | 更新 Gitee 仓库中的 Pull Request | 
| | `merge_pull_request` | 合并 Gitee 仓库中的 Pull Request | 
| 用户操作 | `get_user` | 获取 Gitee 用户信息 | 
| | `get_current_user` | 获取当前认证的 Gitee 用户信息 | 

## 用法

### 配置项

- `GITEE_API_BASE_URL`: 可选项，Gitee OpenAPI Endpoint，默认值为 `https://gitee.com/api/v5`
- `GITEE_PERSONAL_ACCESS_TOKEN`: 必填项，Gitee 账户的个人访问令牌（PAT），可通过 Gitee 的账户设置，获取对应帐号的 [个人访问令牌](https://gitee.com/profile/personal_access_tokens)


### 通过 NPX 运行 MCP 服务器

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

### 通过 Docker 容器运行 MCP 服务器

1. 获取 Docker 镜像

```bash
# 从 DockerHub 获取
docker pull normalcoder/gitee-mcp-server

# 自行构建
docker build -t normalcoder/gitee-mcp-server .
```

2. 配置 MCP 服务器

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

## 开发说明

### 安装依赖

```bash
npm install
```

### 构建

```bash
npm run build
```

构建成功后，`/dist` 即为可运行的 MCP 服务器。

### 运行服务器

```bash
npm start
```

MCP 服务器将运行在 stdio 上，这使得它可以作为 MCP 客户端的子进程使用。

### 构建 Docker 镜像

你也可以使用 Docker 运行服务器：

```bash
docker build -t normalcoder/gitee-mcp-server .
```

使用 Docker 运行 MCP 服务器：

```bash
docker run -e GITEE_PERSONAL_ACCESS_TOKEN=<YOUR_TOKEN> normalcoder/gitee-mcp-server
```

### 调试 MCP 服务器

你可以使用 `@modelcontextprotocol/inspector` 进行调试：

在仓库根目录创建一个 `.env` 文件存放环境变量配置：

```.env
GITEE_API_BASE_URL=https://gitee.com/api/v5
GITEE_PERSONAL_ACCESS_TOKEN=<YOUR_TOKEN>
```

运行调试工具启动服务和 Web 调试界面：

```bash
npx @modelcontextprotocol/inspector npm run start --env-file=.env
```

工程中内置了一个 `debug()` 函数，可以用于输出打印调试信息，使用方法如下：

```typescript
import { debug } from './common/utils.js';

debug('要记录的消息');
debug('带有数据的消息：', { key: 'value' });
```

## 依赖

- `@modelcontextprotocol/sdk`：MCP SDK 用于服务器实现
- `universal-user-agent`：用于生成用户代理字符串
- `zod`：用于模式验证
- `zod-to-json-schema`：用于将 Zod 模式转换为 JSON 模式

## 许可

基于 MIT 许可证授权。你可以自由使用、修改和分发软件，必须遵守 MIT 许可证的条款和条件。有关更多详细信息，请参阅项目仓库中的 [LICENSE](./LICENSE) 文件。

## 相关链接

- [Model Context Protocol](https://modelcontextprotocol.io)
- [Gitee](https://gitee.com)