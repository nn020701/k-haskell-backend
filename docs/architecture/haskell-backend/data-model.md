# 数据模型

| 类型/表示 | 定义位置 | 创建与消费 | 边界/不变量 |
| --- | --- | --- | --- |
| `API 'Req` / `API 'Res` | `kore-rpc-types/.../Kore/JsonRpc/Types.hs` | JSON-RPC dispatch、Proxy、Kore/Booster handlers | `ToJSON (API 'Res)`；跨进程协议边界 |
| `ExecuteRequest` / `ExecuteResult` | 同上 | client 构造，handler 消费/返回 | 含 state、depth、reason、logs 等协议字段 |
| `KorePattern` | `Kore/Syntax/Json/Types.hs` | JSON decode/encode 与 pattern conversion | 可序列化；不同于内部 term |
| `Term` | `Booster/Pattern/Base.hs` | Booster matcher、simplifier、rewriter | `Term TermAttributes (TermF Term)`；内部表示 |
| `Predicate` | `Booster/Pattern/Base.hs` | pattern condition 和 SMT/rewrite 条件 | `newtype Predicate = Predicate Term` |
| `Substitution` | `Booster/Pattern/Base.hs` | matching/规则应用 | `Map Variable Term`，变量键应唯一 |
| `Pattern` | `Booster/Pattern/Base.hs` | request internalise、rewrite/result externalise | term 与 predicate 的组合；内部表示 |
| Legacy `Pattern variable` | `Kore/Internal/Pattern.hs` | `verifyIn` 后的 execution/simplification | `Conditional variable (TermLike variable)` |
| Legacy `Predicate`/`Substitution` | `Kore/Internal/Predicate.hs`、`Substitution.hs` | Kore simplifier/rewrite | 与 Booster 类型不是同一类型 |
| `RuleInfo` / `ProgramState` | `Kore/Rewrite.hs` | `Exec.rpcExec` 的状态与规则信息 | 运行时内部状态 |
| `RewriteState` / `RewriteResult` | `Booster/Pattern/Rewrite.hs` | Booster rule application | 表示步骤、结果和 trace；不直接是 RPC schema |
| `ServerState` | `Kore.JsonRpc` | RPC startup 创建，handler 读取/更新 | 保存 serialized/loaded/received modules |
| `LogLine` | `Kore.JsonRpc.Types.ContextLog` | proxy capture 注入 response | 可 JSON 序列化，跨 RPC 边界 |

**Unknown**：当前文档未对每个类型的所有 constructor 不变量作穷尽证明；修改前应回到
定义和构造点搜索。数据在 Booster 与 Kore 之间通常需经 `Internalise`/`Externalise` 或
JSON/协议适配，而非共享 Haskell domain type。
