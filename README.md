# ACL4SSR：个人分流规则与订阅转换配置

这是从 [cmliu/ACL4SSR](https://github.com/cmliu/ACL4SSR) fork 的规则仓库，包含上游分流列表、订阅转换模板，以及本账号独立维护的个人规则。

## 目录与用途

| 路径 | 用途 |
| --- | --- |
| [personal/](./personal/) | 个人直连、Google 服务及其他国外服务规则；优先查看 [维护说明](./personal/README.md) |
| [Clash/](./Clash/) | 按服务整理的域名和 IP 规则列表 |
| [Clash/config/](./Clash/config/) | 供订阅转换服务使用的 INI 配置模板 |
| [.github/workflows/](./.github/workflows/) | Cloudflare CIDR、Adobe 等列表的自动更新任务 |

## 如何维护个人规则

- 明确直连的网站：修改 [personal/direct.list](./personal/direct.list)。
- Google、Google Play、Gemini、YouTube 等服务：修改 [personal/google.list](./personal/google.list)。
- 其他指定使用国外代理的网站：修改 [personal/proxy.list](./personal/proxy.list)。

个人列表采用 Mihomo 的 `classical` / `text` 格式，每行一个规则，不写策略组名称。规则命中的出口由主配置的 `RULE-SET` 指定。

本账号的私有主配置仓库 [clash-config-private](https://github.com/JunfenZhang1/clash-config-private) 引用了这些个人规则。更新后，需要在客户端更新规则提供者并确认实际出口。

## 维护边界

本仓库既有上游内容，也有个人提交。同步上游前应检查差异并保留 `personal/`；不要把它当成没有个人内容的纯备份 fork。节点密码、机场订阅令牌和 GitHub 令牌不要放入本公开仓库。
