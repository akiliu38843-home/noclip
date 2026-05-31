# NOCLIP · 凌晨档案 — 前端外包简报

> 给设计师/前端工程师的项目上下文. 读完这一篇就够动手了.

---

## 1. 一句话讲产品

**让访客在 12 种 1995-2010 的老电脑/老浏览器壳子里, 随机刷到 100+ 个真实老网页, 体验"互联网考古 + 后室"那种迷路感.**

线上版: https://noclip.vercel.app

---

## 2. 它要怎样的"感觉"

借了 **The Backrooms (后室)** 的设定:
- 你"走错门 noclip 进了一个错位的网络空间"
- 每扇门后是 1 个老网页, 套着 1 个老操作系统/老浏览器外壳
- 不能停 (10 秒不动屏幕开始变红, 18 秒强制开门)
- 隐藏出口装得像古董控件 (邮箱 GIF / 关机按钮 / RSS / TRANSMIT 按钮)

**像在凌晨 3 点的网吧, 串了号上了别人的电脑, 翻到 1998 年的网页 — 但没人在管你**.

不是 "复古好看", 是 "**陌生 + 怀旧 + 略微不安**". Vibe 关键词:
- 千禧年虫 / 拨号声 / 雪花屏 / 像素文字
- 死链接的味道 / 网管半夜没关电脑 / 中文 BBS 凌晨灌水
- **不能太精致** — 那是宜家. 要 "网吧机柜上的灰" 那种.

---

## 3. 现在做到哪一步

### 3.1 主产品 `index.html` (1300+ 行, 单文件)

12 种外壳已实现:
| # | 外壳 | 来源 | 状态 |
|---|---|---|---|
| 1 | Windows 98 窗口 | 98.css (MIT) | ✅ |
| 2 | Windows XP | XP.css (MIT) | ✅ |
| 3 | Windows 7 | 7.css (MIT) | ✅ |
| 4 | Mac System 6 | system.css (MIT) | ✅ |
| 5 | DOS Turbo Vision | TuiCss (MIT) | ✅ |
| 6 | NES.css 8-bit | NES.css (MIT) | ✅ |
| 7 | Unix 终端 | terminal.css (MIT) | ✅ |
| 8 | Netscape Navigator 4 | 自写 CSS | ⚠️ 美术粗糙 |
| 9 | Internet Explorer 6 | 自写 CSS | ⚠️ 美术粗糙 |
| 10 | WAP 翻盖手机屏 | 自写 CSS | ⚠️ 美术粗糙 |
| 11 | MSN Messenger | 自写 CSS | ⚠️ 美术粗糙 |
| 12 | BBS ANSI 终端 | 自写 CSS | ⚠️ 美术粗糙 |

