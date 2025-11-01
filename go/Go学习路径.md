# Go 从入门到资深实战专家学习路径（实战版）

## 学习成果（可量化）
- 本机稳定跑并发服务：RPS `>2000`、P99 延迟 `<120ms`、`-race` 无数据竞争、CPU/内存使用可控。
- 交付 3 个可运行项目：CLI 工具、REST+gRPC 服务、分布式任务处理器（含限流/重试/回压）。
- 工程化能力：`go mod` 依赖管理、代码规范（lint/format）、全链路测试（单测/集成/基准）、CI/CD 与 Docker 部署。
- 可观测性：接入 Prometheus 指标、OpenTelemetry Trace、结构化日志三位一体；告警阈值生效。
- 安全与合规：TLS/mTLS、JWT/OAuth2、密钥与配置管理、审计日志。

## 里程碑项目（含验收标准）
- CLI 工具（文件/日志处理管道）
  - 要点：并发流水线（fan-out/fan-in/pipeline）、上下文取消、错误聚合。
  - 验收：在 1GB 输入下正确率 `100%`；性能报告与资源占用达标；单测覆盖 `>80%`。
- REST+gRPC 服务（订单/用户域）
  - 要点：Gin/Fiber + gRPC、分层架构（handler/service/repo）、事务与一致性、拦截器/middleware。
  - 验收：k6 压测 RPS `>2000`、P99 `<120ms`；端到端 Trace/Metric 可见；错误率 `<0.1%`。
- 分布式任务处理器（Worker Pool）
  - 要点：限流（令牌桶）、退避重试、回压、幂等任务；可切 MQ（NATS/Kafka）或本地队列。
  - 验收：在 10 万任务下稳定处理；无重复/丢失；可观测看板与告警有效。

## 核心技能清单（动手重点）
- 语言基础与泛型：类型系统、切片/映射、接口、`type parameter`、约束与可重用库设计。
- 并发模型：goroutine、channel、select、`sync` 原语（Mutex/RWMutex/WaitGroup/Cond/Atomic）、`context` 生命周期与取消。
- 错误与日志：错误包装/分类、`errors.Is/As`、结构化日志（zap/logrus）、请求链路关联（traceId）。
- Web 与 RPC：HTTP（Gin/Fiber）、gRPC（unary/streaming）、拦截器、超时/重试/断路器、中间件栈。
- 数据访问：`database/sql`、sqlx/GORM、事务边界、迁移（go-migrate）、连接池调优。
- 测试与基准：`testing`、`testify`、`httptest`、`gomock`、`testing.B` 基准、`pprof`/`trace` 分析与优化。
- 可观测与运维：Prometheus 指标（直方图/计数器/仪表盘）、OpenTelemetry、日志采集与关联、告警阈值。
- 安全与配置：TLS/mTLS、JWT/OAuth2（go-oidc）、配置管理（viper/env）、密钥与凭据治理。
- 构建与交付：`go build`/`go test`/`go vet`、交叉编译（GOOS/GOARCH）、Docker 多阶段、最小镜像与启动探针。

## 环境与工具
- 版本：Go `>=1.22`；IDE：VS Code/GoLand；静态检查：`golangci-lint`；调试：`dlv`；热加载：`air`。
- 常用库：Gin/Fiber、gRPC/protobuf、sqlx/GORM、zap、viper、testify/gomock、prometheus/client_golang、otel。
- 压测工具：k6、wrk、`vegeta`；分析工具：`pprof`、`go tool trace`、`go doc`。

## 交付物与目录建议
- 代码仓：`go-expert/`
  - `cmd/` 可执行入口（`api`, `worker`, `cli`）
  - `internal/` 领域代码（`handler/service/repo/domain`）
  - `pkg/` 可复用库（限流/重试/通用中间件）
  - `configs/` 配置文件（dev/prod）与示例
  - `scripts/` 构建/测试/压测/部署脚本（Windows PowerShell）
  - `deploy/` Dockerfile 与 Compose；`docs/` 设计与周报；`benchmarks/` 基准报告

## 验收与评分标准
- 指标达标：RPS/P99/错误率/资源占用达标；`-race` 无竞争；无 goroutine 泄漏。
- 测试与质量：单测覆盖 `>70%`（里程碑项目 `>80%`）、lint 通过、基准与优化报告齐备。
- 可靠性：故障注入（超时/网络抖动/下游异常）可恢复；限流/退避/熔断策略有效。
- 运维与交付：镜像体积小、启动迅速、观测看板完善、告警阈值合理。

## 推荐资料（精选）
- 官方：`go.dev`、`Effective Go`、`Go Memory Model`、`Go Blog`。
- 书籍与课程：Go 程序设计语言、Concurrency in Go、Designing Distributed Systems。
- 工程实践：Uber Go Style Guide、Cloud Native Go、OpenTelemetry/Prometheus 文档。