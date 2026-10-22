# LQK8106

**Java 后端开发 · Spring Cloud 微服务**

专注于 Spring Cloud 微服务架构、分布式一致性与性能工程。独立完成两个可运行、可压测、可部署的微服务项目，均在本地完成容器化编排与容量标定。

---

## 项目

### [zx-learn · 知行智学](https://github.com/LQK8106/zx-learn)

AI 驱动的在线教育微服务平台 · Java 21

- 18 个 Maven 模块 / 16 个微服务（学员端 + 管理端），覆盖课程、学习记录、订单支付、优惠券秒杀、学情分析
- 未引入分布式事务框架，以本地消息表 + 消费流水唯一键幂等 + 8 项跨库对账 SQL 实现最终一致性
- 数据库层一致性设计：生成列 + 唯一索引兜底重复购买，课程名额以原子条件更新防超卖
- 优惠券秒杀：Redis Lua 原子预扣 + 令牌桶限流 + MQ 削峰，实测拒绝路径峰值 6,144 QPS / P99 150ms
- AI 智能助教：多 Agent 架构（意图路由 + 4 个业务 Agent）、Redis 会话记忆、pgvector RAG、SSE 流式输出

### [CodeJudge · 分布式在线编程评测平台](https://github.com/LQK8106/CodeJudge)

Java 21 微服务（8 个后端服务 + Vue 3 前端）

- 异步判题链路：RocketMQ 解耦 + 数据库租约 CAS 认领（条件更新替代分布式锁）+ 租约过期 CAS 接管
- 多语言安全沙箱：Docker 隔离 Java / Python / C++ / Go，只读根文件系统、断网、cgroup 限额、cap-drop ALL、自定义 seccomp、非 root 运行
- 性能标定：恒定负载实测 3,108 req/s、55.9 万样本零错误；1 小时长稳 887 万样本零错误；提交接口 P99 129ms
- 竞赛实时榜：WebSocket 推送（P95 5.1ms、0 丢帧）+ Redis ZSet 封榜快照 / 终榜重建
- 工程质量：JaCoCo 335 项单测 + vitest 136 项 + 98 项功能回归全绿，Docker Compose 一键编排

---

## 技术栈

```
语言        Java 21 · SQL · Python · JavaScript
后端        Spring Boot 3.3.5 · Spring Cloud 2023.0.3 · Spring Cloud Alibaba 2023.0.3.2 · MyBatis-Plus
中间件      MySQL 8 · Redis 7 · RocketMQ · pgvector
容器运维    Docker · Docker Compose · Linux
测试性能    JMeter · JaCoCo · vitest · Prometheus + Grafana
前端        Vue 3 · Element Plus
```
