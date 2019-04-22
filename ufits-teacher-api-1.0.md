## 孕产平台教练端
#### 提示：所有返回值均为json，状态码为http状态码
### 1 获取短信验证码 
+ 请求方式：GET
+ 地址：/v1/teacher/users/sms_code?phone_number=phone_number
+ 参数：
    + [string] phone_number - 手机号
+ 响应：
    + 状态1：200 - OK
    
        {
            "errors": [
                {
                    "status": "200",
                    "title": "OK"
                }
            ]
        }
        
    + 状态2：400 - Bad Request
    
        {
            "errors": [
                {
                    "status": "400",
                    "title": "手机号不符合要求"
                }
            ]
        }
        
    + 状态2：404 - Not Found
    
        {
            "errors": [
                {
                    "status": "404",
                    "title": "用户不存在或已被禁用"
                }
            ]
        }
        
### 2 根据小程序code登录
+ 请求方式：POST
+ 地址：/v1/teacher/users/login_from_code?code=code
+ 参数：
    + [string] code - 小程序code
+ 响应：
    + 状态1：200 - OK
    
        {
            "data": {
                "token": "token"    // 登录状态
            }
        }
    
 ### 3 根据code和获取到的用户授权信息登录
 + 请求方式：POST
 + 地址：/v1/teacher/users/login_from_userinfo
 + 参数：json
 
    {
        "data": {
            "code": "code",                 // 小程序code
            "phoneNumber": "phoneNumber",   // 手机号
            "nickName": "nickName",         // 昵称
            "gender": gender                // 性别，0-女，1-男，int型
            "address": "address",           // 住址
            "avatar": "avatar",             // 头像url
        }
    }
  
 + 响应：
    + 状态1：200 - OK
        
        {
            "data": {
                "token": "token"    // 登录状态
            }
        }
        
### 4 通过手机号登录
+ 请求方式：POST
+ 地址：/v1/teacher/users/login_from_phone
+ 参数：
    + [string] phone_number - 手机号
    + [string] sms_code - 短信验证码
+ 响应：
    + 状态1：200 - OK
        
        {
            "data": {
                "token": "token"
            }
        }
        
### 5 获取所有项目
+ 请求方式：GET
+ 地址：/v1/teacher/projects
+ 参数：无
+ 说明：调用本接口需要教练级权限
+ 响应：
    + 状态1：200 - OK
       
       {
           "data": [
               {
                   "id": 2,                                     // 客户来源id
                   "projectTitle": "收费体验课",                 // 项目名称
                   "classTime": 0,                              // 课时数
                   "money": 0,                                  // 项目金额
                   "subProjects": [                             // 子项目
                       {
                           "id": 10,                            // 子项目id
                           "projectTitle": "2节收费体验课",     // 子项目名称
                           "classTime": 14,                     // 子项目课时数
                           "money": 9600                        // 子项目金额
                       }
                   ]
               },
               {
                   "id": 1,
                   "projectTitle": "免费体验课",
                   "classTime": 0,
                   "money": 0,
                   "subProjects": [
                       {
                           "id": 11,
                           "projectTitle": "1节免费体验课",
                           "classTime": 1,
                           "money": 0
                       }
                   ]
               }
           ]
       }
       
    + 状态2：401 - Unauthorized
    
        {
            "errors": [
                {
                    "status": "401",            // 响应状态码
                    "title": "Unauthorized",    // 状态描述
                    "detail": "detail"          // 错误详情
                }
            ]
        }
        
### 6 获取客户来源
+ 请求方式：GET
+ 地址：/v1/teacher/customer_sources
+ 参数：无
+ 说明：调用本接口需要教练级权限，参考5状态2
+ 响应：
    + 状态1：200 - OK
    
        {
            "data": [
                {
                    "id": 3,
                    "sourceTitle": "线上"
                },
                {                                           // 第一级为来源类别
                    "id": 2,                                // 来源id
                    "sourceTitle": "医院",                  // 来源名称 
                    "subCustomerSource": [                  // 第二级为具体来源
                        {                                   
                            "id": 5,                        // 具体来源id
                            "sourceTitle": "协和医院"       // 具体来源名称
                        }
                    ]
                }
            ]
        }
