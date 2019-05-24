## 孕产平台客户端
+ 2019年04月12日
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

### 教练介绍列表 [GET] /users/clientShowTeacher?filter[identity]=1
+ Parameters
  + identity  0：学生，1：教练
  + sort -modified(从新到旧) | modified(从旧到新)

+ Response 200 (application/json)

      {
        "meta": {
            "totalPages": 1,
            "totalElements": 6,
            "size": 10,
            "number": 1,
            "numberOfElements": 6,
            "first": true,
            "last": true,
            "sort": null
        },
        "links": {
            "self": "/users/clientShowTeacher?filter[identity]=1&page[number]=1&page[size]=10",
            "first": "/users/clientShowTeacher?filter[identity]=1&page[number]=1&page[size]=10",
            "last": "/users/clientShowTeacher?filter[identity]=1&page[number]=1&page[size]=10"
        },
        "data": [
            {
                "id": 2,
                "realName": "白求恩",
                "jobTitle": "高级教练",
                "photo": "http://static.mifanxing.com/iyyren/image/201806/06/1638/347865732702420992.jpg",
                "hasCard": false
            },
            {
                "id": 3,
                "realName": "张三",
                "jobTitle": "中级教练",
                "photo": "http://static.mifanxing.com/iyyren/image/201803/15/1453/317761140065189888.jpg",
                "hasCard": false
            },
            {
                "id": 4,
                "realName": "小高",
                "jobTitle": "助教",
                "photo": "http://static.mifanxing.com/iyyren/image/201803/15/1453/317761140065189888.jpg",
                "hasCard": false
            },
            {
                "id": 5,
                "realName": "ycl",
                "hasCard": false
            },
            {
                "id": 18,
                "realName": "生日快了",
                "jobTitle": "高级教师",
                "photo": "tupian.jpg",
                "hasCard": false
            },
            {
                "id": 22,
                "realName": "张老师",
                "jobTitle": "高级教师",
                "photo": "tupian.jpg",
                "hasCard": false
            }
        ]
      }

### 教练详情 [GET] /users/{id}
+ Parameters
    + id - 教练id（示例id=2）
+ Response 200 (application/json)
    
      {
        "data": {
            "id": 24,
            "enabled": 1,
            "creator": 0,
            "modifier": 0,
            "created": "2019-05-07 16:49:37",
            "modified": "2019-05-07 16:49:37",
            "wechatId": "oGxm-4vdnp2-gDUaiov4yxlTYwQU",
            "phoneNumber": "17600261644",
            "pwdLogIn": 0,
            "identity": 1,
            "isAdmin": 0,
            "nickname": "小白",
            "realName": "江小白",
            "sex": 1,
            "organizationId": 0,
            "pregnancyStage": 0,
            "regionId": 301,
            "address": "山西运城",
            "avatar": "https://wx.qlogo.cn/mmopen/vi_32/vib6CNBXrDLZcicF9cZsC7uLFwclnN7RXAgVnOYr9Ipfn6gT9QR8m8IMFx5UicPxniboHtVhty8aib29BDazXNL5ssw/132",
            "jobTitle": "中级教师",
            "photo": "https://wx.qlogo.cn/mmopen/vi_32/vib6CNBXrDLZcicF9cZsC7uLFwclnN7RXAgVnOYr9Ipfn6gT9QR8m8IMFx5UicPxniboHtVhty8aib29BDazXNL5ssw/132",
            "sexName": "男",
            "region": {
                "id": 301,
                "parentId": 231,
                "regionTitle": "运城市",
                "parent": {
                    "id": 231,
                    "parentId": 0,
                    "regionTitle": "山西省"
                }
            },
            "hasCard": false
        }
      }


### 用户修改个人信息[PUT]/users/profiles/{id}
+ Description
    + [MUST] authenticated
+ Request (application/json)
    
      {
    	"data":{
    		"nickname":"青城",
    		"realName":"张三1",
    		"sex":0,
    		"identity":"1",
    		"phoneNumber":"18810649838",
    		"birthday":"1967-01-01",
    		"pregnancyStage":1,
    		"pregnancyDate":"2017-06-22",
    		"address":"北京市丰台区云谷创业园",
    		"regionId":3,
    		"remarks":"个人同行业后台已经还特意与金太阳备注！！"
    	}
      }

+ Response 200
    
      {
        "data": 1
       }

### 获取手机验证码[PUTCH]/v1/teacher/users/sms_code?phone_number={id}
+ Parameters
    + phone_number - 手机号码
+ Request (application/json)
    
      {
        "errors": [
            {
                "status": "200",
                "title": "OK"
            }
        ]
      }

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
    + thumbnail (String) - 缩略图
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
                        "thumbnail": "http://static.mifanxing.com/article/image/215/69/4577111.jpg",
                        "description": "上菜鸟winVB让她宝宝贝贝人不同让宝宝",
                        "pictures": [
                            "http://static.mifanxing.com/iyyren/image/201806/06/1638/347865732702420992.jpg"
                        ]
                    },
                    {
                        "id": 7,
                        "courseTitle": "产前锻炼",
                        "thumbnail": "http://static.mifanxing.com/article/image/215/69/4577111.jpg",
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
                        "thumbnail": "http://static.mifanxing.com/article/image/215/69/4577111.jpg",
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
                        "thumbnail": "http://static.mifanxing.com/article/image/215/69/4577111.jpg",
                        "description": "上菜鸟winVB让她宝宝贝贝人不同让宝宝",
                        "pictures": [
                            "http://static.mifanxing.com/iyyren/image/201806/06/1638/347865732702420992.jpg"
                        ]
                    }
                ]
            }
        ]
      }
    
### 课程服务特别推荐列表 [GET] /courses?filter[recommend]=1&sort=-modified
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
                    "direction": "DESC",
                    "property": "modified",
                    "ignoreCase": false,
                    "nullHandling": "NATIVE",
                    "descending": true,
                    "ascending": false
                }
            ]
        },
        "links": {
            "self": "/courses?filter[recommend]=1&sort=-modified&page[number]=1&page[size]=10",
            "first": "/courses?filter[recommend]=1&sort=-modified&page[number]=1&page[size]=10",
            "last": "/courses?filter[recommend]=1&sort=-modified&page[number]=1&page[size]=10"
        },
        "data": [
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
                "recommend": 1,
                "pictures": [
                    "http://static.mifanxing.com/iyyren/image/201806/06/1638/3478657327024209921.jpg",
                    "http://static.mifanxing.com/iyyren/image/201806/06/1638/3478657327024209922.jpg"
                ]
            },
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
                "recommend": 1,
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
                "recommend": 1,
                "pictures": [
                    "http://static.mifanxing.com/iyyren/image/201806/06/1638/347865732702420992.jpg"
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
            "thumbnail": "http://static.mifanxing.com/article/image/215/69/4577111.jpg",
            "description": "上菜鸟winVB让她宝宝贝贝人不同让宝宝",
            "content": "合同如火如荼好人挺好玩儿是的深V是VB填入黑胡椒一次次地CSAC阿萨阿所产生的吃的是草",
            "recommend": 1,
            "pictures": [
                "http://static.mifanxing.com/iyyren/image/201806/06/1638/347865732702420991.jpg"
            ],
            "levelTitle": "高级"
        }
      }

