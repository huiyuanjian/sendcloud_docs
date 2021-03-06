
开发者利用**模板**, 可以方便的为不同用户批量发送相似内容.

通过 API 可以对邮件模板进行查询, 添加, 删除, 修改操作.
    
- - -        

##查询 ( 批量查询 )

返回邮件模板的基本信息
    
**URL**    
```
http://api.sendcloud.net/apiv2/template/list
```
    
**HTTP请求方式**
```bash
post    get
```
    
**参数说明**    
    
|参数|类型|必须|说明|
|:---|:---|:---|:---|
|apiUser|string|是|API_USER|
|apiKey|string|是|API_KEY|
|invokeName|string|否|邮件模板调用名称|
|templateType|int|否|邮件模板类型: 0(触发), 1(批量)|
|templateStat|int|否|邮件模板状态: -2(未提交审核), -1(审核不通过), 0(待审核), 1(审核通过)|
|start|int|否|查询起始位置, 取值区间 [0-], 默认为 0|
|limit|int|否|查询个数, 取值区间 [0-100], 默认为 100|
    
    
**请求示例**
```
http://api.sendcloud.net/apiv2/template/list?apiUser=***&apiKey=***&start=0&limit=3&templateStat=1
```
    
**返回值说明**
    
|参数|说明|
|:---|:---|
|name|邮件模板名称|
|invokeName|邮件模板调用名称|
|templateType|模板类型|
|templateStat|审核状态|
|gmtCreated|邮件模板创建时间|
|gmtModified|邮件模板修改时间|

**返回值示例**
```
{
  "info": {
    "dataList": [
      {
        "name": "ifaxin账单",
        "invokeName": "***",
        "templateType": 1,
        "templateStat": 1,
        "gmtCreated": "2013-11-21 16:37:41",
        "gmtUpdated": "2015-06-12 19:44:07"
      },
      {
        "name": "ifaxin密码找回",
        "invokeName": "***",
        "templateType": 0,
        "templateStat": 1,
        "gmtCreated": "2013-11-21 16:39:53",
        "gmtUpdated": "2013-11-21 16:39:53"
      }
    ],
    "total": 42,
    "count": 2
  },
  "statusCode": 200,
  "message": "请求成功",
  "result": true
}
```

- - -        

##查询

返回邮件模板的详细信息
    
**URL**    
```
http://api.sendcloud.net/apiv2/template/get
```
    
**HTTP请求方式**
```bash
post    get
```
    
**参数说明**    
    
|参数|类型|必须|说明|
|:---|:---|:---|:---|
|apiUser|string|是|API_USER|
|apiKey|string|是|API_KEY|
|invokeName|string|是|邮件模板调用名称|
    
**请求示例**
```
http://api.sendcloud.net/apiv2/template/get?apiUser=***&apiKey=***&invokeName=test
```
    
**返回值说明**
    
|参数|说明|
|:---|:---|
|name|邮件模板名称|
|invokeName|邮件模板调用名称|
|templateType|模板类型|
|templateStat|审核状态|
|gmtCreated|邮件模板创建时间|
|gmtModified|邮件模板修改时间|
|html|模板内容|
|contentSummary|邮件摘要|
|subject|模板标题|

**返回值示例**
```
{
  "statusCode": 200,
  "info": {
    "data": {
      "name": "SendCloud测试样本",
      "invokeName": "15_invoke_2",
      "templateType": 0,
      "templateStat": 1,
      "gmtCreated": "2015-02-02 17:01:43",
      "gmtUpdated": "2015-04-16 15:04:12",
      "html": "<p>你太棒了！你已成功的从SendCloud发送了一封测试邮件，接下来快登录前台去完善账户信息吧！12</p>\n",
      "subject": "来自SendCloud的第一封邮件！",
	  "contentSummary":"shesh"
    }
  },
  "message": "请求成功",
  "result": true
}
```

- - -
    
