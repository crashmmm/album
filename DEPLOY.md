# 部署与发布配置 · Deployment

## 📍 当前状态（2026-07-08）

### 仓库
- **GitHub**: https://github.com/crashmmm/album
- **主分支**: `main`（每次 push 自动触发 GitHub Pages 部署）
- **本地路径**: `E:\desktop\program\平板电子相册\pad-album\`

### 部署链接
| 平台 | 链接 | 状态 | 用途 |
|---|---|---|---|
| **GitHub Pages** | `https://crashmmm.github.io/album/` | ✅ 在线 | **主推**（朋友圈分享用） |
| Cloudflare Pages | `https://album-5w4.pages.dev` | ✅ 在线 | 备份（**已弃用** —— 微信风控） |
| 本地 file:// | `file:///E:/desktop/program/平板电子相册/pad-album/index.html` | ⚠️ 部分功能 | 开发调试（IndexedDB 持久） |

### 朋友圈分享
- **主推链接**：`https://crashmmm.github.io/album/`
- **备用**：[url.cn](https://url.cn) 短链中转（如果 github.io 偶发被微信风控时）
- **缩略图**：GitHub 自动抓 `share-preview.png`（朋友圈链接预览用）

---

## 📁 文件结构

```
pad-album/
├── index.html              # 主程序（~110 KB，单文件零依赖）
├── manifest.json           # PWA 配置（display: fullscreen, orientation: any）
├── mc-brand.svg            # mc 品牌 logo（紫渐变胶囊 + 文字）
├── share-preview.svg       # 社交分享预览图（矢量源，可改文字重新生成 PNG）
├── share-preview.png       # 社交分享预览图（1200×630 PNG，68 KB，微信/朋友圈/Twitter 通用）
├── _headers                # Cloudflare Pages 缓存策略（已弃用 Pages 后无作用，保留可复用）
├── README.md               # 项目介绍
└── DEPLOY.md               # 本文件 · 部署与发布配置
```

### 关键文件说明
- **`index.html` 头部**：含完整 og:\* / twitter:\* / apple-touch-icon meta（社交分享优化）
- **`index.html` 底部**：含"关于 · 第三方开源许可"区（Feather Icons MIT + 本项目 MIT 完整文本）
- **`_headers`**：Cloudflare Pages 缓存策略，如果以后再迁 Pages 可以直接用

---

## 🎯 关键技术决策

| 维度 | 选择 | 理由 |
|---|---|---|
| 架构 | 单文件 HTML | 零依赖，朋友圈分享方便，部署简单 |
| 图片存储 | 浏览器本地（File System Access）| 隐私优先，无后端 |
| 跨平台 | 桌面 Chrome / Edge / Android / HarmonyOS / **不支持 iOS Safari** | File System Access API 不支持 iOS |
| 全屏方案 | PWA `display: fullscreen` + 方向锁 | 移动端添加到主屏幕后零 UI 全屏 |
| 部署 | GitHub Pages | 微信友好（H5 用户场景），零成本 |
| 许可 | MIT | 允许自由使用 / 修改 / 商用 |
| 第三方 | Feather Icons（MIT）—— 21 个 SVG 图标 | 完整保留原路径 + 完整 MIT 文本署名 |

---

## 📝 Commit 历史（最近 5 次）

| Hash | 说明 |
|---|---|
| `2fc4f4b` | docs: og URL 切回 GitHub Pages（朋友圈主推链接）|
| `7191383` | feat: og URL 切到 Cloudflare Pages + 微信内引导浮窗 + 缓存策略 _headers |
| `3199a1b` | feat: 微信/社交分享预览（og:title/description/image + twitter:card + 1200×630 PNG）|
| `77954cd` | docs: GitHub Desktop 同步 + LF 归一化 |
| `0872657` | docs: Add files via upload |

---

## 🛠 未来扩展规划

### 微信小程序（计划中）
- **仓库命名建议**：`crashmmm/album-miniprogram`（独立仓库）
- **目录结构**（占位）：
  ```
  album-miniprogram/
  ├── miniprogram/
  │   ├── app.js
  │   ├── app.json
  │   ├── app.wxss
  │   ├── project.config.json
  │   ├── sitemap.json
  │   └── pages/
  │       └── index/   # web-view 套壳：<web-view src="https://crashmmm.github.io/album/"/>
  └── README.md
  ```
- **业务域名白名单**（mp.weixin.qq.com → 开发管理 → 开发设置 → 业务域名）：
  - 添加 `crashmmm.github.io`
  - 下载校验文件 → 放到 `crashmmm/album` 仓库根目录 → commit & push
- **小程序类目**建议：工具 → 图片处理（个人主体）/ 工具 → 效率（企业主体）

### WebView 套壳 vs 原生重写
| 方案 | 适合场景 |
|---|---|
| **WebView 套壳**（推荐）| 想快速上线，H5 体感可接受，IndexedDB 偶尔清空可接受 |
| **原生重写** | 想正经做产品，类目齐全，需要稳定持久化 |

### 未来如果做其他工具类项目
建议**新建独立仓库**（每个项目一个 `crashmmm/<project-name>`），方便管理：
- `crashmmm/<tool-1>`
- `crashmmm/<tool-2>`
- `crashmmm/album`（当前）
- `crashmmm/album-miniprogram`（未来）

---

## 🔧 故障排查

### 朋友圈分享没显示缩略图
1. 微信爬虫需要几分钟抓 og:* meta → 等 5-10 分钟
2. 用 [opengraph.xyz](https://www.opengraph.xyz/) 验证 og meta 是否被正确抓取
3. 微信会缓存缩略图 → 改文件名（如 `share-preview-v2.png`）强制刷新

### 国内访问 github.io 慢
- 正常现象（3-10s 加载），可以用 url.cn 短链中转
- 朋友圈体验：能打开就行，3 秒加载不致命

### Git push 超时
- 国内连 GitHub 抽风是常态
- **用 GitHub Desktop 推**（走 HTTPS over HTTP/2，更稳）

---

## 📊 朋友圈分享实测

| 平台 | 测试结果 |
|---|---|
| 桌面 Chrome | ✅ 1s 打开 |
| iOS Safari | ✅ 1-2s 打开 |
| Android Chrome | ⚠️ 3-5s 打开 |
| 微信 → 朋友 | ✅ 正常 |
| 微信 → 朋友圈 | ✅ 正常（缩略图显示） |

---

**更新日期**：2026-07-08 · **最后部署版本**：`2fc4f4b`