### 获取短信验证码 [GET] /v1/teacher/users/sms_code?phone_number={id}
+ Response 200 (application/json)

      {
        "errors": [
            {
                "status": "200",
                "title": "OK"
            }
        ]
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
  + filter[recommend]=1&sort=-modified(推荐接口固定参数)
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
            "totalElements": 3,
            "size": 10,
            "number": 1,
            "numberOfElements": 3,
            "first": true,
            "last": true,
            "sort": [
                {
                    "direction": "DESC",
                    "property": "modified",
                    "ignoreCase": false,
                    "nullHandling": "NATIVE",
                    "descending": true,
                    "ascending": false
                }
            ]
        },
        "links": {
            "self": "/activitys?filter[recommend]=1&sort=-modified&page[number]=1&page[size]=10",
            "first": "/activitys?filter[recommend]=1&sort=-modified&page[number]=1&page[size]=10",
            "last": "/activitys?filter[recommend]=1&sort=-modified&page[number]=1&page[size]=10"
        },
        "data": [
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
                "stage": 0,
                "recommend": 1,
                "hasSign": 1,
                "pictures": [
                    "http://static.mifanxing.com/article/image/215/69/4577111.jpg"
                ]
            },
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
                "stage": 0,
                "recommend": 1,
                "hasSign": 1,
                "pictures": [
                    "http://static.mifanxing.com/article/image/215/69/4577111.jpg"
                ]
            },
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
                "stage": 0,
                "recommend": 1,
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
            "organizationId": 2,
            "stage": 0,
            "recommend": 1,
            "hasSign": 1,
            "pictures": [
                "http://static.mifanxing.com/article/image/215/69/4577116.jpg"
            ],
            "organizationTitle": "月子会所"
        }
      } 

### 活动报名 [POST] /activitySigns
+ Description
  +  [MUST] authenticated
+ Request (application/json)

      {
    	 "data":{
    		"activityId":"1",
    		"userId":"4"
    	 }
      }
+ Response 200 (application/json)
    
      {
        "data": {
            "id": 7,
            "type": "activitySigns"
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
  + filter[recommend]=1&sort=-modified(推荐接口固定参数)
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
                    "direction": "DESC",
                    "property": "modified",
                    "ignoreCase": false,
                    "nullHandling": "NATIVE",
                    "descending": true,
                    "ascending": false
                }
            ]
        },
        "links": {
            "self": "/knowledges?filter[recommend]=1&sort=-modified&page[number]=1&page[size]=10",
            "first": "/knowledges?filter[recommend]=1&sort=-modified&page[number]=1&page[size]=10",
            "last": "/knowledges?filter[recommend]=1&sort=-modified&page[number]=1&page[size]=10"
        },
        "data": [
            {
                "id": 4,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "modified": "2019-04-25 10:32:13",
                "knowledgeTitle": "健康知识",
                "content": "贝多芬部分榜单榜单吧",
                "postDate": "2019-04-11 15:10",
                "recommend": 1,
                "pictures": [
                    "http://static.mifanxing.com/article/image/215/69/4577111.jpg"
                ]
            },
            {
                "id": 3,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "modified": "2019-04-25 10:32:09",
                "knowledgeTitle": "产后护理",
                "content": "你发斯蒂芬表大师班",
                "postDate": "2019-04-11 15:09",
                "recommend": 1,
                "pictures": [
                    "http://static.mifanxing.com/article/image/215/69/4577111.jpg"
                ]
            },
            {
                "id": 1,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "modified": "2019-04-25 10:32:01",
                "knowledgeTitle": "备孕知识",
                "content": "美味哦烦么恶女噢未能非农",
                "postDate": "2019-04-11 15:08",
                "recommend": 1,
                "pictures": [
                    "http://static.mifanxing.com/iyyren/image/201806/06/1638/347865732702420992.jpg"
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

## 我的订单
+ Data
  + CardOrder - 订单表 
    + cardId (Long) - 卡标识
    + userId (Long) - 用户标识
    + packageType (int) - 套餐类型，0：新买课，1：续课，2，套餐升级
    + projectTitle (String) - 项目名称
    + cardNumber (String) - 卡号
    + money (BigDecimal) - 金额
    + classTime (BigDecimal) - 总课时数（含赠课数）
    + payMethod (int) - 支付方式，0：大众点评，1：支付宝，2：微信，3：现金，4：刷卡，5：其他
    + effectiveDate (Date) - 有效日期
    + salesperson (Long) - 销售教练
    + remarks (String) - 备注
    + enabled (int) - 0禁用 1启用
    + creator (Long) - 创建人
    + modifier (Long) - 修改人
    + created (date) - 创建时间
    + modified (date) - 修改时间
    + pictures - 图片  

### 我的订单列表 [GET] /cardOrders?filter[userId]=1&sort=-created

+ Parameters
  + page[number]=1&page[size]=10
  + sort -modified(从新到旧) | modified(从旧到新)
+ Description
    + packageTypeName (String) - 套餐类型名称
    + payMethodName (String) - 支付方式名称
    + salespersonName (String) - 销售教练名称

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
                    "direction": "DESC",
                    "property": "created",
                    "ignoreCase": false,
                    "nullHandling": "NATIVE",
                    "descending": true,
                    "ascending": false
                }
            ]
        },
        "links": {
            "self": "/cardOrders?filter[userId]=1&sort=-created&page[number]=1&page[size]=10",
            "first": "/cardOrders?filter[userId]=1&sort=-created&page[number]=1&page[size]=10",
            "last": "/cardOrders?filter[userId]=1&sort=-created&page[number]=1&page[size]=10"
        },
        "data": [
            {
                "id": 2,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-04-12 17:32:54",
                "modified": "2019-04-12 17:32:54",
                "cardId": 4,
                "userId": 1,
                "packageType": 1,
                "projectTitle": "免费体验课-续课1节",
                "cardNumber": "201904014000000",
                "money": 3,
                "classTime": 5,
                "payMethod": 2,
                "effectiveDate": "2020-02-01",
                "salesperson": 2,
                "remarks": "不是吧大神，那卖方都南方"
            },
            {
                "id": 3,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-04-12 17:32:54",
                "modified": "2019-04-14 17:32:58",
                "cardId": 5,
                "userId": 1,
                "packageType": 0,
                "projectTitle": "孕产套课-升级12节",
                "cardNumber": "201904014000001",
                "money": 16000,
                "classTime": 25,
                "payMethod": 1,
                "effectiveDate": "2020-03-01",
                "salesperson": 3,
                "remarks": "fd三年内他那样天南地北"
            },
            {
                "id": 1,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-03-14 17:32:48",
                "modified": "2019-03-14 17:32:48",
                "cardId": 4,
                "userId": 1,
                "packageType": 0,
                "projectTitle": "1节免费体验课",
                "cardNumber": "201904014000000",
                "money": 3,
                "classTime": 5,
                "payMethod": 1,
                "effectiveDate": "2020-01-01",
                "salesperson": 1,
                "remarks": "那你说打发布到圣彼得堡"
            }
        ]
      }

### 订单详情 [GET] /cardOrders/{id}

+ Response 200 (application/json)

      {
        "data": {
            "id": 2,
            "enabled": 1,
            "creator": 0,
            "modifier": 0,
            "created": "2019-04-12 17:32:54",
            "modified": "2019-04-12 17:32:54",
            "cardId": 4,
            "userId": 1,
            "packageType": 1,
            "projectTitle": "免费体验课-续课1节",
            "cardNumber": "201904014000000",
            "money": 3,
            "classTime": 5,
            "payMethod": 2,
            "effectiveDate": "2020-02-01",
            "salesperson": 2,
            "remarks": "不是吧大神，那卖方都南方",
            "packageTypeName": "续课",
            "payMethodName": "微信",
            "salespersonName": "贝多芬"
        }
      }

