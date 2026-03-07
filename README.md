# Clash 规则集

个人整理的 Clash 规则集合，专注于 AI 服务、开发者工具、流媒体和社交媒体。

## 文件说明

| 文件 | 说明 | 规则数量 |
|------|------|---------|
| `AI.yaml` | AI 服务（OpenAI、Claude、Gemini 等） | 84 |
| `AI_Dependencies.yaml` | AI 服务依赖域名（验证、CDN 等） | 18 |
| `Google.yaml` | Google 全家桶（搜索、YouTube、Gmail 等） | 39 |
| `Developer.yaml` | 开发者工具（GitHub、GitLab、Docker 等） | 21 |
| `JetBrains.yaml` | JetBrains IDE 及 AI 服务 | 14 |
| `Microsoft.yaml` | 微软服务（Office、OneDrive、Bing 等） | 29 |
| `Apple.yaml` | Apple 服务（iCloud、App Store 等） | 18 |
| `Social.yaml` | 社交通讯（Telegram、Discord、Facebook、WhatsApp、Instagram） | 63 |
| `Twitter.yaml` | Twitter/X、Reddit | 17 |
| `Media.yaml` | 流媒体（Netflix、Disney+、Spotify、TikTok 等） | 78 |
| `Scholar.yaml` | 学术研究（arXiv、Nature、IEEE 等） | 65 |
| `Wikipedia.yaml` | 维基百科全家桶 | 12 |
| `Community.yaml` | 社区服务（linux.do 等） | 4 |
| `config.example.yaml` | 完整 Clash 配置示例 | - |
| `rule-providers.yaml` | 规则提供者配置片段 | - |

## 使用方法

### 方法一：直接使用示例配置

1. 复制 `config.example.yaml` 为你的主配置文件
2. 在 `proxies:` 部分添加你的代理节点
3. 将节点按地区填入对应的节点组

### 方法二：集成到现有配置

将 `rule-providers` 和 `rules` 部分复制到你的配置文件中：

```yaml
rule-providers:
  AI:
    type: file
    behavior: classical
    path: ./myrule/AI.yaml
  # ... 其他规则

rules:
  - RULE-SET,AI,🤖 AI服务
  # ... 其他规则
  - GEOIP,CN,DIRECT
  - MATCH,DIRECT
```

### 方法三：使用 HTTP 方式引用

将规则文件托管到 GitHub 后：

```yaml
rule-providers:
  AI:
    type: http
    behavior: classical
    url: "https://raw.githubusercontent.com/用户名/仓库名/main/myrule/AI.yaml"
    path: ./ruleset/AI.yaml
    interval: 86400
```

## 目录结构

```
Clash/
├── config.yaml          # 主配置文件
└── myrule/              # 规则文件目录
    ├── AI.yaml
    ├── Google.yaml
    ├── ...
    └── config.example.yaml
```

## 规则优先级

规则按以下顺序匹配，匹配成功后不再继续：

```
AI 服务 → Google → 流媒体 → 社交媒体 → 开发者 → Microsoft → Apple → 学术研究 → 社区 → 国内直连 → 兜底
```

## 更新日志

- 2024-03: 初始版本