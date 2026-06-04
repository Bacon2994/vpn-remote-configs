# VPN Remote Configs

个人 VPN / 代理软件远程配置库。

## 目录结构

```text
loon/
  rules/      Loon 分流规则
  rewrites/   Loon 重写规则
  plugins/    Loon 插件
  configs/    Loon 配置片段或完整配置

clash/
  rules/      Clash / Mihomo rule-providers 规则
  providers/  Clash / Mihomo proxy-providers 配置
  configs/    Clash / Mihomo 配置片段或完整配置

shared/
  domains/    跨软件共用域名清单
  ip-cidr/    跨软件共用 IP 网段清单
```

## MapleStory

### Loon

在 Loon 的 `[Remote Rule]` 中添加：

```ini
https://raw.githubusercontent.com/Bacon2994/vpn-remote-configs/main/loon/rules/maplestory.lsr, policy=MapleStory, tag=MapleStory, enabled=true
```

本地 `[Proxy Group]` 需要提前定义 `MapleStory` 策略组，例如：

```ini
MapleStory = select,你的美国节点或订阅策略
```

### Clash / Mihomo

在 Clash / Mihomo 配置里添加：

```yaml
rule-providers:
  maplestory:
    type: http
    behavior: classical
    format: yaml
    url: https://raw.githubusercontent.com/Bacon2994/vpn-remote-configs/main/clash/rules/maplestory.yaml
    path: ./ruleset/maplestory.yaml
    interval: 86400

rules:
  - RULE-SET,maplestory,MapleStory
```

本地 `proxy-groups` 需要提前定义 `MapleStory` 策略组，例如：

```yaml
proxy-groups:
  - name: MapleStory
    type: select
    proxies:
      - 你的美国节点
      - DIRECT
```

## 说明

MapleStory 规则来自本机 Loon 日志中实际命中过的 Nexon 域名、游戏端口和 AWS EC2 网段，并补充 us-west-2 常见 EC2 大段以减少频道随机 IP 漏网。