## 我的课程

+ Data
  + Card - 发卡表 
    + userId (Long) - 学生/用户id
    + cardNumber (String) - 卡号
    + state (int) - 状态，0：审核中，1：正常，2：请假中，3：审核未通过
    + realName (String) - 姓名
    + birthday (Date) - 生日
    + pregnancyStage (int) - 孕产阶段，0：未知，1：备孕，2：怀孕，3：产后
    + pregnancyDate (Date) - 孕产日期
    + address (String) - 地址
    + packageType (int) - 套餐类型，0：新买课，1：续课，2，套餐升级
    + projectId (Long) - 项目标识
    + money (BigDecimal) - 金额
    + classTime (BigDecimal) - 课时数/购课数
    + giftClassTime (BigDecimal) - 赠送课时/课数
    + remainingClassTime (BigDecimal) - 剩余课时
    + salesperson (Long) - 销售教练
    + effectiveDate (Date) - 有效日期
    + customerSourceId (Long) - 客户来源标识
    + payMethod (int) - 支付方式，0：大众点评，1：支付宝，2：微信，3：现金，4：刷卡，5：其他
    + inside (int) - 0：场外，1：场内
    + dtd (int) - 是否有上门，0：否，1：是
    + dtdFee (BigDecimal) - 上门费
    + remarks (String) - 备注
    + leaveRemainingNum (int) - 请假剩余次数
    + leaveRemainingDays (int) - 请假剩余天数
    + enabled (int) - 0禁用 1启用
    + creator (Long) - 创建人
    + modifier (Long) - 修改人
    + created (date) - 创建时间
    + modified (date) - 修改时间
    + pictures - 图片
  + AttendClass - 预约/上课表
    + state (int) - 状态，0：已预约，1：进行中，2：已完结，3：预约失败
    + categoryId (Long) - 上课类型标识
    + attendDate (Date) - 上课日期
    + beginTime (Date) - 上课时间
    + endTime (Date) - 下课时间
    + timeLength (BigDecimal) - 上课时长
    + courseLevelId (Long) - 课程级别标识
    + place (int) - 场所，0：到店，1：上门
    + shopId (Long) - 门店标识
    + address (String) - 上课地址
    + longitude (BigDecimal) - 经度
    + latitude (BigDecimal) - 纬度
    + remarks (String) - 备注
    + enabled (int) - 0禁用 1启用
    + creator (Long) - 创建人
    + modifier (Long) - 修改人
    + created (date) - 创建时间
    + modified (date) - 修改时间 
  + Summary - 小结表 
    + Id (Long) - 同预约上课id
    + studentNum (int) - 到场上课人数
    + studentRemarks (String) - 给客户的备注
    + coachRemarks (String) - 给教练/销售的备注
    + attendClassContent (String) - 上课内容
    + hasDtdFee (int) - 是否收取上门费，0：否，1：是
    + keyUser (String) - 重点用户记录
    + enabled (int) - 0禁用 1启用
    + creator (Long) - 创建人
    + modifier (Long) - 修改人
    + created (date) - 创建时间
    + modified (date) - 修改时间 
  + SummaryAction - 小结动作表 
    + summaryId (Long) - 小结id
    + actionId (Long) - 动作标识
    + groupsCount (int) - 做了几组
    + groupActionCount (int) - 每组几个 
    + enabled (int) - 0禁用 1启用
    + creator (Long) - 创建人
    + modifier (Long) - 修改人
    + created (date) - 创建时间
    + modified (date) - 修改时间  
### 我的课程列表 [GET] /v1/teacher/cards?filter[userId]=2&sort=-modified

+ Parameters
  + page[number]=1&page[size]=10
  + sort -modified(从新到旧) | modified(从旧到新)
+ Description
    + projectName - 项目名称
    + attendClass - 完结的课程
    + SalespersonName  - 销售教练名称

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
            "sort": [
                {
                    "direction": "DESC",
                    "property": "modified",
                    "ignoreCase": false,
                    "nullHandling": "NATIVE",
                    "descending": true,
                    "ascending": false
                }
            ]
        },
        "links": {
            "self": "/v1/teacher/cards?filter[userId]=2&sort=-modified&page[number]=1&page[size]=10",
            "first": "/v1/teacher/cards?filter[userId]=2&sort=-modified&page[number]=1&page[size]=10",
            "last": "/v1/teacher/cards?filter[userId]=2&sort=-modified&page[number]=1&page[size]=10"
        },
        "data": [
            {
                "id": 12,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-04-15 13:48:55",
                "modified": "2019-04-15 13:48:55",
                "userId": 2,
                "cardNumber": "20190415000001",
                "state": 0,
                "realName": "阿斯达",
                "birthday": "2019-04-15",
                "pregnancyStage": 3,
                "pregnancyDate": 1575129600000,
                "address": "上海市静安区福泽小区一单元301室",
                "packageType": 0,
                "projectId": 12,
                "money": 9600,
                "classTime": 14,
                "giftClassTime": 0,
                "remainingClassTime": 11,
                "salesperson": 2,
                "effectiveDate": "2020-05-15",
                "customerSourceId": 2,
                "payMethod": 3,
                "inside": 0,
                "dtd": 0,
                "dtdFee": 0,
                "remarks": "新购卡备注信息",
                "leaveRemainingNum": 2,
                "leaveRemainingDays": 30,
                "projectName": "25节孕产套课",
                "salespersonName": "贝多芬"
            },
            {
                "id": 5,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-02-15 13:48:51",
                "modified": "2019-02-15 13:48:51",
                "userId": 2,
                "cardNumber": "20190414000001",
                "state": 0,
                "realName": "李四",
                "birthday": "2019-04-15",
                "pregnancyStage": 2,
                "pregnancyDate": 1576339200000,
                "address": "上海市静安区福泽小区一单元301室",
                "packageType": 0,
                "projectId": 11,
                "money": 9600,
                "classTime": 1,
                "giftClassTime": 0,
                "remainingClassTime": 8,
                "salesperson": 2,
                "effectiveDate": "2020-02-02",
                "customerSourceId": 2,
                "payMethod": 2,
                "inside": 0,
                "dtd": 0,
                "dtdFee": 0,
                "remarks": "DVD发包人同人本闪电风暴备注信息",
                "leaveRemainingNum": 1,
                "leaveRemainingDays": 10,
                "projectName": "1节免费体验课",
                "salespersonName": "贝多芬"
            }
        ]
      }

### 卡详情 [GET] /v1/teacher/cards/{id}
+ Parameters
    + id - 为开卡的id 
    + 例：id = 4
+ Description
    + projectName - 项目名称
+ Response 200 (application/json)

      {
        "data": {
            "id": 4,
            "enabled": 1,
            "creator": 0,
            "modifier": 0,
            "created": "2019-04-25 13:52:51",
            "modified": "2019-04-25 13:52:51",
            "userId": 1,
            "cardNumber": "20190414000000",
            "state": 1,
            "realName": "海燕",
            "birthday": "2019-04-15",
            "pregnancyStage": 1,
            "address": "上海市黄浦区幸福小区一单元201室",
            "packageType": 0,
            "projectId": 9,
            "money": 12000,
            "classTime": 18,
            "giftClassTime": 0,
            "remainingClassTime": 10,
            "salesperson": 3,
            "effectiveDate": "2021-02-19",
            "payMethod": 1,
            "inside": 1,
            "dtd": 1,
            "dtdFee": 200,
            "remarks": "你是听你说打发布到封神榜备注信息",
            "leaveRemainingNum": 1,
            "leaveRemainingDays": 10,
            "projectName": "12节孕期瑜伽小班课"
        }
      }
    
