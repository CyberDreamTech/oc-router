# OCRouter

**OpenCode 多账号负载均衡网关** — 基于 [codex-lb](https://github.com/Soju06/codex-lb) (MIT License)

将多个 OpenCode API Key 池化到一个统一入口，支持负载均衡、故障切换、用量追踪和 Web 仪表盘。

## 快速开始

```bash
# Docker
docker run -d --name oc-router \
  -p 2455:2455 \
  -v oc-router-data:/var/lib/oc-router \
  ghcr.io/cyberdreamtech/oc-router:latest
```

打开 http://localhost:2455 → 添加 API Key → 完成。

## OpenCode 配置

```jsonc
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "openai": {
      "options": {
        "baseURL": "http://127.0.0.1:2455/v1",
        "apiKey": "{env:OC_ROUTER_API_KEY}"
      }
    }
  }
}
```

## Features

- OpenAI-compatible `/v1/*` 端点（OpenCode 开箱即用）
- 多 Key 负载均衡（round-robin / weighted / least-used）
- 自动故障切换（rate limit、auth error、low balance）
- 用量追踪 + 28 天趋势
- Web 仪表盘（密码 + TOTP 认证）
- SQLite / PostgreSQL

## 底座

本项目 fork 自 [Soju06/codex-lb](https://github.com/Soju06/codex-lb)（v1.20.0-beta.3），适配 OpenCode API Key 池管理。
