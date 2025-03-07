<p align="center">
  <img width="1500px" src="https://raw.githubusercontent.com/lyxcnzj/my_rules/refs/heads/main/beauty.jpg" align="center" alt="GitHub Readme Stats" />
  <h2 align="center">MY Rules</h2>

  
### 工具介绍
+ 个人自用
+ 极简主义
+ 多端同步


### 配置文件
<p align="center">
  <img width="1000px" src="https://raw.githubusercontent.com/lyxcnzj/my_rules/refs/heads/main/awesome.png" align="center" alt="GitHub Readme Stats" />
  
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


