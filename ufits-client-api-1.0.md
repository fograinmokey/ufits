## 孕产平台客户端
+ 2019年04月12 日
    +  孕产平台客户端初始化
    
+ Data
    + id (Long) - ID
    + wechatId (String) - 微信标识
    + phoneNumber (String) - 注册号码
    + identity (int) - 0：学生，1：教练（默认0：学生）
    + nickname (String) - 昵称
    + realName (String) - 真实姓名
    + sex (int) - 性别；0：女，1：男（默认0：女） 
    + birthday (Date) - 生日
    + pregnancyStage (int) - 孕产阶段（0：未知，1：备孕，2：怀孕，3：产后） 
    + pregnancyDate (Date) - 孕产日期
    + address (String) - 住址
    + avatar (String) - 头像
    + jobTitle (String) - 职称认证
    + remarks (String) - 备注/教师介绍
    + photo (String) - 照片
    + enabled (int) - 0禁用 1启用
    + creator (Long) - 创建人
    + modifier (Long) - 修改人
    + created (date) - 创建时间
    + modified (date) - 修改时间

### 教练介绍列表 [GET] /users?filter[identity]=1
+ Parameters
  + identity  0：学生，1：教练
  + sort -modified(从新到旧) | modified(从旧到新)

+ Response 200 (application/json)

      {
        "meta": {
            "totalPages": 1,
            "totalElements": 2,
            "size": 10,
            "number": 1,
            "numberOfElements": 2,
            "first": true,
            "last": true,
            "sort": null
        },
        "links": {
            "self": "/users?filter[identity]=1&page[number]=1&page[size]=10",
            "first": "/users?filter[identity]=1&page[number]=1&page[size]=10",
            "last": "/users?filter[identity]=1&page[number]=1&page[size]=10"
        },
        "data": [
            {
                "id": 2,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-04-10 17:46:41",
                "modified": "2019-04-10 17:46:37",
                "wechatId": "2",
                "phoneNumber": "18331931950",
                "identity": 1,
                "nickname": "健康医师",
                "realName": "贝多芬",
                "sex": 0,
                "birthday": "2018-08-01",
                "pregnancyStage": 0,
                "jobTitle": "高级教练",
                "remarks": "上菜鸟winVB让她宝宝贝贝人不同让宝宝",
                "photo": "http://static.mifanxing.com/iyyren/image/201806/06/1638/347865732702420992.jpg",
                "sexName": "女"
            },
            {
                "id": 3,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-04-11 19:43:49",
                "modified": "2019-04-11 19:46:06",
                "wechatId": "oK9PMsxEZTJgUoG53gYJsdu1UQIE",
                "phoneNumber": "18810649832",
                "identity": 1,
                "nickname": "青城",
                "realName": "张三1",
                "sex": 0,
                "birthday": "1967-01-01",
                "pregnancyStage": 1,
                "pregnancyDate": "2017-06-22",
                "address": "北京市丰台区云谷创业园",
                "avatar": "http://static.mifanxing.com/iyyren/image/201806/06/1638/347865732702420992.jpg",
                "jobTitle": "中级教练",
                "remarks": "个人同行业后台已经还特意与金太阳",
                "photo": "http://static.mifanxing.com/iyyren/image/201803/15/1453/317761140065189888.jpg",
                "sexName": "女"
            }
        ]
      }

### 查询用户详情 [GET] /users/{id}

+ Response 200 (application/json)
    
      {
        "data": {
            "id": 2,
            "enabled": 1,
            "creator": 0,
            "modifier": 0,
            "created": "2019-04-10 17:46:41",
            "modified": "2019-04-10 17:46:37",
            "wechatId": "2",
            "phoneNumber": "18331931950",
            "identity": 1,
            "nickname": "健康医师",
            "realName": "贝多芬",
            "sex": 0,
            "birthday": "2018-08-01",
            "pregnancyStage": 0,
            "jobTitle": "高级教练",
            "remarks": "上菜鸟winVB让她宝宝贝贝人不同让宝宝",
            "photo": "http://static.mifanxing.com/iyyren/image/201806/06/1638/347865732702420992.jpg",
            "sexName": "女"
        }
      }

