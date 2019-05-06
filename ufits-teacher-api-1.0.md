## 孕产平台教练端
#### 提示：所有返回值均为json，状态码为http状态码，注意处理400状态

### 1 登录
#### 1.1 获取短信验证码
+ uri: [GET] /v1/teacher/users/sms_code
+ param: [string] phone_number
+ resp: 200

        {
            "errors": [
                {
                    "status": "200", // 状态码
                    "title": "ok"    // 状态描述
                }
            ]
        }

#### 1.2 登录/注册
+ uri: [POST] /v1/teacher/users
+ param: [json]

        {
            "data": {
                "code": "code",                     // 小程序code，必填
                "iv": "iv",                         // 小程序解密向量，必填
                "encryptedData": "encryptedData",   // 小程序加密数据，必填
                "province": "province",             // 省份，可选
                "city": "city",                     // 城市，可选
                "nickName": "nickName",             // 昵称，可选
                "gender": 2,                        // 性别，可选
                "avatar": "avatar"                  // 头像，可选
            }
        }
        
+ resp: 200

        {
            "data": {
                "token": "token"
            }
        }
        
### 2 我的客户
#### 2.1 获取所有项目，含项目类型和具体项目; 用于教练端 我的客户 -> 发卡 -> 项目名称
+ uri: [GET] /v1/teacher/projects
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
