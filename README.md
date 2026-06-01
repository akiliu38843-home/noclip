# NOCLIP · 凌晨档案

> 一个让你随机穿过 100+ 个 1995-2010 老网页的后室式网站.
> 12 种老电脑外壳 (Win98 / XP / Win7 / Mac System 6 / DOS / NES.css / IE6 / Netscape 4 / WAP / MSN / BBS / Unix Terminal) × 103 个真实老网页, 每开一扇门随机组合.

## 玩法

1. 打开 `index.html` (或访问部署后的 URL)
2. 点屏幕上窗口的 **× 关闭按钮** / 任何房间的 **[exit]** / 底部 **"开下一扇门"** / 或任何时候按 **ESC 键**
3. 故障转场 0.5-2 秒 (黑屏 + 拨号合成声)
4. 10% 概率走 3D 走廊 3-5 秒
5. 落地新房间: 随机外壳套着随机老网页

## 后室味机制

- **拟态门**: 每个外壳的"关闭按钮"都是真门 (不是浮窗按钮)
- **故障转场**: 黑屏 + Web Audio 合成的拨号噪音
- **走廊转场**: 10% 概率进 CSS 3D 黄色走廊
- **里程碑**: 第 7/17/47/100 扇有特殊事件 (47 = Level Fun 强制档案房)
- **不能停**: 10s 不动屏幕开始变红, 18s 强制开门
- **规则随机**: 邻接图 + 深度梯度 + 集群粘着, 不是均匀骰子
- **类型可见**: 5 类房 (档案 / 玩具 / 幻境 / 杂物 / 休息), 顶部时间线显示最近 12 扇
- **安全兜底**: URL 试探 (fetch 探测可达性), Loading 6s 出 retry, ESC 全局换门

## 致谢

外壳框架:
- [98.css](https://github.com/jdan/98.css) MIT
- [XP.css](https://github.com/botoxparty/XP.css) MIT
- [7.css](https://github.com/khang-nd/7.css) MIT
- [system.css](https://github.com/sakofchit/system.css) MIT (Mac System 6)
- [TuiCss](https://github.com/vinibiavatti1/TuiCss) MIT (DOS Turbo Vision)
- [NES.css](https://github.com/nostalgic-css/NES.css) MIT (8-bit)
- [terminal.css](https://github.com/Gioni06/terminal.css) MIT
- Netscape 4 / IE6 / WAP / MSN / BBS ANSI 由本项目自写 CSS

URL 池来源:
- [The Useless Web](https://theuselessweb.com/) curated list (~100 URLs)
- [JODI](https://wwwwwwwww.jodi.org/) 网络艺术正典
- [Cameron's World](https://www.cameronsworld.net/) GeoCities 拼贴
- [Wiby Surprise](https://wiby.me/surprise/) 老风格随机搜索
- Project Gutenberg / RFC Editor / MIT Classics / textfiles.com 等真档案站

灵感:
- [The Backrooms](https://backrooms-wiki.wikidot.com/) Original mythos
- [NicolasSkopek/LIMINAL](https://github.com/NicolasSkopek/LIMINAL) 同构产品 (XP 桌面 + 阈限内容)
- Olia Lialina 网络艺术

## 技术

- 单文件 HTML · 无 build · 无后端 · 状态存浏览器 localStorage
- 嵌套 iframe (外壳 srcdoc + 内容 URL)
- Web Audio API 合成拨号声 + 心跳声
- CSS 3D perspective 走廊

## License

MIT. 引用外壳框架各自的 license. URL 池里的 link 仅作为 iframe 链接, 内容归原作者.


## Fonts

This project uses fonts from the **Int10h Oldschool PC Font Pack v2.2** (https://int10h.org/oldschool-pc-fonts/) licensed under [CC-BY-SA-4.0](https://creativecommons.org/licenses/by-sa/4.0/). See `fonts/LICENSE.txt`.
