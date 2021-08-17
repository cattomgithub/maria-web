# Maria - 鞠亚
![](https://img.shields.io/badge/release-v1.0.0-red.svg?style=for-the-badge&logo=appveyor)

鞠亚，一个基础服务支持系统。

名字来自《Date A Live》中 Fraxinus 舰载电脑管理系统 AI —— 或守鞠亚。

## 说明
该项目是我练习 shell 脚本和云原生相关技术的作品

也正是为了不断的完善她，我才会不断学习...

## 目标
- 容器化
- 自动化
- 高可用性
- 随时无缝迁移

## 目前实现的功能
- **近乎**全自动部署各类服务
  
  当然，由于目前脚本写的还是比较粗糙，有时候出错时还是要手动处理

- 自动配置 `Nginx`

- 健全的容器网络隔离策略

- 自动更新文件

## 即将实现的功能
- [x] 利用脚本文件实现全自动部署
- [x] 基于 `acme.sh` 的证书自动部署
- [ ] 证书健康监控
- [ ] 考虑采用更轻量的 Web 程序，如 `Caddy`

## 暂时无法实现的功能
使用 `Kubernetes` 或 `Docker Swarm` 代替 `Docker` 和 `Docker Compose`

> 由于二者都是集群化技术，且目前我的两台主力服务器并不在同一地域，为保证服务稳定性，暂不考虑实现

## 文件架构
```
.
├── 1-Azure-HK
│   ├── docker-compose.yml
│   ├── Dockerfile-Nginx
│   ├── Dockerfile-Prometheus
│   ├── get.acme
│   │   ├── index.html
│   │   └── README.md
│   ├── grafana.json
│   ├── homepage
│   │   ├── index.html
│   │   └── README.md
│   ├── maria.sh
│   ├── nginx
│   │   ├── conf.d
│   │   │   ├── blog.conf
│   │   │   ├── get.acme.conf
│   │   │   ├── git.conf
│   │   │   ├── homepage.conf
│   │   │   ├── monitor.conf
│   │   │   ├── proxy
│   │   │   │   ├── blog.conf
│   │   │   │   ├── git.conf
│   │   │   │   ├── monitor.conf
│   │   │   │   └── webhook-hk.conf
│   │   │   ├── rewrite
│   │   │   ├── status.conf
│   │   │   └── webhook-hk.conf
│   │   └── nginx.conf
│   ├── prometheus.yml
│   ├── status
│   │   ├── config.js
│   │   ├── favicon.ico
│   │   ├── index.html
│   │   ├── README.md
│   │   └── static
│   │       ├── css
│   │       │   └── main.0a38b630.css
│   │       ├── js
│   │       │   ├── main.4a0f818c.js
│   │       │   └── main.4a0f818c.js.LICENSE.txt
│   │       └── media
│   │           └── background.549ae6ef.png
│   └── webhook
│       ├── blog.sh
│       ├── maria.sh
│       └── webhook.json
├── 2-Qcloud-Guangzhou
│   ├── cloud
│   │   ├── cloudreve
│   │   ├── conf.ini
│   │   └── README.md
│   ├── docker-compose.yml
│   ├── Dockerfile
│   ├── maria.sh
│   ├── nginx
│   │   ├── conf.d
│   │   │   ├── cloud.conf
│   │   │   ├── comment.conf
│   │   │   ├── game.conf
│   │   │   ├── proxy
│   │   │   │   ├── cloud.conf
│   │   │   │   ├── game.conf
│   │   │   │   └── webhook-gz.conf
│   │   │   ├── rewrite
│   │   │   └── webhook-gz.conf
│   │   └── nginx.conf
│   └── webhook
│       ├── maria.sh
│       └── webhook.json
├── deploy.md
├── LICENSE
├── maria.sh
├── nginx-conf-template
│   ├── proxy
│   │   └── test.conf
│   ├── rewrite
│   └── test.conf
└── README.md
```
## 服务架构
```
├── Github Page
│   └── Start (https://start.cattom.site/)
├── 1-Azure-HK
│   ├── Gitea (https://git.cattom.site/)
│   ├── Webhook (https://webhook-hk.cattom.site/)
│   ├── Homepage (https://cattom.site/)
│   ├── Status - UptimeRobot (https://status.cattom.site/)
│   ├── Blog - Hugo (https://blog.cattom.site/)
│   ├── Get.acme 【get.acme.sh 镜像，方便中国大陆内的机器安装】【目前唯一公共服务】  (https://get.acme.cattom.site/)
│   └── Monitor - Grafana (https://monitor.cattom.site/)
│       └── Prometheus
└── 2-Qcloud-Guangzhou
    ├── Comment - Wline (https://comment.cattom.site:83/)
    ├── Game - Flatris (https://game.cattom.site:82/)
    └── Cloud - Cloudreve (https://cloud.cattom.site:81/)
```
## 依赖
- Microsoft Azure
- 腾讯云 轻量应用服务器
- 阿里云 对象文件存储
- Cloudflare Worker
- 博客: `Hugo`
- 容器化: `Docker` 和 `Docker Compose`
- Webhook: [`adnanh/webhook`](https://github.com/adnanh/webhook)
- 服务器管理: 宝塔面板
