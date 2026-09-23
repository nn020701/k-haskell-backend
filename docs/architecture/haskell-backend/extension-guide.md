# 扩展指南

| 场景 | 入口与常见修改面 | 测试与文档影响 |
| --- | --- | --- |
| 新 RPC 方法/协议字段 | `kore-rpc-types/.../Types.hs` 的 request/result/API，Kore `respond`，Booster `JsonRpc` 与 Proxy | RPC integration；更新 overview、execution flow、data model、术语 |
| 修改 execute/rewrite | `Kore.Exec.rpcExec`、`Kore.Rewrite*`，或 `Booster.Pattern.Rewrite`、Proxy fallback | execute/Booster integration；更新 execution flow、component map |
| 修改 simplification | `Kore.Simplify.API.evalSimplifier` 或 Booster `Pattern.Util` | simplify RPC 与 unit tests；更新 execution/data 文档 |
| 新 builtin | `Kore/Builtin/` 或 `Booster/Builtin*.hs`，并检查 definition/term 表示 | 单元与集成测试；更新 component/data/terminology |
| SMT 查询/配置 | `app/rpc/Main.hs:runSMT`、`Kore/Rewrite/SMT/`、`Booster/SMT/` | SMT error/行为测试；更新 execution/data 文档 |
| log/trace | `Kore.Log*`、`Booster.Log*`、`LogCapture`、protocol log types | logging integration；更新 execution 和 protocol 说明 |
| LLVM 加速 | `Booster.LLVM*` 与 `Server.hs` 的 library 初始化 | LLVM integration；更新 overview/component map |
| 新测试 | Cabal test-suite 与 `test/rpc-server/` / `booster/test/rpc-integration/` | 记录测试路径；无需改变协议文档除非语义变化 |

**Unknown**：本 revision 未确认独立的“primitive”扩展注册点或 pyk-specific server API；
不要创建虚构的 hook。每次改动先区分 protocol compatibility、engine-local 语义和 proxy
路由影响，并在[变更记录](change-log.md)中追加条目。
