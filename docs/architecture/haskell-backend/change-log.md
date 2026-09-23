# 架构文档变更记录

## 2026-07-16：初次建立

- 基线：`feat/guided_execute@700919986`。
- 覆盖：构建产物、Kore/Booster/Proxy/RPC/SMT/LLVM、核心类型、关键 RPC 与启动链路、
  测试入口和扩展影响。
- 未覆盖：仓库外 K、pyk 与 solver 的实现；所有高阶/条件编译调用的穷尽运行时证明。
- 待验证：每个 Booster simplify/fallback 分支和外部工具实际部署拓扑。

后续条目应包含日期、功能/变更、涉及模块、更新文档及待补充内容。
