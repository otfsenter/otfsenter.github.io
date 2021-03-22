# 内部的3大流程

## SD

service deploy



- 工单管理
- 服务部署
- 集群管理
- 变更管理
- 灰度管理
- IaC服务
- 容器服务
- 函数部署
- 模型部署
- SQL执行
- 中间件部署

## ITR

issue to resolve

- 告警管理
- 告警屏蔽
- 告警修复
- 事件管理
- 安全事件
- 域名预案管理
- 服务状态
- 问题跟踪
- AIOps
- 调用链
- DCG管理
- Zabbix监控
- 服务监控

## BCM

Business Continuity Management

 

- Chaos Monkey
- 健康管家
- BCM问题管理



## EAP 

Event Automation Platform - 事件自动化平台

- 作业平台
- 定时任务
- ChatOPs 规则、流程



# 内部-功能模块

## 权限管理





## CMDB

configure management database



- 域名管理
- 主机管理
- 网络管理（EIP、ELB、SLB）

## 配置管理



## 部署

- 集群管理
- 部署管理



## 作业平台

- 工具库

  - 日志清理
  - 数据提取

- 快速脚本执行

- 定时任务

- 主机权限申请

- 作业清单

- 文件分发（上传）

## EAP

Event Automation Platform - 事件自动化平台

- ChatOps

## 告警系统

- 告警列表
- 告警抑制
- 告警修复
- 告警修复日志
- 告警接收配置
- 告警收敛规则
- 告警通知统计报表
- 语音值班配置
- 告警模拟测试
- 业务报表

## 业务监控

- zabbix模板管理
  - 模板设置
  - 绑定集群
  - 绑定具体服务器
- 插件管理



# github-spug

[github地址](https://github.com/openspug/spug)



## 主机管理
## 主机批量执行
## 主机在线终端
## 文件在线上传下载
## 应用发布部署
## 在线任务计划
## 配置中心
## 监控
## 报警

# github-CODO

[总体文档地址](https://github.com/opendevops-cn/opendevops)



## codo-admin

  基于Tornado实现，提供Restful风格的API，提供基于RBAC的完善权限管理，可对所有用户的操作进行审计 

  

## codo-cron

  基于Tornado框架实现的一套定时任务系统，完全兼容Linux Crontab支持到秒级 

  

## codo-task

  基于Tornado实现，系统核心调度，可分布式扩展 

  

## codo-cmdb

  基于Tornado实现的一套资产管理系统,

  支持AWS、阿里云、腾讯云、华为云自动拉取资产信息等 

  

## codo-kerrigan

  基于Tornado实现的一套配置中心，

  可基于分项目、环境管理配置，语法高亮、对比历史版本、快速回滚等，并提供Restful风格的API 

  

## codo-tools

  CODO运维工具支持：

  告警管理、告警自愈、项目管理、事件管理、加密解密、随机密码、提醒管理等 

  

## codo-dns

  支持多区域智能解析、可视化Bind操作、操作日志记录等。

  支持阿里云、腾讯云、DNSPod、GoDaddy等厂商的云解析







  

  