# MoviePilot V2 🎬

观影助手 - Docker 一站式部署方案

## 快速开始

```bash
# 1. 配置环境变量
cp .env.example .env
# 编辑 .env 填入 TMDB_API_KEY 等必要信息

# 2. 启动所有服务
docker compose up -d

# 3. 访问服务
# - MoviePilot:  http://localhost:3000
# - qBittorrent: http://localhost:8082  (admin / adminadmin)
# - Jackett:     http://localhost:9117
```

## 服务说明

| 服务 | 端口 | 说明 |
|------|------|------|
| MoviePilot | 3000 | 主程序：影片搜索、订阅、刮削、整理 |
| qBittorrent | 8082 | BT 下载器 |
| Jackett | 9117 | 索引器：聚合搜索各站点资源 |

## 目录结构

```
moviepilotv2/
├── docker-compose.yml    # 容器编排
├── .env.example          # 环境变量模板
├── config/               # MoviePilot 配置
├── media/                # 媒体库目录
├── downloads/            # 下载目录
├── qbittorrent/config/   # qBittorrent 配置
└── jackett/config/       # Jackett 配置
```

## 必要配置

1. **TMDB API Key** — 去 https://www.themoviedb.org/settings/api 申请
2. 填入 `.env` 文件后重启：`docker compose restart moviepilot`

## ☕ 支持 / Support

如果这个教程对你有帮助，欢迎请我喝杯咖啡：

**USDT (TRC20)**
```
TVbQerV1SF4MXB1JCcAzQxarewHwEPYTKm
```
