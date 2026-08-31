# 📈 Daily Signal Report · 每日信号报告

一个纯静态的每日 Alpha 信号报告站点，覆盖四大品种，开箱即用，无需构建、无需后端。

- 🥇 **黄金 All Alphas**（Au）
- 🛢️ **原油 All Alphas**（SC）
- 📊 **股指 All Alphas**（Stock Index）
- 🏦 **国债 All Alphas**（Treasury）

## ✨ 特性

- **零依赖部署**：全部为静态 HTML，任意静态托管（GitHub Pages、Nginx、OSS 等）直接可用
- **自动适配设备**：入口页根据屏幕宽度自动跳转对应版本 —— 宽度 < 768px 打开 `_mobile.html`，否则打开 `_pc.html`
- **自包含图表**：报告页内嵌 Plotly（CDN 加载），单文件即可完整展示，方便归档与分享

## 📂 目录结构

```
daily_signal_report/
├── index.html          # 入口导航页（报告列表 + 设备自动跳转）
└── reports/            # 每日报告（PC 版 / 移动版成对出现）
    ├── au_all_alphas_pc.html             # 黄金 · PC 版
    ├── au_all_alphas_mobile.html         # 黄金 · 移动版
    ├── sc_all_alphas_pc.html             # 原油 · PC 版
    ├── sc_all_alphas_mobile.html         # 原油 · 移动版
    ├── stock_index_all_alphas_pc.html    # 股指 · PC 版
    ├── stock_index_all_alphas_mobile.html# 股指 · 移动版
    ├── treasury_all_alphas_pc.html       # 国债 · PC 版
    └── treasury_all_alphas_mobile.html   # 国债 · 移动版
```

## 🚀 使用

### 本地预览

直接用浏览器打开 `index.html` 即可；或启动任意静态服务器：

```bash
python -m http.server 8000
# 然后访问 http://localhost:8000
```

### 更新每日报告

用新生成的报告文件覆盖 `reports/` 下的同名文件即可，文件命名约定：

```
reports/<品种>_all_alphas_{pc|mobile}.html
```

新增品种时，除在 `reports/` 放入对应的 `_pc.html` 与 `_mobile.html` 外，还需在 `index.html` 的报告列表中添加一条带 `data-base` 属性的入口。

## 🔧 工作原理

`index.html` 为每个报告入口维护一个 `data-base`（文件基础名）。点击时按当前视口宽度拼接后缀：

```js
window.innerWidth < 768 ? '_mobile.html' : '_pc.html'
```

## 🛠️ 技术栈

- 入口页：原生 HTML / CSS / JavaScript，无框架
- 报告页：[Plotly.js](https://plotly.com/javascript/)（经 CDN 加载）静态导出