### 卡上课记录列表 [GET] /studentAttendClass/attendClassRecord?cardId={id}
+ Parameters
    + {id} 为开卡的id 
    + 例：id = 4
+ Description
    + attendTypeName - 课程性质
    + attendTimeBucket - 上课时间段
    + mianCoachName - 主教练
    + assistCoachName - 助练
    + placeName -场所名称
+ Response 200 (application/json)
    
      {
        "data": [
            {
                "id": 4,
                "categoryId": 1,
                "attendDate": "2019-04-16",
                "beginTime": "16:17",
                "endTime": "16:30",
                "place": 0,
                "attendTypeName": "公开课",
                "attendTimeBucket": "2019-04-16 16:17-16:30",
                "mianCoachName": "贝多芬",
                "assistCoachName": "小高",
                "placeName": "到店"
            },
            {
                "id": 5,
                "categoryId": 2,
                "attendDate": "2019-04-17",
                "beginTime": "16:34",
                "endTime": "16:44",
                "place": 1,
                "attendTypeName": "私教课",
                "attendTimeBucket": "2019-04-17 16:34-16:44",
                "mianCoachName": "张三",
                "placeName": "上门"
            }
        ]
      }

### 课程小结 [GET] /summary/{id}

+ Parameters
    + id - 小结id 
    + 例：id = 4
+ Description
    + actionTitle - 动作库标题
    + actionImage  - 动作库图片
    + attendRecord - 上课记录
+ Response 200 (application/json)

       {
        "data": {
            "id": 4,
            "enabled": 1,
            "creator": 0,
            "modifier": 0,
            "created": "2019-04-15 20:07:38",
            "modified": "2019-04-15 20:07:32",
            "studentNum": 1,
            "studentRemarks": "客户上课认真~~给用户的备注",
            "coachRemarks": "教练上课指导好！",
            "hasDtdFee": 0,
            "placeName": "到店",
            "attendTimeBucket": "2019-04-16 16:17~16:30",
            "attendRecord": [
                {
                    "id": 1,
                    "summaryId": 4,
                    "actionId": 1,
                    "groupsCount": 5,
                    "groupActionCount": 600,
                    "actionTitle": "俯卧撑",
                    "actionImage": "http://static.mifanxing.com/iyyren/image/201806/06/1638/347865732702420992.jpg"
                }
            ],
            "placeAddress": "上海市静安区胜利路521号",
            "mianCoachName": "贝多芬",
            "assistCoachName": "小高",
            "task": [
                {
                    "id": 1,
                    "enabled": 1,
                    "creator": 0,
                    "modifier": 0,
                    "taskId": 4,
                    "actionId": 1,
                    "groupsCount": 2,
                    "groupActionCount": 30,
                    "actionTitle": "俯卧撑",
                    "actionImage": "http://static.mifanxing.com/iyyren/image/201806/06/1638/347865732702420992.jpg"
                },
                {
                    "id": 2,
                    "enabled": 1,
                    "creator": 0,
                    "modifier": 0,
                    "taskId": 4,
                    "actionId": 2,
                    "groupsCount": 4,
                    "groupActionCount": 100,
                    "actionTitle": "仰卧起坐",
                    "actionImage": "http://static.mifanxing.com/iyyren/image/201806/06/1638/347865732702420992.jpg"
                }
            ]
        }
      }


### 课程小结中我的评价展示 [GET] /comments/commentsDetails
+ Parameters
    + userId - 用户id
    + attendClassId - 上课id 
    + ?userId=1&attendClassId=1（示例）
+ Description
    + content - 评价内容
+ Response 200 (application/json)

      {
        "data": {
            "id": 2,
            "enabled": 1,
            "creator": 0,
            "modifier": 0,
            "created": "2019-04-16 19:01:10",
            "modified": "2019-04-16 19:01:08",
            "studentAttendClassId": 1,
            "userId": 1,
            "attendClassId": 1,
            "content": "第三方不放过还让他辉丰股份那个一样号如果还让他",
            "coachScore": 0,
            "attendClassScore": 0,
            "serviceScore": 0
        }
      }

### 上课记录详情[GET]/summaryActions{id}

+ Response 200 (application/json)
    
      {
        "data": {
            "id": 35,
            "summaryId": 56,
            "actionId": 1,
            "groupsCount": 5,
            "groupActionCount": 12,
            "actionTitle": "俯卧撑",
            "actionImage": "http://static.mifanxing.com/iyyren/image/201806/06/1638/347865732702420992.jpg",
            "categoryTitle": "室内",
            "ranking": 0
        }
      }

### 课后作业详情[GET]/taskActions{id}

+ Response 200 (application/json)

      {
        "data": {
            "id": 25,
            "enabled": 1,
            "creator": 24,
            "modifier": 0,
            "created": "2019-05-20 18:50:43",
            "modified": "2019-05-20 18:50:43",
            "taskId": 55,
            "actionId": 3,
            "groupsCount": 22,
            "groupActionCount": 22,
            "actionTitle": "瑜伽锻炼",
            "categoryTitle": "室内",
            "ranking": 0,
            "actionImage": "http://static.mifanxing.com/iyyren/image/201806/06/1638/347865732702420992.jpg"
        }
      }

## 我的老师
### 开卡教练列表[GET] /v1/teacher/cards/openCardCoach?userId=1
+ Parameters
    + userId id 用户id
+ Description
    + 解释：当开卡状态为0：审核中，3：审核未通过时教练不在列表中展示
+ Response 200 (application/json)
    
      {
        "data": [
            {
                "id": 2,
                "realName": "白求恩",
                "jobTitle": "高级教练",
                "coachContent": "教练详情介绍。。",
                "photo": "http://static.mifanxing.com/iyyren/image/201806/06/1638/347865732702420992.jpg",
                "hasCard": false
            },
            {
                "id": 3,
                "realName": "张三",
                "jobTitle": "中级教练",
                "photo": "http://static.mifanxing.com/iyyren/image/201803/15/1453/317761140065189888.jpg",
                "hasCard": false
            }
        ]
      }

### 为用户服务过教练列表[GET]/studentAttendClass/userCoach?userId=1
    
+ Parameters
    + userId  用户id
+ Response 200 (application/json)

      {
        "data": [
            {
                "id": 4,
                "realName": "小高",
                "jobTitle": "助教",
                "photo": "http://static.mifanxing.com/iyyren/image/201803/15/1453/317761140065189888.jpg"
            }
        ]
      }

## 我的作业
+ Data
  + Task - 作业表 
    + id (Long) - 主键，同预约/上课id
    + userId (Long) - 给谁的作业（冗余）
    + enabled (int) - 0禁用 1启用
    + creator (Long) - 创建人
    + modifier (Long) - 修改人
    + created (date) - 创建时间
    + modified (date) - 修改时间
  + TaskAction - 作业动作库表 
    + taskId (Long) - 作业id
    + actionId (Long) - 动作id
    + groupsCount (int) - 做了几组
    + groupActionCount (int) - 每组几个
    + enabled (int) - 0禁用 1启用
    + creator (Long) - 创建人
    + modifier (Long) - 修改人
    + created (date) - 创建时间
    + modified (date) - 修改时间
