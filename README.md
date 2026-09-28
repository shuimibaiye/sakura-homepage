# 橘子皮の异世小屋

一个单页式的个人异世界主题主页 —— 角色设定、综合图鉴、技能与武器展示，配天气挂件和音乐播放器。

> 纯静态站点，无需构建步骤：克隆下来直接双击 `index.html` 就能跑。

---

## ✨ 功能一览

| 模块 | 说明 |
| --- | --- |
| 🎭 角色设定 | 人设条目展示，支持在线编辑 |
| 📚 综合图鉴 | 可增删改的图鉴系统，数据存于 `localStorage` |
| ⚔️ 技能 / 武器 | 技能与武器卡片，含专属立绘 |
| 🌤️ 天气挂件 | 通过 `open-meteo` 拉取实时天气 |
| 📍 访客定位 | 依次回退 `ip.sb` / `ipapi.is` / `ipwho.is` 获取地区 |
| 🎵 音乐播放器 | 本地背景音乐循环播放 |
| 🖼️ 动态背景 | 多张异世界插画轮播 |

## 📁 目录结构

```
Sakura/
├── index.html              # 站点全部内容（HTML + CSS + JS 单文件）
├── assets/
│   ├── Background/         # 背景插画
│   ├── Profile/            # 头像
│   ├── Weapon/             # 武器立绘
│   └── vendor/             # Tailwind CSS（本地内置，离线可用）
└── Music/                  # 背景音乐（未纳入版本库，见下）
```

## 🚀 本地运行

```bash
git clone https://github.com/<你的用户名>/sakura-homepage.git
cd sakura-homepage
```

直接双击 `index.html`，或起个本地服务（推荐，避免部分浏览器的本地文件策略限制）：

```bash
python -m http.server 8000
# 然后访问 http://localhost:8000
```

## 🌐 在线访问

已启用 GitHub Pages：

```
https://<你的用户名>.github.io/sakura-homepage/
```

## 🎵 添加音乐

`Music/` 目录里的 3 个 MP3 总约 294 MB，其中两个单文件超过 GitHub 的 100 MB 硬上限，
因此**默认未纳入版本库**（保留在你本地磁盘上）。想一起传的话有三种方案：

**方案 A —— Git LFS（保留原文件）**

```bash
git lfs install
git lfs track "Music/*.mp3"
git add .gitattributes
# 编辑 .gitignore，删掉 "Music/" 那一行
git add Music/
git commit -m "chore: 通过 Git LFS 纳入背景音乐"
git push
```

> 免费额度为 1 GB 存储 / 1 GB 月流量，294 MB 装得下，但流量消耗较快。
> 另外 GitHub Pages 不提供 LFS 文件，线上站点仍听不到音乐。

**方案 B —— 压缩码率**

```bash
# 需要 ffmpeg
for f in Music/*.mp3; do ffmpeg -i "$f" -b:a 128k "Music/compressed/$(basename "$f")"; done
```

128 kbps 后总体积约 90 MB，可正常直传。

**方案 C —— 外链托管**

把音乐放到支持直链的网盘或对象存储，改 `index.html` 里 `<audio>` 的 `src`。

## 📝 说明

- 页面数据（图鉴、角色条目等）保存在浏览器 `localStorage`，换设备不会同步。
- `assets/Weapon` 与 `assets/Background` 中的插画版权归原作者所有，仅供个人展示，
  请勿用于商业用途。
- 站点依赖 `cdn.tailwindcss.com`、`cdn.jsdelivr.net` 与公开 IP / 天气 API，
  离线环境下样式与天气挂件会失效。

---

**保留所有权利** · 个人作品，转载请注明出处。