### 修改个人信息[PUTCH]/users/{id}
+ Description
    + [MUST] authenticated
    + [MUST] 
+ Request (application/json)
    
      {
    	 "data":{
    		"wechatId":"oK9PMsxEZTJgUoG53gYJsdu1UQIE",
    		"phoneNumber":"18810649832",
    		"identity":"1",
    		"nickname":"青城",
    		"realName":"张三1",
    		"sex":0,
    		"birthday":"1967-01-01",
    		"pregnancyStage":1,
    		"pregnancyDate":"2017-06-22",
    		"address":"北京市丰台区云谷创业园",
    		"avatar":"http://static.mifanxing.com/iyyren/image/201806/06/1638/347865732702420992.jpg",
    		"jobTitle":"中级教练",
    		"remarks":"个人同行业后台已经还特意与金太阳",
    		"photo":"http://static.mifanxing.com/iyyren/image/201803/15/1453/317761140065189888.jpg"
    	 }
      }

+ Response 200

## 课程服务
+ Data
  + CourseLevel - 课程级别表 
    + levelTitle (String) - 级别名称
    + description (String) - 级别描述
    + timeCoefficient (BigDecimal) - 时长系数
    + enabled (int) - 0禁用 1启用
    + creator (Long) - 创建人
    + modifier (Long) - 修改人
    + created (date) - 创建时间
    + modified (date) - 修改时间
  + Course - 课程表
    + levelId (Long) - 级别标识
    + courseTitle (String) - 课程名称
    + description (String) - 课程描述
    + content (String) - 课程内容
    + recommendedCoefficient (BigDecimal) - 推荐系数
    + enabled (int) - 0禁用 1启用
    + creator (Long) - 创建人
    + modifier (Long) - 修改人
    + created (date) - 创建时间
    + modified (date) - 修改时间
    + pictures - 图片

### 课程服务列表 [GET] /courseLevels
+ Parameters
  + sort -modified(从新到旧) | modified(从旧到新)
+ Description
  + courses 课程数据
  + pictures 课程图片
+ Response 200 (application/json)
    
      {
        "meta": {
            "totalPages": 1,
            "totalElements": 3,
            "size": 10,
            "number": 1,
            "numberOfElements": 3,
            "first": true,
            "last": true,
            "sort": null
        },
        "links": {
            "self": "/courseLevels?page[number]=1&page[size]=10",
            "first": "/courseLevels?page[number]=1&page[size]=10",
            "last": "/courseLevels?page[number]=1&page[size]=10"
        },
        "data": [
            {
                "id": 1,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-04-10 15:19:18",
                "modified": "2019-04-10 15:19:18",
                "levelTitle": "初级",
                "timeCoefficient": 0.5,
                "courses": [
                    {
                        "id": 6,
                        "courseTitle": "产前体检",
                        "description": "上菜鸟winVB让她宝宝贝贝人不同让宝宝",
                        "pictures": [
                            "http://static.mifanxing.com/iyyren/image/201806/06/1638/347865732702420992.jpg"
                        ]
                    },
                    {
                        "id": 7,
                        "courseTitle": "产前锻炼",
                        "description": "米内特我惹你本宝宝搜索发布导包导包",
                        "pictures": [
                            "http://static.mifanxing.com/iyyren/image/201806/06/1638/3478657327024209921.jpg",
                            "http://static.mifanxing.com/iyyren/image/201806/06/1638/3478657327024209922.jpg"
                        ]
                    }
                ]
            },
            {
                "id": 2,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-04-10 18:34:48",
                "modified": "2019-04-10 18:34:43",
                "levelTitle": "中级",
                "timeCoefficient": 1,
                "courses": [
                    {
                        "id": 4,
                        "courseTitle": "孕期锻炼",
                        "description": "上菜鸟winVB让她宝宝贝贝人不同让宝宝",
                        "pictures": [
                            "http://static.mifanxing.com/iyyren/image/201806/06/1638/347865732702420992.jpg"
                        ]
                    }
                ]
            },
            {
                "id": 3,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-04-10 18:34:51",
                "modified": "2019-04-10 18:34:46",
                "levelTitle": "高级",
                "timeCoefficient": 1.5,
                "courses": [
                    {
                        "id": 1,
                        "courseTitle": "产后恢复",
                        "description": "上菜鸟winVB让她宝宝贝贝人不同让宝宝",
                        "pictures": [
                            "http://static.mifanxing.com/iyyren/image/201806/06/1638/347865732702420992.jpg"
                        ]
                    }
                ]
            }
        ]
      }
    
