# 平板电子相册 · mc定制

一个**纯前端的单文件 HTML 电子相册**。把闲置的手机、平板、显示器改造成一个"会呼吸的电子相框"。

![intro](mc-brand.svg)

## ✨ 核心特性

- **单文件 HTML**：整个程序就是一个 `index.html`，无需构建、无后端、无依赖
- **完全本地运行**：不联网，不上传任何图片，所有文件通过浏览器原生文件系统 API 读取
- **多文件夹 / 嵌套扫描**：支持相册文件夹整体加入，自动递归扫描子目录
- **多平台**：Android / HarmonyOS / Windows（Chrome / Edge 内核）
- **触屏友好**：UI 自动淡出不打扰，dock 按钮放大适合手指点

## 🎬 播放

- 顺序 / 随机 / 单文件夹循环
- 切换时间：3s / 5s / 10s / 30s / 自定义
- 转场动画：淡入 / 滑动 / 缩放 / Ken Burns / **瞬切**
- 适配模式：Contain（留边）/ Cover（铺满）/ Actual（实际像素）
- 屏幕方向：自动 / 锁定横屏 / 锁定竖屏

## 🖼️ 特色功能

- 🕶 **屏保模式**：可设 1~120 分钟无操作自动黑屏，进屏保显示大时钟（时分秒 + 日期 + 星期）
- 🎨 **视觉沉浸**：进入播放模式自动进入全屏视觉（背景 vignette + 图片"相框"阴影 + dock 自动隐藏）
- 🔍 **缩略图栏**：底部一行缩略图，点击跳转
- 🔄 **进度条**：图片切换进度可视化
- ⚙️ **完整快捷键**：`Space` 暂停 · `← →` 切换 · `R` 旋转 · `F` 全屏 · `H` 隐藏 UI · `S` 设置 · `A` 关于

## 📱 支持的图片格式

JPG / JPEG / PNG / GIF / WebP / BMP / AVIF / SVG / HEIC（取决于浏览器原生支持）

## 🚀 部署 / 使用

### 最简单（直接打开）

1. 下载 `index.html` 到本地
2. 用 Chrome / Edge 双击打开

### GitHub Pages（推荐：手机访问）

1. 把本仓库推送到 GitHub
2. repo → **Settings** → **Pages**
3. Source 选 `main` / `(root)`
4. 等 1-2 分钟，会生成 `https://<用户名>.github.io/album/` 这种链接
5. 在手机 Chrome / 浏览器打开

部署到 HTTPS 后可以享受：
- ✅ `showDirectoryPicker` 完整功能（能选整个相册文件夹）
- ✅ 文件夹权限**自动持久化**（下次打开不需要重新授权）
- ✅ 完整的 fullscreen API（真·全屏，隐藏手机地址栏）

### 本地局域网测试

如果只是想在手机上测试但不想公开仓库，可以用 `python -m http.server` 或 `npx http-server` 在 PC 起个本地服务器，然后用 `http://<电脑局域网IP>:8000` 在手机浏览器访问。

## 📂 文件说明

```
.
├── index.html      # 主程序（97 KB · 单文件）
├── mc-brand.svg    # mc 定制品牌 SVG（紫渐变胶囊 logo）
└── README.md       # 本文件
```

## 🔧 技术细节

- **目标平台**：Android / HarmonyOS / Windows；浏览器要求：基于 Chromium 86+
- **关键 API**：
  - File System Access API（`showDirectoryPicker`）— Chrome / Edge 桌面端首选
  - `<input webkitdirectory>` — 旧浏览器 / 部分移动端
  - `<input type=file multiple>` — 终极兜底（多选图片）
  - Fullscreen API — 桌面端可用
  - IndexedDB — 持久化文件夹授权
  - localStorage — 持久化设置

- **零第三方库**：完全用浏览器原生能力实现
- **图标**：内联 Feather Icons（MIT License）

## 📜 第三方开源许可

| 项目 | 说明 | 许可 |
|---|---|---|
| 浏览器原生 API | File System Access · Fullscreen · IndexedDB | 平台内置 |
| 第三方 JS 库 | **无** —— 单文件零依赖 | — |
| 图标 | Feather Icons（MIT）— 内联 SVG | MIT |

## ⚠️ 已知限制

- **iOS Safari 不在支持列表**（早期反馈聚焦在 Android / HarmonyOS / Windows）
- **微信内置浏览器**不支持文件夹选择 API（仅可多选图片）；如需完整功能请用 Chrome / 系统浏览器打开 GitHub Pages 链接
- **需要在本地打开 HEIC 图片**：浏览器原生是否支持取决于版本，Chromium 90+ 已能解码部分 HEIC

## 🤝 反馈

打开程序 → 右下角 / 屏幕底部"关于 / 许可"区有完整功能说明和快捷键。

---

**© 2026 mc定制 · 设计开发**
