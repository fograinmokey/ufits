## 孕产平台教练端
#### 友情提示：所有返回值均为json，状态码为http状态码，注意处理400系等状态，文档标明字段没有返回说明没有值，注意空值判断

### 1 注册、登录
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
                "token": "token",   // 登录状态标识
                "userId": 3         // 用户id
            }
        }
   
### 2 我的课表
#### 2.1 根据日期获取教师课程列表
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
                        "timeRange": "2019-05-07 12:51-14:51",          // 时间段
                        "courseTypeId": 2,                              // 课程类型id
                        "courseType": "私教课",                         // 课程类型
                        "strState": "未完成",                           // 完成状态
                        "address": "方庄妇幼保健院",                    // 场所
                        "courseName": "12节孕期瑜伽小班课"              // 标题
                    }
                ]
            }
        }
        
#### 2.2 获取课表详情
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
                "datetimeRange": "2019-05-07 12:51-14:51",              // 上课时间段
                "courseTypeId": 2,                                      // 课程类型id 
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
        
#### 2.3 获取查询日期的年月下的天是否有课
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
        
#### 2.4 获取课程小结
    用于教练端 我的客户 -> 购买项目 -> 课程详情 -> 课程小结
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

#### 2.5 根据评估id获取评估
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
                "gestationEx": "gestationEx",                   // 妊娠特殊情况, 可空
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
                "studentName": "张小芳",                        //  姓名
                "courses": [                                    // 修复计划
                    {
                        "id": 14,                               // 课程id
                        "thumbnail": "http://static.mifanxing.com/article/image/215/69/0000001.jpg",    // 缩略图
                        "courseDesc": "此课程适应孕期产妇15",    // 课程描述
                        "courseName": "孕期瑜伽15期"            // 课程标题
                    }
                ],
                "images": [                                     // 照片记录
                    "2019-04-30/2309f5e6be3341d1a2ff3e265e20b2dc.jpg"   // 照片地址
                ]
            }
        }   
        
### 3 我的客户
#### 3.1 获取所有项目，含项目类型和具体项目
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

#### 3.2 通过手机号或客户名搜索客户
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
        
#### 3.3 获取当前教练的所有学生
    用于教练端 我的客户模块 展示用户列表
+ uri: 

        [GET] /v1/teacher/users/students
        
+ param: 无
+ resp: 200

        {
            "data": [
                {
                    "id": 25,                                           // 学员id
                    "realName": "张小芳",                               // 学员名
                    "firstLetter": "Z",                                 // 学员名首字母
                    "gender": 0,                                        // 性别：0：女，1：男
                    "phoneNum": "17085145711",                          // 手机号
                    "avatar": "https://wx.qlogo.cn/mmopKFAwN4k94gw/0",  // 头像
                    "state": 0                                          // 状态，0：审核中，1：正常，2：请假中，3：审核未通过
                }
            ]
        }

#### 3.4 获取学员基本信息
    用于教练端 我的客户 -> 客户信息 -> 基本信息
+ uri: 

        [GET] /v1/teacher/users/{id}
        
+ param: 

        [long] id 学员id
        
+ resp: 200

        {
            "data": {
                "id": 25,                                               // 学员id
                "nickName": "小芳",                                     // 昵称
                "realName": "张小芳",                                   // 姓名
                "gender": 0,                                            // 性别：0：女，1：男
                "birthday": "2002-04-20",                               // 生日
                "phoneNum": "17085145711",                              // 手机号
                "maternityStageTag": 3,                                 // 孕产阶段，0：未知，1：备孕，2：怀孕，3：产后
                "maternityDate": "2019-05-08",                          // 孕产日期
                "address": "贵州省贵阳市云岩区创业路2栋3单元32f",         // 住址
                "comment": "比较瘦",                                    // 备注
                "cards": [                                              // 学员拥有的卡列表
                    {
                        "cardId": 41,                                   // 卡id
                        "cardNumber": "20190425000001"                  // 卡号
                    }
                ],
                "isMainCoach": 1                                        // 是否是主教练，0：不是，1：是
            }
        }
        
