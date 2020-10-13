# CD项目接口文档

## 1. 全局返回

::: tip code值说明
*  0 Success       请求成功  
*  1 BUSINES_ERROR 业务错误  
*  2 AUTH_FAILURE  鉴权失败  
*  3 NOT_FOUND     未发现资源  
:::

## 2.鉴权模块
### 2.1 登录
**Url:** `0`  
**Method:** `POST`  
**Header:**  
**Content-Type:** `application/json;charset=UTF-8`    
**Param:**  
```json
{
  "username":"jijiangkun",
  "password":"asdhashdkaskdhhkhaksdkjs=="
}
```
**Result:**  
```json
{
    "state": 0,
    "msg": "请求成功",
    "data": "amlqaWFuZ2t1bjEyMzQ1NjAuMzAzNTU0OTgwODY3ODQ1MDU="
}
``` 
### 2.2 登出
**Url:** `/api/auth/loginOut`  
**Method:** `POST`  
**Header:**  
**AccessToken:** `MTExODA4NzYxNTg3MjA5NDIwOV80NkRGRTRCMjAxNkU0ODZEODJBMUMzODNDNUMyNzlFMQ==`  
**Content-Type:** `application/json;charset=UTF-8`   
**Param:**  
```json
{
  "token":"MTExODA4NzYxNTg3MjA5NDIwOV80NkRGRTRCMj"
}
``` 
**Result:**  
```json
{
    "state": 0,
    "msg": "退出成功",
    "data": null
}
``` 
## 3.角色模块
### 3.1 保存(修改)角色
**Url:** `/api/authFun/role/saveRole`  
**Method:** `POST`  
**Header:**  
**Content-Type:** `application/json;charset=UTF-8`  
**AccessToken:** `MTExODA4NzYxNTg3MjA5NDIwOV80NkRGRTRCMjAxNkU0ODZEODJBMUMzODNDNUMyNzlFMQ==`  
**Param:**  
```json
{
  "rid":"1",           //传入rid为修改
  "rname":"超级管理员", //必填
  "enable":"0"         //必填
}
```
**Result:**  
```json
{
    "state": 0,
    "msg": "保存成功",
    "data": null
}
``` 
**Result:**  
```json
{
    "state": 1,
    "msg": "角色已存在",
    "data": null
}
``` 
**Error**
```json
{
    "state": 1,
    "msg": "请求参数不能为空",
    "data": null
}
``` 
### 3.2 获取角色分页
**Url:** `/api/authFun/role/pageRole`  
**Method:** `POST`  
**Header:**  
**Content-Type:** `application/json;charset=UTF-8`  
**AccessToken:** `MTExODA4NzYxNTg3MjA5NDIwOV80NkRGRTRCMjAxNkU0ODZEODJBMUMzODNDNUMyNzlFMQ==`  
**Param:**  
```json
{
  "currPage":"1",
  "pageSize":"10",
  "param":{
	  "rname":"1"    //非必填,角色名称
  }
}
```
**Result:**  
```json
{
    "state": 0,
    "msg": "请求成功",
    "data": {
        "currPage": 1,
        "pageSize": 10,
        "data": [
            {
                "rid": 1,
                "rname": "超级管理员1",
                "enable": "0",
                "rlist": []
            },
            {
                "rid": 2,
                "rname": "超级管理员1",
                "enable": "0",
                "rlist": []
            }
        ],
        "totals": 2,
        "totalPage": 1
    }
}
``` 
### 3.3 删除角色
**Url:** `/api/authFun/role/deleteRole/{rid}`  
**Method:** `GET`  
**Header:**  
**Content-Type:** `application/json;charset=UTF-8`  
**AccessToken:** `MTExODA4NzYxNTg3MjA5NDIwOV80NkRGRTRCMjAxNkU0ODZEODJBMUMzODNDNUMyNzlFMQ==`  
**Param:**  
```json
{
    "state": 0,
    "msg": "删除成功",
    "data": null
}
```
**Result:**  
```json
{
    "state": 1,
    "msg": "角色正在被使用",
    "data": null
}
``` 
### 3.4 角色关联资源
**Url:** `/api/authFun/role/saveRoleRes`  
**Method:** `POST`  
**Header:**  
**Content-Type:** `application/json;charset=UTF-8`  
**AccessToken:** `MTExODA4NzYxNTg3MjA5NDIwOV80NkRGRTRCMjAxNkU0ODZEODJBMUMzODNDNUMyNzlFMQ==`  
**Param:**  
```json
{
    "rid": 0,        //角色id
    "resId":[0,1,1]  //资源id
}
```
**Result:**  
```json
{
    "state": 0,
    "msg": "保存成功",
    "data": null
}
``` 
**Error**
```json
{
    "state": 1,
    "msg": "参数不能为空",
    "data": null
}
```  
### 3.5 获取角色资源id与默认菜单树
**Url:** `/api/authFun/role/findRoleResTree/{rid}`  
**Method:** `GET`  
**Header:**  
**Content-Type:** `application/json;charset=UTF-8`  
**AccessToken:** `MTExODA4NzYxNTg3MjA5NDIwOV80NkRGRTRCMjAxNkU0ODZEODJBMUMzODNDNUMyNzlFMQ==`  
**Result:**  
```json
{
    "state": 0,
    "msg": "请求成功",
    "data": {
        "rids": [8,7,18,9], //拥有的权限id
        "tree": [
            {
                "parentId": 0,
                "level": null,
                "path": "/",
                "treePath": null,
                "id": 7,
                "lable": "系统管理",
                "icon": "fa fa-wrench",
                "type": "0",
                "child": [
                    {
                        "parentId": 7,
                        "level": null,
                        "path": "roleList",
                        "treePath": null,
                        "id": 8,
                        "lable": "角色管理",
                        "icon": "fa fa-address-card",
                        "type": "1",
                        "child": null
                    },
                    {
                        "parentId": 7,
                        "level": null,
                        "path": "resList",
                        "treePath": null,
                        "id": 9,
                        "lable": "菜单管理",
                        "icon": "fa fa-bars",
                        "type": "1",
                        "child": null
                    }
                ]
            }
        ]
    }
}
``` 
**Error**
```json
{
    "state": 1,
    "msg": "参数不能为空",
    "data": null
}
```  
## 4.资源模块
### 4.1 保存(修改)资源
**Url:** `/api/authFun/res/saveRes`  
**Method:** `POST`  
**Header:**  
**Content-Type:** `application/json;charset=UTF-8`  
**AccessToken:** `MTExODA4NzYxNTg3MjA5NDIwOV80NkRGRTRCMjAxNkU0O`   
**Param:**  
```json
{
  "id":"1",                 //传入为修改
  "name":"资源名",           //必填
  "parentId":0,             //必填
  "enable":"0",             //必填
  "type":"1",               //必填1树2菜单路由3按钮
  "icon":"fa fa-class",     //必填图标
  "path":"admin"            //必填路由名称
}
```
**Result:**  
```json
{
    "state": 0,
    "msg": "保存成功",
    "data": null
}
``` 
**Error**
```json
{
    "state": 1,
    "msg": "参数不能为空",
    "data": null
}
``` 
```json
{
    "state": 1,
    "msg": "资源已存在",
    "data": null
}
```
### 4.2 删除资源
**Url:** `/api/authFun/res/deleteRes/{rid}`  
**Method:** `GET`  
**Header:**  
**Content-Type:** `application/json;charset=UTF-8`  
**AccessToken:** `MTExODA4NzYxNTg3MjA5NDIwOV80NkRGRTRCMjAxNkU0ODZEODJBMUMzODNDNUMyNzlFMQ==`  
**Result:**  
```json
{
    "state": 0,
    "msg": "删除成功",
    "data": null
}
``` 
**Error**
```json
{
    "state": 1,
    "msg": "资源正在使用",
    "data": null
}
```  
### 4.3 获取资源树
**Url:** `/api/authFun/res/findResTree`  
**Method:** `POST`  
**Header:**  
**Content-Type:** `application/json;charset=UTF-8`  
**AccessToken:** `MTExODA4NzYxNTg3MjA5NDIwOV80NkRGRTRCMjAxNkU0ODZEODJBMUMzODNDNUMyNzlFMQ==`  
**Result:**  
```json
{
    "state": 0,
    "msg": "请求成功",
    "data": [
        {
            "parentId": 0,
            "level": null,
            "path": "/",
            "treePath": null,
            "id": 7,
            "lable": "系统管理",
            "icon": "fa fa-wrench",
            "type": "0",
            "child": [
                {
                    "parentId": 7,
                    "level": null,
                    "path": "/",
                    "treePath": null,
                    "id": 8,
                    "lable": "角色管理",
                    "icon": "fa fa-address-card",
                    "type": "1",
                    "child": null
                },
                {
                    "parentId": 7,
                    "level": null,
                    "path": "/",
                    "treePath": null,
                    "id": 6,
                    "lable": "用户管理",
                    "icon": "fa fa-users",
                    "type": "1",
                    "child": null
                }
            ]
        }
    ]
}
``` 
### 4.4 根据父id获取下一级菜单
**Url:** `/api/authFun/res/findNextRes/{parentId}`  
**Method:** `GET`  
**Header:**  
**Content-Type:** `application/json;charset=UTF-8`  
**AccessToken:** `MTExODA4NzYxNTg3MjA5NDIwOV80NkRGRTRCMjAxNkU0ODZEODJBMUMzODNDNUMyNzlFMQ==`  
**Result:**  
```json
{
    "state": 0,
    "msg": "请求成功",
    "data": [
        {
            "parentId": 0,
            "level": null,
            "path": "/",
            "treePath": null,
            "id": 7,
            "lable": "系统管理1",
            "icon": "fa fa-wrench",
            "type": "0",
            "child": []
        },
        {
            "parentId": 0,
            "level": null,
            "path": "/",
            "treePath": null,
            "id": 7,
            "lable": "系统管理1",
            "icon": "fa fa-wrench",
            "type": "0",
            "child": []
        }
    ]
}
``` 
### 4.5 按钮级别级别资源表格  
角色相关
|  资源名称   | 资源代号  | 资源图标 |
|  ----    | ----        | ---- |
| 角色列表  | role:list   | fa fa-list-ol |
| 角色编辑  | role:update | fa fa-user-circle |
| 添加角色  | role:add    | fa fa-user-plus |
| 删除角色  | role:delete | fa fa-user-times |
| 角色授权  | role:per    | fa fa-check-square |
| 人员关联  | role:user   | fa fa-link |
资源相关
|  资源名称   | 资源代号  | 资源图标 |
|  ----    | ----        | ---- |
| 菜单列表  | res:list    | fa fa-list-ol |
| 添加菜单  | res:add     | fa fa-plus |
| 修改菜单  | res:update  | fa fa-pencil-square-o |
| 菜单删除  | res:delete  | fa fa-trash |
人员相关
|  资源名称   | 资源代号  | 资源图标 |
|  ----    | ----        | ---- |
| 人员列表  | admin:list    | fa fa-list-ol |
| 添加人员  | admin:add     | fa fa-plus-circle |
| 修改人员  | admin:update  | fa fa-pencil-square-o |
| 删除人员  | admin:delete  | fa fa-trash |
## 5.用户模块
### 5.1 保存(修改)用户
**Url:** `/api/authFun/admin/saveAdmin`  
**Method:** `GET`  
**Header:**  
**Content-Type:** `application/json;charset=UTF-8`  
**AccessToken:** `MTExODA4NzYxNTg3MjA5NDIwOV80NkRGRTRCMjAxNkU0O`    
**Param:**  
```json
{
  "id":"1",                 //传入为修改
  "username":"用户名",                    //必填
  "password":"ahshgasbasjh",             //非必填
  "enable":"0",                          //非必填
  "phone":"132-------",                  //必填
  "name":"fa fa-class",                  //必填姓名
}
```
**Result:**  
```json
{
    "state": 0,
    "msg": "保存成功",
    "data": null
}
``` 
**Error**
```json
{
    "state": 1,
    "msg": "参数不能为空",
    "data": null
}
``` 
### 5.2 获取用户分页
**Url:** `/api/authFun/admin/pageAdmin`  
**Method:** `POST`  
**Header:**  
**Content-Type:** `application/json;charset=UTF-8`  
**AccessToken:** `MTExODA4NzYxNTg3MjA5NDIwOV80NkRGRTRCMjAxNkU0O`    
**Param:**  
```json
{
  "currPage":"1",                 //当前页
  "pageSize":"30",                //分页条数
  "param":{
      "username":"user",          //用户名
      "phone":"132---",           //电话
      "name":"阿坤"               //姓名
  }
}
```
**Result:**  
```json
{
    "state": 0,
    "msg": "请求成功",
    "data": {
        "currPage": 1,
        "pageSize": 30,
        "data": [
            {
                "id": 1,
                "username": "jijiangkun",
                "name": "jjk",
                "enable": "0",
                "phone": "13289419964",
                "role": {
                    "rid": 1,
                    "rname": "超级管理员",
                    "enable": "0",
                    "rlist": [
                        {
                            "id": 5,
                            "name": "菜单管理",
                            "level": 1,
                            "parentId": 0,
                            "enable": "0",
                            "treePath": "5",
                            "type": "1",
                            "icon": "fa fa-bars",
                            "path": "/"
                        },
                        {
                            "id": 7,
                            "name": "系统管理",
                            "level": 1,
                            "parentId": 0,
                            "enable": "0",
                            "treePath": "7",
                            "type": "1",
                            "icon": "fa fa-wrench",
                            "path": "/"
                        },
                        {
                            "id": 6,
                            "name": "用户管理",
                            "level": 1,
                            "parentId": 0,
                            "enable": "0",
                            "treePath": "6",
                            "type": "1",
                            "icon": "fa fa-users",
                            "path": "/"
                        }
                    ]
                }
            },
            {
                "id": 3,
                "username": "ygt",
                "name": "ygt",
                "enable": "0",
                "phone": "132-------",
                "role": null
            }
        ],
        "totals": 2,
        "totalPage": 1
    }
}
```  
### 5.3 删除用户
**Url:** `/api/authFun/admin/deleteAdmin/{id}`  
**Method:** `GET`  
**Header:**  
**Content-Type:** `application/json;charset=UTF-8`  
**AccessToken:** `MTExODA4NzYxNTg3MjA5NDIwOV80NkRGRTRCMjAxNkU0O`    
**Result:**  
```json
{
    "state": 0,
    "msg": "删除成功",
    "data": null
}
```  
### 5.4 获取登录用户资源
**Url:** `/api/authFun/admin/findResByAdmin`  
**Method:** `POST`  
**Header:**  
**Content-Type:** `application/json;charset=UTF-8`  
**AccessToken:** `MTExODA4NzYxNTg3MjA5NDIwOV80NkRGRTRCMjAxNkU0O`  
**Param:**  
```json
{
  "token":"MTExODA4NzYxNTg3MjA5NDIw"  //必填
}
```
**Result:**  
```json
{
    "state": 0,
    "msg": "请求成功",
    "data": {
        "resList":[//资源列表
        {
            "parentId": 0,
            "level": null,
            "path": "/",
            "treePath": null,
            "id": 6,
            "title": "用户管理",
            "icon": "fa fa-users",
            "children": null
        },
        {
            "parentId": 0,
            "level": null,
            "path": "/",
            "treePath": null,
            "id": 7,
            "title": "系统管理",
            "icon": "fa fa-wrench",
            "children": null
        },
        {
            "parentId": 0,
            "level": null,
            "path": "/",
            "treePath": null,
            "id": 5,
            "title": "菜单管理",
            "icon": "fa fa-bars",
            "children": null
        }],
        "perBtn":["sys:add","res:add"]//按钮权限
        }
}
```  
### 5.5 获取登录用户信息
**Url:** `/api/authFun/admin/findAdminRole`  
**Method:** `POST`  
**Header:**  
**Content-Type:** `application/json;charset=UTF-8`  
**AccessToken:** `MTExODA4NzYxNTg3MjA5NDIwOV80NkRGRTRCMjAxNkU0O`  
**Param:**  
```json
{
  "token":"MTExODA4NzYxNTg3MjA5NDIw"  //必填
}
```
**Result:**  
```json
{
    "state": 0,
    "msg": "请求成功",
    "data": {
        "name": "jjk",
        "avatar": "http://127.0.0.1:8082/file.jpg", //头像
        "roles": [                                  //角色
            "admin"
        ],
        "introduction": ""                          //简介
    }
}
``` 
**Error**
```json
{
    "state": 1,
    "msg": "参数不能为空",
    "data": null
}
``` 
### 5.6 获取登录用户按钮权限
**Url:** `/api/authFun/admin/findAdminPerBtn`  
**Method:** `POST`  
**Header:**  
**Content-Type:** `application/json;charset=UTF-8`  
**AccessToken:** `MTExODA4NzYxNTg3MjA5NDIwOV80NkRGRTRCMjAxNkU0O`  
**Param:**  
```json
{
  "token":"MTExODA4NzYxNTg3MjA5NDIw"  //必填
}
```
**Result:**  
```json
{
    "state": 0,
    "msg": "请求成功",
    "data": {
        "name": "jjk",
        "avatar": "http://127.0.0.1:8082/file.jpg", //头像
        "roles": [                                  //角色
            "admin"
        ],
        "introduction": ""                          //简介
    }
}
``` 
**Error**
```json
{
    "state": 1,
    "msg": "参数不能为空",
    "data": null
}
``` 
### 5.7 人员关联角色
**Url:** `/api/authFun/admin/AdminLinkRole`  
**Method:** `POST`  
**Header:**  
**Content-Type:** `application/json;charset=UTF-8`  
**AccessToken:** `MTExODA4NzYxNTg3MjA5NDIwOV80NkRGRTRCMjAxNkU0O`  
**Param:**  
```json
{
  "rid":1,        //角色id,必填
  "aids":[1,2]    //人员id集合,必填
}
```
**Result:**  
```json
{
    "state": 0,
    "msg": "关联成功",
    "data": null
}
``` 
**Error**
```json
{
    "state": 1,
    "msg": "参数不能为空",
    "data": null
}
or
{
    "state": 1,
    "msg": "参数有误",
    "data": null
}
``` 
## 6.车队模块
### 6.1 保存(修改)车辆
**Url:** `/api/carFun/car/saveCar`  
**Method:** `POST`  
**Header:**  
**Content-Type:** `application/json;charset=UTF-8`  
**AccessToken:** `MTExODA4NzYxNTg3MjA5NDIwOV80NkRGRTRCMjAxNkU0O`    
**Param:**  
```json
{
    "id": 7,         //传入为修改
    "carCode": "1",  //车辆编号
    "carName": "1",  //车辆名称  
    "carType": "0"   //车辆类型
}
```
**Result:**  
```json
{
    "state": 0,
    "msg": "保存成功",
    "data": null
}
``` 
**Error**
```json
{
    "state": 1,
    "msg": "参数不能为空",
    "data": null
}
{
    "state": 1,
    "msg": "车辆已存在",
    "data": null
}
``` 
### 6.2 删除车辆
**Url:** `/api/carFun/car/deleteCar/{id}`  
**Method:** `GET`  
**Header:**  
**Content-Type:** `application/json;charset=UTF-8`  
**AccessToken:** `MTExODA4NzYxNTg3MjA5NDIwOV80NkRGRTRCMjAxNkU0O`    
**Result:**  
```json
{
    "state": 0,
    "msg": "删除成功",
    "data": null
}
``` 
## 7.自用模块
### 7.1 消息提醒列表分页
**Url:** `/api/pubFun/tm/findTipMsg`  
**Method:** `POST`  
**Header:**  
**Content-Type:** `application/json;charset=UTF-8`  
**AccessToken:** `MTExODA4NzYxNTg3MjA5NDIwOV80NkRGRTRCMjAxNkU0O`    
**Param:**  
```json
{
  "currPage":"1",
  "pageSize":"10",
  "param":{
	  "msgSign":"0",                      //读取标识,0未读,1已读  非必填
      "checkAll":"0",                     //0查自己，1查全部     非必填
      "actionTime":"2020-07-25 15:30:30", //开始时间             非必填
      "endTime":"2020-07-27 15:40:40"     //结束时间             非必填           
  }
}
```  
**Error**
```json
{
    "state": 1,
    "msg": "参数不能为空",
    "data": null
}
```  
**Result:**  
```json
{
    "state": 0,
    "msg": "请求成功",
    "data": {
        "records": [
            {
                "id": 2002,
                "optime": "2020-07-22T13:03:30.000+0000",
                "uptime": null,
                "msg": "{\"time\":\"2020-07-22 21:03:30\"}",
                "aid": 1,
                "msgSign": "0",
                "username": null,
                "checkAll": "0",
                "actionTime": null,
                "endTime": null
            }
        ],
        "total": 1030,
        "size": 10,
        "current": 1,
        "pages": 103
    }
}
``` 