### 我的作业列表[GET]/tasks?filter[userId]=1&sort=-modified
+ Parameters
  + userId - 用户id（例用户为1）
  + page[number]=1&page[size]=10
  + sort -modified(从新到旧) | modified(从旧到新)
+ Description
    + mianCoachName - 主教练
    + assistCoachName - 助教
    + attendDate  - 课程上课时间
    + created - 作业创建时间

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
            "sort": [
                {
                    "direction": "DESC",
                    "property": "modified",
                    "ignoreCase": false,
                    "nullHandling": "NATIVE",
                    "ascending": false,
                    "descending": true
                }
            ]
        },
        "links": {
            "self": "/tasks?filter[userId]=1&sort=-modified&page[number]=1&page[size]=10",
            "first": "/tasks?filter[userId]=1&sort=-modified&page[number]=1&page[size]=10",
            "last": "/tasks?filter[userId]=1&sort=-modified&page[number]=1&page[size]=10"
        },
        "data": [
            {
                "id": 5,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-04-18 17:49:20",
                "modified": "2019-04-18 17:49:12",
                "userId": 1,
                "mianCoachName": "张三",
                "attendDate": "2019-04-17"
            },
            {
                "id": 4,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-04-18 17:49:17",
                "modified": "2019-04-18 17:49:10",
                "userId": 1,
                "mianCoachName": "贝多芬",
                "assistCoachName": "小高",
                "attendDate": "2019-04-16"
            }
        ]
      }

### 课后作业内容描述[GET]/attendClass/attendClassSimpleDesc
+ Parameters
  + userId - 用户id（例用户为4）
  + userId=4&attendClassId=14（示例）
+ Description
    + attendTypeName - 课程分类性质
    + attendTimeBucket - 上课时间段
    + mianCoachName  - 主教练名称
    + attendClassNumber - 预约课上课人数
    + projectName -  项目名称
    + studentAttendClassStateName - 预约课状态

+ Response 200 (application/json)
    
       {
        "data": {
            "id": 14,
            "enabled": 1,
            "creator": 0,
            "modifier": 0,
            "state": 0,
            "categoryId": 2,
            "attendDate": "2019-04-25",
            "beginTime": "18:17",
            "endTime": "18:50",
            "timeLength": 0,
            "courseLevelId": 3,
            "place": 1,
            "shopId": 0,
            "address": "上海市宜家小区201室",
            "remarks": "",
            "attendTypeName": "私教课",
            "attendTimeBucket": "2019-04-25 18:17~18:50",
            "mianCoachName": "白求恩",
            "attendClassNumber": 1,
            "projectName": "孕产套课",
            "cardNumber": "20190422000000",
            "studentAttendClassStateName": "已预约",
            "placeName": "上门"
        }
     }

### 本节课后作业列表[GET]/taskActions?filter[taskId]=4
+ Parameters
  + userId - 用户id（例用户为4）
  + page[number]=1&page[size]=10
  + sort -modified(从新到旧) | modified(从旧到新)
+ Description
    + mianCoachName - 主教练
    + assistCoachName - 助教
    + attendDate  - 课程上课时间
    + created - 作业创建时间

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
            "self": "/taskActions?filter[taskId]=4&page[number]=1&page[size]=10",
            "first": "/taskActions?filter[taskId]=4&page[number]=1&page[size]=10",
            "last": "/taskActions?filter[taskId]=4&page[number]=1&page[size]=10"
        },
        "data": [
            {
                "id": 1,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "taskId": 4,
                "actionId": 1,
                "groupsCount": 2,
                "groupActionCount": 30,
                "actionTitle": "俯卧撑",
                "actionImage": "http://static.mifanxing.com/iyyren/image/201806/06/1638/347865732702420992.jpg"
            },
            {
                "id": 2,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "taskId": 4,
                "actionId": 2,
                "groupsCount": 4,
                "groupActionCount": 100,
                "actionTitle": "仰卧起坐",
                "actionImage": "http://static.mifanxing.com/iyyren/image/201806/06/1638/347865732702420992.jpg"
            }
        ]
      }

### 本节课后作业详情[GET]/taskActions/1   

+ Response 200 (application/json)

      {
        "data": {
            "id": 8,
            "enabled": 1,
            "creator": 0,
            "modifier": 0,
            "taskId": 6,
            "actionId": 5,
            "groupsCount": 1,
            "groupActionCount": 0,
            "actionTitle": "腿部按摩1111",
            "categoryTitle": "有氧室",
            "ranking": 0,
            "actionImage": "http://static.mifanxing.com/iyyren/image/201806/06/1638/1111111111.jpg"
        }
      }

## 我的预约
+ Data
  + Attachment - 图片表 
    + id (Long) - 
    + attUrl (String) - 
    + enabled (int) - 0禁用 1启用
    + creator (Long) - 创建人
    + modifier (Long) - 修改人
    + created (date) - 创建时间
    + modified (date) - 修改时间 

### 我的预约列表[GET]/studentAttendClass/myMakeAnAppointment

+ Parameters
  + userId - 用户id（例如用户id为1）
  + userId=2（示例）
  
+ Description
    + leaveTimeBucket - 请假时间
    + leaveStateName - 请假状态名称
+ Response 200 (application/json)

      {
        "data": [
            {
                "id": 5,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-04-23 14:03:01",
                "modified": "2019-04-23 14:02:59",
                "state": 0,
                "categoryId": 1,
                "attendDate": "2019-04-17",
                "beginTime": "16:34",
                "endTime": "16:44",
                "timeLength": 1.5,
                "courseLevelId": 1,
                "place": 1,
                "shopId": 0,
                "address": "",
                "remarks": "",
                "attendTypeName": "公开课",
                "attendTimeBucket": "16:34-16:44",
                "mianCoachName": "张三",
                "placeName": "上门"
            },
            {
                "id": 4,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-04-16 14:02:57",
                "modified": "2019-04-16 14:02:54",
                "state": 0,
                "categoryId": 2,
                "attendDate": "2019-04-16",
                "beginTime": "16:17",
                "endTime": "16:30",
                "timeLength": 2,
                "courseLevelId": 2,
                "place": 0,
                "shopId": 1,
                "address": "上海市黄浦区幸福小区一单元201室",
                "remarks": "东方国际南方",
                "attendTypeName": "私教课",
                "attendTimeBucket": "16:17-16:30",
                "mianCoachName": "白求恩",
                "assistCoachName": "小高",
                "placeName": "到店"
            }
        ]
      }

### 预约详情[GET]/studentAttendClass/myMakeAnAppointment/details?attendClassId={attendClassId}&userId={userId}
+ Parameters
  + attendClassId - 用户预约课id
  + userId - 用户id
  + attendClassId=14&userId=4 （私教课程详情接口事例）
  + attendClassId=8&userId=1  （公开课程详情接口事例）
+ Description
    + attendTypeName - 课程性质
    + attendTimeBucket - 上课时间段
    + attendClassNumber - 上课人数
    + projectName - 项目名称
    + studentAttendClassStateName - 学生上课状态
    + placeName - 私教课场所名称
    + clubName - 公开课会所名称
    + isShowSign -  签到是否展示（true：展示，false：不展示）
