# Clash / Mihomo

Clash / Mihomo 支持远程分流配置，通常通过 `rule-providers` 引用。

## MapleStory

远程 ruleset 地址：

```text
https://raw.githubusercontent.com/Bacon2994/vpn-remote-configs/main/clash/rules/maplestory.yaml
```

配置示例：

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
