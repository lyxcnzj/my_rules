<p align="center">
  <img width="1500px" src="https://raw.githubusercontent.com/lyxcnzj/my_rules/refs/heads/main/beauty.jpg" align="center" alt="GitHub Readme Stats" />
  <h2 align="center">Clash Rules Lite</h2>

  
### 工具介绍
+ 个人自用
+ 极简主义
+ 多端同步
+ 免费cdn

### 如何自定义
1. fork 本仓库：[Fork lyxcnzj/my_rules](https://github.com/lyxcnzj/my_rules/fork) 
2. 触发 GitHub Action 中的 `Generate Rules for Clash` 工作流
3. 编辑 `xx-rules.txt` 以自定义规则
4. 在对应的 Clash 上刷新配置文件

<div align="center">
  <center>
    <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="https://user-images.githubusercontent.com/35565811/184524456-e956ef59-4577-44e9-9b99-4a8684b77e40.png">
    <br>
    <div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999;
    padding: 2px;">启动流水线示意图</div>
  </center>
</div>


Tips:
> a. 可通过访问进行验证 `https://cdn.jsdelivr.net/gh/{你的GITHUB用户名}/my_rules@release/`   
> b. **该仓中以 rules.txt 结尾的文件，都会缓存到 jsdelivr CDN中，可以自定义！**



+ jsdelivr CDN 缓存没有更新怎么办？

> 这是因为 jsdelivr CDN 缓存的原因，一般来说是 24小时刷新缓存，但是这样太慢了！   
> 不过 jsdelivr CDN 也提供手动刷新缓存的方法：
```
# 假设你的文件 URL 是这样：
https://cdn.jsdelivr.net/xxx/xxx...

# 那么把域名中的 cdn 改为 purge 即可：
https://purge.jsdelivr.net/xxx/xxx...

```
然后访问这个文件新 URL 就会提示你刷新成功！

### 配置文件
<p align="center">
  <img width="1000px" src="https://raw.githubusercontent.com/lyxcnzj/my_rules/refs/heads/main/awesome.png" align="center" alt="GitHub Readme Stats" />
  <h2 align="center">Clash Rules Lite</h2>
  
```
# 锚点
pr: &pr {type: select, proxies: [节点选择, 自建节点, 机场节点, 直连]}

# 机场订阅，名称不能重复
proxy-providers:
  01自建:
    type: http
    interval: 1800
    health-check:
      enable: true
      url: https://www.gstatic.com/generate_204
      interval: 300
    proxy: 直连
    url: "你的订阅地址"
  02机场:
    type: http
    interval: 1800
    health-check:
      enable: true
      url: https://www.gstatic.com/generate_204
      interval: 300
    proxy: 直连
    url: "你的订阅地址"



proxies:
- name: "直连"
  type: direct
  udp: true

proxy-groups:
  - {name: 节点选择, type: select, icon: "https://raw.githubusercontent.com/Vbaethon/HOMOMIX/main/Icon/Color/Large/Meta_1.png", proxies: [自建节点, 机场节点, 直连]}
  - {name: 自建节点, type: select, icon: "https://raw.githubusercontent.com/Vbaethon/HOMOMIX/main/Icon/Color/Large/Home.png", use: [01自建]} 
  - {name: 机场节点, type: select, icon: "https://raw.githubusercontent.com/Vbaethon/HOMOMIX/main/Icon/Color/Large/Bytedance.png", use: [02机场]}
  - {name: Google, icon: "https://raw.githubusercontent.com/Vbaethon/HOMOMIX/main/Icon/Color/Large/Google.png", <<: *pr}
  - {name: YouTube, icon: "https://raw.githubusercontent.com/Vbaethon/HOMOMIX/main/Icon/Color/Large/YouTube.png", <<: *pr} 
  - {name: Telegram, icon: "https://raw.githubusercontent.com/Vbaethon/HOMOMIX/main/Icon/Color/Large/Telegram.png", <<: *pr}
  - {name: GitHub, icon: "https://raw.githubusercontent.com/Vbaethon/HOMOMIX/main/Icon/Color/Large/GitHub.png", <<: *pr}
  - {name: AI, icon: "https://raw.githubusercontent.com/Vbaethon/HOMOMIX/main/Icon/Color/Large/ChatGPT.png", <<: *pr}
  - {name: Talkatone, type: select, icon: "https://raw.githubusercontent.com/Vbaethon/HOMOMIX/main/Icon/Color/Large/Chained.png", use: [01自建]}
  - {name: Trade, type: select, icon: "https://raw.githubusercontent.com/Vbaethon/HOMOMIX/main/Icon/Color/Large/Claud.png", use: [01自建]}
  - {name: 漏网之鱼, icon: "https://raw.githubusercontent.com/Vbaethon/HOMOMIX/main/Icon/Color/Large/Scholar.png", <<: *pr}
rules:
  - RULE-SET,private_domain,直连
  - RULE-SET,direct_domain_diy,直连
  - RULE-SET,DNS,节点选择
  - RULE-SET,proxy_domain,节点选择
  - RULE-SET,ai,AI
  - RULE-SET,github_domain,GitHub
  - RULE-SET,youtube_domain,YouTube
  - RULE-SET,google_domain,Google
  - RULE-SET,telegram_domain,Telegram
  - RULE-SET,trade_domain,Trade
  - RULE-SET,geolocation-!cn,节点选择
  - RULE-SET,cn_domain,直连
  - RULE-SET,direct_domain,直连
  - RULE-SET,google_ip,Google,no-resolve
  - RULE-SET,telegram_ip,Telegram,no-resolve
  - RULE-SET,talkatone,Talkatone,no-resolve
  - RULE-SET,cn_ip,直连
  - MATCH,节点选择
rule-anchor:
  ip: &ip {type: http, interval: 86400, behavior: ipcidr, format: mrs}
  domain: &domain {type: http, interval: 86400, behavior: domain, format: mrs}
  lyx: &lyx {type: http, interval: 86400, behavior: domain, format: text}
  class: &class {type: http, interval: 86400, behavior: classical, format: text}
rule-providers: 
  private_domain: { <<: *domain, url: "https://raw.githubusercontent.com/MetaCubeX/meta-rules-dat/meta/geo/geosite/private.mrs" }
  direct_domain_diy: { <<: *class, url: "https://raw.githubusercontent.com/lyxcnzj/my_rules/refs/heads/main/direct.list" }
  direct_domain: { <<: *class, url: "https://raw.githubusercontent.com/lyxcnzj/my_rules/refs/heads/main/Direct.list" }
  proxy_domain: { <<: *class, url: "https://raw.githubusercontent.com/lyxcnzj/my_rules/refs/heads/main/proxy.list" }
  DNS: { <<: *class, url: "https://raw.githubusercontent.com/lyxcnzj/my_rules/refs/heads/main/DNS.list" }
  ai: { <<: *lyx, url: "https://raw.githubusercontent.com/lyxcnzj/my_rules/refs/heads/main/AI.list" }
  youtube_domain: { <<: *domain, url: "https://raw.githubusercontent.com/MetaCubeX/meta-rules-dat/meta/geo/geosite/youtube.mrs" }
  google_domain: { <<: *domain, url: "https://raw.githubusercontent.com/MetaCubeX/meta-rules-dat/meta/geo/geosite/google.mrs" }
  github_domain: { <<: *domain, url: "https://raw.githubusercontent.com/MetaCubeX/meta-rules-dat/meta/geo/geosite/github.mrs" }
  telegram_domain: { <<: *domain, url: "https://raw.githubusercontent.com/MetaCubeX/meta-rules-dat/meta/geo/geosite/telegram.mrs" }
  gfw_domain: { <<: *domain, url: "https://raw.githubusercontent.com/MetaCubeX/meta-rules-dat/meta/geo/geosite/gfw.mrs" }
  geolocation-!cn: { <<: *domain, url: "https://raw.githubusercontent.com/MetaCubeX/meta-rules-dat/meta/geo/geosite/geolocation-!cn.mrs" }
  cn_domain: { <<: *domain, url: "https://raw.githubusercontent.com/MetaCubeX/meta-rules-dat/meta/geo/geosite/cn.mrs" }
  cn_ip: { <<: *ip, url: "https://raw.githubusercontent.com/MetaCubeX/meta-rules-dat/meta/geo/geoip/cn.mrs" }
  google_ip: { <<: *ip, url: "https://raw.githubusercontent.com/MetaCubeX/meta-rules-dat/meta/geo/geoip/google.mrs" }
  telegram_ip: { <<: *ip, url: "https://raw.githubusercontent.com/MetaCubeX/meta-rules-dat/meta/geo/geoip/telegram.mrs" }
  talkatone: { <<: *class, url: "https://raw.githubusercontent.com/lyxcnzj/my_rules/refs/heads/main/talkatone.list" }
  trade_domain: { <<: *class, url: "https://raw.githubusercontent.com/lyxcnzj/my_rules/refs/heads/main/trade.list" }


```


```
# 锚点
pr: &pr {type: select, proxies: [节点选择, 自建节点, 机场节点, 链式代理, 直连]}

# 机场订阅，名称不能重复
proxy-providers:
  01自建:
    type: http
    interval: 1800
    health-check:
      enable: true
      url: https://www.gstatic.com/generate_204
      interval: 300
    proxy: 直连
    url: "你的订阅地址"
  02机场:
    type: http
    interval: 1800
    health-check:
      enable: true
      url: https://www.gstatic.com/generate_204
      interval: 300
    proxy: 直连
    url: "你的订阅地址"



proxies:
- name: "直连"
  type: direct
  udp: true

proxy-groups:
  - {name: 节点选择, type: select, icon: "https://raw.githubusercontent.com/Vbaethon/HOMOMIX/main/Icon/Color/Large/Meta_1.png", proxies: [自建节点, 机场节点, 链式代理, 直连]}
  - {name: 自建节点, type: select, icon: "https://raw.githubusercontent.com/Vbaethon/HOMOMIX/main/Icon/Color/Large/Home.png", use: [01自建]} 
  - {name: 机场节点, type: select, icon: "https://raw.githubusercontent.com/Vbaethon/HOMOMIX/main/Icon/Color/Large/Bytedance.png", use: [02机场]}
  - {name: 链式代理, type: relay, icon: "https://raw.githubusercontent.com/Vbaethon/HOMOMIX/main/Icon/Color/Large/Failover.png", proxies: [中转节点, 落地节点]} 
  - {name: 中转节点, type: select, icon: "https://raw.githubusercontent.com/Vbaethon/HOMOMIX/main/Icon/Color/Large/Chained_2.png", include-all: true,filter: "^((?!(直连)).)*$"}
  - {name: 落地节点, type: select, icon: "https://raw.githubusercontent.com/Vbaethon/HOMOMIX/main/Icon/Color/Large/Dolphin.png", include-all: true,filter: "^((?!(直连)).)*$"}
  - {name: Google, icon: "https://raw.githubusercontent.com/Vbaethon/HOMOMIX/main/Icon/Color/Large/Google.png", <<: *pr}
  - {name: YouTube, icon: "https://raw.githubusercontent.com/Vbaethon/HOMOMIX/main/Icon/Color/Large/YouTube.png", <<: *pr} 
  - {name: Telegram, icon: "https://raw.githubusercontent.com/Vbaethon/HOMOMIX/main/Icon/Color/Large/Telegram.png", <<: *pr}
  - {name: GitHub, icon: "https://raw.githubusercontent.com/Vbaethon/HOMOMIX/main/Icon/Color/Large/GitHub.png", <<: *pr}
  - {name: AI, icon: "https://raw.githubusercontent.com/Vbaethon/HOMOMIX/main/Icon/Color/Large/ChatGPT.png", <<: *pr}
  - {name: Talkatone, type: select, icon: "https://raw.githubusercontent.com/Vbaethon/HOMOMIX/main/Icon/Color/Large/Chained.png", use: [01自建]}
  - {name: Trade, type: select, icon: "https://raw.githubusercontent.com/Vbaethon/HOMOMIX/main/Icon/Color/Large/Claud.png", use: [01自建]}
  - {name: 漏网之鱼, icon: "https://raw.githubusercontent.com/Vbaethon/HOMOMIX/main/Icon/Color/Large/Scholar.png", <<: *pr}
rules:
  - RULE-SET,private_domain,直连
  - RULE-SET,direct_domain_diy,直连
  - RULE-SET,DNS,节点选择
  - RULE-SET,proxy_domain,节点选择
  - RULE-SET,ai,AI
  - RULE-SET,github_domain,GitHub
  - RULE-SET,youtube_domain,YouTube
  - RULE-SET,google_domain,Google
  - RULE-SET,telegram_domain,Telegram
  - RULE-SET,trade_domain,Trade
  - RULE-SET,geolocation-!cn,节点选择
  - RULE-SET,cn_domain,直连
  - RULE-SET,direct_domain,直连
  - RULE-SET,google_ip,Google,no-resolve
  - RULE-SET,telegram_ip,Telegram,no-resolve
  - RULE-SET,talkatone,Talkatone,no-resolve
  - RULE-SET,cn_ip,直连
  - MATCH,节点选择
rule-anchor:
  ip: &ip {type: http, interval: 86400, behavior: ipcidr, format: mrs}
  domain: &domain {type: http, interval: 86400, behavior: domain, format: mrs}
  lyx: &lyx {type: http, interval: 86400, behavior: domain, format: text}
  class: &class {type: http, interval: 86400, behavior: classical, format: text}
rule-providers: 
  private_domain: { <<: *domain, url: "https://raw.githubusercontent.com/MetaCubeX/meta-rules-dat/meta/geo/geosite/private.mrs" }
  direct_domain_diy: { <<: *class, url: "https://raw.githubusercontent.com/lyxcnzj/my_rules/refs/heads/main/direct.list" }
  direct_domain: { <<: *class, url: "https://raw.githubusercontent.com/lyxcnzj/my_rules/refs/heads/main/Direct.list" }
  proxy_domain: { <<: *class, url: "https://raw.githubusercontent.com/lyxcnzj/my_rules/refs/heads/main/proxy.list" }
  DNS: { <<: *class, url: "https://raw.githubusercontent.com/lyxcnzj/my_rules/refs/heads/main/DNS.list" }
  ai: { <<: *lyx, url: "https://raw.githubusercontent.com/lyxcnzj/my_rules/refs/heads/main/AI.list" }
  youtube_domain: { <<: *domain, url: "https://raw.githubusercontent.com/MetaCubeX/meta-rules-dat/meta/geo/geosite/youtube.mrs" }
  google_domain: { <<: *domain, url: "https://raw.githubusercontent.com/MetaCubeX/meta-rules-dat/meta/geo/geosite/google.mrs" }
  github_domain: { <<: *domain, url: "https://raw.githubusercontent.com/MetaCubeX/meta-rules-dat/meta/geo/geosite/github.mrs" }
  telegram_domain: { <<: *domain, url: "https://raw.githubusercontent.com/MetaCubeX/meta-rules-dat/meta/geo/geosite/telegram.mrs" }
  gfw_domain: { <<: *domain, url: "https://raw.githubusercontent.com/MetaCubeX/meta-rules-dat/meta/geo/geosite/gfw.mrs" }
  geolocation-!cn: { <<: *domain, url: "https://raw.githubusercontent.com/MetaCubeX/meta-rules-dat/meta/geo/geosite/geolocation-!cn.mrs" }
  cn_domain: { <<: *domain, url: "https://raw.githubusercontent.com/MetaCubeX/meta-rules-dat/meta/geo/geosite/cn.mrs" }
  cn_ip: { <<: *ip, url: "https://raw.githubusercontent.com/MetaCubeX/meta-rules-dat/meta/geo/geoip/cn.mrs" }
  google_ip: { <<: *ip, url: "https://raw.githubusercontent.com/MetaCubeX/meta-rules-dat/meta/geo/geoip/google.mrs" }
  telegram_ip: { <<: *ip, url: "https://raw.githubusercontent.com/MetaCubeX/meta-rules-dat/meta/geo/geoip/telegram.mrs" }
  talkatone: { <<: *class, url: "https://raw.githubusercontent.com/lyxcnzj/my_rules/refs/heads/main/talkatone.list" }
  trade_domain: { <<: *class, url: "https://raw.githubusercontent.com/lyxcnzj/my_rules/refs/heads/main/trade.list" }

```


