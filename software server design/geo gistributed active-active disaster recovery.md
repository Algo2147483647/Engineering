# Geo-Distributed Multiple-Active Disaster Recovery

[TOC]

## Multiple-Active 

![geo_gistributed_active-active_disaster_recovery](./assets/geo_gistributed_active-active_disaster_recovery.svg)

## Geo-Distributed Multiple-Active



![Geo-Distributed Active-Active](./assets/Geo-Distributed Active-Active.svg)

### Data synchronization middleware

Cross-data-center latency is a critical factor that cannot be overlooked. Efforts should be made to minimize cross-data-center calls to avoid latency issues. The storage in both data centers must act as **primary databases**, with data being **synchronized bidirectionally** between them. Implementing such a **dual-primary architecture** requires the development of a dedicated **data synchronization middleware** to enable seamless bidirectional synchronization.

### Router 分片

分片的核心思路在于，**让同一个用户的相关请求，只在一个机房内完成所有业务「闭环」，** **不再出现「跨机房」访问**。