# Haskell Backend 架构文档

本文档集面向 `services/k-haskell-backend` 的维护者与 Agent，记录从源码、构建定义和测试
恢复的架构事实，而非逐文件注释。本次基线：`feat/guided_execute@700919986`（2026-07-16）。

推荐顺序：先读 [系统概览](system-overview.md)，再读[组件地图](component-map.md)与
[执行流](execution-flow.md)，随后按需要查阅[数据模型](data-model.md)、
[模块索引](module-reference.md)、[扩展指南](extension-guide.md)和[术语](terminology.md)。

| 文档 | 职责 |
| --- | --- |
| `system-overview.md` | 系统边界、产物、运行模式和外部连接 |
| `component-map.md` | 按职责划分的组件及其输入输出 |
| `execution-flow.md` | 入口到执行、SMT 和错误的动态证据链 |
| `module-reference.md` | 重要模块的索引与修改风险 |
| `data-model.md` | 领域、协议和执行状态类型 |
| `extension-guide.md` | 常见变更的影响范围与测试 |
| `terminology.md` | 本仓库术语 |
| `change-log.md` | 文档维护记录 |

维护规则：每次修改入口、协议、执行引擎或核心类型后，复核相应文档中的源码路径和图边，
将不能直接证明的结论标为 **Inferred** 或 **Unknown**，并向 `change-log.md` 追加记录。
已知缺失：本文不证明 LLVM、pyk 或 K 的仓库外运行时实现；它们在本仓库中可见的配置、
调用或测试接口会单独标记。
