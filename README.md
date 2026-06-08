# MoviePilot V2 🎬

> 观影助手 — 一站式 Docker 媒体自动化管理解决方案
> Media Assistant — All-in-One Docker Media Automation Solution

---

## 📑 目录 / Table of Contents

- [📖 项目简介 / What is MoviePilot V2](#-项目简介--what-is-moviepilot-v2)
- [🏗️ 系统架构 / System Architecture](#️-系统架构--system-architecture)
- [🚀 快速开始 / Quick Start](#-快速开始--quick-start)
- [⚙️ 环境变量配置 / Environment Configuration](#️-环境变量配置--environment-configuration)
- [📋 服务端口一览 / Service Ports](#-服务端口一览--service-ports)
- [📂 目录结构 / Directory Structure](#-目录结构--directory-structure)
- [🔧 下载器配置 / Downloader Setup](#-下载器配置--downloader-setup)
- [📺 媒体服务器集成 / Media Server Integration](#-媒体服务器集成--media-server-integration)
- [🎯 媒体刮削与元数据 / Media Scraper & Metadata](#-媒体刮削与元数据--media-scraper--metadata)
- [📥 自动下载规则与订阅 / Auto-Download Rules & Subscriptions](#-自动下载规则与订阅--auto-download-rules--subscriptions)
- [🔔 通知配置 / Notification Setup](#-通知配置--notification-setup)
- [🧩 索引器配置 / Indexer Setup](#-索引器配置--indexer-setup)
- [🐳 Docker 命令参考 / Docker Commands Reference](#-docker-命令参考--docker-commands-reference)
- [⚠️ 常见问题与排错 / Common Issues & Troubleshooting](#️-常见问题与排错--common-issues--troubleshooting)
- [🛠️ 小技巧 / Tips & Tricks](#️-小技巧--tips--tricks)
- [☕ 支持这个项目 / Support This Project](#-支持这个项目--support-this-project)

---

## 📖 项目简介 / What is MoviePilot V2

**中文**

MoviePilot V2 是一款强大的**媒体自动化管理工具**，基于 Docker 容器化部署，帮助你自动完成从影片搜索、订阅、下载、元数据刮削到媒体库整理的**全流程自动化**。它集成了索引器、下载器和媒体服务器，让你轻松搭建属于自己的私人影音系统。

核心特性：

- 🎬 **自动订阅** — 设定想看的内容，有新资源自动下载
- 🏷️ **智能刮削** — 自动获取 TMDB 元数据（封面、简介、演员、评分）
- 📂 **自动整理** — 按规则整理到媒体库目录，电影/电视剧自动分类
- 🔗 **多服务集成** — 支持 Emby / Jellyfin / Plex 媒体服务器
- 📥 **多下载器** — 支持 qBittorrent、Transmission 等主流下载器
- 🌐 **多索引器** — 支持 Jackett、Prowlarr 等索引聚合工具
- 🔔 **消息通知** — 支持 Telegram、Server酱、微信等多种通知渠道

---

**English**

MoviePilot V2 is a powerful **media automation management tool** deployed via Docker containers. It automates the entire media workflow — from searching, subscribing, and downloading, to metadata scraping and library organization — so you can build your own private home theater system effortlessly.

Core Features:

- 🎬 **Auto Subscription** — Subscribe to movies/shows, new releases get downloaded automatically
- 🏷️ **Smart Scraping** — Automatically fetch TMDB metadata (posters, synopsis, cast, ratings)
- 📂 **Auto Organization** — Sort media into libraries with movie/TV show categorization
- 🔗 **Multi-Service Integration** — Compatible with Emby / Jellyfin / Plex media servers
- 📥 **Multi-Downloader** — Supports qBittorrent, Transmission, and more
- 🌐 **Multi-Indexer** — Supports Jackett, Prowlarr, and other index aggregators
- 🔔 **Notifications** — Send alerts via Telegram, ServerChan, WeChat, and more

---

## 🏗️ 系统架构 / System Architecture

**中文**

MoviePilot V2 采用微服务架构，核心组件协同工作：

**English**

MoviePilot V2 uses a microservice architecture where core components work together:

```
                    ┌─────────────────────────────┐
                    │     索引器 / Indexer         │
                    │  (Jackett / Prowlarr)        │
                    │  ← 搜索各站资源 / Search BT  │
                    └─────────────┬───────────────┘
                                  │
                                  ▼
                    ┌─────────────────────────────┐
                    │      MoviePilot V2           │
                    │  主程序：订阅·刮削·整理       │
                    │  Core: Subscribe·Scrape·Sort │
                    └─────────────┬───────────────┘
                                  │
                    ┌─────────────┴───────────────┐
                    │        下载器 / Downloader    │
                    │  (qBittorrent / Transmission)│
                    │  ← 下载资源 / Download files │
                    └─────────────────────────────┘

            ┌───────────┐    ┌───────────┐    ┌───────────┐
            │   Emby    │    │  Jellyfin │    │    Plex   │
            │  媒体服务器 │    │  媒体服务器 │    │  媒体服务器 │
            └───────────┘    └───────────┘    └───────────┘
```

---

## 🚀 快速开始 / Quick Start

### 前置条件 / Prerequisites

| 项目 / Item | 说明 / Description |
|---|---|
| Docker & Docker Compose | 确保已安装 Docker 24+ 和 Docker Compose v2 |
| TMDB API Key | **必填** — 用于刮削元数据，[免费申请](https://www.themoviedb.org/settings/api) |
| 网络环境 | 需要能访问 BT 站点和 TMDB |

### 一键部署 / One-Click Deployment

**中文**

1. 克隆仓库并进入目录：
2. 配置环境变量文件
3. 一键启动所有服务
4. 访问管理界面

**English**

1. Clone the repo and enter the directory
2. Configure the environment file
3. Start all services with one command
4. Access the web UI

```bash
# 1️⃣ 克隆仓库 / Clone the repository
git clone https://github.com/caizhenwei33-cmyk/moviepilotv2.git
cd moviepilotv2

# 2️⃣ 配置环境变量 / Configure environment variables
cp .env.example .env
# 编辑 .env 文件，填入 TMDB_API_KEY 等必要信息
# Edit .env and set TMDB_API_KEY and other required values
# vim .env 或 nano .env

# 3️⃣ 启动所有服务 / Start all services
docker compose up -d

# 4️⃣ 访问管理界面 / Access management UI
# - MoviePilot:  http://localhost:3000
# - qBittorrent: http://localhost:8082  (admin / adminadmin)
# - Jackett:     http://localhost:9117
```

---

## ⚙️ 环境变量配置 / Environment Configuration

**中文**

所有的配置通过 `.env` 文件（或 `docker-compose.yml` 中的 environment 字段）进行管理。关键配置项如下：

**English**

All configuration is managed via the `.env` file (or the `environment` section in `docker-compose.yml`). Key configuration options:

### 基础配置 / Basic Configuration

| 变量 / Variable | 必填 / Required | 说明 / Description |
|---|---|---|
| `TZ` | 否 | 时区，默认 `Asia/Shanghai` |
| `PUID` | 否 | 运行用户 UID，默认 `1000` |
| `PGID` | 否 | 运行用户 GID，默认 `1000` |
| `UMASK` | 否 | 文件权限掩码，默认 `022` |

### 登录认证 / Authentication

| 变量 / Variable | 必填 / Required | 说明 / Description |
|---|---|---|
| `SUPERUSER` | 是 | 管理员用户名 |
| `SUPERUSER_PASSWORD` | 是 | 管理员密码 |

### TMDB 配置（必填）/ TMDB Configuration (Required)

| 变量 / Variable | 必填 / Required | 说明 / Description |
|---|---|---|
| `TMDB_API_KEY` | **✅ 必填** | TMDB API Key，[申请地址](https://www.themoviedb.org/settings/api) |
| `TMDB_API_DOMAIN` | 否 | TMDB API 域名，默认 `api.themoviedb.org` |

### 下载器配置 / Downloader Configuration

| 变量 / Variable | 必填 / Required | 说明 / Description |
|---|---|---|
| `DOWNLOADER` | 否 | 下载器类型：`qbittorrent` / `transmission` |
| `QB_HOST` | 否 | qBittorrent 地址，如 `http://qbittorrent:8082` |
| `QB_USER` | 否 | qBittorrent 用户名，默认 `admin` |
| `QB_PASSWORD` | 否 | qBittorrent 密码，默认 `adminadmin` |
| `TR_HOST` | 否 | Transmission 地址 |
| `TR_USER` | 否 | Transmission 用户名 |
| `TR_PASSWORD` | 否 | Transmission 密码 |

### 索引器配置 / Indexer Configuration

| 变量 / Variable | 必填 / Required | 说明 / Description |
|---|---|---|
| `INDEXER` | 否 | 索引器类型：`jackett` / `prowlarr` |
| `JACKETT_HOST` | 否 | Jackett 地址，如 `http://jackett:9117` |
| `JACKETT_API_KEY` | 否 | Jackett API Key |
| `PROWLARR_HOST` | 否 | Prowlarr 地址 |
| `PROWLARR_API_KEY` | 否 | Prowlarr API Key |

### 媒体服务器集成 / Media Server Integration

| 变量 / Variable | 必填 / Required | 说明 / Description |
|---|---|---|
| `MEDIA_SERVER` | 否 | 媒体服务器类型：`emby` / `jellyfin` / `plex` |
| `EMBY_HOST` | 否 | Emby 地址，如 `http://emby:8096` |
| `EMBY_API_KEY` | 否 | Emby API Key |
| `JELLYFIN_HOST` | 否 | Jellyfin 地址 |
| `JELLYFIN_API_KEY` | 否 | Jellyfin API Key |
| `PLEX_HOST` | 否 | Plex 地址 |
| `PLEX_TOKEN` | 否 | Plex Token |

---

## 📋 服务端口一览 / Service Ports

| 服务 / Service | 端口 / Port | 说明 / Description |
|---|---|---|
| MoviePilot | `3000` | Web 管理界面 / Web Management UI |
| qBittorrent | `8082` | 下载器管理界面 / Downloader UI |
| qBittorrent | `6881` | BT 下载端口 TCP+UDP / BT Download Port |
| Jackett | `9117` | 索引器管理界面 / Indexer UI |

---

## 📂 目录结构 / Directory Structure

**中文**

```
moviepilotv2/
├── docker-compose.yml      # Docker 容器编排文件 / Service orchestration
├── .env.example            # 环境变量模板 / Environment template
├── config/                 # MoviePilot 配置文件 / Configuration files
├── media/                  # 整理后的媒体库目录 / Organized media library
│   ├── movies/             # 电影 / Movies
│   └── tvshows/            # 电视剧 / TV Shows
├── downloads/              # 下载中的临时文件 / Download in progress
├── qbittorrent/
│   └── config/             # qBittorrent 配置 / qBittorrent config
└── jackett/
    └── config/             # Jackett 配置 / Jackett config
```

---

## 🔧 下载器配置 / Downloader Setup

### qBittorrent

**中文**

qBittorrent 是本项目默认集成的下载器，启动后即可通过 `http://localhost:8082` 访问。

**English**

qBittorrent is the default downloader integrated with this project. After startup, access it at `http://localhost:8082`.

```yaml
# docker-compose.yml 中的 qBittorrent 配置片段
# qBittorrent configuration snippet in docker-compose.yml
qbittorrent:
  image: lscr.io/linuxserver/qbittorrent:latest
  container_name: qbittorrent
  ports:
    - "8082:8082"       # Web UI
    - "6881:6881"       # TCP
    - "6881:6881/udp"   # UDP
  volumes:
    - ./qbittorrent/config:/config
    - ./downloads:/downloads
  environment:
    - PUID=1000
    - PGID=1000
    - TZ=Asia/Shanghai
    - WEBUI_PORT=8082
```

> ⚠️ **安全提示**：首次登录后请立即修改默认密码 `adminadmin`！

> ⚠️ **Security Tip**: Change the default password `adminadmin` immediately after first login!

### Transmission

**中文**

你也可以使用 Transmission 替代 qBittorrent，只需修改环境变量：

**English**

You can also use Transmission instead of qBittorrent — just change the environment variables:

```yaml
# 在 MoviePilot 环境变量中配置 / Configure in MoviePilot env
environment:
  - DOWNLOADER=transmission
  - TR_HOST=http://transmission:9091
  - TR_USER=admin
  - TR_PASSWORD=your_password
```

---

## 📺 媒体服务器集成 / Media Server Integration

**中文**

MoviePilot 支持与三大主流媒体服务器集成，下载整理完成后自动通知媒体库刷新。

**English**

MoviePilot integrates with three major media servers and automatically triggers library refresh after downloading and organizing.

### Emby

```yaml
environment:
  - MEDIA_SERVER=emby
  - EMBY_HOST=http://emby:8096
  - EMBY_API_KEY=your_emby_api_key
```

### Jellyfin

```yaml
environment:
  - MEDIA_SERVER=jellyfin
  - JELLYFIN_HOST=http://jellyfin:8096
  - JELLYFIN_API_KEY=your_jellyfin_api_key
```

### Plex

```yaml
environment:
  - MEDIA_SERVER=plex
  - PLEX_HOST=http://plex:32400
  - PLEX_TOKEN=your_plex_token
```

> 💡 **提示**：获取 Plex Token 的方法是在 Plex Web 中打开任意资源，查看 URL 中的 `X-Plex-Token` 参数。

> 💡 **Tip**: To get your Plex Token, open any media in Plex Web and look for the `X-Plex-Token` parameter in the URL.

---

## 🎯 媒体刮削与元数据 / Media Scraper & Metadata

**中文**

MoviePilot 使用 TMDB (The Movie Database) 作为元数据来源，自动获取以下信息：

- 🖼️ **海报和背景图** — 电影/电视剧海报、背景墙纸
- 📝 **简介与剧情** — 剧情概要、标签、类型
- 👥 **演员与职员** — 导演、演员列表
- ⭐ **评分** — TMDB 评分、IMDb 评分
- 🏷️ **分类标签** — 类型、年代、国家

**English**

MoviePilot uses TMDB (The Movie Database) as its metadata source, automatically fetching:

- 🖼️ **Posters & Backdrops** — Movie/TV show posters and wallpapers
- 📝 **Synopsis & Plot** — Plot summaries, tags, genres
- 👥 **Cast & Crew** — Directors, actors
- ⭐ **Ratings** — TMDB ratings, IMDb ratings
- 🏷️ **Category Tags** — Genre, year, country

### 获取 TMDB API Key

| 步骤 / Step | 说明 / Description |
|---|---|
| 1️⃣ | 访问 [TMDB API 设置页](https://www.themoviedb.org/settings/api) |
| 2️⃣ | 注册或登录 TMDB 账号 |
| 3️⃣ | 点击"创建 API Key"（选择 Developer 类型即可） |
| 4️⃣ | 复制生成的 API Key |
| 5️⃣ | 填入 `.env` 文件的 `TMDB_API_KEY=` |

```bash
# .env 文件示例 / Example .env content
TMDB_API_KEY=your_tmdb_api_key_here
TMDB_API_DOMAIN=api.themoviedb.org
```

---

## 📥 自动下载规则与订阅 / Auto-Download Rules & Subscriptions

**中文**

MoviePilot 的核心功能之一是**智能订阅系统**，实现"想看的自动下、新出的自动追"。

### 订阅流程

1. **搜索影片** — 在 MoviePilot Web UI 中搜索你想看的电影或电视剧
2. **点击订阅** — 搜索结果中选择目标并点击"订阅"按钮
3. **自动监控** — 系统会定期通过索引器搜索该资源
4. **自动下载** — 发现匹配的资源后自动推送到下载器
5. **自动整理** — 下载完成后自动刮削元数据并整理到媒体库
6. **通知推送** — 通过配置的通知渠道告知你下载完成（可选）

### 下载规则

你可以通过以下维度自定义下载规则：

- **质量偏好** — 4K / 1080p / 720p
- **资源类型** — BluRay / WEB-DL / HDTV / REMUX
- **语言字幕** — 中文字幕、双语字幕
- **大小限制** — 最小/最大文件大小
- **做种要求** — 最小做种时间/分享率

---

**English**

One of MoviePilot's core features is the **intelligent subscription system** — "subscribe once, download automatically."

### Subscription Workflow

1. **Search** — Search for movies or TV shows in the MoviePilot Web UI
2. **Subscribe** — Click the "Subscribe" button on your target
3. **Auto Monitor** — The system periodically searches via your indexer
4. **Auto Download** — Matching releases are pushed to your downloader automatically
5. **Auto Organize** — After download, metadata is scraped and files are organized
6. **Notification** — Get notified when download completes (optional)

### Download Rules

You can customize download rules by:

- **Quality Preference** — 4K / 1080p / 720p
- **Source Type** — BluRay / WEB-DL / HDTV / REMUX
- **Subtitles** — Chinese subtitles, bilingual subtitles
- **Size Limits** — Minimum/maximum file sizes
- **Seeding Requirements** — Minimum seed time/ratio

---

## 🔔 通知配置 / Notification Setup

**中文**

MoviePilot 支持多种通知渠道，让您第一时间了解下载进度。

**English**

MoviePilot supports multiple notification channels to keep you informed of download progress.

### Telegram 通知 / Telegram Notifications

```yaml
environment:
  - TELEGRAM_TOKEN=123456:ABC-DEF1234ghIkl-zyx57W2v1u123ew11
  - TELEGRAM_CHAT_ID=123456789
```

| 参数 / Parameter | 说明 / Description |
|---|---|
| `TELEGRAM_TOKEN` | Bot Token，向 [@BotFather](https://t.me/BotFather) 申请 |
| `TELEGRAM_CHAT_ID` | 你的 Telegram 用户 ID，向 [@userinfobot](https://t.me/userinfobot) 查询 |

### Server酱 通知 / ServerChan Notifications

```yaml
environment:
  - SERVERCHAN_SCKEY=your_sckey_here
```

### 其他通知渠道 / Other Notification Channels

MoviePilot 还支持：
- **WeChat 微信** — 通过企业微信或 Server酱推送
- **Bark** — iOS 推送工具
- **Slack** — 团队协作推送
- **Webhook** — 自定义 HTTP 回调

---

## 🧩 索引器配置 / Indexer Setup

### Jackett

**中文**

Jackett 是一个索引聚合工具，将多个 BT 站点的搜索接口统一为标准 API。

**English**

Jackett is an index aggregator that unifies multiple BT site search APIs into a standard interface.

```yaml
environment:
  - INDEXER=jackett
  - JACKETT_HOST=http://jackett:9117
  - JACKETT_API_KEY=your_jackett_api_key
```

**Jackett 使用步骤 / Jackett Setup Steps：**

1. 访问 `http://localhost:9117`
2. 点击"Add Indexer"添加你拥有的站点（如馒头、PT 站等）
3. 添加完成后复制页面顶部的 **API Key**
4. 将 API Key 填入 `.env` 文件的 `JACKETT_API_KEY`
5. 在 MoviePilot 设置中选择 Jackett 作为索引器

### Prowlarr

**中文**

Prowlarr 是另一个强大的索引管理器，支持与 Sonarr/Radarr 生态无缝集成。

**English**

Prowlarr is another powerful indexer manager with seamless integration into the Sonarr/Radarr ecosystem.

```yaml
environment:
  - INDEXER=prowlarr
  - PROWLARR_HOST=http://prowlarr:9696
  - PROWLARR_API_KEY=your_prowlarr_api_key
```

---

## 🐳 Docker 命令参考 / Docker Commands Reference

| 命令 / Command | 说明 / Description |
|---|---|
| `docker compose up -d` | 启动所有服务 / Start all services |
| `docker compose down` | 停止所有服务 / Stop all services |
| `docker compose logs -f` | 查看实时日志 / View real-time logs |
| `docker compose restart moviepilot` | 重启 MoviePilot / Restart MoviePilot |
| `docker compose ps` | 查看服务状态 / Check service status |
| `docker compose pull` | 拉取最新镜像 / Pull latest images |
| `docker compose up -d` (after pull) | 更新到最新版 / Update to latest version |

```bash
# 更新流程 / Update workflow
docker compose pull          # 拉取最新镜像
docker compose up -d         # 重新创建容器
docker image prune           # 清理旧镜像（可选）
```

---

## ⚠️ 常见问题与排错 / Common Issues & Troubleshooting

### 1. TMDB API 连接失败 / TMDB API Connection Failed

**问题 / Issue**：刮削时无法获取元数据，日志中显示 API 错误。

**Solution / 解决**：
```
✅ 检查 .env 中 TMDB_API_KEY 是否填写正确
✅ 检查 TMDB_API_DOMAIN 是否可访问（国内用户可能需要代理）
✅ 运行 docker compose restart moviepilot 重启
```

### 2. 无法连接下载器 / Cannot Connect to Downloader

**问题 / Issue**：MoviePilot 提示无法连接 qBittorrent/Transmission。

**Solution / 解决**：
```
✅ 确认下载器容器正常运行：docker compose ps
✅ 检查 QB_HOST/TR_HOST 地址是否正确（容器内使用服务名而非 localhost）
✅ 检查用户名和密码是否匹配
✅ 确保下载器 Web UI 已启用
```

### 3. 找不到种子 / No Torrents Found

**问题 / Issue**：订阅后长时间无下载，Jackett 搜索不到资源。

**Solution / 解决**：
```
✅ 确认 Jackett 中已添加站点且站点可访问
✅ 检查 JACKETT_API_KEY 是否正确
✅ 确认种子资源确实存在（手动在 Jackett 中搜索验证）
✅ 部分 PT 站需要配置 Cookie 或 Passkey
```

### 4. 权限问题 / Permission Issues

**问题 / Issue**：下载或整理时出现 Permission denied 错误。

**Solution / 解决**：
```bash
# 确保 PUID/PGID 与宿主机的用户 ID 匹配
# Make sure PUID/PGID match your host user ID
id  # 查看当前用户 UID/GID
# 然后在 .env 中设置：
PUID=1000
PGID=1000

# 修复目录权限 / Fix directory permissions
sudo chown -R 1000:1000 ./media ./downloads ./config
```

### 5. 磁盘空间不足 / Disk Space Full

**问题 / Issue**：下载空间不足导致任务失败。

**Solution / 解决**：
```
✅ 在下载器中设置合理的磁盘空间限制
✅ 定期清理不需要的种子和文件
✅ 设置做种时间限制，自动删除旧种子
✅ 考虑将 media 目录映射到更大的存储空间（如 NAS）
```

### 6. 容器无法启动 / Container Fails to Start

**问题 / Issue**：运行 `docker compose up -d` 后容器立即退出。

**Solution / 解决**：
```bash
# 查看具体错误日志 / Check specific error logs
docker compose logs moviepilot

# 常见的端口冲突 / Common port conflicts
# 检查端口是否被占用 / Check if ports are already in use
sudo lsof -i :3000
sudo lsof -i :8082
```

---

## 🛠️ 小技巧 / Tips & Tricks

| 中文 | English |
|---|---|
| 🔄 **定时整理**：MoviePilot 会自动按规则整理媒体文件到 `./media/` | 🔄 **Scheduled Organizing**: MoviePilot automatically organizes media files into `./media/` |
| 📁 **目录监控**：放入 `./downloads/` 的种子会自动被识别 | 📁 **Directory Watch**: Torrents placed in `./downloads/` are auto-detected |
| 📺 **NAS 集成**：将 `./media/` 映射到 NAS 共享目录，方便多设备播放 | 📺 **NAS Integration**: Map `./media/` to a NAS share for multi-device playback |
| 🔍 **手动搜索**：在 Web UI 中可手动搜索并触发下载 | 🔍 **Manual Search**: Search and trigger downloads directly from the Web UI |
| 📊 **日志查看**：`docker compose logs -f moviepilot` 实时跟踪 | 📊 **Live Logs**: `docker compose logs -f moviepilot` to track activity |
| 🏷️ **自定义分类**：可在配置中自定义电影/电视剧的分类规则 | 🏷️ **Custom Categories**: Configure custom categorization rules for your library |

### 推荐扩展 / Recommended Extensions

- 🌟 **Prowlarr** — Jackett 的现代替代品，与 Radarr/Sonarr 生态更好兼容
- 🌟 **FlareSolverr** — 解决部分站点需要 Cloudflare 验证的问题
- 🌟 **Bazarr** — 自动下载字幕的利器

---

## ☕ 支持这个项目 / Support This Project

如果你觉得这个教程对你有帮助，欢迎请我喝杯咖啡 ☕  
你的支持是我持续更新的最大动力！非常感谢！🙏

If you find this tutorial helpful, feel free to buy me a coffee ☕  
Your support is my biggest motivation to keep improving! Thank you so much! 🙏

**USDT (TRC20)**
```
TVbQerV1SF4MXB1JCcAzQxarewHwEPYTKm
```

---

> **有问题或建议？** 欢迎联系: **caizhenwei33@gmail.com**  
> **Questions or suggestions?** Feel free to reach out: **caizhenwei33@gmail.com**