100+ 个老网页 URL (来源: The Useless Web, Wiby, Cameron's World, JODI, textfiles.com, Project Gutenberg 等).

机制:
- **拟态门**: 关闭按钮就是开下扇门 (不是浮窗 ×)
- **故障转场**: 0.5-2s 黑屏 + Web Audio 合成的拨号噪音
- **走廊转场**: 10% 概率进 CSS 3D 黄色走廊 (向后室 Level 0 致敬)
- **规则随机**: 邻接图 + 深度梯度 + 集群粘着 (不是均匀骰子)
- **5 种房型**: 档案 / 玩具 / 幻境 / 杂物 / 休息 — 顶部时间线显示最近 12 扇
- **里程碑**: 第 7/17/47/100 扇有特殊事件 (47 = Level Fun 强制档案房)
- **安全兜底**: URL 试探 (fetch 探测), Loading 6s 出 retry, ESC 全局换门
- 状态存浏览器 localStorage

### 3.2 大房间 `large-rooms/*.html`

10% 概率走进"大房间" — 一整个主题站, 不是单页. 已建 2 间:

| 文件 | 主题 | 来源真实数据 |
|---|---|---|
| `geocities-heartland.html` | 1997 GeoCities 邻居街区 (暖黄/comic sans) | 30 个 Wayback CDX 验证 >4KB 的真实 GeoCities 邻里页 |
| `geocities-area51.html` | 1997 Area51 X档案/UFO 阴谋论 dossier (黑底/绿 CRT) | 30 个 Wayback 验证的 X-Files/UFO/MIB/Hynek 学派 真实老页面 |

两间都有"**入门仪式**":
- Heartland: 拨号 modem 动画 3.5 秒 + 拨号声合成
- Area51: 终端密语口令 prompt (输 4+ 字符放行, 几个彩蛋词: ROSWELL / MULDER / MAJESTIC12)

### 3.3 决策页 `decisions/next-room-pick.html`

之前给用户挑下扇大房间的 HTML 决策器. 不是产品的一部分, 是工作流的一部分. 可不动.

---

## 4. 现在的痛点 / 想找 claude design 帮什么

### 4.1 美术 (优先级最高)

**5 个自写 CSS 的外壳** (Netscape 4 / IE6 / WAP / MSN / BBS) 视觉粗糙. 不是没还原成功, 是"画得太干净", 缺**灰尘感 + 像素失真 + 死链浪漫**. 希望:
- Netscape 4 → 真还原 1996 年的 chrome (灰金属按钮 + Cosmo 字体 + 进度条爬墙)
- IE6 → Win XP 蓝色顶栏 + 一堆免费 toolbar 横条 (Yahoo / Google / Ask)
- WAP → 翻盖屏幕 96×64 px 黑绿
- MSN → 真 Messenger 2003 配色 + 卡通 emoticon
- BBS ANSI → 真 ANSI art 字符画当背景, 不是绿字了事

7 个开源外壳本身 OK, 但**外壳里的小细节**也可以加味: 鼠标光标变手指、CSS 字体抗锯齿关掉模拟低分辨率、屏幕反光叠加.

### 4.2 转场动画

现在的 "黑屏 + 拨号声" 0.5-2 秒太单调. 想要:
- 雪花屏 / Hi-8 录像带卡带 / VHS 跟踪条
- 拟态 BIOS 启动 (有时换出鸡蛋扇)
- CRT 关机收缩成一条线再黑屏

### 4.3 大房间扩展 (用户已挑下一批)

待做大房间清单 (按用户优先级排):
1. **GeoCities Area51 续集** (本周做, 框架已有)
2. **IRC 频道实时聊天回放** — mIRC UI + 真 chatlog 打字回放 (用 irclogs.ubuntu.com 公开归档)
3. **2007 博客圈 RSS 长读** — NetNewsWire 风 RSS reader + 12 个 Wayback 博客快照

未来还想做: BBS 拨号站 / MySpace 2005 国外乐队页 / DAO 死提案广场.

### 4.4 不要触碰的硬约束

- **不要引入 build** — 必须保持单文件 HTML, 无 npm install, 无 webpack
- **不要换框架** — 不要 React/Vue/Svelte, 纯 vanilla JS
- **不要换 host** — 部署在 Vercel 静态
- **iframe 嵌 Wayback `if_` 模式 URL 必须保留** — 这是内容支柱
- **后室机制不能丢**: 拟态门 / 不能停 / ESC 全局逃 / 规则随机 / 里程碑
- **3 个用户硬性偏好**:
  - BBS 选国外站点 (不要中文 BBS)
  - MySpace 不要周杰伦 / 不要华语乐队 (用 MCR / FOB 等 emo punk)
  - GeoCities 可以多做几个不同主题 (邻居 / 阴谋 / 热带 / 太空)

---

## 5. 技术栈

- **HTML/CSS/JS**: 纯原生, 无框架, 单文件 (`index.html` ~ 60KB)
- **状态**: 浏览器 localStorage (访问历史, 走过的门, 计数器)
- **iframe**: 双层嵌套 (外壳 `srcdoc` + 内容 URL via `if_` 模式 Wayback)
- **音频**: Web Audio API 实时合成 (无音频文件)
- **3D**: 纯 CSS `perspective` (走廊转场)
- **依赖**: 7 个开源 CSS 框架通过 CDN (`unpkg`/`jsdelivr`) 引入, 不打包
- **部署**: Vercel 静态, GitHub source: github.com/akiliu38843-home/noclip

---

## 6. 文件结构

```
noclip/
├── index.html              # 主产品 (61KB, 1309 行)
├── large-rooms/
│   ├── geocities-heartland.html   # Web1 大房间 1: 邻居街区
│   └── geocities-area51.html      # Web1 大房间 2: 阴谋论档案
├── decisions/
│   └── next-room-pick.html        # 工作流决策器 (不是产品)
├── README.md
└── HANDOFF.md              # ← 你正在读
```

---

## 7. 沟通方式 (重要)

产品负责人是**非技术背景**. 报进度时:
- 用大白话 + 生活化类比
- 不要堆术语 (出现的术语立刻翻译)
- 不要扔 stacktrace 或长 JSON
- 报数字前先讲方法 (例: "我扫了 Wayback 5000 个快照, 取内容大小 >5KB 的 30 个", 不要扔个"30 个" 就走)
- 失败也讲方法 (诚实失败 > 假装通过)

时间偏好: 周一-五 9:30-19:00 是活跃时间. 那之外别后台搞动作.

---

## 8. 法律 / 内容边界

- 全部用户内容来自 Wayback Machine 公开归档 (1996-2010)
- 不嵌 paywall 网站 / Google / 现役商业站
- 不抓任何用户数据 (无后端, 无登录)
- MIT License