+ Response 200 (application/json)（私教课程展示）
    
      {
        "data": {
            "id": 14,
            "enabled": 1,
            "creator": 0,
            "modifier": 0,
            "created": "2019-04-28 13:32:59",
            "modified": "2019-04-28 13:32:59",
            "state": 3,
            "categoryId": 2,
            "attendDate": "2019-04-30",
            "beginTime": "18:20",
            "endTime": "18:50",
            "timeLength": 0,
            "courseLevelId": 3,
            "place": 1,
            "shopId": 0,
            "regionId": 6,
            "address": "上海市宜家小区201室",
            "remarks": "",
            "attendTypeName": "私教课",
            "attendTimeBucket": "2019-04-30 18:20~18:50",
            "mianCoachName": "白求恩",
            "attendClassNumber": 1,
            "projectName": "孕产套课",
            "cardNumber": "20190422000000",
            "studentAttendClassStateName": "已取消",
            "studentAttendClassId": 11,
            "region": {
                "id": 6,
                "parentId": 5,
                "regionTitle": "黄浦区",
                "parent": {
                    "id": 5,
                    "parentId": 4,
                    "regionTitle": "上海市",
                    "parent": {
                        "id": 4,
                        "parentId": 0,
                        "regionTitle": "上海"
                    }
                }
            },
            "placeName": "上门",
            "showSign": true
        }
      }
+ Response 200 (application/json)（公开课程展示）
    
        {
        "data": {
            "id": 8,
            "enabled": 1,
            "creator": 0,
            "modifier": 0,
            "state": 0,
            "categoryId": 1,
            "attendDate": "2019-04-25",
            "beginTime": "17:13",
            "endTime": "17:53",
            "timeLength": 0,
            "courseLevelId": 3,
            "place": 0,
            "shopId": 1,
            "regionId": 6,
            "address": "上海市静安区胜利路521号",
            "remarks": "",
            "attendTypeName": "公开课",
            "attendTimeBucket": "2019-04-25 17:13~17:53",
            "mianCoachName": "白求恩",
            "assistCoachName": "小高",
            "attendClassNumber": 3,
            "clubName": "幸福月子门店",
            "projectName": "12节孕期瑜伽小班课",
            "cardNumber": "20190414000000",
            "studentAttendClassStateName": "已预约",
            "studentAttendClassId": 12,
            "region": {
                "id": 6,
                "parentId": 5,
                "regionTitle": "黄浦区",
                "parent": {
                    "id": 5,
                    "parentId": 4,
                    "regionTitle": "上海市",
                    "parent": {
                        "id": 4,
                        "parentId": 0,
                        "regionTitle": "上海"
                    }
                }
            },
            "placeName": "到店",
            "showSign": true
        }
      }

### 取消预约[GET]/studentAttendClass/UpDateStudentAttendClassState
+ Parameters
  + userId - 用户id（必填）
  + studentAttendClassId - 学生预约课id（必填）
  + attendClassId - 预约课程id（必填）
  + attendClassId=14&userId=4&studentAttendClassId=11（大于12小时开课示例）
  + attendClassId=17&userId=1&studentAttendClassId=15（小于12小时开课示例）
+ Response 201 (application/json)（取消预约课程成功）
   
      {
         "data": 1
      } 
+ Response 201 (application/json)（取消预约课程失败）

      {
        "errors": [
            {
                "status": "400",
                "title": "Bad Request",
                "detail": "该私教课开课前12小时内不能取消预约！"
            }
        ]
      }

### 签到[GET]/studentAttendClass/studentAttendClassSiginIn
+ Parameters
  + userId - 用户id（必填）
  + studentAttendClassId - 学生预约课id（必填）
  + userId=2&studentAttendClassId=5（示例）
+ Description
    + [MUST] authenticated
    + true - 已签到
+ Response 201 (application/json)
    
      {
         "data": true
      }
### 预约详情评价[POST]/comments
+ Parameters
  + userId - 用户id（必填）
  + studentAttendClassId - 学生预约课id（必填）
  + attendClassId - 预约课程id（必填）
  + content - 评价内容
  + coachScore - 教练评价
  + attendClassScore - 课程评价
  + attendClassScore - 服务评价
  + attachmentIds - 上传图片返回的id（非必填）
+ Description
    + [MUST] authenticated
+ Request（application/json）

      {
    	"data":{
    		"studentAttendClassId":"9",
    		"userId":"5",
    		"attendClassId":"4",
    		"content":"我的评价是教练不错，动作到位，很有作用。",
    		"coachScore":"5",
    		"attendClassScore":"5",
    		"serviceScore":"5",
    		"attachmentIds":[3]
    	}
      }

+ Response 201 (application/json)
    
      {
         "data": 1
      }    

## 请假申请
+ Data
  + CardLeave - 请假表 
    + cardId (Long) - 开卡id
    + state (int) - 状态，0：待批准，1：已批准，2：未允许
    + leaveDays (int) - 请假天数 
    + beginDate (Date) - 请假开始日期
    + endDate (Date) - 请假结束日期
    + leaveReason (String) - 请假理由
    + enabled (int) - 0禁用 1启用
    + creator (Long) - 创建人
    + modifier (Long) - 修改人
    + created (date) - 创建时间
    + modified (date) - 修改时间 

### 请假申请列表[GET]/v1/teacher/cards
+ Parameters
  + userId - 用户id（例如用户id为1）
  + state - 卡状态（解释：1：正常，2：请假申请列表中只有1，2情况才可以展示）
  + filter[userId]=1&filter[state]=1&filter[state]=2&sort=-created (请假申请列表)
  + page[number]=1&page[size]=10
  + sort -modified(从新到旧) | modified(从旧到新) 
  
+ Description
    + leaveTimeBucket - 请假时间
    + leaveStateName - 请假状态名称
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
                    "direction": "DESC",
                    "property": "created",
                    "ignoreCase": false,
                    "nullHandling": "NATIVE",
                    "descending": true,
                    "ascending": false
                }
            ]
        },
        "links": {
            "self": "/v1/teacher/cards?filter[userId]=1&filter[state]=1&filter[state]=2&sort=-created&page[number]=1&page[size]=10",
            "first": "/v1/teacher/cards?filter[userId]=1&filter[state]=1&filter[state]=2&sort=-created&page[number]=1&page[size]=10",
            "last": "/v1/teacher/cards?filter[userId]=1&filter[state]=1&filter[state]=2&sort=-created&page[number]=1&page[size]=10"
        },
        "data": [
            {
                "id": 4,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-01-15 13:48:48",
                "modified": "2019-01-15 13:48:48",
                "userId": 1,
                "cardNumber": "20190414000000",
                "state": 1,
                "realName": "海燕",
                "birthday": "2019-04-15",
                "pregnancyStage": 1,
                "address": "上海市黄浦区幸福小区一单元201室",
                "packageType": 0,
                "projectId": 9,
                "money": 12000,
                "classTime": 18,
                "giftClassTime": 0,
                "remainingClassTime": 10,
                "salesperson": 3,
                "effectiveDate": "2020-01-01",
                "customerSourceId": 1,
                "payMethod": 1,
                "inside": 1,
                "dtd": 1,
                "dtdFee": 200,
                "remarks": "你是听你说打发布到封神榜备注信息",
                "leaveRemainingNum": 2,
                "leaveRemainingDays": 20,
                "projectName": "12节孕期瑜伽小班课",
                "salespersonName": "张三"
            },
            {
                "id": 24,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "userId": 1,
                "cardNumber": "20190418000000",
                "state": 2,
                "realName": "海燕",
                "birthday": "1970-04-18",
                "pregnancyStage": 0,
                "pregnancyDate": 1557417600000,
                "address": "上海壹号公馆455号",
                "packageType": 0,
                "projectId": 3,
                "money": 12345,
                "classTime": 15,
                "giftClassTime": 0,
                "remainingClassTime": 10,
                "salesperson": 2,
                "effectiveDate": "2020-05-01",
                "customerSourceId": 2,
                "payMethod": 3,
                "inside": 1,
                "dtd": 1,
                "dtdFee": 0,
                "remarks": "高耗能高好难过",
                "leaveRemainingNum": 2,
                "leaveRemainingDays": 30,
                "projectName": "孕期瑜伽小班课",
                "salespersonName": "贝多芬"
            },
            {
                "id": 32,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "userId": 1,
                "cardNumber": "20190422000000",
                "state": 2,
                "realName": "小文",
                "birthday": "2019-04-22",
                "pregnancyStage": 0,
                "pregnancyDate": 1555862400000,
                "address": "上海市黄浦区胜利路321号",
                "packageType": 0,
                "projectId": 4,
                "money": 8000,
                "classTime": 40,
                "giftClassTime": 0,
                "remainingClassTime": 20,
                "salesperson": 1,
                "effectiveDate": "2021-04-22",
                "customerSourceId": 3,
                "payMethod": 3,
                "inside": 1,
                "dtd": 1,
                "dtdFee": 0,
                "leaveRemainingNum": 5,
                "leaveRemainingDays": 30,
                "projectName": "孕产套课",
                "salespersonName": "熊爱华"
            }
        ]
      }
   