#### 3.5 修改学员基本信息
    用于教练端 我的客户 -> 客户信息 -> 基本信息
+ uri: 

        [PUT] /v1/teacher/users/{id}
        
+ param: 

    [long] id 学员id
    
+ resp: 200

        {
            "data": {
                "nickName": "nickName",             // 昵称
                "realName": "realName",             // 姓名
                "gender": 0,                        // 性别：0：女，1：男
                "birthday": "2019-05-09",           // 生日
                "maternityStageTag": 3,             // 孕产阶段，0：未知，1：备孕，2：怀孕，3：产后
                "maternityDate": "2019-05-05",      // 孕产日期
                "address": "address",               // 住址
                "comment": "comment"                // 评论
            }
        }   
        
#### 3.6 获取会员卡信息
    用于教练端 我的客户 -> 基本信息 -> 查看卡详情
 + uri: 
 
        [GET] /v1/teacher/cards/id/41
        
+ param: 

        [long] id 卡id
        
+ resp: 200

        {
            "data": {
                "cardId": 41,                                       // 卡id
                "cardNumber": "20190425000001",                     // 卡号
                "userName": "张小芳",                               // 学员名
                "phoneNumber": "17085145711",                       // 手机
                "maternityStageTag": 3,                             // 孕产阶段，0：未知，1：备孕，2：怀孕，3：产后
                "maternityDate": "2019-05-08",                      // 孕产日期
                "birthday": "2001-04-20",                           // 生日
                "address": "贵州省贵阳市云岩区创业路2栋3单元32f",     // 住址
                "packageType": 0,                                   // 套餐类型，0：新买课，1：续课，2，套餐升级
                "projectId": 17,                                    // 项目id
                "money": 10000,                                     // 金额
                "purchaseCourseNumber": 100,                        // 购课数
                "giveCourseNumber": 2,                              // 赠课数
                "remainCourseNumber": 80,                           // 剩余课时数
                "inDoorFee": 0,                                     // 上门费
                "payWay": 2,                                        // 支付方式，0：大众点评，1：支付宝，2：微信，3：现金，4：刷卡，5：其他
                "effectiveDate": "2019-05-30",                      // 有效期
                "customerSourceId": 4,                              // 来源id
                "customerSource": "方庄妇幼保健院",                  // 来源
                "coachId": 5,                                       // 销售教练id
                "coachName": "ycl",                                 // 销售教练名
                "cooperationCoach": {                               // 合作教练
                    "5": "ycl",                                     // 教练id：教练名
                    "26": "李四"
                },
                "placeType": 0,                                     // 场内外，0：场外，1：场内
                "doorType": 0,                                      // 是否有上门，0：否，1：是
                "comment": "没有",                                  // 备注
                "mainCoachTag": 1,                                  // 是否是主教练，0：否，1：是
                "giveCardDate": "2019-05-08",                       // 开卡日期
                "cardState": 0,                                     // 状态，0：审核中，1：正常，2：请假中，3：审核未通过
                "projectTitle": "免费体验课子项1"                    // 项目名
            }
        }
        
#### 3.7 获取用户购买项目（即所有卡）
    用于教练端 我的客户->客户信息->购买项目 列表展示
+ uri: 
        
        [GET] /v1/teacher/cards/student/25
                
+ param:

        [long] studentId 学员id
                                                                                     
+ resp: 200

                {
                    "data": [
                        {
                            "cardId": 41,                           // 卡id
                            "cardNumber": "20190425000001",         // 卡号
                            "effectiveDate": "2019-05-30",          // 有效期
                            "projectTitle": "免费体验课子项1",       // 项目名称
                            "remainingClassTime": 80,               // 剩余课时
                            "created": 1557308772000                // 可忽略
                        }
                    ]
                }
                
