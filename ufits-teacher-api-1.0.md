## 孕产平台教练端
#### 提示：所有返回值均为json，状态码为http状态码，注意处理400状态
### 1 获取短信验证码 
+ 请求方式：GET
+ 地址：/v1/teacher/users/sms_code
+ 参数：
    + [string] phone_number
+ 响应：
    + 示例：
    
            {
                "errors": [
                    {
                        "status": "status",
                        "title": "title"
                    }
                ]
            }
            
    + 状态：status - title
       + 200 - OK
       + 400 - 手机号不符合要求
       + 404 - 用户不存在或已被禁用
    + 说明：
      + phone_number：手机号
      + status：状态码，同HTTP状态码
      + title：状态说明
      
### 2 根据小程序code登录
+ 请求方式：POST
+ 地址：/v1/teacher/users/login_from_code
+ 参数：
    + [string] code
+ 响应：
    + 示例：
    
            {
                "data": {
                    "token": "token"
                }
            }
    
    + 状态：
      + 200 - OK
    + 说明：
      + code：小程序code
      + token：登录状态标识
    
 ### 3 根据code和获取到的用户授权信息登录
 + 请求方式：POST
 + 地址：/v1/teacher/users/login_from_userinfo
 + 参数:
    
        {
            "data": {
                "code": "code",               
                "nickName": "nickName",      
                "gender": gender              
                "address": "address",        
                "avatar": "avatar",
                "phoneNum": "phoneNum",
                "phoneNumType": "phoneNumType",
                "smsCode": "smsCode"
                "iv": "iv",
                "encryptedData": "encryptedData"          
            }
        }
  
+ 响应：
    + 示例：
    
            {
                "data": {
                    "token": "token"
                }
            }
                        
    + 状态：
      + 200 - OK
    + 说明：
      + code：小程序code
      + nickName：昵称
      + gender：性别，0-女，1-男，int型
      + address：住址，为省市县等的拼装
      + avatar：头像url
      + phoneNum: 手机号
      + phoneNumType: 手机号类型，0-微信绑定手机号，1-其它手机号，2-ufits会员手机号
      + smsCode: 短信验证码，可选
      + iv：微信小程序加密算法初始向量，可选
      + encryptedData：微信小程序获取手机号加密数据，可选
      + token：登录状态标识，需要需要登录的接口时需将Authorization作为键，token值作为值放入header中，需要权限的接口皆为需要登录接口
        
### 4 通过手机号登录
+ 请求方式：POST
+ 地址：/v1/teacher/users/login_from_phone
+ 参数：
    + [string] phone_number
    + [string] sms_code
+ 响应：
    + 示例：
    
            {
                "data": {
                    "token": "token"
                }
            }
    
    + 状态：
      + 200 - OK
    + 说明：
      + phone_number：手机号
      + sms_code：短信验证码     
      + token：登录状态标识
      
### 5 获取所有项目
+ 请求方式：GET
+ 地址：/v1/teacher/projects 
+ 参数：无
+ 响应：
    + 成功示例：
    
            {
               "data": [
                   {
                       "id": id,                                    
                       "projectTitle": "projectTitle",             
                       "classTime": classTime,                             
                       "money": money,                               
                       "subProjects": [                        
                           {
                               "id": id,                          
                               "projectTitle": "projectTitle",    
                               "classTime": classTime,                    
                               "money": money                       
                           }
                       ]
                   }
               ]
           }
           
    + Unauthorized示例：
    
            {
                "errors": [
                    {
                        "status": "status",         
                        "title": "title",   
                        "detail": "detail"       
                    }
                ]
            }
            
    + 状态：
      + 200 - OK
      + 401 - Unauthorized
    + 说明：调用本接口需要教练级权限
      + id：客户来源id    
      + projectTitle：项目名称
      + classTime：课时数
      + money：项目金额
      + subProjects 子项目
      + detail：错误详情
        
### 6 获取客户来源
+ 请求方式：GET
+ 地址：/v1/teacher/customer_sources
+ 参数：无
+ 说明：调用本接口需要教练级权限，参考5状态2
+ 响应：
    + 示例：
    
            {
                "data": [
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
        
### 7 开卡
+ 请求方式：POST
+ 地址：/v1/teacher/cards
+ 参数：

        {
            "data": {               
                "phoneNumber": "17085145610",           // 手机号
                "projectId": 9,                         // 项目id
                "userName": "任盈盈",                   // 用户名
                "birthday": "1993-10-10",               // 生日
                "maternityStageTag": 3,                 // 孕产阶段标识, 0-未知，1-备孕，2-怀孕，3-产后
                "maternityDate": "2019-10-10",          // 孕产日期
                "address": "北京市丰台区南方庄22号路",   // 住址
                "money": 3000,                          // 金额
                "coachId": 3,                           // 销售教练id
                "effectiveDate": "2022-10-10",          // 卡有效期
                "customerSourceId": 5,                  // 客户来源id（子选项id）
                "payWay": 2,                            // 支付方式标识，0-大众点评，1-支付宝，2-微信，3-现金，4-刷卡，5-其他
                "placeType": 1,                         // 场内或场外标识，0-场外，1-场内
                "doorType": 1,                          // 是否上门标识，0-到店，1-上门
                "inDoorFee": 20                         // 上门费，可无，无则不显示
                "purchaseCourseNumber": 30              // 购课数
                "giveCourseNumber"：5                   // 赠课数，可无
                "comment": "comment"                    // 备注，可无
            }
        }
        
+ 说明：调用本接口需要教练级权限，参考5
+ 响应：
    + 状态：200 - OK
    + 示例
        
            {
                "errors": [
                    {
                        "status": "200",
                        "title": "OK"
                    }
                ]
            }
            
### 8 获取会员卡信息
+ 说明：需要教练权限
+ 地址：[GET]  /v1/teacher/cards/id/3
+ 参数：id - 会员卡id
+ 返回值：

        {
            "data": {
                "cardId": 27,                               // 卡id
                "cardNumber": "20190422000001",             // 卡号
                "userName": "任盈盈",                       // 用户姓名
                "phoneNumber": "17085645710",               // 手机号 
                "maternityStageTag": 3,                     // 孕产阶段, 0-未知，1-备孕，2-怀孕，3-产后
                "maternityDate": "2019-10-10",              // 孕产日期
                "birthday": "1993-10-10",                   // 生日
                "address": "北京市丰台区南方庄22号路",        // 住址
                "packageType": 0,                           // 套餐类型，0-新买课，1-续课，2-套餐升级
                "projectId": 9,                             // 项目id（有子项目使用子项目id）
                "money": 3000,                              // 金额
                "purchaseCourseNumber": 30,                 // 购课数
                "giveCourseNumber": 0,                      // 赠课数
                "remainCourseNumber": 30,                   // 剩余课数
                "inDoorFee": 0,                             // 上门费
                "payWay": 2,                                // 支付方式标识，0-大众点评，1-支付宝，2-微信，3-现金，4-刷卡，5-其他
                "effectiveDate": "2022-10-10",              // 卡有效期
                "customerSourceId": 5,                      // 客户来源id
                "coachId": 3,                               // 销售教练id
                "placeType": 1,                             // 场内或场外标识，0-场外，1-场内
                "doorType": 1,                              // 是否上门标识，0-到店，1-上门                             
                "comment": "comment",                       // 备注
                "giveCardDate": "2019-04-22",               // 发卡日期
                "cardState": 0,                             // 卡状态，0-审核中，1-正常，2-请假中，3-审核未通过
                "projectTitle": "12节孕期瑜伽小班课"         // 项目名称
            }
        }
