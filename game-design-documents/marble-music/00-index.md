# 音乐物理沙盒 GDD（v1）总索引

## 文档信息

- 功能代号：`001-music-physics-sandbox`
- 目标平台：PC Web（桌面浏览器）
- 技术栈基线：`Vite + TypeScript + Matter.js + Web Audio API + Canvas 2D`
- 文档语言：中文（英文术语附中文语义）
- 版本状态：可执行版本（对齐当前实现与测试资产）

## 用户确认的最终规则（强约束）

- 播放态控制：`Space` 为播放/停止，不提供暂停。
- Timeline 显示策略：播放时隐藏，仅编辑模式可见并用于回看。
- 预测线策略：仅编辑模式显示。
- 音乐触发策略：每次触发都完整播放包络，可重叠发声。
- 主球跟随策略：存在多个小球时，点击小球仅表示选中；按 `Space` 启动播放时，若有选中球则跟随该球，否则不自动跟随；用户始终可手动平移/缩放视窗。

## GDD 分卷结构

1.  [`01-product-vision-scope.md`](./01-product-vision-scope.md)：产品目标、用户、范围与边界
2.  [`02-core-loop-and-gameplay-systems.md`](./02-core-loop-and-gameplay-systems.md)：核心循环与玩法系统
3.  [`03-interaction-design-input-flow.md`](./03-interaction-design-input-flow.md)：交互设计与输入映射
4.  [`04-ui-ux-visual-design.md`](./04-ui-ux-visual-design.md)：界面结构、状态与视觉规范
5.  [`05-audio-music-visualization.md`](./05-audio-music-visualization.md)：音频系统、参数与可视化规则
6.  [`06-technical-architecture.md`](./06-technical-architecture.md)：技术架构与模块职责
7.  [`07-data-model-save-contracts.md`](./07-data-model-save-contracts.md)：数据模型、序列化与存档契约
8.  [`08-test-plan-acceptance.md`](./08-test-plan-acceptance.md)：测试策略、验收矩阵与发布门禁
9.  [`09-roadmap-and-risks.md`](./09-roadmap-and-risks.md)：演进路线与风险管理

## 阅读顺序建议

- 产品/策划：[01](./01-product-vision-scope.md) -> [02](./02-core-loop-and-gameplay-systems.md) -> [03](./03-interaction-design-input-flow.md) -> [04](./04-ui-ux-visual-design.md)
- 客户端开发：[02](./02-core-loop-and-gameplay-systems.md) -> [05](./05-audio-music-visualization.md) -> [06](./06-technical-architecture.md) -> [07](./07-data-model-save-contracts.md)
- QA：[03](./03-interaction-design-input-flow.md) -> [04](./04-ui-ux-visual-design.md) -> [08](./08-test-plan-acceptance.md)
- 迭代规划：[09](./09-roadmap-and-risks.md)
