# 术语

| 术语 | 本仓库含义 | 容易混淆项 |
| --- | --- | --- |
| Kore | `kore/` legacy Haskell engine，亦是 definition/语法名称 | 不是 `kore-rpc-types` package |
| Booster | `booster/` 的快速 engine 与 proxy 工具 | `kore-rpc-booster` 同时使用 Kore engine |
| Proxy | `booster/tools/booster/Proxy.hs` 的双引擎 request 路由器 | 不等于网络反向代理 |
| Pattern | Booster 的 `Pattern`，或 Kore 的 `Conditional TermLike` | 两个 engine 的 Haskell 类型不同 |
| Predicate | pattern 的逻辑条件；Booster 中包装 `Term` | 不等同 JSON `KorePattern` |
| Substitution | 变量到 term 的映射 | 需区分 Booster `Map Variable Term` 与 Kore 类型 |
| `HaltReason` | RPC execute result 的停止原因 | 与异常/`ErrorObj` 不同 |
| `ServerState` | Kore RPC 的 loaded/serialized/received module 状态 | 不等同 Booster state |
| internalise/externalise | 协议/JSON 与 engine 内部表示的转换 | 不是 import/export 关系 |
| side condition | 规则适用时的逻辑约束 | 当前具体类型随 engine 而不同，须查调用点 |