### 查看请假记录列表[GET]/cardLeaves
+ Parameters
  + cardId - 卡id（例如卡id为4）
  + filter[cardId]=4&sort=-modified
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
                    "direction": "DESC",
                    "property": "modified",
                    "ignoreCase": false,
                    "nullHandling": "NATIVE",
                    "descending": true,
                    "ascending": false
                }
            ]
        },
        "links": {
            "self": "/cardLeaves?filter[cardId]=4&sort=-modified&page[number]=1&page[size]=10",
            "first": "/cardLeaves?filter[cardId]=4&sort=-modified&page[number]=1&page[size]=10",
            "last": "/cardLeaves?filter[cardId]=4&sort=-modified&page[number]=1&page[size]=10"
        },
        "data": [
            {
                "id": 3,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-04-23 18:36:21",
                "modified": "2019-04-23 18:36:12",
                "cardId": 4,
                "state": 2,
                "leaveDays": 7,
                "beginDate": "2019-02-24",
                "endDate": "2019-03-02",
                "leaveTimeBucket": "2019-02-24~2019-03-02",
                "leaveStateName": "未允许"
            },
            {
                "id": 2,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-04-23 18:36:19",
                "modified": "2019-04-23 18:36:09",
                "cardId": 4,
                "state": 1,
                "leaveDays": 7,
                "beginDate": "2019-04-14",
                "endDate": "2019-04-20",
                "leaveTimeBucket": "2019-04-14~2019-04-20",
                "leaveStateName": "已批准"
            },
            {
                "id": 1,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-04-23 18:36:17",
                "modified": "2019-04-23 18:36:07",
                "cardId": 4,
                "state": 0,
                "leaveDays": 7,
                "beginDate": "2019-05-01",
                "endDate": "2019-05-04",
                "leaveTimeBucket": "2019-05-01~2019-05-04",
                "leaveStateName": "待批准"
            }
        ]
      }
### 我要请假[POST]/cardLeaves
+ Parameters
  + cardId - 卡id
  + beginDate - 请假开始日期
  + endDate - 请假结束日期
  + leaveReason - 请假理由
+ Description
    + [MUST] authenticated
+ Request（application/json）

       {
    	 "data":{
    		 "cardId":4,
    		 "beginDate":"2019-02-24",
    		 "endDate":"2019-03-03",
    		 "leaveReason":"由于近期出差，不能上课，希望予以批注，谢谢~"
    	 }
      } 
      
+ Response 200 (application/json) 
      
       {
        "data": {
            "id": 20,
            "type": "cardLeaves"
         }
       }
    
## 我的该变
+ Data
  + Attachment - 图片表 
    + id (Long) - id
    + attUrl (String) - 图片访问地址
    + attTitle (String) - 图片名称
    + extension (String) - 扩展名
    + filesize (int) - 文件大小
    + description (String) - 图片描述
    + enabled (int) - 0禁用 1启用
    + creator (Long) - 创建人
    + modifier (Long) - 修改人
    + created (date) - 创建时间
    + modified (date) - 修改时间
### 我的改变列表[GET]/evaluations/myChange?userId=1
+ Parameters
  + userId - 用户id（例如用户id为1）
+ Description
    + mianCoachName - 主教练
    + assistCoachName - 助教
    + attendDate  - 课程上课时间
    + created - 作业创建时间
+ Response 200 (application/json)

      {
        "data": [
            {
                "id": 15,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-04-19 11:24:20",
                "modified": "2019-04-19 11:24:05",
                "attUrl": "http://static.mifanxing.com/article/image/215/69/4577111.jpg",
                "attTitle": "我的改变",
                "extension": "jpg",
                "filesize": 0,
                "description": "我的改变用户展示"
            },
            {
                "id": 14,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-04-19 11:24:18",
                "modified": "2019-04-19 11:24:02",
                "attUrl": "http://static.mifanxing.com/article/image/215/69/4577111.jpg",
                "attTitle": "我的改变",
                "extension": "jpg",
                "filesize": 0,
                "description": "我的改变用户展示"
            },
            {
                "id": 12,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-04-19 11:24:10",
                "modified": "2019-04-19 11:23:53",
                "attUrl": "http://static.mifanxing.com/article/image/215/69/4577111.jpg",
                "attTitle": "我的改变",
                "extension": "jpg",
                "filesize": 0,
                "description": "我的改变用户展示"
            },
            {
                "id": 11,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-04-19 11:24:08",
                "modified": "2019-04-19 11:23:50",
                "attUrl": "http://static.mifanxing.com/article/image/215/69/4577111.jpg",
                "attTitle": "我的改变",
                "extension": "jpg",
                "filesize": 0,
                "description": "我的改变用户展示"
            }
        ]
      }

## 评估方案
+ Data
  + Attachment - 图片表 
    + id (Long) - 主键，同预约/上课主键相同
    + userId (Long) - 学生/用户标识
    + realName (String) - 姓名
    + age (int) - 年龄
    + gestationNum (int) - 妊娠次数
    + childbirth (Date) - 分娩日期
    + babyBirthWeight (String) - 宝宝出生体重
    + gestationEx (String) - 妊娠特殊情况
    + sleepTime (String) - 睡眠时长
    + abdomenMuscleSeparateLen (String) - 腹直肌总分离长度
    + abdomenMuscleDepth (String) - 腹直肌深度
    + bust (String) - 胸围
    + waistline (String) - 腰围
    + abdomenling (String) - 腹围
    + hipline (String) - 臀围
    + height (String) - 身高
    + weight (String) - 体重
    + bmi (String) - BMI指数
    + others (String) - 其他
