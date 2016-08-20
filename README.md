#MeishanServer
###眉山检察院项目

####Test HOST URL: http://192.168.1.20:8080
####Final HOST  URL: 内网IP地址

####登录之后会产生一个`Token`,在之后的请求中需要`携带Token`来进行操作
####所有返回数据的格式均为json


##接口说明

----
##登录接口 POST Tested
####URL
	/user/login
####Request
名称|类型|说明
---|---|---
username|string|用户名
password|string|密码

####Response
名称|类型|说明
---|---|---
errCode|int|错误码(0:成功登录、1:失败登录)
msg|string|错误信息
token|string|登录凭证

----
##新建主表接口 POST Tested
####URL
	/form/create
####Request
名称|类型|说明
---|---|---
token|string|登陆凭证
zone|string|地区(3字符)
year|string|年(4字符)
category|char|分类(1字符)

####Response	
名称|类型|说明
---|---|---
errCode|int|错误码(0:成功、1:失败)
msg|string|错误信息
account|string|主表账号

----
##上传附件 POST Tested
####URL
	/form/upload_attachfile
####Request
名称|类型|说明
---|---|---
account|string|账号
token|string|登录凭证
attach|file|附件文件

####Response
名称|类型|说明
---|---|---
errCode|int|错误码(0:成功、1:失败)
msg|string|错误信息


----
##上传附表 POST Tested
####URL
	/form/upload_attachform
####Request
名称|类型|说明
---|---|---
account|string|账号
token|string|登陆凭证
attach|file|附表文件

####Response
名称|类型|说明
---|---|---
errCode|int|错误码(0:成功、1:失败)
msg|string|错误信息


----
##取消附表 POST Tested
####URL
	/form/remove
####Request
名称|类型|说明
---|---|---
account|string|账号
token|string|登陆凭证
id|string|附表id

####Response
名称|类型|说明
---|---|---
errCode|int|错误码(0:成功、1:失败)
msg|string|错误信息



----
##查询接口 GET Tested
####URL
	/form/search
####Request
名称|类型|说明|是否必须
---|---|---|---
token|string|登录凭证|是
name|string|姓名搜索|否
account|string|账号搜索|否
id_card|string|身份证搜索|否
start_time|date|起始时间|否
end_time|date|结束时间|需要有start_time

####Response
名称|类型|说明
---|---|---
errCode|int|错误码(0:成功、1:失败)
msg|string|错误信息
data|list|列表所需的form_object

####form_object
名称|类型|说明
---|---|---
name|string|姓名
account|string|账号
id_card|string|身份证号
release_date|date|刑满日期



----
##获取检查表数据接口 POST Tested
####URL
	/form/show
####Request
名称|类型|说明|是否必须
---|---|---|---
token|string|登录凭证|是
account|string|账号搜索|否

####Response
名称|类型|说明
---|---|---
msg|string|操作结果
data|string|很长的主表字符串
other|list<string>|附表地址列表
attach|list<{string,string}>|附件列表

####attach object
名称|类型|说明
---|---|---
name|string|文件名
url|string|下载链接

----
##修改接口 POST Tested
####URL
	/form/modify
####Request
名称|类型|说明|是否必须
---|---|---|---
token|string|登录凭证|是
account|string|账号搜索|否

####Response



----
##导出接口 GET Depricated
####URL
	/form/export
####Request
名称|类型|说明
---|---|---
token|string|登录凭证
account|string|检查表账号

####Response
名称|类型|说明
---|---|---
errCode|int|错误码(0:成功、1:失败)
msg|string|错误信息
url|string|导出文件地址



----
##用户列表 GET Tested
####URL
	/user/list
####Request
名称|类型|说明
---|---|---
token|string|登录凭证	
####Response
名称|类型|说明
---|---|---
errCode|int|错误码(0:成功、1:失败)
msg|string|错误信息
data|list|用户信息列表

####User Object
名称|类型|说明
---|---|---
user_id|string|用户id
account|string|用户账号
zone|string|地区
username|string|用户名
job|string|职务
permission|int|权限



----
##用户删除 POST Tested
####URL
	/user/remove
####Request
名称|类型|说明
---|---|---
token|string|登录凭证	
user_id|string|用户id
####Response
名称|类型|说明
---|---|---
errCode|int|错误码(0:成功、1:失败)
msg|string|错误信息



----
##用户创建 POST Tested
####URL
	/uesr/create
####Request
名称|类型|说明
---|---|---
token|string|登录凭证	
account|string|账号
username|string|用户名
password|string|密码
zone|string|地区
job|string|职位
permission|int|权限


----
##查看罚金总数 POST Tested
####URL
    form/fines
####Request
名称|类型|说明
---|---|---
token|string|登录凭证	
start_time|date|开始时间戳
end_time|date|结束时间戳

####Response
名称|类型|说明
---|---|---
errCode|int|错误码(0:成功、1:失败)
msg|string|错误信息
fines|array<财产刑罚金,没收财产,服刑期间履行,机关纠正执行>|罚金数列表


----
##查看已经释放但是没有交完罚款的列表 POST Tested
####URL
    /notify
####Request
名称|类型|说明
---|---|---
token|string|登录凭证	

####Response
名称|类型|说明
---|---|---
errCode|int|错误码(0:成功、1:失败)
msg|string|错误信息
data|array<姓名,账号,释放日期,省份证号>|账号列表



----
##将某个主表标记为交清罚款 POST Tested
####URL
    /charge
####Request
名称|类型|说明
---|---|---
token|string|登录凭证	
account|string|账号

####Response
名称|类型|说明
---|---|---
errCode|int|错误码(0:成功、1:失败)
msg|string|信息



----
##模糊查询 POST Tested
####URL
    /advanced_search
####Request
名称|类型|说明
---|---|---
token|string|登录凭证	
category|char|分类
year|int|年(4位)
zone|string|地区(3位)

####Response
名称|类型|说明
---|---|---
errCode|int|错误码(0:成功、1:失败)
msg|string|信息
data|<list,fines>|信息

list:用户信息数组<姓名,账号,身份证号,释放日期>
fines:罚金统计<财产刑罚金,没收财产,服刑期间履行,机关纠正执行>
