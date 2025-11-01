# Redis 从入门到资深实战专家学习路径（实战版）

## 学习成果（可量化）
- 缓存与会话：命中率 `>95%`、穿透率 `<0.5%`、击穿与雪崩可控；核心接口 P99 `<50ms`（含缓存与回源）。
- 并发与任务：分布式锁具备“栅栏令牌（fencing token）”与过期续约；10 万任务流水线稳定处理，重复率 `<0.1%`。
- 事件与流：Streams 消费组在断电后可恢复，按键内幂等确保至少一次语义；滞留消息清理规则完善。
- 持久化与恢复：RDB + AOF 混合持久化，数据丢失窗口 `<=1s`（AOF 每秒 `fsync`）；单机恢复 `<2min`。
- 高可用与扩展：Sentinel 故障切换 `<10s`；Cluster 重分片无感（有节流）；跨机房读模型与一致性取舍清晰。
- 可观测与运维：指标与日志齐全（命中率/延迟/内存/连接/慢查询/阻塞操作），告警阈值生效。
- 安全与合规：ACL 最小权限、TLS、密钥轮换、审计日志与数据治理清单。

## 里程碑项目（含验收标准）
- 高性能缓存 + 会话系统
  - 要点：Cache-Aside/Write-Through/Write-Behind、批量与穿透防护（Bloom/空值缓存）、热点 Key 治理（副本与分片）、一致性与回源降级。
  - 验收：命中率 `>95%`、P99 `<50ms`、雪崩演练通过（多层 TTL/随机抖动/限流）；回源熔断与降级有效。
- 分布式锁与任务调度
  - 要点：锁键约定（含资源维度）、续约与看门狗、栅栏令牌避免幻写、Lua 原子脚本、死锁自愈与“幂等任务”。
  - 验收：在 1 万并发下无长时间“双持锁”，任务重复率 `<0.1%`，释放与续约记录可审计。
- 事件总线与流处理（Streams）
  - 要点：消费组、pending list 回补、幂等键、错误重试与 DLQ；与 Kafka/RabbitMQ 对比与协同（轻量事件）。
  - 验收：断电恢复后消息不丢不重（幂等保障），滞留治理策略完善，Lag 与延迟面板可视化。

## 核心技能清单（动手重点）
- 数据结构：String/Hash/List/Set/ZSet/Bitmap/HyperLogLog/Geo/Streams；典型场景与容量评估。
- 键空间治理：TTL/过期策略、Keyspace Notifications、大 Key/热 Key 排查与拆分、命名规范与分层。
- 高并发基础：Pipeline/事务（`MULTI/EXEC`）/Lua（`EVALSHA`）/脚本重试与幂等设计。
- 持久化与复制：RDB/AOF（混合、重写）、复制与一致性、`appendfsync`/阻塞操作分析。
- 内存与淘汰：`maxmemory` 策略（`volatile-*`/`allkeys-*`/`noeviction`）、碎片与压缩、对象编码（SDS/ziplist/listpack）。
- 高可用与扩展：Sentinel、Cluster（槽位、迁移与再平衡）、Proxy 层（Twemproxy/Redis Cluster Proxy）与限流治理。
- 观测与诊断：`INFO`/Slowlog/`MONITOR`/`LATENCY DOCTOR`、Redis Exporter（Prometheus+Grafana）、阻塞命令排查。
- 安全与合规：ACL、TLS、AUTH 管理、审计与日志留存、数据脱敏与隐私治理。

## 环境与工具
- 运行环境：Windows + Docker Desktop（可选 WSL2）；`redis:6/7` 镜像。
- 客户端与工具：`redis-cli`、`redis-benchmark`、`rdb-tools`、`redis-exporter`、`valkey`（可选）。
- SDK 与框架：Go（go-redis）、Java（Lettuce/Redisson）、Node（ioredis）。
- 压测与演练：`redis-benchmark`、k6/vegeta（端到端）、故障注入脚本。

## 交付物与目录建议
- 代码仓：`redis-expert/`
  - `modules/cache/`（多级缓存与穿透治理）
  - `modules/lock/`（分布式锁与任务治理）
  - `modules/streams/`（消费组与回补）
  - `monitoring/`（Prometheus+Grafana 面板与告警）
  - `scripts/`（部署/演练/压测与运维脚本）
  - `docs/`（设计/周报/复盘/演练剧本）

## 验收与评分标准
- 指标达标：命中率/延迟/任务重复率/恢复时间/故障切换/持久化窗口在阈值内。
- 稳定性：雪崩/击穿/穿透/锁丢失/消息堆积等演练通过；具备回补与降级方案。
- 工程化：约定与规范（键空间/TTL/命名）落地、监控与告警完善、脚本与剧本齐备。

## 推荐资料（精选）
- 官方文档：Redis.io（Persistence/Replication/Cluster/Streams/ACL）
- 特别主题：Redis Streams 官方指南、Antirez 博客、ElastiCache/阿里云 Redis 最佳实践
- 工具与生态：Redis Exporter、Redisson/Lettuce、go-redis、rdb-tools