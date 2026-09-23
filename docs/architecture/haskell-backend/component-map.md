# 组件地图

| 组件 | Confirmed 目录/模块 | 职责、输入输出 | 依赖与测试 |
| --- | --- | --- | --- |
| 入口与配置 | `kore/app/rpc/Main.hs`、`booster/tools/booster/Server.hs` | 解析 CLI、加载 definition、创建 server/日志/SMT；输入文件和选项，输出监听服务 | 依赖 `GlobalMain`、`Kore.JsonRpc`、Booster；Cabal executable stanza |
| RPC 协议 | `kore-rpc-types/src/Kore/JsonRpc/Types.hs` | JSON 可序列化 request/result 和 `API` GADT | 被 Kore 与 Booster import；RPC tests |
| Legacy Kore 引擎 | `kore/src/Kore/JsonRpc.hs`、`Kore/Exec.hs`、`Kore/Simplify/API.hs` | 验证 pattern，执行、化简、证明和建模 | 消费 protocol 与 indexed definition；`kore-test`、`test/rpc-server/` |
| Booster 引擎 | `booster/library/Booster/JsonRpc.hs`、`Pattern/` | 快速 JSON-RPC 执行、term/pattern 操作、rewrite | `booster/unit-tests/`、`booster/test/rpc-integration/` |
| Proxy | `booster/tools/booster/Proxy.hs` | 请求级 Booster/Kore 编排、fallback、日志捕获 | `respondEither` 被 Server 注册 |
| SMT | `Kore/Rewrite/SMT/`、`SMT.hs`、`Booster/SMT/` | solver 配置、声明 lemma、运行查询 | Kore RPC 启动时创建 solver；SMT error tests |
| Builtin/LLVM | `Kore/Builtin/`、`Booster/Builtin*.hs`、`Booster/LLVM*.hs` | 内建语义和 LLVM 加速接口 | Booster server 选择性加载动态库；LLVM integration |
| 可观测性 | `Kore/Log/`、`Booster/Log/`、`LogCapture` | logger、context、请求日志捕获与 API log entry | Proxy 在两个 engine 上安装 capture |

稳定边界是 JSON-RPC types、CLI/definition 输入和文档文件名；`Pattern/Rewrite`、Kore
simplifier 等为实现细节，变更时仍需评估其调用者。详细模块见[模块索引](module-reference.md)。
