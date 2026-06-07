# MoviePilot V2 使用说明 🎬

MoviePilot V2 是一个自动化观影助手，帮你完成影片搜索、订阅、下载、刮削、整理的一条龙服务。

---

## 系统架构

```
            ┌─────────────┐
            │   Jackett   │  ← 索引器：搜索各站点资源
            └──────┬──────┘
                   │
            ┌──────▼──────┐
            │  MoviePilot │  ← 主程序：自动订阅、刮削、整理
            └──────┬──────┘
                   │
            ┌──────▼──────┐
            │ qBittorrent │  ← 下载器
            └─────────────┘
```

## 首次使用

### 1. 获取 TMDB API Key（必填）

MoviePilot 需要 TMDB 来获取影片的封面、简介、演员等元数据。

1. 打开 https://www.themoviedb.org/settings/api
2. 注册/登录 TMDB 账号
3. 申请 API Key（选 Developer 即可）
4. 把 Key 填入 `.env` 文件中的 `TMDB_API_KEY`

### 2. 配置索引器（Jackett）

Jackett 用于搜索各资源站点。

1. 启动后访问 http://localhost:9117
2. 添加你有的站点（如 馒头、PT 站等）
3. 复制 Jackett 的 API Key，填入 `.env` 的 `JACKETT_API_KEY`
4. 在 MoviePilot 设置中配置索引器为 Jackett

### 3. 配置下载器

访问 http://localhost:8082
- 默认账号: `admin`
- 默认密码: `adminadmin`
- 建议修改密码并填入 `.env` 的 `QB_PASSWORD`

## 目录说明

| 目录 | 用途 |
|------|------|
| `./media/` | 整理后的影片存放目录（电影 / 电视剧按目录分类） |
| `./downloads/` | 下载中的临时文件 |
| `./config/` | MoviePilot 配置文件 |
| `./qbittorrent/config/` | qBittorrent 配置 |
| `./jackett/config/` | Jackett 配置 |

**建议**: 如果使用 NAS，把 `./media/` 映射到 NAS 共享目录，方便其他设备播放。

## 常用命令

```bash
# 启动所有服务
docker compose up -d

# 查看日志
docker compose logs -f

# 重启某个服务（比如改配置后）
docker compose restart moviepilot

# 更新到最新版
docker compose pull
docker compose up -d

# 停止所有服务
docker compose down
```

## 端口一览

| 服务 | 端口 | 说明 |
|------|------|------|
| MoviePilot | 3000 | Web 管理界面 |
| qBittorrent | 8082 | 下载器管理界面 |
| qBittorrent | 6881 | BT 下载端口（TCP+UDP） |
| Jackett | 9117 | 索引器管理界面 |

## 小技巧

- **订阅功能**：在 MoviePilot 搜索影片后点击订阅，有新资源会自动下载
- **目录监控**：放到 `./downloads/` 里的种子会自动被识别
- **通知推送**：配置 Telegram 或 Server酱，下载完成主动提醒
- **定时整理**：MoviePilot 会自动按规则整理媒体文件到 `./media/`

---

> 有问题或建议请联系: **caizhenwei33@gmail.com**