### 课程服务特别推荐列表 [GET] /courses?filter[recommendedCoefficient:ge]=1&sort=recommendedCoefficient
+ Parameters
  + sort -modified(从新到旧) | modified(从旧到新)
+ Response 200 (application/json)

      {
        "meta": {
            "totalPages": 1,
            "totalElements": 3,
            "size": 10,
            "number": 1,
            "numberOfElements": 3,
            "first": true,
            "last": true,
            "sort": [
                {
                    "direction": "ASC",
                    "property": "recommended_coefficient",
                    "ignoreCase": false,
                    "nullHandling": "NATIVE",
                    "ascending": true,
                    "descending": false
                }
            ]
        },
        "links": {
            "self": "/courses?filter[recommendedCoefficient:ge]=1&sort=recommendedCoefficient&page[number]=1&page[size]=10",
            "first": "/courses?filter[recommendedCoefficient:ge]=1&sort=recommendedCoefficient&page[number]=1&page[size]=10",
            "last": "/courses?filter[recommendedCoefficient:ge]=1&sort=recommendedCoefficient&page[number]=1&page[size]=10"
        },
        "data": [
            {
                "id": 4,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-04-12 11:22:12",
                "modified": "2019-04-11 11:22:02",
                "levelId": 2,
                "courseTitle": "孕期锻炼",
                "description": "上菜鸟winVB让她宝宝贝贝人不同让宝宝",
                "recommendedCoefficient": 1,
                "pictures": [
                    "http://static.mifanxing.com/iyyren/image/201806/06/1638/347865732702420992.jpg"
                ]
            },
            {
                "id": 1,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-04-10 15:20:05",
                "modified": "2019-04-10 15:20:05",
                "levelId": 3,
                "courseTitle": "产后恢复",
                "description": "上菜鸟winVB让她宝宝贝贝人不同让宝宝",
                "content": "合同如火如荼好人挺好玩儿是的深V是VB填入黑胡椒一次次地CSAC阿萨阿所产生的吃的是草",
                "recommendedCoefficient": 2,
                "pictures": [
                    "http://static.mifanxing.com/iyyren/image/201806/06/1638/347865732702420992.jpg"
                ]
            },
            {
                "id": 7,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-04-12 11:22:19",
                "modified": "2019-04-12 11:22:09",
                "levelId": 1,
                "courseTitle": "产前锻炼",
                "description": "米内特我惹你本宝宝搜索发布导包导包",
                "recommendedCoefficient": 3,
                "pictures": [
                    "http://static.mifanxing.com/iyyren/image/201806/06/1638/3478657327024209921.jpg",
                    "http://static.mifanxing.com/iyyren/image/201806/06/1638/3478657327024209922.jpg"
                ]
            }
        ]
      }
      
### 查询课程详情 [GET] /courses/{id}

