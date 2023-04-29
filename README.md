# 一篇文章记录折腾优雅上网那些事
2023年4月29日 开篇 持续更新

## 1 Warp的折腾记录
为了使用ChatGPT，特意购买了一台美区服务器，专门为OpenAI开路，然后，用了不到半个月，ip噶了...
原本想开一台AWS的US区lightsail，不用管速度，主打一个游击战，ChatGPT一ban我，我就换ip，结果发现，AWS的ip被ChatGPT封完了，真是美国人何苦为难美国人。
那咱就另辟蹊径呗，于是发现了CloudFlare家的一款产品[WARP](https://1.1.1.1/)，不多说了，开始整活吧。
今天的目标：warp在ubuntu上的配置、warp的桌面端优选ip

### 1.1 Warp是什么
Warp本质上属于一个VPN软件，它基于wireguard的VPN协议，利用cloudflare在全球的节点，帮助用户可以通过离自己最近的节点代理后上网，除了今天介绍在linux上跑服务，它还有PC和Mac的桌面端，可以提供一键直连服务。
### 1.2 自己折腾Warp时发现的一些tips
1、warp会通过一些技术手段定位你的ip，所以一些非原生ip很有可能会飘定位，例如你买的非原生ip美国vps，它帮你选择节点时，可能会给你一个国内的节点（具体不知道怎么追溯ip定位的，有兴趣的同学可以自行拓展一下），这就很蠢，我好不容易出国了，warp又强制把我送回来了，但本文会着重解决这个问题。  
2、假设你通过本文下述的优选ip配置完warp桌面端后，warp给了你一个在国内的ip，这个ip可以访问google的服务，因为cloudflare可能对google服务做过优化，奈飞啥的就别想了。  
3、warp解锁奈飞这件事，我不太确定，大家说行就行吧。  

### 1.3 Warp官方文档
[官网文档在这](https://developers.cloudflare.com/warp-client/get-started/linux/)  
不管在哪一个os下，warp始终有两个软件在效力，第一 [warp-cli] 脚手架，负责设置项目；第二 [warp-svc] 服务，负责程序运行  
官方的文档说的比较明确，这里不再赘述，有兴趣的小伙伴可以研究官网文档，没兴趣的，直接上脚本。
