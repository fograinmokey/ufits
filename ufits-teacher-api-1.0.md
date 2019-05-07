## 孕产平台教练端
#### 提示：所有返回值均为json，状态码为http状态码，注意处理400系等状态，文档标明字段没有返回说明没有值，注意空值判断

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


### 3 我的课表
#### 3.1 根据日期获取教师课程列表; 用于教练端 我的课表首页展示
+ uri: [GET] /v1/teacher/courses/home
+ param: [Date] date 查询日期
+ resp: 200

        {
            "data": {
                "courseNum": 1, // 多少课
                "courses": [
                    {
                        "id": 13,                                       // 上课分类id
                        "timeRange": "2019-05-07 12:51 - 14:51",        // 时间段
                        "courseType": "私教课",                         // 课程类型
                        "strState": "未完成",                           // 完成状态
                        "address": "方庄妇幼保健院",                    // 场所
                        "courseName": "12节孕期瑜伽小班课"              // 标题
                    }
                ]
            }
        }
        
#### 3.2 获取课表详情; 用于教练端 我的课表首页 -> 课表详情
+ uri: [GET] /v1/teacher/courses/home/detail
+ param: [long] coachAttendClassId 上课分类id
+ resp: 200

        {
            "data": {
                "peopleNumber": 1,                                      // 上课人数
                "cardNumber": "20190416000002",                         // 学员卡号
                "studentName": "小龙女",                                // 学员名字
                "datetimeRange": "2019-05-07 12:51 - 14:51",            // 上课时间段 
                "courseType": "私教课",                                 // 课程类型
                "state": "未完成",                                      // 完成状态，已完成/未完成
                "address": "方庄妇幼保健院",                             // 上课场所
                "detailAddress": "北京市丰台区南方庄99号院",             // 上课地址
                "courseSummaryId": "courseSummaryId",                   // 课程小结id
                "customerAssessId": "customerAssessId",                 // 评估id
                "mainCoachName": "mainCoachName",                       // 主教练名
                "helpCoachName": "helpCoachName",                       // 助教名
                "attendClassContent": "attendClassContent"              // 上课内容
            }
        }
        
#### 3.3 获取查询日期的年月下的天是否有课; 用于教练端 我的课表首页日期控件展示
+ uri: [GET] /v1/teacher/courses/home/tip
+ param: [Date] queryDate 查询日期
+ resp: 200

        {
            "data": [
                {
                    "1": 0
                },
                {
                    "2": 0
                },
                {
                    "3": 0
                },
                {
                    "4": 0
                },
                {
                    "5": 0
                },
                {
                    "6": 0  // 查询所在年月中的天对应的状态，有课为1，无课为0
                },
                {
                    "7": 1
                },
                {
                    "8": 0
                },
                {
                    "9": 0
                },
                {
                    "10": 0
                },
                {
                    "11": 0
                },
                {
                    "12": 0
                },
                {
                    "13": 0
                },
                {
                    "14": 0
                },
                {
                    "15": 0
                },
                {
                    "16": 0
                },
                {
                    "17": 0
                },
                {
                    "18": 0
                },
                {
                    "19": 0
                },
                {
                    "20": 0
                },
                {
                    "21": 0
                },
                {
                    "22": 0
                },
                {
                    "23": 0
                },
                {
                    "24": 0
                },
                {
                    "25": 0
                },
                {
                    "26": 0
                },
                {
                    "27": 0
                },
                {
                    "28": 0
                },
                {
                    "29": 0
                },
                {
                    "30": 0
                },
                {
                    "31": 0
                }
            ]
        }
        