+ Response 200 (application/json)
    
      {
        "data": {
            "id": 1,
            "enabled": 1,
            "creator": 0,
            "modifier": 0,
            "created": "2019-04-10 15:20:05",
            "modified": "2019-04-10 15:20:05",
            "levelId": 3,
            "courseTitle": "产后恢复",
            "description": "上菜鸟winVB让她宝宝贝贝人不同让宝宝",
            "content": "合同如火如荼好人挺好玩儿是的深V是VB填入黑胡椒一次次地CSAC阿萨阿所产生的吃的是草",
            "recommendedCoefficient": 2,
            "pictures": [
                "http://static.mifanxing.com/iyyren/image/201806/06/1638/347865732702420992.jpg"
            ]
        }
      }  

## 活动报名
+ Data
  + Activity - 活动表 
    + activityTitle (String) - 活动标题
    + content (String) - 活动内容
    + postDate (Date) - 发布时间
    + recommendOrder (int) - 推荐系数
    + hasSign (int) - 是否可以报名；0：否，1：是（默认1可报名）
    + enabled (int) - 0禁用 1启用
    + creator (Long) - 创建人
    + modifier (Long) - 修改人
    + created (date) - 创建时间
    + modified (date) - 修改时间
  + ActivitySign - 活动报名表
    + activityId (int) - 活动标识
    + userId (int) - 用户标识
    + enabled (int) - 0禁用 1启用
    + creator (Long) - 创建人
    + modifier (Long) - 修改人
    + created (date) - 创建时间
    + modified (date) - 修改时间
    + pictures - 图片
 
### 活动列表 [GET] /activitys
+ Parameters
  + filter[recommendOrder:ge]=1&sort=recommendOrder(推荐接口固定参数)
  + page[number]=1&page[size]=10
  + sort -modified(从新到旧) | modified(从旧到新)
+ Response 200 (application/json)(活动列表展示)
    
      {
        "meta": {
            "totalPages": 1,
            "totalElements": 2,
            "size": 10,
            "number": 1,
            "numberOfElements": 2,
            "first": true,
            "last": true,
            "sort": null
        },
        "links": {
            "self": "/activitys?page[number]=1&page[size]=10",
            "first": "/activitys?page[number]=1&page[size]=10",
            "last": "/activitys?page[number]=1&page[size]=10"
        },
        "data": [
            {
                "id": 1,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-04-11 11:41:01",
                "modified": "2019-04-11 11:41:04",
                "activityTitle": "孕妇一日游活动",
                "content": "报辅导班投标人突然不容易被被污染别人吧不要让",
                "postDate": "2019-04-11 11:05",
                "recommendOrder": 0,
                "hasSign": 1,
                "pictures": [
                    "http://static.mifanxing.com/article/image/215/69/4577111.jpg"
                ]
            },
            {
                "id": 2,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-04-11 11:41:09",
                "modified": "2019-04-11 11:41:06",
                "activityTitle": "别的地方活动",
                "content": "办公设备的深V的深V定时",
                "postDate": "2019-04-11 11:10",
                "recommendOrder": 2,
                "hasSign": 1,
                "pictures": [
                    "http://static.mifanxing.com/article/image/215/69/4577111.jpg"
                ]
            }
        ]
      }
