# 模块索引

| 类别 | 模块（路径） | 作用与风险 |
| --- | --- | --- |
| Entry point | `Main`（`kore/app/rpc/Main.hs`） | legacy RPC 生命周期、SMT 注入；改动影响启动和资源释放 |
| Entry point | `Main`（`booster/tools/booster/Server.hs`） | proxy CLI、definition/LLVM/log 初始化；高风险配置边界 |
| Public/core API | `Kore.JsonRpc`（`kore/src/Kore/JsonRpc.hs`） | `respond`、`runServer`；协议到 legacy engine 的适配 |
| Public/core API | `Kore.JsonRpc.Types`（`kore-rpc-types/src/.../Types.hs`） | request/result/API GADT；序列化兼容性风险最高 |
| Execution engine | `Proxy`（`booster/tools/booster/Proxy.hs`） | engine 路由与 fallback；改变会影响所有 RPC 行为 |
| Execution engine | `Booster.Pattern.Rewrite` | `RewriteState`、`RewriteResult` 和规则应用；高风险语义模块 |
| Domain model | `Booster.Pattern.Base` | `Term`、`Predicate`、`Pattern`、`Substitution`；跨 Booster engine 的核心表示 |
| Domain model | `Kore.Internal.Pattern`、`Predicate`、`Substitution` | legacy conditional pattern 模型 |
| Infrastructure | `Booster.SMT.Interface`、`SMT` | solver 控制与翻译；外部进程/可满足性风险 |
| Infrastructure | `Booster.Log*`、`Kore.Log*` | 日志、capture 和诊断；协议 log 字段的兼容风险 |
| Test/support | `test/rpc-server/`、`booster/test/rpc-integration/` | 端到端 RPC 行为；按方法/场景选择回归测试 |

低重要性 helper 仅在其出口被引用时加入此表；direct import 需通过 module header 复核，
caller 需通过调用位置复核。
