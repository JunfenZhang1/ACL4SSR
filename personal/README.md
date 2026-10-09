# 自定义 Mihomo 分流规则 — 按服务分类

所有 `*.list` 均采用 `behavior: classical`、`format: text`，一行一条 `DOMAIN` / `DOMAIN-SUFFIX` 规则；**不写策略组名称**，由私有主配置的 `RULE-SET` 统一决定出口。

| 文件 | 放什么 | 主配置出口 |
| --- | --- | --- |
| [`direct.list`](./direct.list) | 明确要求直连的网站、个别例外 | `DIRECT` |
| [`google.list`](./google.list) | Google 登录、搜索、Google Play、Gemini、AI Studio、NotebookLM、YouTube、Google CDN | `🌐 谷歌服务`（默认 `🚀 节点选择2`） |
| [`proxy.list`](./proxy.list) | 其他指定走国外代理的网站（**不要写 Google 域名**） | `🌍 国外服务` |

## 分流优先级（在 `mixed.yaml` 中）

1. 个人直连例外 `personal-direct`
2. Google 专用规则 `personal-google`，以及上游 Google/YouTube 动态规则
3. 普通国外代理补充 `personal-proxy`
4. ChatGPT、其他 AI、国内外通用规则与最后兜底

## 新增网站时如何选文件

- 谷歌旗下服务与其登录、AI、资源、下载域名 → `google.list`
- 其他需要代理的域名 → `proxy.list`
- 用户明确希望直连的域名 → `direct.list`
- 不要在两个文件中重复放置同一 Google 域名；如确需覆盖，先明确更高优先级的直连例外。

更新 GitHub 后在 Mihomo 客户端更新对应规则提供者或重载配置；如果 `store-selected` 记住了策略组旧选项，还要手动确认实际出口。客户端网络的实际生效情况仍需测试。