+ Response 200 (application/json)(近期活动推荐列表展示)

      {
        "meta": {
            "totalPages": 1,
            "totalElements": 4,
            "size": 10,
            "number": 1,
            "numberOfElements": 4,
            "first": true,
            "last": true,
            "sort": [
                {
                    "direction": "ASC",
                    "property": "recommend_order",
                    "ignoreCase": false,
                    "nullHandling": "NATIVE",
                    "ascending": true,
                    "descending": false
                }
            ]
        },
        "links": {
            "self": "/activitys?filter[recommendOrder:ge]=1&sort=recommendOrder&page[number]=1&page[size]=10",
            "first": "/activitys?filter[recommendOrder:ge]=1&sort=recommendOrder&page[number]=1&page[size]=10",
            "last": "/activitys?filter[recommendOrder:ge]=1&sort=recommendOrder&page[number]=1&page[size]=10"
        },
        "data": [
            {
                "id": 3,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-04-11 11:41:14",
                "modified": "2019-04-11 11:41:12",
                "activityTitle": "某某活动",
                "content": "欧泊今年尽可能地深V是DVD是",
                "postDate": "2019-04-11 11:14",
                "recommendOrder": 1,
                "hasSign": 1,
                "pictures": [
                    "http://static.mifanxing.com/article/image/215/69/4577111.jpg"
                ]
            },
            {
                "id": 2,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-04-11 11:41:09",
                "modified": "2019-04-11 11:41:06",
                "activityTitle": "别的地方活动",
                "content": "办公设备的深V的深V定时",
                "postDate": "2019-04-11 11:10",
                "recommendOrder": 2,
                "hasSign": 1,
                "pictures": [
                    "http://static.mifanxing.com/article/image/215/69/4577111.jpg"
                ]
            },
            {
                "id": 4,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-04-11 11:41:22",
                "modified": "2019-04-11 11:41:18",
                "activityTitle": "哈哈活动",
                "content": "难舍难分大部分大师班北师大版",
                "postDate": "2019-04-11 11:15",
                "recommendOrder": 3,
                "hasSign": 1,
                "pictures": [
                    "http://static.mifanxing.com/article/image/215/69/4577111.jpg"
                ]
            },
            {
                "id": 5,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-04-11 11:47:34",
                "modified": "2019-04-11 11:47:31",
                "activityTitle": "风儿活动",
                "content": "那个防守打法部署到发布发布放到",
                "postDate": "2019-04-11 11:47",
                "recommendOrder": 4,
                "hasSign": 1,
                "pictures": [
                    "http://static.mifanxing.com/article/image/215/69/4577111.jpg"
                ]
            }
        ]
      }

### 查询活动详情 [GET] /activitys/{id}

+ Response 200 (application/json)
    
      {
        "data": {
            "id": 1,
            "enabled": 1,
            "creator": 0,
            "modifier": 0,
            "created": "2019-04-11 11:41:01",
            "modified": "2019-04-11 11:41:04",
            "activityTitle": "孕妇一日游活动",
            "content": "报辅导班投标人突然不容易被被污染别人吧不要让",
            "postDate": "2019-04-11 11:05",
            "recommendOrder": 0,
            "hasSign": 1,
            "pictures": [
                "http://static.mifanxing.com/article/image/215/69/4577111.jpg"
            ]
        }
      } 
### 查询活动报名 [GET] /activitySigns/usersinUp?userId={id}&activityId={id}
+ Parameters
  +  userId 用户ID
  +  activityId 活动ID
+ Description
  +  查询活动报名接口与客户端查看活动详情接口共同用，做用户对本活动是否参加的操作
  +  isShow;1为该用户已报名，0为此用户未报名

+ Response 200 (application/json)

      {
        "data": {
            "activityId": 3,
            "userId": 1,
            "isShow": 1
        }
      }

## 孕产知识
+ Data
  + Knowledge - 孕产知识表 
    + knowledgeTitle (String) - 知识库标题
    + content (String) - 知识库内容
    + postUserName (String) - 作者
    + postDate (Date) - 发布时间
    + recommendOrder (int) -推荐系数
    + enabled (int) - 0禁用 1启用
    + creator (Long) - 创建人
    + modifier (Long) - 修改人
    + created (date) - 创建时间
    + modified (date) - 修改时间
    + pictures - 图片  

### 孕产知识列表 [GET] /knowledges
+ Parameters
  + filter[recommendOrder:ge]=1&sort=recommendOrder(推荐接口固定参数)
  + page[number]=1&page[size]=10
  + sort -modified(从新到旧) | modified(从旧到新)
