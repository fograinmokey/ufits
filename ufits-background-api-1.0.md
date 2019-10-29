## 孕产平台后台
#### 友情提示：
    1 所有返回值均为json，状态码为http状态码，注意处理400系等状态;
    2 文档标明字段没有返回说明没有值，注意空值判断;
    3 访问图片需要加上/images/前缀;

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

        [POST] /v1/teacher/cards
        
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
               "payWay": 2,                             // 支付方式，0：大众点评团购，1：支付宝，2：微信，3：现金，4：刷卡，5：其他，6：大众点评闪惠
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
               "payWay": 2,                             // 支付方式，0：大众点评团购，1：支付宝，2：微信，3：现金，4：刷卡，5：其他，6：大众点评闪惠
               "effectiveDate": "2020-04-20",           // 卡有效期
               "coachId": 5,                            // 销售教练id
               "cooperationCoach": {
                    "26": "李四"                        // 合作教练id和名字
               },
               "placeType": 0,                          // 场内外，0：场外，1：场内
               "doorType": 1,                           // 是否有上门，0：否，1：是
               "comment": "no comment",                 // 备注
               "editTag": "check",                      // 修改状态，当值为check时为后台审核操作，为空或其它值则不是
               "checkState"                             // 审核状态，通过为on，不通过为off  
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
        
#### 1.8 判断用户是否登录
    用于后台用户管理 -> 回访客户 回访人列表
+ uri: 

        [GET] /v1/teacher/users/isLogin
        
+ param: 无
+ header: 

        Authorization: "93b824a2-5f99-4cc4-bcce-aea99ea893dc"   // token
        
+ resp: 200

        {
            "data": true    // 登录状态，true：已登录，false：未登录
        }
        
### 2 回访
#### 2.1 获取回访人
    用于后台提交回访中的回访人列表显示
+ uri:

        [GET] /admin/backVisits/admin      
+ resp: 200
        
        {
          "data": {
            "16": "张无忌",    // 回访教练id
            "34": "张三",      // 回访教练名
            "51": "坤坤",
            "69": "gilfoyle",
            "71": "tengli"
          }
        }
        
#### 2.2 回访状态（固定内容）
    用于后台提交回访中的回访状态列表显示
    
    1 无意向会员     // 标识、描述
    2 有意向未到店
    3 约访到店
    4 客户已到访
    5 （首次）报名-准会员
    6 （非首次）报名-准会员      
    
#### 2.3 提交回访
    用于后台提交回访
+ uri:

        [POST] /admin/backVisits