### 评估方案列表[GET]/evaluations
+ Parameters
  + userId - 用户id（例用户为1）
  + filter[userId]=1&sort=-modified

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
                    "direction": "DESC",
                    "property": "modified",
                    "ignoreCase": false,
                    "nullHandling": "NATIVE",
                    "descending": true,
                    "ascending": false
                }
            ]
        },
        "links": {
            "self": "/evaluations?filter[userId]=1&sort=-modified&page[number]=1&page[size]=10",
            "first": "/evaluations?filter[userId]=1&sort=-modified&page[number]=1&page[size]=10",
            "last": "/evaluations?filter[userId]=1&sort=-modified&page[number]=1&page[size]=10"
        },
        "data": [
            {
                "id": 6,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-04-19 11:28:50",
                "modified": "2019-04-19 11:28:49",
                "state": 0,
                "userId": 1,
                "realName": "熊爱华",
                "age": 18,
                "gestationEx": "0",
                "mianCoachName": "张三"
            },
            {
                "id": 7,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-04-19 11:28:47",
                "modified": "2019-04-19 11:28:43",
                "state": 0,
                "userId": 1,
                "realName": "熊爱华",
                "age": 19,
                "gestationEx": "0",
                "mianCoachName": "贝多芬"
            },
            {
                "id": 4,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-04-19 11:28:32",
                "modified": "2019-04-19 11:28:35",
                "state": 1,
                "userId": 1,
                "realName": "熊爱华",
                "age": 19,
                "gestationNum": 2,
                "childbirth": "2019-04-22",
                "babyBirthWeight": "7",
                "gestationEx": "0",
                "childbirthMode": 0,
                "spontaneousLaborEx": "0,1,2,3,4",
                "caesareanEx": "0,1",
                "sleepCondition": 0,
                "sleepLackReason": 2,
                "sleepTime": "3",
                "mentality": 1,
                "appetite": 0,
                "posture": "1,2",
                "neck": 1,
                "neckAbout": 0,
                "neckEx": "1,2",
                "arm": "1,2",
                "shoulder": 1,
                "shoulderAbout": 0,
                "shoulderEx": "1,2",
                "wrist": "1,2",
                "waist": 1,
                "waistAbout": 0,
                "waistEx": "1,2",
                "pelvis": 1,
                "pelvisAbout": 2,
                "pelvisEx": "1,2",
                "sciaticNerve": 1,
                "sciaticNerveEx": "1,2",
                "leg": "1,2",
                "pelvicFloor": "0,2",
                "abdomenMuscle": 0,
                "abdomenMuscleAbout": 1,
                "abdomenMuscleSeparateLen": "两厘米",
                "abdomenMuscleDepth": "两毫米",
                "abdomenWall": 1,
                "bust": "胸围八十",
                "waistline": "腰围六十",
                "abdomenling": "腹围三十",
                "hipline": "臀围三十五",
                "height": "身高一米七",
                "weight": "体重50公斤",
                "bmi": "BMI指数1",
                "others": "其它数据",
                "mianCoachName": "贝多芬",
                "assistCoachName": "小高"
            }
        ]
      }

### 评估方案详情[GET]/evaluations/clientDetails/{id}
+ Parameters
  + id - 评估id（例id为51）
+ Description
+ Response 200 (application/json)

      {
        "data": {
            "id": 51,
            "state": "提交",
            "userId": 27,
            "realName": "黄蓉",
            "age": 22,
            "gestationNum": 34,
            "childbirth": "2019-05-21",
            "babyBirthWeight": "12",
            "gestationEx": "妊娠情况很特殊",
            "childbirthMode": "顺产",
            "spontaneousLabor": [
                "有侧切",
                "撕裂Ⅰ度"
            ],
            "sleepCondition": "欠缺",
            "sleepLackReason": "易惊醒",
            "sleepTime": "21",
            "mentality": "不佳",
            "appetite": "不佳",
            "posture": [
                "下交叉综合证",
                "扁平足"
            ],
            "neck": "无不适",
            "arm": "无不适",
            "shoulder": "有不适",
            "shoulderAbout": "左",
            "shoulderEx": "僵硬",
            "wrist": "无不适",
            "waist": "有不适",
            "waistAbout": "右腰",
            "waistEx": [
                "僵硬",
                "疼痛"
            ],
            "pelvis": "有不适",
            "pelvisAbout": "右",
            "pelvisEx": [
                "僵硬",
                "疼痛"
            ],
            "sciaticNerve": "有",
            "leg": [
                "膝关节痛",
                "足根痛"
            ],
            "pelvicFloor": [
                "压力性尿失禁",
                "急迫性尿失禁"
            ],
            "abdomenMuscle": "阳性",
            "abdomenMuscleAbout": "脐上",
            "abdomenMuscleSeparateLen": "123",
            "abdomenMuscleDepth": "23",
            "abdomenWall": "紧绷疼痛",
            "bust": "12",
            "waistline": "23",
            "abdomenling": "12",
            "hipline": "33",
            "height": "44",
            "weight": "44",
            "courses": [
                {
                    "courseTitle": "产前体检",
                    "thumbnail": "http://static.mifanxing.com/article/image/215/69/4577111.jpg",
                    "description": "上菜鸟winVB让她宝宝贝贝人不同让宝宝"
                },
                {
                    "courseTitle": "产前锻炼",
                    "thumbnail": "http://static.mifanxing.com/article/image/215/69/4577111.jpg",
                    "description": "米内特我惹你本宝宝搜索发布导包导包"
                }
            ],
            "pictures": [
                "2019-05-21/a843d8161d394b3083eeaf66bca627ab.png"
            ]
        }
      }

### 客户端轮播图列表[GET] /admin/banners/clientBanner
+ Parameters
  + page[number]=1&page[size]=10
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
                    "direction": "DESC",
                    "property": "modified",
                    "ignoreCase": false,
                    "nullHandling": "NATIVE",
                    "descending": true,
                    "ascending": false
                }
            ]
        },
        "links": {
            "self": "/admin/banners?sort=-modified&page[number]=1&page[size]=10",
            "first": "/admin/banners?sort=-modified&page[number]=1&page[size]=10",
            "last": "/admin/banners?sort=-modified&page[number]=1&page[size]=10"
        },
        "data": [
            {
                "id": 3,
                "attUrl": "http://static.mifanxing.com/iyyren/image/201806/06/1638/347865732702420992.jpg",
                "bannerTitle": "最新孕产知识",
                "bannerUrl": "localhost:8398/knowledges/1",
                "targetId": 1
            },
            {
                "id": 2,
                "attUrl": "http://static.mifanxing.com/iyyren/image/201806/06/1638/347865732702420992.jpg",
                "bannerTitle": "最新活动",
                "bannerUrl": "localhost:8398/activitys/1",
                "targetId": 1
            },
            {
                "id": 1,
                "attUrl": "http://static.mifanxing.com/iyyren/image/201806/06/1638/347865732702420992.jpg",
                "bannerTitle": "最新课程",
                "bannerUrl": "localhost:8398/courses/1",
                "targetId": 1
            }
        ]
      }

### 会员中心模块动态提示[GET]/users/student/{id}   
+ Parameters
  + id - 用户ID （示例id=4）
+ Description
    + orderDisplay - 我的订单模块
    + courseDisplay - 我的课程模块
    + teacherDisplay - 我的老师模块
    + taskDisplay - 我的作业模块
    + attendClassDisplay - 我的预约模块
    + leaveApplyDisplay - 请假申请模块
    + changeDisplay - 我的改变模块
    + evaluationDisplay - 评估方案模块
    + true:为有新的动态可展示；false：为没有新的动态不展示
+ Response 200 (application/json)

      {
        "data": {
            "orderDisplay": false,
            "courseDisplay": false,
            "teacherDisplay": false,
            "taskDisplay": false,
            "attendClassDisplay": false,
            "leaveApplyDisplay": false,
            "changeDisplay": false,
            "evaluationDisplay": false
        }
      }