+ Response 200 (application/json)(孕产知识列表展示)
    
      {
        "meta": {
            "totalPages": 1,
            "totalElements": 4,
            "size": 10,
            "number": 1,
            "numberOfElements": 4,
            "first": true,
            "last": true,
            "sort": null
        },
        "links": {
            "self": "/knowledges?page[number]=1&page[size]=10",
            "first": "/knowledges?page[number]=1&page[size]=10",
            "last": "/knowledges?page[number]=1&page[size]=10"
        },
        "data": [
            {
                "id": 1,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "knowledgeTitle": "备孕知识",
                "content": "美味哦烦么恶女噢未能非农",
                "postDate": "2019-04-11 15:08",
                "recommendOrder": 2,
                "pictures": [
                    "http://static.mifanxing.com/iyyren/image/201806/06/1638/347865732702420992.jpg"
                ]
            },
            {
                "id": 2,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "knowledgeTitle": "产前知识",
                "content": "南方不方便大幅度发不发达",
                "postDate": "2019-04-11 15:08",
                "recommendOrder": 1,
                "pictures": [
                    "http://static.mifanxing.com/iyyren/image/201806/06/1638/3478657327024209921.jpg"
                ]
            },
            {
                "id": 3,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "knowledgeTitle": "产后护理",
                "content": "你发斯蒂芬表大师班",
                "postDate": "2019-04-11 15:09",
                "recommendOrder": 3,
                "pictures": [
                    "http://static.mifanxing.com/article/image/215/69/4577111.jpg"
                ]
            },
            {
                "id": 4,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "knowledgeTitle": "健康知识",
                "content": "贝多芬部分榜单榜单吧",
                "postDate": "2019-04-11 15:10",
                "recommendOrder": 0,
                "pictures": [
                    "http://static.mifanxing.com/article/image/215/69/4577111.jpg"
                ]
            }
        ]
      }

+ Response 200 (application/json)(孕产推荐列表展示)
    
      {
        "meta": {
            "totalPages": 1,
            "totalElements": 3,
            "size": 10,
            "number": 1,
            "numberOfElements": 3,
            "first": true,
            "last": true,
            "sort": [
                {
                    "direction": "ASC",
                    "property": "recommend_order",
                    "ignoreCase": false,
                    "nullHandling": "NATIVE",
                    "ascending": true,
                    "descending": false
                }
            ]
        },
        "links": {
            "self": "/knowledges?filter[recommendOrder:ge]=1&sort=recommendOrder&page[number]=1&page[size]=10",
            "first": "/knowledges?filter[recommendOrder:ge]=1&sort=recommendOrder&page[number]=1&page[size]=10",
            "last": "/knowledges?filter[recommendOrder:ge]=1&sort=recommendOrder&page[number]=1&page[size]=10"
        },
        "data": [
            {
                "id": 2,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "knowledgeTitle": "产前知识",
                "content": "南方不方便大幅度发不发达",
                "postDate": "2019-04-11 15:08",
                "recommendOrder": 1,
                "pictures": [
                    "http://static.mifanxing.com/iyyren/image/201806/06/1638/3478657327024209921.jpg"
                ]
            },
            {
                "id": 1,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "knowledgeTitle": "备孕知识",
                "content": "美味哦烦么恶女噢未能非农",
                "postDate": "2019-04-11 15:08",
                "recommendOrder": 2,
                "pictures": [
                    "http://static.mifanxing.com/iyyren/image/201806/06/1638/347865732702420992.jpg"
                ]
            },
            {
                "id": 3,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "knowledgeTitle": "产后护理",
                "content": "你发斯蒂芬表大师班",
                "postDate": "2019-04-11 15:09",
                "recommendOrder": 3,
                "pictures": [
                    "http://static.mifanxing.com/article/image/215/69/4577111.jpg"
                ]
            }
        ]
      }

### 孕产知识详情 [GET] /knowledges/{id}

+ Response 200 (application/json)

      {
        "data": {
            "id": 1,
            "enabled": 1,
            "creator": 0,
            "modifier": 0,
            "knowledgeTitle": "备孕知识",
            "content": "美味哦烦么恶女噢未能非农",
            "postDate": "2019-04-11 15:08",
            "recommendOrder": 2,
            "pictures": [
                "http://static.mifanxing.com/iyyren/image/201806/06/1638/347865732702420992.jpg"
            ]
        }
      }