#### 3.8 获取卡的课程详情
    用于教练端 我的客户 -> 客户信息 -> 购买项目 -> 课程详情
+ uri:

        [GET] /v1/teacher/courses/card/detail?cardId=41     
        
+ param: 

        [long] cardId 卡id
        
+ resp: 200

        {
            "data": {
                "cardId": 41,                               // 卡id
                "projectName": "免费体验课子项1",            // 项目
                "classTime": 100,                           // 课时数
                "remainClassTime": 80,                      // 剩余课时数
                "effectiveDate": "2019-05-30",              // 有效期
                "buyDate": "2019-05-08",                    // 时间
                "cardClassRecords": [                       // 此卡上课记录（已完成的上课列表）
                    {
                        "summaryId": 2,                     // 小结id
                        "beginTime": "2019-05-09 14:51",    // 上课时间
                        "classDate": "2019-05-09",          // 上课日期
                        "classTypeId": 2,                   // 课程类型id
                        "classType": "私教课",              // 课程类型名
                        "classTitle": "免费体验课子项1",     // 课程服务标题
                        "classCoachName": "ycl"             // 上课教练
                    }
                ]
            }
        }              
        
#### 3.9 获取为这个学员（卡）服务的教练
    用于教练端 我的客户 -> 购买项目 -> 服务教练名单
+ uri: 

        [GET] /v1/teacher/coach-attends/coaches-for-student?cardId=41
        
+ param:

        [long] cardId 卡id
        
+ resp: 200

        {
            "data": [
                {
                    "id": 5,                    // 教练id
                    "realName": "ycl",          // 教练名
                    "jobTitle": "中级教练",      // 职称
                    "photo": "https://wx.qbEtrEEV45pl84k94gw/0"     // 照片
                }
            ]
        }    
        
#### 3.10 获取所有教练
    用于教练端 我的客户 -> 客户信息 -> 购买项目 -> 课程详情 -> 服务教练名单 -> 添加 -> 添加服务教练列表
    用于教练端 我的客户 -> 开卡 -> 销售教练/合作教练的选择
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
        
#### 3.11 获取课程小结
    用于教练端 我的课表 -> 课表详情 -> 查看课程小结 
+ tip: 同 3.4         

#### 3.12 获取教练详情
    用于教练端 我的客户 -> 客户信息 -> 购买项目 -> 服务教练名单 -> 教练详情
+ uri: 

        [GET] /v1/teacher/users/coach-detail/5
        
+ param: 

        [long] coachId 教练id
        
+ resp: 200

        {
            "data": {
                "realName": "ycl",                  // 姓名
                "jobTitle": "中级教练",             // 职称
                "photo": "https://wx.qq.gw/0",     // 照片
                "coachContent": "没有。"           // 教师详细介绍
            }
        }
        
#### 3.13 获取所有项目，含项目类型和具体项目
    用于教练端 我的客户 -> 发卡 -> 项目名称
+ uri: 

    [GET] /v1/teacher/projects
    
+ param: 无
+ resp: 200

        {
            "data": [
                {
                    "id": 1,                                    // 项目分类id
                    "projectTitle": "免费体验课",                // 项目分类名
                    "subProjects": [                            // 项目
                        {
                            "id": 1,                            // 项目id
                            "projectTitle": "免费体验课33",      // 项目名
                            "classTime": 0,                     // 课时数
                            "money": 0                          // 金额
                        }
                    ]
                }
            ]
        }
        
#### 3.14 获取客户来源列表，包含合作机构和机构类别
    用于教练端 我的客户 -> 开卡 -> 来源
+ uri: 

        [GET] /v1/teacher/organizations
        
