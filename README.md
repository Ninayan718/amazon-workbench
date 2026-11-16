# 亚马逊工作台

单干卖家的经营与反馈工作台：选品 / Listing / 广告 / 数据核算 / 反馈 / 周报。

单文件网页、零依赖、离线可用（PWA，可添加到主屏幕）。所有文件与计算都在浏览器本地完成，数据只存本机，不上传服务器。

## 七个页面

- **总览**：工作台数据底座，KPI 与四个环节入口，可导入本地 result.json
- **选品 / Listing / 广告**：模块框架与引擎索引（后续接入）
- **数据**：报表核算引擎 + 每日目标看板
  - 选结算 CSV（Custom Unified Transaction）+ 成本 XLSX，浏览器本地算按天/按 MSKU 真实利润
  - 一键把核算结果送入每日记录
  - 每天填订单/销售额USD/利润¥/广告花费$/ACOS，按月到手目标反推今日需赚与需几单
  - 前 3 天广告数据按稳健型给当天预算与 ACOS 要求
- **反馈**：经营（可控动作 / 选品漏斗 / 3·7 天回看）与学习（亚马逊知识 / 其他学习两个独立子区、规则复核、学用桥）
- **周报**：五段汇总——工作台与利润 / 经营 / 数据目标 / 亚马逊知识 / 其他学习；规则版免配置，可选 AI 复盘

## 技术

- 利润核算：纯 JS 解析 xlsx（不用 DecompressionStream，兼容旧版 iOS Safari 与微信内置浏览器）
- 口径：订单 13 项结算字段带符号求和，减采购与空运头程；提现排除；非订单费用单列
- localStorage：`amz_feedback_v1`（反馈与每日记录）、`amz_workbench_v1`（result.json）、`amz_profit_v1`（核算结果）
- 源码在 `src/`，改完 `python3 build.py` 合成，再 `cp index.html manifest.json sw.js dist/`，最后 `node deploy.js` 上线
