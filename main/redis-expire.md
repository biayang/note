# redis过期

## 依赖

依赖计算机时钟，调整时钟会令key立刻过期。  

## 方式

### 被动删除

当一些客户端尝试访问它时，key会被发现并主动的过期。  

### 主动删除(定期删除)

1. 测试随机的20个keys进行相关过期检测。  
2. 删除所有已经过期的keys。  
3. 如果有多于25%的keys过期，重复步奏1.  

> src/expire.c activeExpireCycle()

## 复制AOF过期

slaves不会独立处理过期（会等到master执行DEL命令）。
