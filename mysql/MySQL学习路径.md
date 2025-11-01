# MySQL 从入门到资深实战专家学习路径（实战版）

## 学习成果（可量化）
- 性能与稳定：复杂查询 P95 `<200ms`、写入延迟 P95 `<80ms`、在并发 500 下稳态 QPS `>3000`（本机+Docker）
- 一致性与事务：避免超卖/脏读/不可重复读/幻读，死锁率 `<0.1%` 并可自动恢复
- 高可用与容灾：主从复制延迟 `<500ms`（负载下），自动故障切换 `<30s`；备份恢复 RTO `<15min`、RPO `<1min`
- 可观测与运维：PMM/Performance Schema 指标齐全，告警阈值（复制滞后/死锁/慢查询）有效
- 安全与合规：最小权限（RBAC/GRANT）、TLS 加密、审计日志与密钥治理清单

## 里程碑项目（含验收标准）
- 订单-库存一致性服务（单库 InnoDB）
  - 目标：防止超卖，保证并发下事务一致性
  - 要点：表结构与索引设计、事务边界、隔离级别（RR/RC）、悲观/乐观并发控制、幂等更新
  - 验收：并发 1e5 下单仿真无超卖、P99 `<200ms`、死锁自动重试成功率 `>99%`
- 高可用集群（主从/半同步/读写分离）
  - 目标：搭建 1 主 2 从，读写分离与自动故障切换
  - 要点：`Group Replication` 或 `async + semi-sync`、`ProxySQL`/`Orchestrator`、只读库一致性校验
  - 验收：复制延迟 `<500ms`、故障切换 `<30s`、业务无感（最少错误）
- 备份与容灾演练（全量+增量+PITR）
  - 目标：实现可定期备份与秒级增量恢复
  - 要点：`Percona XtraBackup`、`binlog` 定位、自动化脚本、恢复演练剧本
  - 验收：RTO `<15min`、RPO `<1min`、演练记录完整可回放

## 核心技能清单（动手重点）
- 存储引擎与结构：InnoDB 页结构/索引（B+树）、二级索引与回表、聚簇索引、Redo/Undo、双写与刷脏
- 模型与约束：范式与反范式、外键/唯一/检查约束、生成列、JSON/虚拟列、时间序列/订单模型设计
- 索引与优化：联合索引、覆盖索引、前缀索引、不可见索引、直方图、统计信息、`EXPLAIN`/`optimizer trace`
- 事务与锁：MVCC、`autocommit` 坑、`gap/next-key` 锁、意向锁、锁升级、死锁检测与重试策略
- 查询与重写：谓词下推、索引选择、子查询改写、`JOIN` 顺序、`derived`/`materialization`、`CTE`
- 配置与调优：`innodb_buffer_pool_size`、`redo log size`、`flush_log_at_trx_commit`、`io_capacity`、连接池参数
- 分区与大表：`RANGE/HASH/LIST` 分区、冷热分离、归档与历史表、分区裁剪与维护
- 复制与一致性：`binlog` 格式（ROW/STATEMENT/MIXED）、半同步、`GTID`、延迟监控与补偿
- 备份与恢复：`mysqldump` vs `XtraBackup`、增量备份、PITR、校验与演练
- 监控与排障：Performance Schema、`sys` 库、慢查询日志、`pt-query-digest`、PMM
- 安全与合规：用户/角色、`GRANT/REVOKE`、最小权限、TLS/SSL、审计插件、数据脱敏与隐私治理
- 变更与发布：在线 DDL（`ALGORITHM=INPLACE`）、`pt-online-schema-change`、灰度发布与回滚策略

## 环境与工具
- 版本与平台：MySQL `8.0.x`、Windows + Docker Desktop、可选 WSL2
- 管理与客户端：MySQL Shell/Workbench、mycli、DBeaver
- 性能与诊断：Percona Toolkit、PMM（Prometheus+Grafana）、`pt-query-digest`、`innotop`
- 高可用与代理：Orchestrator、ProxySQL/MaxScale
- 备份与恢复：Percona XtraBackup、mydumper/myloader、`mysqlbinlog`

## 交付物与目录建议
- 代码与脚本：`mysql-expert/`（`schema/`、`procedures/`、`migrations/`、`benchmarks/`、`scripts/`）
- 监控与告警：`monitoring/`（PMM Dashboard 导出、慢查分析报告、复制延迟告警）
- 演练与手册：`playbooks/`（故障切换、备份恢复、变更发布剧本），`docs/`（设计/周报/复盘）

## 验收与评分标准
- 指标达标：查询/写入延迟、QPS、复制延迟、RTO/RPO、死锁率均在阈值内
- 稳定性：故障注入（主库宕机/网络抖动/锁竞争/表膨胀）均能自愈或按剧本快速恢复
- 工程化：版本化迁移、变更有审计、监控与告警完善、发布与回滚规范

## 推荐资料（精选）
- 官方文档：MySQL 8.0 Reference Manual、InnoDB Architecture、Performance Schema、Sys Schema
- 实战与工具：Percona Blog、Percona Toolkit、PMM 文档、Orchestrator/ProxySQL 文档
- 系统设计：High Performance MySQL（第 3/4 版）、Designing Data-Intensive Applications