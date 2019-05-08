## 孕产平台教练端
#### 友情提示：所有返回值均为json，状态码为http状态码，注意处理400系等状态，文档标明字段没有返回说明没有值，注意空值判断

### 1 登录
#### 1.1 获取短信验证码
+ uri: 

        [GET] /v1/teacher/users/sms_code
        
+ param: 

        [string] phone_number 手机号
        
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
+ uri: 

        [POST] /v1/teacher/users
        
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
#### 2.1 获取所有项目，含项目类型和具体项目
    用于教练端 我的客户 -> 发卡 -> 项目名称
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


### 3 我的课表
#### 3.1 根据日期获取教师课程列表
    用于教练端 我的课表首页展示
+ uri: 

        [GET] /v1/teacher/courses/home
        
+ param: 

        [Date] date 查询日期，如：2019/05/07
        
+ resp: 200

        {
            "data": {
                "courseNum": 1, // 多少课
                "courses": [
                    {
                        "id": 13,                                       // 上课分类id
                        "timeRange": "2019-05-07 12:51-14:51",        // 时间段
                        "courseType": "私教课",                         // 课程类型
                        "strState": "未完成",                           // 完成状态
                        "address": "方庄妇幼保健院",                    // 场所
                        "courseName": "12节孕期瑜伽小班课"              // 标题
                    }
                ]
            }
        }
        
#### 3.2 获取课表详情
    用于教练端 我的课表首页 -> 课表详情
+ uri: 

        [GET] /v1/teacher/courses/home/detail
        
+ param: 

        [long] coachAttendClassId 上课分类id
        