+ param: json

        {
            "data": {
               "studentId": 24,                             // 学员id               
               "coachId": 34,                               // 教练id
               "visitStatus": 2,                            // 回访状态标识：1、无意向会员；2、有意向未到店；3、约访到店；4、客户已到访；5、（首次）报名-准会员；6、（非首次）报名-准会员
               "content": "询问锻炼情况。",                  // 回访内容
               "nextVisitDatetime": "2019-09-27 18:41:22"   // 下次回访时间，可选
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
        
#### 2.4 获取用户回访记录
    用于后台用户管理中的用户回访记录和查询所有回访记录
+ uri: 

        [GET] /admin/backVisits
+ param:

        [int] page[number]  当前是第几页，默认为1
        [int] page[size]    每页多少条数据，默认为10
        [long] studentId    可选，学员id，不填查出所有记录，否则查出该学员回访记录
+ resp: 200

        {
          "data": {
            "total": 1,                                     // 用户回访记录条数
            "totalPages": 1,                                // 总页数
            "backVisitVOList": [
              {
                "backVisitId": 2,                           // 回访记录id
                "coachId": 34,                              // 回访人Id
                "coachName": "张三",                        // 回访人姓名
                "studentId": 24,                            // 被访学员id
                "studentName": "江小白",                    // 学员姓名
                "phoneNumber": "17600261644",               // 学员手机号
                "visitStatus": 2,                           // 回访状态标识：1、无意向会员；2、有意向未到店；3、约访到店；4、客户已到访；5、（首次）报名-准会员；6、（非首次）报名-准会员
                "visitStatusContent": "有意向未到店",        // 回访状态内容
                "visitDatetime": "2019-09-27"               // 回访时间
              }
            ]
          }
        } 
        
#### 2.5 获取回访记录详情
    用于后台管理查看用户回访记录详情
+ uri:

        [GET] /admin/backVisits/{id}     
+ param:

        [long] id 回访记录id
+ resp: 200
        
        {
          "data": {
            "backVisitId": 2,                                   // 回访记录id
            "coachId": 34,                                      // 回访人Id
            "coachName": "张三",                                // 回访人姓名
            "studentId": 24,                                    // 被访学员id
            "studentName": "江小白",                            // 学员姓名
            "phoneNumber": "17600261644",                       // 学员手机号
            "visitStatus": 2,                                   // 回访状态标识：1、无意向会员；2、有意向未到店；3、约访到店；4、客户已到访；5、（首次）报名-准会员；6、（非首次）报名-准会员
            "visitStatusContent": "有意向未到店",                // 回访状态内容
            "content": "进行深入友好的交流，询问锻炼情况。",      // 回访内容
            "visitDatetime": "2019-09-27",                      // 回访时间
            "nextVisitDatetime": "2019-09-29"                   // 下次回访时间，可能无
          }
        }      
        
#### 2.6 更新回访详情
    用于后台管理回访详情页面的编辑
+ uri:

        [PATCH] /admin/backVisits/{id}
+ param:

        [long] id 回访id
        [json]
        {
            "data": {
               "visitStatus": 2,                            // 回访状态标识：1、无意向会员；2、有意向未到店；3、约访到店；4、客户已到访；5、（首次）报名-准会员；6、（非首次）报名-准会员
               "content": "询问锻炼情况。",                  // 回访内容
               "nextVisitDatetime": "2019-09-27 18:41:22"   // 下次回访时间，可选
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
        
#### 2.7 回访记录查询
    用于后台管理回访列表搜索
+ uri:

        [GET] /admin/backVisits/search
+ param:

        [int]       page[number]          可选，当前是第几页，默认为1
        [int]       page[size]            可选，每页多少条数据，默认为10
        [long]      studentId             可选，被访学员id
        [string]    studentName           可选，用户名，支持前向模糊搜索如：张三丰，可通过张、张三、张三丰这样来模糊搜索，不支持三、三丰
        [string]    phoneNumber           可选，手机号，支持前向模糊搜索
        [int]       visitStatus           可选，回访状态标识：1、无意向会员；2、有意向未到店；3、约访到店；4、客户已到访；5、（首次）报名-准会员；6、（非首次）报名-准会员
        [long]      coachId               可选，回访人
        [datetime]  visitDatetime         可选，回访时间，格式为yyyy/MM/dd
+ resp: 200

        {
          "data": {
            "total": 7,                                             // 用户回访记录数
            "totalPages": 1,                                        // 页数
            "backVisitVOList": [                                    // 列表数据
              {
                "backVisitId": 2,                                   // 回访id
                "coachId": 34,                                      // 回访人id
                "coachName": "张三",                                // 回访人
                "studentId": 24,                                    // 用户id
                "studentName": "江小白",                            // 用户名
                "phoneNumber": "17600261644",                       // 手机号
                "visitStatus": 2,                                   // 回访状态标识：1、无意向会员；2、有意向未到店；3、约访到店；4、客户已到访；5、（首次）报名-准会员；6、（非首次）报名-准会员
                "content": "进行深入友好的交流，询问锻炼情况。",      // 回访记录
                "nextVisitDatetime": "2019-09-29",                  // 下次回访时间
                "visitDatetime": "2019-09-27"                       // 回访时间
              },
              {
                "backVisitId": 3,
                "coachId": 34,
                "coachName": "张三",
                "studentId": 25,
                "studentName": "李白",
                "phoneNumber": "17085145711",
                "visitStatus": 2,
                "content": "进行深入友好的交流，询问锻炼情况2。",
                "nextVisitDatetime": "2019-09-29",
                "visitDatetime": "2019-09-27"
              }
            ]
          }
        }  
        
### 3 日志
#### 3.0 日志类型id及对应名字
    1	新开会员卡
    2	会员卡续课
    3	会员卡套餐升级
    4	删除会员卡
    5	修改会员卡
    6	审核会员卡
    7	审核请假
    8	新增用户
    9	删除用户
    10	修改用户
    11	新增回访
    12	修改回访
    13	新增课程分类
    14	删除课程分类
    15	修改课程分类
    16	新增课程服务分类
    17	删除课程服务分类
    18	修改课程服务分类
    19	新增课程
    20	删除课程
    21	修改课程
    22      导出到Excel

#### 3.1 保存日志
+ uri: 
        
      [POST] /ufitslogs

+ param: json
        
        {
          "data": {
            "logTypeCode": 5,                   // 日志类型编码，如 3.0 所示
            "cardId": 5,                        // 可选，会员卡id
            "studentId": 3,                     // 可选，学员id
            "message": "Ufits log test 001."    // 日志内容
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
        
#### 3.2 获取日志详情
+ uri:

      [GET] /ufitslogs/{logId}

+ param:
    
      [long] logId 日志id
      
+ resp: 201

       {
         "data": {
           "id": 14,                                   // 日志id
           "logTypeCode": 5,                           // 日志类型标识
           "logTypeName": "修改会员卡",                 // 日志类型名
           "cardId": 5,                                // 会员卡id
           "cardNumber": "20190414000001",             // 会员卡号
           "studentId": 3,                             // 学员id
           "studentName": "的分公司的国际法都死了",     // 学员名
           "phoneNumber": "18810649831",               // 学员手机号
           "message": "Ufits log test 007.",           // 日志内容
           "creatorName": "江小白",                    // 操作人
           "createDateTime": "2019-10-18 10:21"        // 操作时间
         }
       }
       
#### 3.3 获取日志列表
+ uri:

      [GET] /ufitslogs
      
+ param     

      [int] page[number] 可选，当前是第几页，默认为1
      [int] page[size]   可选，每页多少条数据，默认为10     
      
+ resp: 200

      {
        "data": {
          "pages": 2,                                     // 总页数
          "count": 15,                                    // 总数据条数
          "ufitsLogs": [
            {
              "id": 14,                                   // 日志id
              "logTypeCode": 5,                           // 日志类型标识
              "logTypeName": "修改会员卡",                 // 日志类型名
              "cardId": 5,                                // 会员卡id
              "cardNumber": "20190414000001",             // 会员卡号
              "studentId": 3,                             // 学员id
              "studentName": "的分公司的国际法都死了",      // 学员名
              "phoneNumber": "18810649831",               // 学员手机号
              "message": "Ufits log test 007.",           // 日志内容
              "creatorName": "江小白",                     // 操作人
              "createDateTime": "2019-10-18 10:21"         // 操作时间
            }
          ]
        }
      }    
      
#### 3.4 日志搜索
    可根据内容、创建者、创建时间组合搜索；前端根据正则表达式判断是手机号还是姓名
+ uri:

      [GET] /ufitslogs/search
      
+ param:

      [int]     page[number]    可选，当前是第几页，默认为1
      [int]     page[size]      可选，每页多少条数据，默认为10     
      [long]    id              可选，日志id
      [int]     logTypeCode     可选，日志类型标识
      [string]  cardNumber      可选，会员卡号
      [string]  phoneNumber     可选，会员手机号
      [string]  studentName     可选，会员名 
      [long]    creatorId       可选，操作人id
      [string]  creatorName     可选，操作人名字
      [string]  createDateTime  可选，操作时间, 格式为"yyyy/MM/dd [[HH]:[mm]:[ss]]"，中括号表示可选
      
+ resp: 200

      {
          "data": {
            "pages": 2,                                     // 总页数
            "count": 15,                                    // 总数据条数
            "ufitsLogs": [
              {
                "id": 14,                                   // 日志id
                "logTypeCode": 5,                           // 日志类型标识
                "logTypeName": "修改会员卡",                 // 日志类型名
                "cardId": 5,                                // 会员卡id
                "cardNumber": "20190414000001",             // 会员卡号
                "studentId": 3,                             // 学员id
                "studentName": "的分公司的国际法都死了",      // 学员名
                "phoneNumber": "18810649831",               // 学员手机号
                "message": "Ufits log test 007.",           // 日志内容
                "creatorName": "江小白",                     // 操作人
                "createDateTime": "2019-10-18 10:21"         // 操作时间
              }
            ]
          }
      }                                                                                                                                                                                                                                                                                                
