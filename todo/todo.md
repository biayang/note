# todo

DNS nameserver

## proj

- 服务器架构
  - 接入层
    - 对外协议
    - 内部协议
    - 版本校验
    - 聊天与广播
    - session
    - 加密
    - 压缩
  - 逻辑层
  - 缓存层
  - 持久化层
    - 一致性
    - 高可用
    - 优化
    - 扩容缩容
  - 网络链路
    - 全球同服
    - 分区同服
- 代码框架
  - 定时任务
    - 秒级
  - 充值
    - 订单
    - 验证
    - 回调发奖
  - log系统
    - 收集
    - 分级
    - 查询
    - 归档
    - 清除
  - git流
    - 分支管理
    - tag
    - 回滚
    - 合并与向上合并
  - 异常监控
    - 较大数据
    - 异常数值
  - 打点统计
  - 压测
  - 单元测试
  - 性能优化
- 功能设计
  - 成就（历史/近期行为）
  - 排行
  - 活动
  - 过期数据清除
  - 队列排队
  - 物品统一增减
  - 领奖邮箱
  - VIP系统
- 配置
  - 导出
    - 指定表
    - 差异（新增新改）
  - 格式
    - string
    - int
    - array
  - 分表
  - 合并行
- 开发者工具
  - 临时修改配置
    - 调服务器时间
    - 调配置数值
  - 查改玩家数据
  - 查删缓存
  - 报错信息
  - API文档
  - 导入导出备份数据
- 多语言翻译系统
  - 权限
  - 工作流
- 发布系统
  - 版本
    - 各模块版本
    - 差异资源
  - 资源上传
    - 差异上传
    - rebase
    - 定期删除
  - 发布
    - 灰度
      - 按地理
      - 按逻辑服
      - 按渠道
      - 按uid
    - 独立审核
  - 切维护
    - 单服
    - 全服
  - 白名单（开发者账号）
    - uid
    - 公司IP
  - 黑名单
    - IP
    - uid
  - hotfix
- 运营
  - 在线
  - 收入
  - 活动
  - 公告
  - 发补偿
    - 范围
      - 单人
      - 全服
    - 权限
    - 操作记录
- 文档

## issues

- 某DB实例压力大
- 某玩家请求多
- trace一次请求的所有log(不跨服务、跨服务)
- 慢请求
- pay记录过多如何处理
- 支付校验都有啥

- oncall dingding
- release dingding
- activity dingding

## code

CURL
gRPC  
protobuff  
mq  
etcd  
nginx源码  
redis源码  

## geektime

05 从零开始学架构  
07 微服务核心架构20讲  
14 深入浅出gRPC-李林峰  
20 如何设计一个秒杀系统  
29 趣谈网络协议音频修复版  
31 从零开始学微服务  
32 深入剖析Kubernetes  
33 算法面试通关40讲  
35 Go语言核心36讲  
44 MySQL实战45讲  
46 数据结构与算法之美  
50 Linux性能优化实战  
53 程序员的数学基础课  
54 Nginx核心知识100讲  
57 10x程序员工作法 (已完结)  
76 趣谈Linux操作系统  
79 web协议详解与抓包实战  
80 深入浅出计算机组成原理  

## tool

tk  
批量文件改名 前缀 后缀 匹配  
dotfile  
ssh 秘钥管理 IP列表管理  
