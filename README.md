# obsidian-echarts

> **ECharts 6 for Obsidian** — 将 Apache ECharts 6 最新版带入 Obsidian

[![license](https://img.shields.io/badge/license-MIT-blue)](LICENSE)
[![echarts](https://img.shields.io/badge/ECharts-6.x-brightgreen)](https://echarts.apache.org/)
[![obsidian](https://img.shields.io/badge/Obsidian-0.15%2B-blue)](https://obsidian.md/)

## 背景

原项目 [cumany/obsidian-echarts](https://github.com/cumany/obsidian-echarts) 已停止更新，内置 **ECharts 5.3.2**（2022年发布）。本 Fork 将 ECharts 引擎升级到 **6.x**，保持 API 完全兼容的同时获得性能和新特性。

## 功能

| 特性 | 说明 |
|------|------|
| 📊 **全部图表类型** | 折线、柱状、饼图、散点、雷达、热力图、K线、漏斗、仪表盘、桑基图等 |
| 🎨 **主题/调色板** | 支持 `setTheme()` 切换 dark/light/custom 主题 |
| 📐 **响应式自适应** | 图表自动适配容器宽度，支持分栏/移动端 |
| 🔗 **交互能力** | 鼠标悬停提示、数据区域缩放、图例筛选、工具箱导出 |
| 🧩 **dataviewjs 集成** | 与 Dataview 插件联动，从 JSON/Markdown 动态渲染图表 |
| ⚡ **代码块模式** | 直接在笔记中写 ECharts option 配置即可出图 |

## 升级内容（vs 原版）

| 项目 | 原版 (cumany) | 本版本 |
|------|---------------|--------|
| **ECharts 版本** | 5.3.2 (2022) | **6.x (最新)** |
| **渲染性能** | 标准 | ↑ 渲染引擎优化，大数据量更流畅 |
| **新特性支持** | — | ✅ ECharts 6 新增图表组件 & 配置项 |
| **词云扩展** | echarts-wordcloud 2.x | ⏳ 暂移除（等待 wordcloud 3.x 适配） |
| **构建时间** | 2022-06 | 2026-06 |

## 安装

### 手动安装

1. 下载本仓库的 `main.js` + `manifest.json` + `styles.css`
2. 放入 Vault 的 `.obsidian/plugins/obsidian-echarts/` 目录
3. Obsidian 设置 → 第三方插件 → 启用 **obsidian echarts**
4. 同时需安装并启用 [Dataview](https://github.com/blacksmithgu/obsidian-dataview) 插件

### 使用方式

**方式一：直接写配置**

````markdown
```echarts
{
  "title": { "text": "销售数据", "left": "center" },
  "xAxis": { "type": "category", "data": ["周一","周二","周三","周四","周五"] },
  "yAxis": { "type": "value" },
  "series": [{ "type": "bar", "data": [120, 200, 150, 80, 70] }]
}
```
````

**方式二：dataviewjs 动态数据**

````markdown
```dataviewjs
const raw = await app.vault.adapter.read('data/my-data.json')
const data = JSON.parse(raw)

const option = {
  title: { text: '动态图表', left: 'center' },
  tooltip: { trigger: 'axis' },
  xAxis: { type: 'category', data: data.items.map(x => x.name) },
  yAxis: { type: 'value' },
  series: [{ type: 'line', data: data.items.map(x => x.value), smooth: true }]
}

this.container.createEl('div', { cls: 'echarts-container' })
app.plugins.plugins['obsidian-echarts'].render(option, this.container)
```
````

## 致谢

- [Apache ECharts](https://echarts.apache.org/) — 强大的可视化库
- [cumany/obsidian-echarts](https://github.com/cumany/obsidian-echarts) — 原始插件
- [Obsidian](https://obsidian.md/) — 优秀的知识管理工具
