# Proxy_Rule

自用的一些代理规则。规则文件本身不带策略，策略在 Loon 里加订阅时选。

## 文件

| 文件 | 内容 | Loon 里怎么用 |
|---|---|---|
| `steam.txt` | Steam 下载与内容域名 | 远程规则，policy 选代理组 |
| `apple-ai-cn-direct.txt` | 国行 Siri / 来电询问，5 条 | 远程规则，policy = DIRECT |
| `apple-ai-cn-proxy.txt` | Apple Intelligence PCC、区域校验、视觉智能，25 条 | 远程规则，policy = Available（或你自己的代理组） |
| `apple-ai-cn.plugin` | 上面两组打包成 Loon 插件，含策略 | 配置 > 插件，整包订阅 |

## 关于 apple-ai-cn

来自 Erosion 的 Surge 模块 `Erosion-AppleIntelligence-CN.sgmodule`，2026-11-26 转写成 Loon 格式。

- 直连组必须真直连。被代理接管后国行 Siri 和「询问来电原因」会失效。
- 代理组需要支持 UDP/QUIC 的美区节点。
- `apple-relay.apple.com` / `mask.icloud.com` / `ropes.apple.com` 解析在 AS714（Apple）。iRingo WeatherKit 里有一条 `AND((IP-ASN 714/6185),(PROTOCOL,QUIC)) → REJECT-DROP`，会把它们的 QUIC 掐掉。所以这组规则要排在它前面：用插件（插件规则 > 订阅规则），或者直接写进主配置 `[Rule]` 最上面（本地规则 > 插件规则）。
- iRingo 的 Siri 插件会 MITM `guzzoni.smoot.apple.com` 改国家码，和直连组互斥，别同时开。

## 远程地址

```
https://raw.githubusercontent.com/FredLin5/Proxy_Rule/main/apple-ai-cn-direct.txt
https://raw.githubusercontent.com/FredLin5/Proxy_Rule/main/apple-ai-cn-proxy.txt
https://raw.githubusercontent.com/FredLin5/Proxy_Rule/main/apple-ai-cn.plugin
```