+ param: 无
+ resp: 200

        {
            "data": [
                {
                    "id": 1,                                    // 来源类别id
                    "sourceTitle": "合作机构分类1",              // 来源类别名
                    "subCustomerSource": [
                        {
                            "id": 1,                            // 来源id
                            "sourceTitle": "北京月子会所"        // 来源名
                        }
                    ]
                }
            ]
        } 
        
#### 3.15 开卡
    用于教练端 我的客户 -> 发卡
+ uri: 

        [GET] /v1/teacher/cards
        
+ param: json

        {
            "data": {               
               "userName": "黄蓉",                      // 学员名
               "phoneNumber": "17085145713",            // 手机
               "maternityStageTag": 3,                  // 孕产阶段，0：未知，1：备孕，2：怀孕，3：产后
               "maternityDate": "2019-04-09",           // 孕产日期
               "birthday": "2009-05-09",                // 生日
               "address": "北京市丰台区方庄桥南",        // 住址
               "packageType": 0,                        // 套餐类型，0：新买课，1：续课，2，套餐升级
               "projectId": 18,                         // 项目id
               "money": 600,                            // 金额
               "purchaseCourseNumber": 5,               // 购课数
               "giveCourseNumber": 1,                   // 赠课数
               "inDoorFee": 5,                          // 上门费
               "payWay": 2,                             // 支付方式，0：大众点评，1：支付宝，2：微信，3：现金，4：刷卡，5：其他
               "effectiveDate": "2020-04-20",           // 卡有效期
               "customerSourceId": 4,                   // 客户来源id
               "coachId": 5,                            // 销售教练
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
                     
#### 3.16 修改卡信息
    用于教练端 我的客户 -> 基本信息 -> 查看卡详情 -> 修改
+ uri: 

        [PUT] /v1/teacher/cards/42
        
+ param: 

        [long] id 卡id
        
        {
            "data": {               
               "userName": "黄蓉",                      // 学员名
               "phoneNumber": "17085145713",            // 手机
               "maternityStageTag": 3,                  // 孕产阶段，0：未知，1：备孕，2：怀孕，3：产后
               "maternityDate": "2019-04-09",           // 孕产日期
               "birthday": "2009-05-09",                // 生日
               "address": "北京市丰台区方庄桥南",        // 详细住址
               "packageType": 1,                        // 套餐类型，0：新买课，1：续课，2，套餐升级
               "projectId": 19,                         // 项目标识
               "money": 600,                            // 金额
               "purchaseCourseNumber": 5,               // 课时数/购课数
               "giveCourseNumber": 1,                   // 赠送课时/课数
               "remainCourseNumber": 3,                 // 剩余课时
               "inDoorFee": 5,                          // 上门费
               "payWay": 2,                             // 支付方式，0：大众点评，1：支付宝，2：微信，3：现金，4：刷卡，5：其他
               "effectiveDate": "2020-04-20",           // 有效日期
               "customerSourceId": 4,                   // 来源合作机构标识
               "coachId": 5,                            // 销售教练
               "cooperationCoach": {        
               		"26": "李四"                          // 合作教练，id：name
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
        
#### 3.17 添加服务教练
    用于教练端 我的客户 -> 购买项目 -> 课程详情 -> 服务教练名单 -> 添加
+ uri: 
        [GET] /v1/teacher/coach-attends            
        
### 4 我的课程
#### 4.1 获取当前教练的未完成的课程列表
    用于教练端 我的课程模块未完成课程列表展示
+ uri: 

        [POST] /v1/teacher/coach-attend-classes
        
+ param: json
        
        {
            "data": {
                "studentId": 27,    // 学员id
                "cardId": 45,       // 卡id
                "coachIds": [
                    5,              // 教练id
                    26,
                    28
                ]
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
        
+ param: 无
+ resp: 200

        {
            "data": {
                "uncompletedCourseNum": 1,                      // 未完成的课程数
                "courses": [
                    {
                        "timeRange": "2019-05-07 12:51-14:51",  // 上课时间段
                        "courseTypeId": 2,                      // 课程类型id
                        "courseType": "私教课",                 // 课程类型名
                        "state": 0,                             // 状态：0：已预约，1：已签到，2：已签退，3：已总结，4：已结束，5：预约失败
                        "acId": 18,                             // 预约上课id
                        "nature": 1,                            // 课程性质，0：公开，1：私教
                        "address": "上门",                      // 地址
                        "courseName": "12节孕期瑜伽小班课"       // 课程名
                    }
                ]
            }
        }     
        
#### 4.2 获取私教性质课程分类
    用于教练端 我的课程 -> 预约 -> 课程分类
+ uri: 

        [GET] /v1/teacher/att-class-cats
        
+ param: 无
+ resp: 200

        {
            "data": [
                {
                    "id": 2,                // 分类id
                    "title": "私教课"       // 分类名  
                },
                {
                    "id": 5,
                    "title": "查房"
                },
                {
                    "id": 8,
                    "title": "体验课"
                }
            ]
        }
        
#### 4.3 获取课程级别（课程服务）
    用于教练端 我的课程模块 -> 预约 -> 课程服务
+ uri: 

        [GET] /v1/teacher/course-levels
        
+ param: 无
+ resp: 200

        {
            "data": [
                {
                    "id": 1,            // 级别id
                    "title": "初级"     // 级别名  
                },
                {
                    "id": 2,
                    "title": "中级"
                },
                {
                    "id": 3,
                    "title": "高级"
                }
            ]
        }                    
        
#### 4.4 获取合作机构，不包含分类
    用于教练端 我的课程 -> 预约 -> 场所 选到店时使用
+ uri:

        [GET] /v1/teacher/organizations/list
        
+ param: 无
+ resp: 200

        {
            "data": [
                {
                    "id": 1,                        // 机构id
                    "sourceTitle": "北京月子会所"    // 机构名
                },
                {
                    "id": 2,
                    "sourceTitle": "月子会所"
                },
                {
                    "id": 3,
                    "sourceTitle": "上海妇幼保健院1"
                },
                {
                    "id": 4,
                    "sourceTitle": "方庄妇幼保健院"
                }
            ]
        }
        
#### 4.5 根据手机号获取用户姓名、卡号、项目名
    用于教练端 我的课程 -> 预约 输了手机号名字自动关联
+ uri: 

        [GET] /v1/teacher/users?phoneNum=17085145713
        
+ param: 

        [string] phoneNum 学员手机号
        
+ resp: 200
    
        {
            "data": {
                "phoneNum": "17085145713",                  // 学员手机号
                "name": "黄蓉",                             // 学员姓名
                "cardNumNameMap": {
                    "20190510000002": "收费体验课子项2"     // 学员卡号和项目名
                }
            }
        }      
        
#### 4.6 预约
    用于教练端 我的课程模块 -> 预约
+ uri: 

        [POST] /v1/teacher/attend-classes
        
+ param: json

        {
            "data": {               
               "categoryId": 2,                 // 课程分类id
               "phoneNum": "17085145713",       // 会员手机号
               "name": "黄蓉",                  // 会员姓名
               "cardNum": "20190510000002",     // 会员卡号
               "doorType": 0,                   // 场所，0：到店，1：上门
               "organizationId": 4,             // 可选，如果到店则需要调用5.4接口获取合作店铺
               "timeLength": 40,                // 上课时长，以分钟为单位
               "attendDate": "2019-05-15",      // 开课日期
               "beginTime": "10:10:10",         // 上课时间
               "courseLevelId": 4,              // 课程服务，需调用5.3获取
               "comment": "comment123",         // 备注
               "longitude": 23.45,              // 经度
               "latitude": 45.22                // 维度
            }
        }    
        
+ resp: 201

        {
            "errors": [
                {
                    "status": "201",
                    "title": "Created"
                }
            ]
        }                                                                                                                                                                                                                                                                                         
