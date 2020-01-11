# 微服务 容量规划

## 容量评估

一般通过线上压测进行容量评估。

- **压测**
  - 指标
    - 系统指标 CPU、MEM、DISK、IO
    - 服务指标 响应平均耗时、P999耗时、错误率、响应大于1s的比例
  - 方式
    - 单机压测
      - 模拟线上流量
      - TCP-Copy拷贝线上流量
    - 集群压测
      - 逐渐减少线上机器节点

## 调度决策

将实际负荷转化为水位线，作为扩缩容的依据。  
如：区间加权计算水位线。响应时间0~10ms=1； 10~50ms=2； 50~100ms=4；100~200ms=8；200~500ms=16；500ms+=32。按比例加和。

- **水位线**
  - 扩容 扩容一定百分比的机器数量
  - 缩容 缩小一定百分比的机器数量
    - 渐进式 每5min获取一次水位线，执行计划缩容的10%、30%、50%、100%