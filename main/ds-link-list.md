# 链表

## 概念

非连续，非顺序(随机离散存储)的有若干节点组成。

## 结构

### 单向链表

head  
node {data, next(last指向null)}
len  

### 双向链表

head  
node {data, prev, next(last指向null)}  
len  

### 循环链表

head  
node {data, prev, next(last指向head)}  
len  

## 类别

线性表

## 操作

### 查 O(n)

1. 查找的指针定位到head。
2. 根据next指针逐一向后查找。

### 增

#### 尾部增加 O(n)

1. 尾部的next指向新节点

#### 头部增加 O(1)

1. 新节点的next指向原先头节点
2. 新节点变为头节点

#### 中部增加 O(n)

1. 插入位置的前置节点的next指向新节点。
2. 新节点的next指针指向前置节点的next指针原先指向的节点。

### 改 O(n)

### 删

#### 尾部删除 O(n)

1. 倒数第二的next指向null

#### 头部删除 O(1)

1. 头节点的next节点设为头节点

#### 中间删除 O(n)

1. 要删除节点i前置节点的next指向i的下一节点

## 特点

头添加，头删除

## 问题

丧失随机访问能力