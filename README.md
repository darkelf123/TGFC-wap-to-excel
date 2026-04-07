# TGFC-wap-to-excel
# TGFC摸鱼助手 (Excel伪装)

> 把 TGFC俱乐部 WAP 论坛伪装成 Microsoft Excel 表格界面，让你在公司摸鱼时更加安全。

![版本](https://img.shields.io/badge/版本-3.0-green) ![许可证](https://img.shields.io/badge/许可证-MIT-blue) ![平台](https://img.shields.io/badge/平台-Tampermonkey-orange)

---

## 效果预览

启用后，TGFC 论坛页面会被完整替换为 Excel 风格界面：

- 顶部显示绿色 Excel 标题栏、菜单栏、功能区和公式栏
- 帖子列表以电子表格行的形式呈现
- 帖子详情以三列表格（楼层/作者 · 内容 · 时间）呈现
- 底部显示 Sheet 标签页翻页栏和状态栏
- 鼠标悬停单元格时，公式栏会同步显示单元格内容

---

## 功能特性

### 列表页
- 帖子列表转换为 Excel 行，每行显示：作者、回复数、浏览数、最后回帖 ID、帖子标题、分页链接
- 置顶帖以绿色高亮区分
- 底部 Sheet 标签栏对应帖子列表的翻页

### 详情页
- 每条楼层显示为独立表格行，包含楼号、作者名、帖子内容、发帖时间和引用链接
- 自动过滤 `posted by wap, platform: xxx` 等设备信息和广告
- 表格上方保留可点击的面包屑导航（`TGFC俱乐部 >> 灌水与情感 >> 帖子标题`），外观为纯文本，无超链接颜色和下划线
- 底部内置快速回复框，直接在 Excel 界面内发帖
- Sheet 标签栏对应帖子的分页翻页

### 通用
- 公式栏显示面包屑路径，鼠标悬停单元格时临时显示单元格内容
- 模式开关状态持久化保存，刷新页面后自动恢复
- 支持快捷键 `Ctrl + Shift + X` 快速切换

---

## 安装方法

### 第一步：安装 Tampermonkey

前往浏览器扩展商店安装 [Tampermonkey](https://www.tampermonkey.net/)：

| 浏览器 | 链接 |
|--------|------|
| Chrome | [Chrome 网上应用店](https://chrome.google.com/webstore/detail/tampermonkey/dhdgffkkebhmkfjojejmpbldmpobfkfo) |
| Edge | [Microsoft Edge 加载项](https://microsoftedge.microsoft.com/addons/detail/tampermonkey/iikmkjmpaadaobahmlepeloendndfphd) |
| Firefox | [Firefox 附加组件](https://addons.mozilla.org/firefox/addon/tampermonkey/) |

### 第二步：安装脚本

1. 点击 Tampermonkey 图标 → **创建新脚本**
2. 删除编辑器中的全部默认内容
3. 将 `tgfc_excel_disguise.js` 的全部内容粘贴进去
4. 按 `Ctrl + S` 保存

### 第三步：访问论坛

打开 [s.tgfcer.com](https://s.tgfcer.com/wap/) 后，页面右上角会出现绿色的「**摸鱼模式**」按钮，点击即可启用。

---

## 使用说明

| 操作 | 方式 |
|------|------|
| 启用 / 退出摸鱼模式 | 点击页面右上角按钮，或按 `Ctrl + Shift + X` |
| 翻页 | 点击底部 Sheet 标签栏中的页码 |
| 查看帖子 | 点击 B 列中的帖子标题链接 |
| 返回列表 | 点击详情页顶部面包屑中的版块名称 |
| 快速回复 | 在详情页底部表格行中输入内容，点击「发送」 |
| 引用回复 | 点击 C 列中的「引用」链接 |

---

## 适用范围

脚本仅对以下域名生效：

```
s.tgfcer.com/wap/*
wap.tgfcer.com/*
```

---

## 注意事项

- **分辨率**：界面针对 **1080P 桌面屏幕**优化，在移动端或低分辨率屏幕下列宽比例可能不理想
- **登录状态**：快速回复功能需要已登录 TGFC 账号，未登录状态下点击发送会被服务器拒绝
- **图片显示**：默认不加载图片（WAP 页面默认行为），如需查看图片请点击详情页面包屑导航旁的「显图」链接
- **模式记忆**：启用状态通过 `localStorage` 记录，清除浏览器数据后需重新开启

---

## 技术说明

| 项目 | 说明 |
|------|------|
| 运行时机 | `document-end`（DOM 加载完成后执行） |
| 样式注入 | `GM_addStyle` |
| 状态存储 | `localStorage`（key: `tgfc_excel_mode`） |
| 页面类型判断 | `URLSearchParams` 解析 `action` 参数 |
| 表格渲染 | 列表页用 `display:table` 模拟，详情页用原生 `<table>` |
| 列宽策略 | `table-layout:auto` + `width:1px; white-space:nowrap` 实现内容自适应列宽 |
| 表单提交 | 触发原始 `<input type="submit">` 的 `.click()`，确保 `name="submit"` 字段随请求一起发送 |

---

## 致谢

本脚本基于 [S1摸鱼助手(excel)](https://greasyfork.org/scripts/557042) 的思路，由 Gemini 原创，针对 TGFC WAP 页面结构重新适配开发。

---

## 许可证

[MIT License](https://opensource.org/licenses/MIT)
