# emplatform
环保监测管理平台
# 1.em_platform-API 
# 2018/5/2
<!-- TOC -->

- [0. tips](#0-tips)
- [1. 企业用户](#1-企业用户)
  - [1.1 登录](#11-登录)
  - [1.2 档案管理](#12-档案管理)
 	 - [1.2.1. 修改档案](#121-修改档案)
 	 - [1.2.2. 查询档案](#122-查询档案)
  - [1.3 数据监测](#13-数据监测)
 	 - [1.3.1. 本企业实时数据查询](#131-修改档案)
 	 - [1.3.2. 查询本企业历史数据](#132-查询档案)
 	 - [1.3.3. 报警显示](#133-报警显示)
  - [1.4 清洗管理](#14-清洗管理)
 	 - [1.4.0. 获取某企业所有设备信息](#140-获取某企业所有设备信息)
 	 - [1.4.1. 查询历史清洗记录](#141-查询历史清洗记录)
 	 - [1.4.2. 新增清洗记录](#142-新增清洗记录)
	 - [1.4.3. 待清洗消息提醒](#143-待清洗消息提醒)
  - [1.5 异常管理](#15-修改密码)
 	 - [1.5.1. 异常查询](#151-异常查询)
 	 - [1.5.2. 异常申报](#152-异常申报)
- [2. 环保部门模块](#2-环保部门模块)

<!-- /TOC -->

# 0. tips
时间格式 unix时间戳
例子
```json
{
    "error": {
        "returnCode": 0,
        "returnMessage": "请求成功",
        "returnUserMessage": "请求成功"
    },
    "data": {
        "id": null,
        "eid": "001",
        "type": null,
        "name": "餐饮1",
        "oamCompany": "A运维",
        "level": "A",
        "equNum": "2",
        "area": "黑龙江省",
        "password": "001"
    }
}
```

---
# 1企业用户
## 1.1 登录
- POST  /basic/login  
- payload :  
```json
{  
    "account": "账号",
    "password": "密码"  
}
```
- return :
```json
{
    "error": {
        "returnCode": 0,
        "returnMessage": "请求成功",
        "returnUserMessage": "请求成功"
    }
	 "data": 
	 {
	 "account":"账号",
	 "role":"0 企业用户 1 环保部门"
        "loginResult":"success/fail"
	 }
}
```
---
## 1.2 档案管理
### 1.2.1 修改档案
- POST  /enterprise/modifyInfo  
- payload :  
```json
{  
	"eid" :"企业id",
    "type": "企业类型",
    "name":"企业名称"
    "oamCompany": "运维公司",
	"level":"餐饮级别A/B/C,企业用户不可修改,环保部门可以"
	"area":"地区",
	"password":"密码"
}
```
- return :
```json
{
    "error": {
        "returnCode": 0,
        "returnMessage": "请求成功",
        "returnUserMessage": "请求成功"
    }
	"data":null
}
```
### 1.2.2 查询档案
- POST  /enterprise/showInfo
- payload :
```json
{
    "eid": "账号",
}
```
- return :
```json
{
    "error": {
        "returnCode": 0,
        "returnMessage": "请求成功",
        "returnUserMessage": "请求成功"
    }
	"data": {
        "eid": "001",
        "type": "类型",
        "name": "餐饮1",
        "oamCompany": "A运维",
        "level": "A",
        "equNum": "2",
        "area": "黑龙江省",
    }
}
```
### 1.2.3 新增环保设施

- POST   /equipment/addEquipment
```json{
{
    "eid": "企业id ",
    "equId": "设施id 可以传多个以‘,’分隔 或者传单个id",
}
```
---
## 1.3 数据监测
### 1.3.1 本企业实时数据查询
socket长连接
待定。
### 1.3.2 查询本企业历史设施数据
- POST  /equipmentFlow/showDataByEid
- payload :
```json{
    "eid": "账号必须",
	"startTime":"起始时间设默认时间",
	"endTime":"结束时间至今"
	"isRegular":"是否正常0正常 1 不正常"
}
```
- return :
```json
{
    "error": {
        "returnCode": 0,
        "returnMessage": "请求成功",
        "returnUserMessage": "请求成功"
    }

	"data": {
        "ename": "企业名称",
        "eid": "企业id",
        "equId": "设施id",
        "state": "设施状态值",
        "time": "时间",
    },{},{}
}
```
### 1.3.3 异常数据报警提醒
长连接
待定
---
## 1.4 清洗管理
### 1.4.0 获取某企业所有设备信息
- POST  /equipment/showEquData
- payload :
```json
{
    "eid": "企业账号必传",
}
```
- return :
```json
{
    "error": {
        "returnCode": 0,
        "returnMessage": "请求成功",
        "returnUserMessage": "请求成功"
    }
	"data": {
        "ename": "企业名称",
        "eid": "企业id",
        "equId": "设施id",
    },{},{}
}
```
### 1.4.1 查询历史清洗记录
- POST  /equipmentFlow/showEquCleanData
- payload :
```json
{
    "eid": "企业账号必传",
	"equId":"设备账号选传",
	"startTime":"开始时间 不选传个默认值"
	"endTime":"结束时间不选 传至今"
}
```
- return :
```json
{
    "error": {
        "returnCode": 0,
        "returnMessage": "请求成功",
        "returnUserMessage": "请求成功"
    }
	"data": {
	{
        "ename": "企业名称",
        "eid": "企业id",
        "equId": "设施id",
        "cleanTime": "时间",
	"reason":"清洗原因"},
	{}
    }
}
```
### 1.4.2 新增清洗记录
- POST  /equipmentFlow/showEquCleanData
- payload :
```json
{
    "eid": "企业账号必传",
	"equId":"设备账号选传",
	"cleanTime":"开始时间 不选传当前时间"
	"reason":"清洗原因选传"
}
```
- return :
```json
{
    "error": {
        "returnCode": 0,
        "returnMessage": "请求成功",
        "returnUserMessage": "请求成功"
    }
	"data":null
}
```
### 1.4.3 待清洗消息提醒
长连接 待定
---
## 1.5 异常管理
### 1.5.1 异常查询
- POST  /abnormal/showAbnormalData
- payload :
```json
{
    "eid": "企业账号必传 可多传，号分隔",
	"equId":"设备账号选传",
	"startTime":"开始时间 不选传个默认值",
	"endTime":"结束时间不选 传至今",
	"isdeal":"是否处理完毕 0 未处理 1 处理 2都要"
	}
```
- return :
```json
{
    "error": {
        "returnCode": 0,
        "returnMessage": "请求成功",
        "returnUserMessage": "请求成功"
    }
	"data": {
	{
	"recordId":"异常记录编号",
        "ename": "企业名称",
        "eid": "企业id",
        "equId": "设施id",
        "abnormalReason": "异常原因",
	"isdeal":"是否处理完毕 同上"
	"createTime":"发生时间"，
	"dealTime":"当未处理时为0 处理时间"},
	{}
    }
}
```
### 1.5.2 异常申报
- POST  /abnormal/dealAbnormal
- payload :
```json
{	
	"recordId":"异常记录编号",
	"equId": "设施id",
	"abnormalReason": "异常原因 选传",
	"dealTime":"处理时间选传 需在异常发生时间之后 默认当前时间",
	}
```
- return :
```json
{
    "error": {
        "returnCode": 0,
        "returnMessage": "请求成功",
        "returnUserMessage": "请求成功"
    }
	"data": null
}
```
---
# 2 环保部门模块
## 2.1 登录
- POST  /basic/login  
- payload :  
```json
{  
    "account": "账号",
    "password": "密码"  
}
```
- return :
```json
{
    "error": {
        "returnCode": 0,
        "returnMessage": "请求成功",
        "returnUserMessage": "请求成功"
    }
	 "data": 
	 {
	 "account":"账号"，
	 "role":"0 企业用户 1 环保部门"
	 }
}
```
---
## 2.2 数据监测
### 2.2.1 实时查询
长连接
### 2.2.2 历史数据查询
同企业接口
---
##  2.3 档案管理
### 2.3.1 档案查询
可查询所有企业档案
- Get  /enterprise/showAllInfo
- payload :
```json
{
}
```
- return :
```json
{
    "error": {
        "returnCode": 0,
        "returnMessage": "请求成功",
        "returnUserMessage": "请求成功"
    }
	"data": {
	{   "eid": "001",
        "type": "类型",
        "name": "餐饮1",
        "oamCompany": "A运维",
        "level": "A",
        "equNum": "2",
        "area": "黑龙江省",
	},
	{	"eid": "001",
        "type": "类型",
        "name": "餐饮1",
        "oamCompany": "A运维",
        "level": "A",
        "equNum": "2",
        "area": "黑龙江省",}
    }
}
```
/根据条件检索 同企业接口
### 2.3.2 档案修改
同企业接口
### 2.3.3 新增企业档案
- POST  /enterprise/addEnterprise  
- payload :  
```json
{  
	"eid" :"企业id",
    "type": "企业类型",
	"name":"企业名称"
    "oamCompany": "运维公司",
	"level":"餐饮级别A/B/C",
	"area":"地区",
	"password":"密码"
}
```
- return :
```json
{
    "error": {
        "returnCode": 0,
        "returnMessage": "请求成功",
        "returnUserMessage": "请求成功"
    }
	"data":null
}
```

---
## 2.4 清洗管理
清洗记录查询 同企业接口
## 2.5 异常管理
异常记录查询 同企业接口
## 2.6 执法统计
### 2.6.1 新增执法记录
- POST  /lawEnforcementRecord/addRecord
```json
{    
    "environmentalId": "环保人员id ",
    "ename": "被监督企业名称",
    "eid": "被监督企业id",
    "time": "执法时间",
    "lawEnforcementResult":"执法结果 文字",
}
```
- return :
```json
{
    "error": {
        "returnCode": 0,
        "returnMessage": "请求成功",
        "returnUserMessage": "请求成功"
    }
	"data":"1 插入成功"
}
```
---
### 2.6.2 执法记录查询
- POST  /lawEnforcementRecord/showRecord
- payload :
```json
{
    "environmentalId": "环保人员id 选传",
        "eid": "被监督企业id 选传",
	"startTime":"开始时间 不选传个默认值",
	"endTime":"结束时间不选 传至今",
	}
```
- return :
```json
{
    "error": {
        "returnCode": 0,
        "returnMessage": "请求成功",
        "returnUserMessage": "请求成功"
    }
	"data": {
        {
	"environmentalId":"环保人员id",
	"recordId":"记录编号"	
	"ename": "被监督企业名称",
        "eid": "被监督企业id",
	"envName":"执法部门名称",	
        "time": "执法时间",
        "lawEnforcementResult": "执法结果"},
	{}
    }
}
```
---
### 2.6.1 修改执法记录
- POST  /lawEnforcementRecord/modifyRecord
```json
{   
	"recordId":"记录编号"，	
   	"environmentalId": "环保人员id ",
    	"eid": "被监督企业id",
   	"time": "执法时间",
    	"lawEnforcementResult": "执法结果 文字",
}
```
- return :
```json
{
    "error": {
        "returnCode": 0,
        "returnMessage": "请求成功",
        "returnUserMessage": "请求成功"
    }
	"data":null
}
```
---