##添加
    
**URL**    
```
http://api.sendcloud.net/apiv2/template/add
```
    
**HTTP请求方式**
```bash
post    get
```
    
|参数|类型|必须|说明|
|:---|:---|:---|:---|
|apiUser|string|是|API_USER|
|apiKey|string|是|API_KEY|
|invokeName|string|是|邮件模板调用名称|
|name|string|是|邮件模板名称|
|html|string|是|html格式内容|
|text|string|否|text格式内容|
|subject|string|是|模板标题|
|templateType|int|是|邮件模板类型: 0(触发), 1(批量)|

提示: 

1. html 内容中可以使用[变量](../guide/base.md#_4)
2. html 内容过长或有特殊字符应使用 post 请求
3. 模板个数最多为 1000 个
     
**请求示例**
```
curl -d 'apiUser=***&apiKey=***&invokeName=testtemplate&name=test&html=<p>add new template</p>&subject=test_subject&templateType=1' http://api.sendcloud.net/apiv2/template/add
```
 
**返回值说明**
    
|参数|说明|
|:---|:---|
|name|邮件模板名称|
|invokeName|邮件模板调用名称|
|templateType|模板类型|
|templateStat|审核状态|
|gmtCreated|邮件模板创建时间|
|gmtModified|邮件模板修改时间|
|html|模板内容|
|subject|模板标题|
    
**返回值示例**
```
{
  "statusCode": 200,
  "info": {
    "data": {
      "name": "test",
      "invokeName": "testtemplate",
      "templateType": 0,
      "templateStat": 0,
      "gmtCreated": "2015-10-16 10:42:01",
      "gmtUpdated": "",
      "html": "<p>add new template</p>",
      "subject": "test_subject"
    }
  },
  "message": "请求成功",
  "result": true
}
```
 
- - -
    
##删除
    
**URL**    
```
http://api.sendcloud.net/apiv2/template/delete
```
    
**HTTP请求方式**
```bash
post    get
```
    
**参数说明**    
    
|参数|类型|必须|说明|
|:---|:---|:---|:---|
|apiUser|string|是|API_USER|
|apiKey|string|是|API_KEY|
|invokeName|string|是|邮件模板调用名称|
    
**请求示例**
```
curl http://api.sendcloud.net/apiv2/template/delete?apiUser=***&apiKey=***&invokeName=test
```
    
**返回值说明**
    
|参数|说明|
|:---|:---|
|count|成功删除的邮件模板个数|    
    
**返回值示例**
```
{
  "statusCode": 200,
  "message": "请求成功",
  "result": true,
  "info": {
    "count": 1
  }
}

```
 
- - -
    
##修改
    
用于修改模板的名称, 内容, 主题, 模板类型

**URL**    
```
http://api.sendcloud.net/apiv2/template/update
```
    
**HTTP请求方式**
```bash
post    get
```

|参数|类型|必须|说明|
|:---|:---|:---|:---|
|apiUser|string|是|API_USER|
|apiKey|string|是|API_KEY|
|invokeName|string|是|邮件模板调用名称|
|name|string|否|邮件模板名称|
|html|string|否|html格式内容|
|subject|string|否|模板标题|
|templateType|int|否|邮件模板类型: 0(触发), 1(批量)|

提示: 

1. html 内容中可以使用[变量](index.md#_2)
2. html 内容过长或有特殊字符应使用 post 请求
    
**请求示例**
```
curl -d 'apiUser=***&apiKey=***&invokeName=testtemplate&name=test&html=<p>update template</p>&subject=test&templateType=1' http://api.sendcloud.net/apiv2/template/update
```
    
**返回值说明**
    
|参数|说明|
|:---|:---|
|count|成功修改的模板个数|
    
**返回值示例**
```
{
  "statusCode": 200,
  "message": "请求成功",
  "result": true,
  "info": {
    "count": 1
  }
}
```

    


