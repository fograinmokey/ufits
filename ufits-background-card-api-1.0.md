## 孕产平台 卡管理
#### 友情提示：所有返回值均为json，状态码为http状态码，注意处理400系等状态，文档标明字段没有返回说明没有值，注意空值判断

### 1 开卡
#### 1.1 通过手机号或客户名搜索客户
    用于后台管理 会员卡管理 -> 开卡 -> 开卡用户
+ uri: 

        [GET] /v1/teacher/users/search
        
+ param: 二填一

        [string] phoneNum 手机号
        [string] customerName 学员名
        
+ resp: 200

        {
            "data": [
                {
                    "id": 25,                                                              // 学员id
                    "realName": "张小芳",                                                  // 学员名
                    "firstLetter": "Z",                                                    // 学员名首字母
                    "gender": 0,                                                           // 学员性别：0：女，1：男
                    "phoneNum": "17085145711",                                             // 学员手机号
                    "avatar": "https://wx.qlogo.cn/mmopen/vi_32/Q0jEEV45pl84k94gw/0",      // 学员头像
                    "state": 0,                     // 状态，0：审核中，1：正常，2：请假中，3：审核未通过
                    "otherAddCoachName": "ycl"     // 其他添加教练的名字，可空，非空则显示 "某某添加"，否则不显示
                }
            ]
        }
                            
#### 1.2 获取所有项目，含项目类型和具体项目
    用于后台管理 会员卡管理 -> 开卡 -> 项目选择
+ uri: 

        [GET] /v1/teacher/projects
    
+ param: 无
+ resp: 200

        {
            "data": [
                {
                    "id": 1,                                        // 项目类型id
                    "projectTitle": "免费体验课",                    // 项目类型名
                    "subProjects": [
                        {
                            "id": 17,
                            "projectTitle": "免费体验课子项1",
                            "classTime": 3,                         // 课时数
                            "money": 0                              // 金额
                        }
                    ]
                },
                {
                    "id": 2,
                    "projectTitle": "收费体验课",
                    "subProjects": [
                        {
                            "id": 18,
                            "projectTitle": "收费体验课子项1",
                            "classTime": 5,
                            "money": 300
                        },
                        {
                            "id": 19,
                            "projectTitle": "收费体验课子项2",
                            "classTime": 4,
                            "money": 0
                        }
                    ]
                },
                {
                    "id": 3,
                    "projectTitle": "孕期瑜伽小班课",
                    "subProjects": [
                        {
                            "id": 15,
                            "projectTitle": "孕期瑜伽小班课子项1",
                            "classTime": 10,
                            "money": 1500
                        }
                    ]
                },
                {
                    "id": 4,
                    "projectTitle": "孕产套课",
                    "subProjects": [
                        {
                            "id": 16,
                            "projectTitle": "孕产套课子项1",
                            "classTime": 40,
                            "money": 6000
                        }
                    ]
                }
            ]
        }
            
#### 1.3 获取所有教练
    用于后台管理 会员卡管理 -> 开卡 -> 销售教练/合作教练的选择
+ uri: 

        [GET] /v1/teacher/users/all-teachers
        
+ param: 无
+ resp: 200

        {
            "data": [
                {
                    "id": 4,                                            // 教练id
                    "realName": "小高",                                 // 姓名
                    "jobTitle": "助教",                                 // 职称
                    "photo": "http://static.mif61140065189888.jpg",     // 照片
                    "phoneNum": "18611194890",                          // 手机
                    "gender": 0,                                        // 性别：0：女，1：男
                    "firstLetter": "X"                                  // 姓大写首字母
                }
            ]
        }
        
#### 1.4 开卡
    用于后台管理 会员卡管理 -> 开卡
+ uri: 

        [GET] /v1/teacher/cards
        
+ param: json

        {
            "data": {
               "userId": 2,                             // 学员id               
               "userName": "黄蓉",                      // 学员名
               "packageType": 0,                        // 套餐类型，0：新买课，1：续课，2，套餐升级
               "projectId": 18,                         // 项目id（子项目）
               "money": 600,                            // 金额
               "purchaseCourseNumber": 5,               // 购课数
               "giveCourseNumber": 1,                   // 赠课数
               "inDoorFee": 5,                          // 上门费
               "payWay": 2,                             // 支付方式，0：大众点评，1：支付宝，2：微信，3：现金，4：刷卡，5：其他
               "effectiveDate": "2020-04-20",           // 卡有效期
               "coachId": 5,                            // 销售教练id
               "cooperationCoach": {
                    "26": "李四"                        // 合作教练id和名字
               },
               "placeType": 0,                          // 场内外，0：场外，1：场内
               "doorType": 1,                           // 是否有上门，0：否，1：是
               "comment": "no comment"                  // 备注
            }
        }
        
+ resp: 

        {
            "errors": [
                {
                    "status": "200",
                    "title": "OK"
                }
            ]
        }                         
         
#### 1.5 修改卡
    用于后台管理 会员卡管理 -> 修改
+ uri: 

        [PUT] /v1/teacher/cards/42
        
+ param: 

        [long] id 卡id
        
        {
            "data": {
               "userId": 2,                             // 学员id               
               "userName": "黄蓉",                      // 学员名
               "packageType": 0,                        // 套餐类型，0：新买课，1：续课，2，套餐升级
               "projectId": 18,                         // 项目id（子项目）
               "money": 600,                            // 金额
               "purchaseCourseNumber": 5,               // 购课数
               "giveCourseNumber": 1,                   // 赠课数
               "inDoorFee": 5,                          // 上门费
               "payWay": 2,                             // 支付方式，0：大众点评，1：支付宝，2：微信，3：现金，4：刷卡，5：其他
               "effectiveDate": "2020-04-20",           // 卡有效期
               "coachId": 5,                            // 销售教练id
               "cooperationCoach": {
                    "26": "李四"                        // 合作教练id和名字
               },
               "placeType": 0,                          // 场内外，0：场外，1：场内
               "doorType": 1,                           // 是否有上门，0：否，1：是
               "comment": "no comment"                  // 备注
            }
        }
        
+ resp: 200

        {
            "errors": [
                {
                    "status": "200",
                    "title": "OK"
                }
            ]
        }
        
#### 1.6 删除一张会员卡
    用于后台管理 会员卡管理 -> 删除操作
+ uri: 
        
        [DELETE] /v1/teacher/cards/{id}
        
+ param: 

        [long] id 卡id
        
+ resp: 204

        {
            "errors": [
                {
                    "status": "204",
                    "title": "No Content"
                }
            ]
        }
        
#### 1.7 根据卡号获取学员信息
    用于后台管理 会员卡管理 -> 点击表格中的卡号
+ uri: 

        [GET] /users/student
        
+ param:

        [string] cardNum 卡号
        
+ resp: 200
        
        {
            "data": {
                "cardNum": "cardNum",               // 卡号
                "projectTitle": "projectTitle",     // 套餐类型(项目名称)
                "classTime": 40.5,                  // 课时数
                "remainingClassTime": 10.3,         // 剩余课时数
                "giftClassTime": 2,                 // 赠送课时
                "getCardDate": "2019-05-17",        // 发卡时间
                "effectiveDate": "2020-10-10",      // 有效时间
                "studentName": "abc",               // 学员姓名
                "phoneNum": "27084159673",          // 学员手机号
                "salespersonName": "efg",           // 销售教练
                "gender": 1,                        // 性别：0：女，1：男
                "address": "address",               // 学员住址
                "avatar": "avatar"                  // 学员头像
            }
        }                                                                                                                                 
