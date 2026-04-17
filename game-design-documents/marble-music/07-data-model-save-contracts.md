# 数据模型、存档与契约

## 1. 核心实体

### Scene

- 关键字段：`id`、`mode`、`gravity`、`selectedBallId`、`entities`、`timeline`。
- 说明：`selectedBallId` 表示“当前选中球”，用于播放启动时的跟随目标判定；可为 `null`。

### Ball

- 关键字段：`id`、`kind=ball`、`x/y`、`vx/vy`、`radius`。
- 规则：播放态仅 Ball 会被物理推进。

### Block

- 关键字段：`id`、`kind=block`、`x/y`、`width/height`、`rotation`。
- 规则：始终静态。

### MusicBlock

- 关键字段：`id`、`kind=music-block`、`x/y`、`width/height`、`noteName`、`volume`、`durationMs`、`timbre=piano`。
- 规则：参数在编辑态可修改，播放态锁定。

### ContactEvent

- 关键字段：`id`、`timeMs`、`ballId`、`musicBlockId`、`noteName`、`volume`。
- 规则：播放时持续记录；编辑态用于回看渲染。

## 2. 存档结构

- 顶层：`version`、`savedAt`、`scene`。
- 存档载体：`localStorage`。
- 版本策略：当前固定 `version=1`，后续升级需提供迁移。

## 3. 存档时机

- 编辑动作后进入节流保存窗口。
- 模式切换（尤其播放结束回编辑）触发一次强制保存。
- 页面可见性变化或离开前可尝试补写（受浏览器限制）。

## 4. 恢复流程

1. 应用初始化读取本地快照。
2. 校验 JSON Schema 与关键字段完整性。
3. 校验通过则恢复场景；失败则回退默认空场景并提示用户。

## 5. 与契约文件对齐

- 契约来源：`specs/001-music-physics-sandbox/contracts/sandbox-state.schema.json`。
- 强约束：
  - `scene.mode` 仅 `edit | play`。
  - `musicBlock.timbre` 固定 `piano`。
  - `volume` 范围 `0~1`。
  - `durationMs` 必须大于 0。
- GDD 与契约冲突时，以契约校验规则优先，并在文档更新中修正叙述。

## 6. 一致性备注

- Timeline 的“隐藏”仅是 UI 层行为，不影响 `scene.timeline` 记录。
- 跟随策略由“选中球 + 启动播放时判定”决定，`selectedBallId` 仅用于启动时决策，不引入额外跟随状态持久化。
- 预测线为运行态计算结果，不进入持久化结构。
