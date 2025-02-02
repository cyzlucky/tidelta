# TiDB-Hackthon2021 - TiDelta 项目 RFC

## 团队介绍

- [abingcbc](https://github.com/abingcbc): 
- [cyzlucky](https://github.com/cyzlucky): Java、React全栈开发。
- [lunlau](https://github.com/lunlau): 
- [Yui-Song](https://github.com/Yui-Song): TiDB 性能测试工程师

## 项目介绍
 一个用户可以方便在本地启动的 TiDB 性能诊断 web 服务

## 项目动机
我们的项目来自 AskTUG 上客户反馈的真实问题：
1. 监控很多，客户需要来回切换，希望能将常用的监控放在一起
![user_feedback1](./media/user_feedbacks1.jpeg)
2. 很多监控日常用不到，遇到问题不知道去看哪些监控
![user_feedback2](./media/user_feedbacks2.jpeg)

- 众所周知，TiDB 有非常强大的监控系统 (Prometheus & Grafana)。但是就是因为太强大了，监控指标太多，对小白用户不是那么友好，对比起来也不容易，为性能调优带来不小的困难。
- TiDelta 能帮助你整合 TiDB 关键路径的性能 metrics，并生成 Metrics Diff Report，方便用户对比任何两个时间段，或者是升级前后、测试库和生产库的性能指标。

## 项目目标
- 目标一：整合现有 TiDB Metrics 数据，整理关键路径时延指标
- 目标二：生成 Metrics Diff report

## 产品设计

### 数据导入：
1. 能直接处理 tiup diag 输出的数据文件，主要是 config 和 monitor。	
2. 将其导入 Prometheus，但是又不会和本地的TiDB的监控数据冲突。（比如将生产库的监控数据，导入测试库一起分析。）


### 数据展示：
1. 输入 Prometheus 连接，连上数据库
2. RAW Data Comparison（基础需求）：

	a. 可选取任何两个数据库，任何两个时间段，方便地对比指定的某个指标，直接展示两个时序图即可。
	
	b. 可选取任同一个数据库，任何两个时间段，方便地对比指定的某个指标，直接展示两个时序图即可。
	
	c. 需要能轻松选择指定 TiDB 已有的所有面板，列出具体指标。
	
3. 列出两个系统的 config，置顶展示不一样的配置项。（只有对比两个系统时才有）
4. Diff Report（高级需求）：

	a. 可选取任何两个数据库，任何两个时间段，对比展示聚合过的TiDB关键路径性能指标表格
	
	b. 可选取任同一个数据库，任何两个时间段，对比展示聚合过的TiDB关键路径性能指标表格
	
	c. Diff Report 可以下载
