# clash-scholar-rule

一个面向学术/科研网站的 Clash 规则集，便于将常见学术站点统一走指定代理或直连，减少手动维护的负担。

本仓库当前包含：
- `clash-scholar-rule.yaml`：学术相关站点的规则列表

> 适用对象：使用 Clash、Clash Meta 等兼容 RULE-SET/Rule Provider 的客户端或内核。

---

## 快速开始

你可以通过两种方式使用本规则集：作为远程 rule-provider 引用，或下载为本地文件引用。

### 方式一：远程 rule-provider 引用（推荐）

在你的主配置中新增如下片段（请根据自身配置调整代理组名称与路径）：

```yaml
rule-providers:
  scholar:
    type: http
    behavior: classical        # 如遇行为类型不兼容，可尝试改为 domain 或 ipcidr
    url: https://raw.githubusercontent.com/RyanL1nk/clash-scholar-rule/main/clash-scholar-rule.yaml
    path: ./ruleset/scholar.yaml
    interval: 86400            # 每 24 小时自动更新一次

rules:
  - RULE-SET,scholar,PROXY_OR_GROUP_NAME
  - MATCH,DIRECT
```

- 将 `PROXY_OR_GROUP_NAME` 替换为你希望用于学术站点的代理组名称（例如：`Proxy`、`🚀 节点选择`、`SCHOLAR` 等）。
- 建议将该规则放在 `MATCH` 之前，以确保优先生效。

### 方式二：下载为本地文件引用

1. 直接下载本仓库的 `clash-scholar-rule.yaml` 到本地（例如保存为 `./ruleset/scholar.yaml`）。
2. 在主配置中按本地文件引用：

```yaml
rule-providers:
  scholar:
    type: file
    behavior: classical
    path: ./ruleset/scholar.yaml

rules:
  - RULE-SET,scholar,PROXY_OR_GROUP_NAME
  - MATCH,DIRECT
```

---

## 常见问答

- 行为类型 behavior 应该用什么？
  - 默认示例为 `classical`。若你的内核报“不支持的行为类型”，可尝试改用 `domain` 或按客户端文档调整。

- 代理组该怎么配？
  - 只要替换 `PROXY_OR_GROUP_NAME` 为你已有的代理组名称即可。若你专门为学术站点建一个组，例如：
    ```yaml
    proxy-groups:
      - name: SCHOLAR
        type: select
        proxies:
          - Proxy
          - DIRECT
    ```
    然后在规则中写 `RULE-SET,scholar,SCHOLAR`。

- 规则优先级如何安排？
  - 将学术规则放在更靠前的位置，确保不被更泛化的规则（如直连、直插流媒体等）覆盖。

---

## 更新与同步

- 远程方式会按 `interval` 自动更新；
- 本地方式请自行定期同步仓库或手动更新文件。

---

## 贡献

欢迎提交 Issue/PR：
- 补充/修正学术站点域名
- 改进规则匹配与分类
- 适配更多 Clash 内核/客户端的用法示例

---

## 免责声明

- 请在遵守所在地法律法规及各网站使用条款的前提下使用本规则集。
- 本项目仅供学习与研究用途，使用后果由使用者自行承担。
