# NOCLIP · 凌晨档案 — 前端外包简报

> 给设计师 / 前端工程师的项目上下文. 读完这一篇就够动手了.
> 任务焦点见 **§ 4** — **最外面的"控制台框架"**, 不是里面的老电脑壳子.

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

**12 种老电脑/浏览器外壳已实现 (这部分别动)**:
| # | 外壳 | 来源 |
|---|---|---|
| 1 | Windows 98 窗口 | 98.css (MIT) |
| 2 | Windows XP | XP.css (MIT) |
| 3 | Windows 7 | 7.css (MIT) |
| 4 | Mac System 6 | system.css (MIT) |
| 5 | DOS Turbo Vision | TuiCss (MIT) |
| 6 | NES.css 8-bit | NES.css (MIT) |
| 7 | Unix 终端 | terminal.css (MIT) |
| 8 | Netscape Navigator 4 | 自写 CSS |
| 9 | Internet Explorer 6 | 自写 CSS |
| 10 | WAP 翻盖手机屏 | 自写 CSS |
| 11 | MSN Messenger | 自写 CSS |
| 12 | BBS ANSI 终端 | 自写 CSS |

100+ 个老网页 URL (来源: The Useless Web, Wiby, Cameron's World, JODI, textfiles.com, Project Gutenberg).

机制 (这些行为别改, 视觉表现可改):
- **拟态门**: 关闭按钮就是开下扇门 (不是浮窗 ×)
- **故障转场**: 0.5-2s 黑屏 + Web Audio 合成的拨号噪音
- **走廊转场**: 10% 概率进 CSS 3D 黄色走廊
- **规则随机**: 邻接图 + 深度梯度 + 集群粘着
- **5 种房型**: 档案 / 玩具 / 幻境 / 杂物 / 休息
- **里程碑**: 第 7/17/47/100 扇有特殊事件
- **不动 10s 屏幕变红, 18s 强制开门**
- 状态存浏览器 localStorage

### 3.2 大房间 `large-rooms/*.html` (4 间, 这部分也别动)

10% 概率进"大房间" — 一整个主题站, 不是单页:

| 文件 | 主题 | 时代 |
|---|---|---|
| `geocities-heartland.html` | 1997 GeoCities 邻居街区 (暖黄/comic sans) | Web 1 |
| `geocities-area51.html` | 1997 Area51 X档案/UFO 阴谋论档案 (黑底/绿 CRT) | Web 1 |
| `irc-channel.html` | mIRC 6.3 风 + 12 段真 IRC chatlog 打字回放 | Web 1 |
| `blog-2007.html` | NetNewsWire 2007 风 + 12 篇 2007 经典英文博客 | Web 2 |

各自有进门仪式 (拨号 / 密语口令 / IRC 连接 / RSS 订阅).

### 3.3 决策页 `decisions/next-room-pick.html`

工作流决策器, 不是产品. 别动.

---

## 4. ⭐️ 真正要重做的东西: **最外面的控制台框架**

参考截图: `current-frame-screenshot.png` (打包在 zip 里).

### 4.1 现在长啥样

整个 `index.html` 的**最外层 chrome** — 现在是黑底 + 灰绿 + 琥珀色等宽字, 像 1980 年代终端调试器:

- **顶部 4 列状态条**: 穿过几扇门 / 当前类型 / 当前外壳 / URL+深度档
- **集群指示行**: "集群: Windows (粘 2)"
- **时间线条**: 最近 12 扇门, 用颜色块标房型 (玩/幻/杂/玩/玩/幻/玩/玩/息/杂/幻)
- **正中间巨大画布**: 显示 "点任何一扇门" — 实际开门后这里换成"外壳 iframe"
- **右侧栏**: 外壳清单 / URL 池来源 / 各版本机制变更 (v1/v2/v3/v4) · 像 changelog 弹窗

这个外层就是**"操作员视角的控制台"** — 玩家是在凌晨 3 点的网管位上, 看着主屏幕里别人在乱串老网页, 旁边一堆调试信息.

### 4.2 它需要承担的功能 (重做时别丢)

| 区域 | 当前显示 | 必保留信息 |
|---|---|---|
| 顶部状态 | 门数 / 房型 / 外壳名 / 深度 / 提示文案 | 这 5 项 |
| 集群指示 | "Windows (粘 2)" 说明走 2 扇 Win 类壳子 | 集群信息 |
| 时间线 | 12 块彩色 chip | 最近 12 扇 + 当前位置 |
| 正中画布 | 大块黑屏待开门 | 这是放外壳 iframe 的地方 |
| 右侧栏 | 12 外壳清单 / URL 池 / 机制 changelog | **可以删** (把 changelog 拿掉, 玩家不需要看) |
| 隐藏出口 | 角落邮箱 / 关机 / TRANSMIT | ESC + 主路由换门要继续生效 |

### 4.3 现在的痛点

1. **太像 dev console** — 用户不是工程师, 不需要看 "粘 2" "深度档 1 (混合)" 这种术语
2. **右侧 changelog 是给我自己看的** — 上线版本应该砍掉
3. **正中央太空旷** — 没开门时占了 70% 屏, 像没加载完的样子
4. **配色割裂** — 控制台是 80 年代终端, 但里面跳出来的可能是 Win XP 蓝色, 跳得太硬

### 4.4 想要的方向 (不限死, 给你参考)

几个画风都行, 你选**最贴 §2 vibe** 的:

- **A. 旧监控录像室**: 整个外层像保安亭, 主屏是 CRT 电视墙的一格, 其他格放过去 11 扇门的截图缩略图. 时间线就是底部的 timecode 条. 周围有"REC ●" "TRACKING" 之类 VHS 标签
- **B. 老网管控制台**: 像 ICQ / Yahoo Messenger 那种伴随窗口集合 — 主窗口是开门画面, 浮动的 sticky note 写着深度档 / 房型, 任务栏底显示门数. **不要 macOS 风**
- **C. CGI/Perl 计数器壁纸时代**: 整张页面就是 1999 年个人主页风的 frameset, 中间 frame 给 iframe, 左侧 frame 是 webring 链接, 顶部 frame 是访客计数. 但这跟内层 GeoCities 大房间太像, 容易撞
- **D. 你自己提**

**统一约束**:
- 不要 macOS 现代风 / 不要 Material / 不要 iOS 玻璃
- 不要彩色渐变 hero — 那是 2020 年 SaaS
- 不要 emoji 大头 (除非反讽用)
- 字体: 可以用 Comic Sans / Times / 等宽 (但**别用 Inter / SF Pro / Roboto**)
- 颜色: 受限调色板 (不要 24-bit 渐变), 比如 Windows 16 色 / NES 64 色 / CGA 4 色

### 4.5 一定不能丢的硬约束

- **不要引入 build** — 保持单文件 HTML, 无 npm install / webpack
- **不要换框架** — 纯 vanilla JS, 不要 React/Vue/Svelte
- **不要换 host** — 部署在 Vercel 静态
- **iframe 嵌 Wayback `if_` 模式 URL 必须保留** — 内容支柱
- **后室机制不能丢**: 拟态门 / 不动屏幕变红 / ESC 全局逃 / 规则随机 / 里程碑
- **状态保留**: 当前外壳 / 深度 / 集群 / 时间线 / 门计数, 都已在 JS 里, 重做时**只换显示层**, 不要重写状态机
- **音频继续 Web Audio 合成**, 不要塞 mp3
- **响应式但只到 720px**: 别管手机, 这是桌面产品

---

## 5. 技术栈

- **HTML/CSS/JS**: 纯原生, 无框架, 单文件 (`index.html` ~ 60KB)
- **状态**: 浏览器 localStorage (访问历史, 走过的门, 计数器)
- **iframe**: 双层嵌套 (外壳 `srcdoc` + 内容 URL via Wayback `if_` 模式)
- **音频**: Web Audio API 实时合成 (无音频文件)
- **3D**: 纯 CSS `perspective` (走廊转场)
- **依赖**: 7 个开源 CSS 框架通过 CDN (`unpkg`/`jsdelivr`) 引入
- **部署**: Vercel 静态, GitHub: github.com/akiliu38843-home/noclip

---

## 6. 文件结构

```
noclip/
├── index.html              # 主产品 (60KB, 1300+ 行)  ← 重做这里的外层 chrome
├── large-rooms/
│   ├── geocities-heartland.html
│   ├── geocities-area51.html
│   ├── irc-channel.html
│   └── blog-2007.html
├── decisions/
│   └── next-room-pick.html
├── current-frame-screenshot.png   # ← 当前控制台框架截图
├── README.md
└── HANDOFF.md              # ← 你正在读
```

---

## 7. 沟通方式 (重要)

产品负责人是**非技术背景**. 报进度时:

- 用大白话 + 生活化类比
- 不要堆术语 (出现的术语立刻翻译)
- 不要扔 stacktrace 或长 JSON
- 报数字前先讲方法 (例: "我扫了 Wayback 5000 个快照, 取 >5KB 的 30 个", 不要扔个"30 个"就走)
- 失败也讲方法 (诚实失败 > 假装通过)
- 配色 / 字体 / 布局先给**真实参考图** (1999 年某个真页面 / 某部老电影 / 某个老软件截图), 不要凭空生成

时间偏好: 周一-五 9:30-19:00 是用户活跃时间.

---

## 8. 法律 / 内容边界

- 全部用户内容来自 Wayback Machine 公开归档 (1996-2010)
- 不嵌 paywall 网站 / Google / 现役商业站
- 不抓任何用户数据 (无后端, 无登录)
- MIT License