+ resp: 200

        {
            "data": {
                "peopleNumber": 1,                                      // 上课人数
                "cardNumber": "20190416000002",                         // 学员卡号
                "studentName": "小龙女",                                // 学员名字
                "datetimeRange": "2019-05-07 12:51-14:51",            // 上课时间段 
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
        
#### 3.3 获取查询日期的年月下的天是否有课
    用于教练端 我的课表首页日期控件展示
+ uri: 

        [GET] /v1/teacher/courses/home/tip
        
+ param: 

        [Date] queryDate 查询日期
        
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
        
#### 3.4 获取小结
    用于教练端 我的客户 -> 购买项目 -> 课程详情 -> 课程小结
    我的课表 -> 课表详情 -> 查看课程小结
+ uri: 

        [GET] /v1/teacher/summaries/{id}
        
+ param: 

        [long] id 小结id
        
+ resp: 200

        {
            "data": {
                "cardNumber": "20190416000002",                 // 卡号
                "datetimeRange": "2019-05-07 12:51-14:51",    // 课程时间段
                "strPlace": "方庄妇幼保健院",                    // 场所
                "studentName": "小龙女",                        // 用户
                "courseTypeId": 2,                              // 课程类型id
                "courseType": "私教课",                         // 课程类型
                "attendClassRecords": [                         // 上课记录
                    {
                        "picUrl": "http://static.mifanxing.com/iyyren/image/201806/06/1638/347865732702420992.jpg", // 图片
                        "actionTitle": "俯卧撑",                 // 标题
                        "count": 2,                              // 共做了几组
                        "num": 10                                // 每组个数
                    },
                    {
                        "picUrl": "http://static.mifanxing.com/iyyren/image/201806/06/1638/347865732702420992.jpg",
                        "actionTitle": "仰卧起坐",
                        "count": 2,
                        "num": 15
                    }
                ],
                "tasks": [                                      // 作业
                    {
                        "picUrl": "http://static.mifanxing.com/iyyren/image/201806/06/1638/347865732702420992.jpg",
                        "actionTitle": "俯卧撑",
                        "count": 2,
                        "num": 10
                    }
                ],
                "coachComment": "学院很认真。",                 // 教练备注
                "customerComment": "教练教得好。",              // 客户评价
                "hasDoorFee": 0                                // 是否收取上门费标识，可忽略
            }
        }

#### 3.5 根据评估id获取评估
    用于教练端 我的课表 -> 课表详情 -> 查看客户评估
+ uri: 

        [GET] /v1/teacher/evaluations/{id}
        
+ param: 
    
        [long] id 评估id
        
+ resp: 200

        {
            "data": {
                "abdomenling": "abdomenling",                   // 腹围
                "abdomenMuscle": 0,                             // 腹直肌，0：阴性，1：阳性
                "abdomenMuscleAbout": 0,                        // 腹直肌位置，0：脐上，1：脐中，2：脐下
                "abdomenMuscleDepth": "abdomenMuscleDepth",     // 腹直肌深度
                "abdomenMuscleSeparateLen": "len",              // 腹直肌总分离长度
                "abdomenWall": 1,                               // 腹壁，正常弹性，1：松软无力，2：紧绷疼痛
                "age": 24,                                      // 会员年龄
                "appetite": 0,                                  // 食欲，0：好，1：一般，2：不佳
                "arm": "1,2",                                   // 手臂评估，0：无不适，1：酸软，2：无力，3：疼痛，4：麻，5：胸廓出口综合征；可多选，逗号隔开
                "babyBirthWeight": "babyBirthWeight",           // 宝宝出生体重
                "BMI": "BMI",                                   // BMI指数
                "bust": "bust",                                 // 胸围
                "caesareanEx": "0",                             // 剖腹产异常，0：疤痕红肿、筋膜远端触痛，1：疤痕增生，2：陈旧疤痕；可多选，逗号隔开
                "childBirth": "2019-05-08 10:10:10",            // 分娩日期
                "childbirthMode": 1,                            // 分娩方式，0：顺产，1：剖腹产
                "gestationEx": "gestationEx",                   // 妊娠特殊情况
                "gestationNum": 2,                              // 妊娠次数
                "height": "height",                             // 身高
                "hipline": "hipline",                           // 臀围
                "leg": "0",                                     // 下肢评估，0：水肿，1：膝关节痛，2：足根痛；可多选，逗号隔开
                "mentality": 0,                                 // 精神状态，0：好，1：一般，2：不佳
                "neck": 0,                                      // 颈部评估，0：无不适，1：有不适
                "neckAbout": 0,                                 // 颈部不适位置，0：左，1：右
                "neckEx": "0",                                  // 颈部不适性质，0：僵硬，1：疼痛，2：酸痛，3：活动受限；可多选，逗号隔开
                "others": "others",                             // 其它
                "pelvicFloor": "0",                             // 盆底功能评估，0：压力性尿失禁，1：急迫性尿失禁；可多选，逗号隔开
                "pelvis": 0,                                    // 骨盆评估，0：无不适，1：有不适
                "pelvisAbout": 0,                               // 骨盆不适位置，0：左，1：右，2：前，3后
                "pelvisEx": "0",                                // 骨盆不适性质，0：僵硬，1：疼痛，2：酸痛，3：下腹明显坠胀感，4：单侧耻骨牵拉感；可多选，逗号隔开
                "posture": "1",                                 // 体态评估，0：正常，1：上交叉综合证，2：下交叉综合证，3：膝外翻、X型腿，4：膝内翻、O型腿，5：扁平足，6：高弓足；可多选，逗号隔开
                "sciaticNerve": 1,                              // 坐骨神经症状，0：无，1：有
                "sciaticNerveEx": "1",                          // 坐骨神经异常，0：伴随腰痛，1：同侧骨盆后侧痛，2：不伴随其他位置痛；可多选，逗号隔开
                "shoulder": 1,                                  // 肩部评估，0：无不适，1：有不适
                "shoulderAbout": 1,                             // 肩部不适位置，0：左，1：右
                "shoulderEx": "2",                              // 肩部不适性质，0：僵硬，1：疼痛，2：酸痛，3：活动受限；可多选，逗号隔开
                "sleepCondition": 1,                            // 睡眠情况，0：充足，1：一般，2：欠缺
                "sleepLackReason": 2,                           // 睡眠欠缺原因，0：入睡难，1：易惊醒，2：照顾宝宝
                "sleepTime": "sleepTime",                       // 睡眠时长
                "spontaneousLaborEx": "2",                      // 顺产异常，0：无撕裂无侧切，1：有侧切，2：撕裂Ⅰ度，3：撕裂Ⅱ度，4：撕裂Ⅲ度，5：撕裂Ⅳ度；可多选，逗号隔开
                "state": 0,                                     // 状态，0：草稿，1：提交
                "waist": 1,                                     // 腰部评估，0：无不适，1：有不适
                "waistAbout": 3,                                // 腰不适位置，0：左腰，1：右腰，3：腰椎
                "waistEx": "2",                                 // 腰部不适性质，0：僵硬，1：疼痛，2：酸痛，3：活动受限；可多选，逗号隔开
                "waistline": "waistline",                       // 腰围
                "weight": "weight",                             // 体重
                "wrist": "wrist",                               // 手腕评估，0：无不适，1：腱鞘炎，2：腕管综合征；可多选，逗号隔开
                "studentId": 6,                                 // 学院id
                "studentName": "张小芳"                          // 会员姓名
            }
        }

### 4 我的客户模块
#### 4.1 通过手机号或客户名搜索客户
    用于教练端 我的客户页面搜索
+ uri: 

        [GET] /v1/teacher/users/search
        
+ param: 二填一

        [String] phoneNum 手机号
        [String] customerName 学员名
        
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
                    "state": 0,  // 状态，0：审核中，1：正常，2：请假中，3：审核未通过
                    "otherAddCoachName": "ycl"     // 其他添加教练的名字，可空，非空则显示 "某某添加"，否则不显示
                }
            ]
        }
        
