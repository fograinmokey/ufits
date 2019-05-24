## 孕产平台后台管理
+ 2019年05月08日
    +  孕产平台后台管理初始化
## 套餐管理
+ Data
  + ProjectCategory - 套餐分类表
    + id (Long) - ID
    + categoryTitle (String) - 分类名称
    + enabled (int) - 0禁用 1启用
    + creator (Long) - 创建人
    + modifier (Long) - 修改人
    + created (date) - 创建时间
    + modified (date) - 修改时间
  + Project - 套餐(项目)表
    + id (Long) - ID
    + categoryId - 项目分类ID
    + projectTitle (String) - 项目名称
    + classTime (BigDecimal) -课时数/购课数
    + giftClassTime (BigDecimal) - 赠送课时/课数
    + money (BigDecimal) - 金额 
    + unitPrice (BigDecimal) - 单价
    + effectiveDays (int) - 有效时间（单位：天）
    + leaveRestrict (int) - 请假限制，0：不限制，1：不允许，2：有限制
    + leavePermitNum (int) - 请假允许次数
    + leavePermitDays (int) - 请假允许天数
    + leaveMinDays (int) - 一次请假最少天数
    + enabled (int) - 0禁用 1启用
    + creator (Long) - 创建人
    + modifier (Long) - 修改人
    + created (date) - 创建时间
    + modified (date) - 修改时间 

### 套餐分类增加[POST] /admin/projectCategories
+ Description
    + [MUST] authenticated
    + [MUST] ROLE_ADMIN | ROLE_SUPER_ADMIN
+ Request (application/json)
    
      {
         "data":{
    		"categoryTitle":"大班课"
    	  }
      }

+ Response 200 (application/json)

      {
        "data": {
            "id": 6,
            "type": "projectCategories"
        }
      }
### 套餐分类修改 [PUT] /admin/projectCategories/{id}
+ Description
    + [MUST] authenticated
    + [MUST] ROLE_ADMIN | ROLE_SUPER_ADMIN
+ Request (application/json)
    
      {
         "data":{
    		"categoryTitle":"大班课1"
    	  }
      }
+ Response 200 (application/json)

### 套餐分类列表 [GET] /admin/projectCategories
+ Parameters
  + filter[categoryTitle:like]=%25孕%25 （'%25'为'%'的转义）
  + page[number]=1&page[size]=10
  + sort -modified(从新到旧) | modified(从旧到新)

+ Response 200 (application/json)

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
            "self": "/admin/projectCategories?page[number]=1&page[size]=10",
            "first": "/admin/projectCategories?page[number]=1&page[size]=10",
            "last": "/admin/projectCategories?page[number]=1&page[size]=10"
        },
        "data": [
            {
                "id": 1,
                "enabled": 1,
                "creator": 5,
                "modifier": 0,
                "created": "2019-05-06 11:34:40",
                "modified": "2019-05-06 11:34:37",
                "categoryTitle": "免费体验课"
            },
            {
                "id": 2,
                "enabled": 1,
                "creator": 5,
                "modifier": 0,
                "created": "2019-05-06 11:35:07",
                "modified": "2019-05-07 18:07:41",
                "categoryTitle": "收费体验课"
            },
            {
                "id": 3,
                "enabled": 1,
                "creator": 5,
                "modifier": 0,
                "created": "2019-05-06 11:35:44",
                "modified": "2019-05-06 11:35:46",
                "categoryTitle": "孕期瑜伽小班课"
            },
            {
                "id": 4,
                "enabled": 1,
                "creator": 5,
                "modifier": 0,
                "created": "2019-05-06 11:36:11",
                "modified": "2019-05-06 11:36:15",
                "categoryTitle": "孕产套课"
            }
        ]
      }

### 套餐分类删除 [DELETE] /admin/projectCategories/{id}
+ Description
    + [MUST] authenticated
    + [MUST] ROLE_ADMIN | ROLE_SUPER_ADMIN
+ Response 204


### 套餐增加[POST] /admin/projects
+ Description
    + [MUST] authenticated
    + [MUST] ROLE_ADMIN | ROLE_SUPER_ADMIN
+ Request (application/json)
    
      {
    	 "data":{
    		"categoryId":2,
    		"projectTitle":"000000节孕产套课",
    		"classTime":"74",
    		"giftClassTime":"2",
    		"money":"6666",
    		"unitPrice":"34",
    		"effectiveDays":"45",
    		"leaveRestrict":"2",
    		"leavePermitNum":"4",
    		"leavePermitDays":"365",
    		"leaveMinDays":"7"
    	 }
      }

+ Response 200 (application/json)

      {
        "data": {
            "id": 22,
            "type": "projects"
        }
      }


### 套餐修改 [PUT] /admin/projects/{id}
+ Description
    + [MUST] authenticated
    + [MUST] ROLE_ADMIN | ROLE_SUPER_ADMIN
+ Request (application/json)
    
      {
    	 "data":{
    		"categoryId":2,
    		"projectTitle":"000000节孕产套课1",
    		"classTime":"74",
    		"giftClassTime":"2",
    		"money":"6666",
    		"unitPrice":"34",
    		"effectiveDays":"45",
    		"leaveRestrict":"2",
    		"leavePermitNum":"4",
    		"leavePermitDays":"365",
    		"leaveMinDays":"7"
    	 }
      }
+ Response 200 (application/json)

### 套餐详情 [GET] /admin/projects/{id}

+ Response 200 (application/json)

      {
        "data": {
            "id": 9,
            "enabled": 1,
            "creator": 0,
            "modifier": 0,
            "created": "2019-04-15 14:50:32",
            "modified": "2019-04-15 14:50:35",
            "categoryId": 5,
            "projectTitle": "12节孕期瑜伽小班课",
            "classTime": 18,
            "giftClassTime": 0,
            "money": 12000,
            "effectiveDays": 90,
            "leavePermitNum": 3,
            "leavePermitDays": 40,
            "leaveMinDays": 0
        }
      }

### 套餐删除 [DELETE] /admin/projects/{id}
+ Description
    + [MUST] authenticated
    + [MUST] ROLE_ADMIN | ROLE_SUPER_ADMIN
+ Response 204

### 套餐列表 [GET] /admin/projects
+ Parameters
  + filter[categoryId]=2（套餐分类查询）
  + filter[projectTitle:like]=%25孕%25 （'%25'为'%'的转义）
  + page[number]=1&page[size]=10
  + sort -modified(从新到旧) | modified(从旧到新)

+ Response 200 (application/json)

      {
        "meta": {
            "totalPages": 2,
            "totalElements": 16,
            "size": 10,
            "number": 1,
            "numberOfElements": 10,
            "first": true,
            "last": false,
            "sort": null
        },
        "links": {
            "self": "/admin/projects?page[number]=1&page[size]=10",
            "first": "/admin/projects?page[number]=1&page[size]=10",
            "next": "/admin/projects?page[number]=2&page[size]=10",
            "last": "/admin/projects?page[number]=2&page[size]=10"
        },
        "data": [
            {
                "id": 1,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-04-15 14:50:11",
                "modified": "2019-04-15 14:50:08",
                "categoryId": 1,
                "projectTitle": "免费体验课",
                "classTime": 0,
                "giftClassTime": 0,
                "money": 0,
                "effectiveDays": 90,
                "leavePermitNum": 0,
                "leavePermitDays": 0,
                "leaveMinDays": 0,
                "categoryTitle": "免费体验课"
            },
            {
                "id": 3,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-04-15 14:50:23",
                "modified": "2019-04-15 14:50:19",
                "categoryId": 3,
                "projectTitle": "孕期瑜伽小班课",
                "classTime": 0,
                "giftClassTime": 0,
                "money": 0,
                "effectiveDays": 90,
                "leavePermitNum": 0,
                "leavePermitDays": 0,
                "leaveMinDays": 0,
                "categoryTitle": "孕期瑜伽小班课"
            },
            {
                "id": 4,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-04-15 14:50:28",
                "modified": "2019-04-15 14:50:26",
                "categoryId": 4,
                "projectTitle": "孕产套课",
                "classTime": 0,
                "giftClassTime": 0,
                "money": 0,
                "effectiveDays": 90,
                "leavePermitNum": 0,
                "leavePermitDays": 0,
                "leaveMinDays": 0,
                "categoryTitle": "孕产套课"
            },
            {
                "id": 9,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-04-15 14:50:32",
                "modified": "2019-04-15 14:50:35",
                "categoryId": 5,
                "projectTitle": "12节孕期瑜伽小班课",
                "classTime": 18,
                "giftClassTime": 0,
                "money": 12000,
                "effectiveDays": 90,
                "leavePermitNum": 3,
                "leavePermitDays": 40,
                "leaveMinDays": 0,
                "categoryTitle": "测试"
            },
            {
                "id": 15,
                "enabled": 1,
                "creator": 5,
                "modifier": 0,
                "created": "2019-05-06 11:41:33",
                "modified": "2019-05-06 11:41:36",
                "categoryId": 3,
                "projectTitle": "孕期瑜伽小班课子项1",
                "classTime": 10,
                "giftClassTime": 2,
                "money": 1500,
                "unitPrice": 200,
                "effectiveDays": 30,
                "leaveRestrict": 2,
                "leavePermitNum": 5,
                "leavePermitDays": 2,
                "leaveMinDays": 1,
                "categoryTitle": "孕期瑜伽小班课"
            },
            {
                "id": 16,
                "enabled": 1,
                "creator": 5,
                "modifier": 0,
                "created": "2019-05-06 11:44:03",
                "modified": "2019-05-06 11:44:05",
                "categoryId": 4,
                "projectTitle": "孕产套课子项1",
                "classTime": 40,
                "giftClassTime": 5,
                "money": 6000,
                "unitPrice": 300,
                "effectiveDays": 60,
                "leaveRestrict": 0,
                "leavePermitNum": 10,
                "leavePermitDays": 5,
                "leaveMinDays": 1,
                "categoryTitle": "孕产套课"
            }
        ]
      }

## 课程管理
+ 课程分类
+ Data
  + AttendClassCategory - 课程分类表
    + id (Long) - ID
    + categoryTitle (String) - 分类名称
    + description (String) - 分类描述
    + nature (int) - 课程性质，0：公开，1：私教
    + enabled (int) - 0禁用 1启用
    + creator (Long) - 创建人
    + modifier (Long) - 修改人
    + created (date) - 创建时间
    + modified (date) - 修改时间

### 课程分类增加[POST] /admin/attendClassCategories
+ Description
    + [MUST] authenticated
    + [MUST] ROLE_ADMIN | ROLE_SUPER_ADMIN
+ Request (application/json)
    
      {
         "data":{
		     "categoryTitle":"查房000",
		     "description":"查房描述000！",
		     "nature":1
	    }
      }

+ Response 200 (application/json)

      {
        "data": {
            "id": 6,
            "type": "attendClassCategories"
        }
      }
### 课程分类修改 [PUT] /attendClassCategories/{id}
+ Description
    + [MUST] authenticated
    + [MUST] ROLE_ADMIN | ROLE_SUPER_ADMIN

+ Request (application/json)
    
      {
    	"data":{
    		"categoryTitle":"查房0001",
    		"description":"查房描述0001",
    		"nature":1
    	 }
      }
+ Response 200 (application/json)

### 课程分类详情 [GET] /attendClassCategories/{id}

+ Response 200 (application/json)

      {
        "data": {
            "id": 6,
            "enabled": 1,
            "creator": 0,
            "modifier": 0,
            "created": "2019-05-08 10:19:05",
            "modified": "2019-05-08 10:20:38",
            "categoryTitle": "查房0001",
            "description": "查房描述0001",
            "nature": 1
        }
      }

### 课程分类列表 [GET] /admin/attendClassCategories
+ Parameters
  + filter[categoryTitle:like]=%25查%25 （'%25'为'%'的转义）
  + page[number]=1&page[size]=10
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
            "self": "/admin/attendClassCategories?page[number]=1&page[size]=10",
            "first": "/admin/attendClassCategories?page[number]=1&page[size]=10",
            "last": "/admin/attendClassCategories?page[number]=1&page[size]=10"
        },
        "data": [
            {
                "id": 1,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-05-05 14:35:37",
                "modified": "2019-05-05 14:35:31",
                "categoryTitle": "公开课",
                "nature": 0
            },
            {
                "id": 2,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-05-05 14:35:40",
                "modified": "2019-05-05 14:35:34",
                "categoryTitle": "私教课",
                "nature": 1
            },
            {
                "id": 3,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-05-05 14:29:28",
                "modified": "2019-05-05 14:29:28",
                "categoryTitle": "助教",
                "description": "描述内容！！！",
                "nature": 0
            },
            {
                "id": 4,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-05-05 14:30:07",
                "modified": "2019-05-05 14:30:07",
                "categoryTitle": "小班课",
                "description": "描述信息！！",
                "nature": 1
            },
            {
                "id": 6,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-05-08 10:19:05",
                "modified": "2019-05-08 10:20:38",
                "categoryTitle": "查房0001",
                "description": "查房描述0001",
                "nature": 1
            }
        ]
      }

### 课程分类删除 [DELETE] /admin/attendClassCategories/{id}
+ Description
    + [MUST] authenticated
    + [MUST] ROLE_ADMIN | ROLE_SUPER_ADMIN
+ Response 204

+ 课程服务
+ Data
  + CourseLevel - 课程分类（级别）表 
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
    + recommend (int) - 是否推荐（默认0：不推荐，1：推荐）
    + enabled (int) - 0禁用 1启用
    + creator (Long) - 创建人
    + modifier (Long) - 修改人
    + created (date) - 创建时间
    + modified (date) - 修改时间
    + pictures - 图片

### 课程服务增加[POST] /admin/courseLevels
+ Description
    + [MUST] authenticated
    + [MUST] ROLE_ADMIN | ROLE_SUPER_ADMIN
+ Request (application/json)
    
      {
    	 "data":{
    		 "levelTitle":"中高级00",
    		 "description":"级别描述信息00",
    	 	 "timeCoefficient":"1.70"
    	 }
      }

+ Response 200 (application/json)

      {
        "data": {
            "id": 5,
            "type": "courseLevels"
        }
      }
### 课程服务修改 [PUT] /admin/courseLevels/{id}
+ Description
    + [MUST] authenticated
    + [MUST] ROLE_ADMIN | ROLE_SUPER_ADMIN
+ Request (application/json)
    
      {
    	 "data":{
    		 "levelTitle":"中高级123",
    		 "description":"级别描述信息123",
    		 "timeCoefficient":"1.70"
    	 }
      }
+ Response 200 (application/json)

### 课程服务列表 [GET] /admin/courseLevels
+ Parameters
  + filter[levelTitle:like]=%25高孕%25 （'%25'为'%'的转义）
  + page[number]=1&page[size]=10
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
            "self": "/admin/courseLevels?page[number]=1&page[size]=10",
            "first": "/admin/courseLevels?page[number]=1&page[size]=10",
            "last": "/admin/courseLevels?page[number]=1&page[size]=10"
        },
        "data": [
            {
                "id": 1,
                "created": "2019-04-10 15:19:18",
                "modified": "2019-04-10 15:19:18",
                "levelTitle": "初级"
            },
            {
                "id": 2,
                "created": "2019-04-10 18:34:48",
                "modified": "2019-04-10 18:34:43",
                "levelTitle": "中级"
            },
            {
                "id": 3,
                "created": "2019-04-10 18:34:51",
                "modified": "2019-04-10 18:34:46",
                "levelTitle": "高级"
            },
            {
                "id": 4,
                "created": "2019-05-05 16:53:36",
                "modified": "2019-05-05 16:55:34",
                "levelTitle": "中高级1"
            },
            {
                "id": 5,
                "created": "2019-05-08 10:33:44",
                "modified": "2019-05-08 10:33:44",
                "levelTitle": "中高级00"
            },
            {
                "id": 6,
                "created": "2019-05-08 10:34:57",
                "modified": "2019-05-08 10:35:20",
                "levelTitle": "中高级123"
            }
        ]
      }

### 课程服务删除 [DELETE] /admin/courseLevels/{id}
+ Description
    + [MUST] authenticated
    + [MUST] ROLE_ADMIN | ROLE_SUPER_ADMIN
+ Response 204

### 课程增加[POST] /admin/courses
+ Parameters
  + attachmentIds - 非必填字段（添加课程图片）
+ Description
    + [MUST] authenticated
    + [MUST] ROLE_ADMIN | ROLE_SUPER_ADMIN
+ Request (application/json)
    
      {
    	"data":{
    		"levelId":4,
    		"courseTitle":"孕期瑜伽12期",
    		"thumbnail":"http://static.mifanxing.com/article/image/215/69/0000001.jpg",
    		"description":"此课程适应孕期产妇12",
    		"content":"课程内容11",
    		"recommend":1,
    		"attachmentIds":[1,2,3,4,5,6]
    	 }
      }

+ Response 200 (application/json)

      {
        "data": {
            "id": 13,
            "type": "courses"
        }
      }


### 课程修改 [PUT] /admin/courses/{id}
+ Description
    + [MUST] authenticated
    + [MUST] ROLE_ADMIN | ROLE_SUPER_ADMIN
+ Request (application/json)
        
      {
    	"data":{
    		"levelId":4,
    		"courseTitle":"孕期瑜伽15期",
    		"thumbnail":"http://static.mifanxing.com/article/image/215/69/0000001.jpg",
    		"description":"此课程适应孕期产妇15",
    		"content":"课程内容11",
    		"recommend":1,
    		"attachmentIds":[1,2,3,4,5]
    	}
      }
      
+ Response 200 (application/json)

### 课程详情 [GET] /admin/courses/{id}

+ Response 200 (application/json)
    
      {
        "data": {
            "id": 14,
            "enabled": 1,
            "creator": 0,
            "modifier": 0,
            "created": "2019-05-08 10:53:35",
            "modified": "2019-05-08 10:54:40",
            "levelId": 4,
            "courseTitle": "孕期瑜伽15期",
            "thumbnail": "http://static.mifanxing.com/article/image/215/69/0000001.jpg",
            "description": "此课程适应孕期产妇15",
            "content": "课程内容11",
            "recommend": 1,
            "pictures": [
                "http://static.mifanxing.com/iyyren/image/201806/06/1638/347865732702420991.jpg",
                "http://static.mifanxing.com/iyyren/image/201806/06/1638/347865732702420992.jpg"
            ]
        }
      }

### 课程删除 [DELETE] /admin/courses/{id}
+ Description
    + [MUST] authenticated
    + [MUST] ROLE_ADMIN | ROLE_SUPER_ADMIN
+ Response 204

### 课程列表 [GET] /admin/courses
+ Parameters
  + filter[levelId]=2（课程分类查询）
  + filter[courseTitle:like]=%25孕%25 （'%25'为'%'的转义）
  + page[number]=1&page[size]=10
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
            "self": "/admin/courses?page[number]=1&page[size]=10",
            "first": "/admin/courses?page[number]=1&page[size]=10",
            "last": "/admin/courses?page[number]=1&page[size]=10"
        },
        "data": [
            {
                "id": 1,
                "created": "2019-04-10 15:20:05",
                "modified": "2019-04-10 15:20:05",
                "levelId": 3,
                "courseTitle": "产后恢复",
                "levelTitle": "高级"
            },
            {
                "id": 4,
                "created": "2019-04-12 11:22:12",
                "modified": "2019-04-11 11:22:02",
                "levelId": 2,
                "courseTitle": "孕期锻炼",
                "levelTitle": "中级"
            },
            {
                "id": 6,
                "created": "2019-04-12 11:22:16",
                "modified": "2019-04-12 11:22:05",
                "levelId": 1,
                "courseTitle": "产前体检",
                "levelTitle": "初级"
            },
            {
                "id": 7,
                "created": "2019-04-12 11:22:19",
                "modified": "2019-04-12 11:22:09",
                "levelId": 1,
                "courseTitle": "产前锻炼",
                "levelTitle": "初级"
            },
            {
                "id": 13,
                "created": "2019-05-08 10:41:09",
                "modified": "2019-05-08 10:41:09",
                "levelId": 4,
                "courseTitle": "孕期瑜伽12期",
                "levelTitle": "中高级1"
            }
        ]
      }

## 动作管理
+ Data
  + ActionCategory - 动作分类表 
    + categoryTitle (String) - 名称
    + description (String) - 描述
    + enabled (int) - 0禁用 1启用
    + creator (Long) - 创建人
    + modifier (Long) - 修改人
    + created (date) - 创建时间
    + modified (date) - 修改时间
  + Action - 动作表
    + categoryId (Long) - 分类ID
    + actionTitle (String) - 名称
    + thumbnail (String) - 缩略图
    + description (String) - 描述
    + content (String) - 内容
    + enabled (int) - 0禁用 1启用
    + creator (Long) - 创建人
    + modifier (Long) - 修改人
    + created (date) - 创建时间
    + modified (date) - 修改时间
    + pictures - 图片
### 动作分类增加[POST] /admin/actionCategories
+ Description
    + [MUST] authenticated
    + [MUST] ROLE_ADMIN | ROLE_SUPER_ADMIN
+ Request (application/json)
    
      {
    	 "data":{
    	 	 "categoryTitle":"有氧室09",
    		 "description":"室内提供充足的氧气"
    	 }
      }

+ Response 200 (application/json)

      {
        "data": {
            "id": 3,
            "type": "actionCategories"
        }
      }
### 动作分类修改 [PUT] /admin/actionCategories/{id}
+ Description
    + [MUST] authenticated
    + [MUST] ROLE_ADMIN | ROLE_SUPER_ADMIN
+ Request (application/json)
    
      {
    	  "data":{
    		 "categoryTitle":"有氧室08",
    		 "description":"室内提供充足的氧气"
    	  }
      }
+ Response 200 (application/json)

### 动作分类列表 [GET] /admin/actionCategories
+ Parameters
  + filter[categoryTitle:like]=%25氧%25  （'%25'为'%'的转义）
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
            "sort": null
        },
        "links": {
            "self": "admin/actionCategories?page[number]=1&page[size]=10",
            "first": "admin/actionCategories?page[number]=1&page[size]=10",
            "last": "admin/actionCategories?page[number]=1&page[size]=10"
        },
        "data": [
            {
                "id": 1,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "categoryTitle": "室内"
            },
            {
                "id": 2,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-05-06 18:05:35",
                "modified": "2019-05-06 18:06:18",
                "categoryTitle": "有氧室",
                "description": "室内提供充足的氧气"
            },
            {
                "id": 3,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-05-08 11:13:27",
                "modified": "2019-05-08 11:14:14",
                "categoryTitle": "有氧室08",
                "description": "室内提供充足的氧气"
            }
        ]
      }

### 动作分类删除 [DELETE] /admin/actionCategories/{id}
+ Description
    + [MUST] authenticated
    + [MUST] ROLE_ADMIN | ROLE_SUPER_ADMIN
+ Response 204


### 动作增加[POST] /admin/actions
+ Parameters
  + attachmentIds - 非必填字段（添加图片）
+ Description
    + [MUST] authenticated
    + [MUST] ROLE_ADMIN | ROLE_SUPER_ADMIN
    + attachmentIds - 为内容图片id（非必填）
+ Request (application/json)
    
      {
    	"data":{
    		"categoryId":2,
    		"actionTitle":"腿部按摩123",
    		"thumbnail":"http://static.mifanxing.com/iyyren/image/201806/06/1638/1111111111.jpg",
    		"description":"腿部锻炼将会缓解肿胀123",
    		"content":"内容部分",
    		"attachmentIds":[1,2,3]
    	}
      }

+ Response 200 (application/json)

      {
        "data": {
            "id": 5,
            "type": "actions"
        }
      }


### 动作修改 [PUT] /admin/actions/{id}
+ Description
    + [MUST] authenticated
    + [MUST] ROLE_ADMIN | ROLE_SUPER_ADMIN
    + attachmentIds - 为内容图片id（非必填）
+ Request (application/json)
        
      {
    	 "data":{
    		"categoryId":2,
    		"actionTitle":"腿部按摩1111",
    		"thumbnail":"http://static.mifanxing.com/iyyren/image/201806/06/1638/1111111111.jpg",
    		"description":"腿部锻炼将会缓解肿胀123",
    		"content":"内容部分",
    		"attachmentIds":[1,2,3]
    	 }
      }
      
+ Response 200 (application/json)

### 动作详情 [GET] /admin/actions/{id}

+ Response 200 (application/json)
    
      {
        "data": {
            "id": 5,
            "enabled": 1,
            "creator": 0,
            "modifier": 0,
            "created": "2019-05-08 11:22:20",
            "modified": "2019-05-08 11:32:29",
            "categoryId": 2,
            "actionTitle": "腿部按摩1111",
            "thumbnail": "http://static.mifanxing.com/iyyren/image/201806/06/1638/1111111111.jpg",
            "description": "腿部锻炼将会缓解肿胀123",
            "content": "内容部分",
            "pictures": [
                "http://static.mifanxing.com/iyyren/image/201806/06/1638/347865732702420991.jpg",
                "http://static.mifanxing.com/iyyren/image/201806/06/1638/347865732702420992.jpg"
            ]
        }
      }

### 动作删除 [DELETE] /admin/actions/{id}
+ Description
    + [MUST] authenticated
    + [MUST] ROLE_ADMIN | ROLE_SUPER_ADMIN
+ Response 204

### 动作列表 [GET] /admin/actions
+ Parameters
  + filter[categoryId]=2（动作分类查询）
  + filter[actionTitle:like]=%25部%25 （'%25'为'%'的转义）
  + page[number]=1&page[size]=10
  + sort -modified(从新到旧) | modified(从旧到新)

+ Response 200 (application/json)

      {
        "meta": {
            "totalPages": 1,
            "totalElements": 5,
            "size": 10,
            "number": 1,
            "numberOfElements": 5,
            "first": true,
            "last": true,
            "sort": null
        },
        "links": {
            "self": "/admin/actions?page[number]=1&page[size]=10",
            "first": "/admin/actions?page[number]=1&page[size]=10",
            "last": "/admin/actions?page[number]=1&page[size]=10"
        },
        "data": [
            {
                "id": 1,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-04-16 16:12:00",
                "modified": "2019-04-16 16:11:53",
                "categoryId": 1,
                "actionTitle": "俯卧撑",
                "thumbnail": "http://static.mifanxing.com/iyyren/image/201806/06/1638/347865732702420992.jpg",
                "categoryTitle": "室内"
            },
            {
                "id": 2,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-04-16 16:12:03",
                "modified": "2019-04-16 16:11:57",
                "categoryId": 1,
                "actionTitle": "仰卧起坐",
                "thumbnail": "http://static.mifanxing.com/iyyren/image/201806/06/1638/347865732702420992.jpg",
                "categoryTitle": "室内"
            },
            {
                "id": 3,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-04-17 09:48:26",
                "modified": "2019-04-17 09:48:24",
                "categoryId": 1,
                "actionTitle": "瑜伽锻炼",
                "thumbnail": "http://static.mifanxing.com/iyyren/image/201806/06/1638/347865732702420992.jpg",
                "categoryTitle": "室内"
            },
            {
                "id": 4,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-05-06 18:13:18",
                "modified": "2019-05-06 18:16:59",
                "categoryId": 2,
                "actionTitle": "腿部按摩1",
                "thumbnail": "http://static.mifanxing.com/iyyren/image/201806/06/1638/1111111111.jpg",
                "description": "腿部锻炼将会缓解肿胀1",
                "content": "内容部分",
                "categoryTitle": "有氧室"
            },
            {
                "id": 5,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-05-08 11:22:20",
                "modified": "2019-05-08 11:32:29",
                "categoryId": 2,
                "actionTitle": "腿部按摩1111",
                "thumbnail": "http://static.mifanxing.com/iyyren/image/201806/06/1638/1111111111.jpg",
                "description": "腿部锻炼将会缓解肿胀123",
                "content": "内容部分",
                "categoryTitle": "有氧室"
            }
        ]
      }

## 孕产知识库管理 
+ Data
  + Knowledge - 孕产知识表 
    + knowledgeTitle (String) - 知识库标题
    + description (String) - 描述
    + content (String) - 知识库内容
    + postUserName (String) - 作者
    + postDate (Date) - 发布时间
    + recommend (int) -是否推荐，0：否，1：是
    + thumbnail (String) - 缩略图
    + enabled (int) - 0禁用 1启用
    + creator (Long) - 创建人
    + modifier (Long) - 修改人
    + created (date) - 创建时间
    + modified (date) - 修改时间
    + pictures - 图片

### 增加[POST] /admin/knowledges
+ Parameters
  + attachmentIds - 非必填字段（添加图片）
+ Description
    + [MUST] authenticated
    + [MUST] ROLE_ADMIN | ROLE_SUPER_ADMIN
    + attachmentIds - 为内容图片id（非必填）
+ Request (application/json)
    
      {
    	"data":{
    		"knowledgeTitle":"孕期了解Ⅲ",
    		"description":"这是一项在孕期的知识",
    		"content":"一、有好的营养 二、有好的睡眠",
    		"postUserName":"李四",
    		"postDate":"2019-05-06 18:47:30",
    		"recommend":1,
    		"thumbnail":"http://static.mifanxing.com/article/image/215/69/111111.jpg",
    		"attachmentIds":[1,2,3]
    	}
      }

+ Response 200 (application/json)

      {
        "data": {
            "id": 7,
            "type": "Knowledges"
        }
      }


### 修改 [PUT] /admin/knowledges/{id}
+ Description
    + [MUST] authenticated
    + [MUST] ROLE_ADMIN | ROLE_SUPER_ADMIN
    + attachmentIds - 为内容图片id（非必填）
+ Request (application/json)
        
      {
    	"data":{
    		"knowledgeTitle":"孕期了解Ⅲ",
    		"description":"这是一项在孕期的知识",
    		"content":"一、有好的营养 二、有好的睡眠asd",
    		"postUserName":"李四",
    		"postDate":"2019-05-06 18:47:30",
    		"recommend":1,
    		"thumbnail":"http://static.mifanxing.com/article/image/215/69/111111.jpg",
    		"attachmentIds":[1,2,3]
    	}
      }
      
+ Response 200 (application/json)

### 详情 [GET] /admin/knowledges/{id}

+ Response 200 (application/json)
    
      {
        "data": {
            "id": 7,
            "enabled": 1,
            "creator": 0,
            "modifier": 0,
            "created": "2019-05-08 11:43:40",
            "modified": "2019-05-08 11:45:10",
            "knowledgeTitle": "孕期了解Ⅲ",
            "description": "这是一项在孕期的知识",
            "content": "一、有好的营养 二、有好的睡眠asd",
            "postUserName": "李四",
            "postDate": "2019-05-06 18:47",
            "recommend": 1,
            "thumbnail": "http://static.mifanxing.com/article/image/215/69/111111.jpg",
            "pictures": [
                "http://static.mifanxing.com/iyyren/image/201806/06/1638/347865732702420991.jpg",
                "http://static.mifanxing.com/iyyren/image/201806/06/1638/347865732702420992.jpg",
                "http://static.mifanxing.com/iyyren/image/201806/06/1638/347865732702420993.jpg"
            ]
        }
      }

### 删除 [DELETE] /admin/knowledges/{id}
+ Description
    + [MUST] authenticated
    + [MUST] ROLE_ADMIN | ROLE_SUPER_ADMIN
+ Response 204

### 列表 [GET] /admin/knowledges
+ Parameters
  + filter[knowledgeTitle:like]=%25部%25 （'%25'为'%'的转义）
  + page[number]=1&page[size]=10
  + sort -modified(从新到旧) | modified(从旧到新)

+ Response 200 (application/json)

      {
        "meta": {
            "totalPages": 1,
            "totalElements": 7,
            "size": 10,
            "number": 1,
            "numberOfElements": 7,
            "first": true,
            "last": true,
            "sort": null
        },
        "links": {
            "self": "/admin/Knowledges?page[number]=1&page[size]=10",
            "first": "/admin/Knowledges?page[number]=1&page[size]=10",
            "last": "/admin/Knowledges?page[number]=1&page[size]=10"
        },
        "data": [
            {
                "id": 1,
                "created": "2019-05-05 18:47:30",
                "modified": "2019-04-25 10:32:01",
                "knowledgeTitle": "备孕知识"
            },
            {
                "id": 2,
                "created": "2019-05-05 18:47:33",
                "modified": "2019-04-25 10:32:07",
                "knowledgeTitle": "产前知识"
            },
            {
                "id": 3,
                "created": "2019-05-05 18:47:36",
                "modified": "2019-04-25 10:32:09",
                "knowledgeTitle": "产后护理"
            },
            {
                "id": 4,
                "created": "2019-05-05 18:47:39",
                "modified": "2019-04-25 10:32:13",
                "knowledgeTitle": "健康知识"
            },
            {
                "id": 5,
                "created": "2019-05-05 18:57:11",
                "modified": "2019-05-05 18:57:55",
                "knowledgeTitle": "孕期了解1"
            },
            {
                "id": 6,
                "created": "2019-05-06 16:30:32",
                "modified": "2019-05-06 16:33:07",
                "knowledgeTitle": "孕期了解Ⅱ"
            },
            {
                "id": 7,
                "created": "2019-05-08 11:43:40",
                "modified": "2019-05-08 11:45:10",
                "knowledgeTitle": "孕期了解Ⅲ"
            }
        ]
      }

## 活动管理
+ Data
  + Activity - 活动表 
    + activityTitle (String) - 活动标题
    + description (String) - 活动描述
    + content (String) - 活动内容
    + postDate (Date) - 发布时间
    + organizationId (int) - 合作机构id
    + stage (int) - 活动阶段：0：无限制，1：备孕，2：孕期，3：产后，4：早教
    + recommend (int) - 是否推荐，0：否，1：是缩略图
    + hasSign (int) - 是否可以报名；0：否，1：是（默认1可报名）
    + thumbnail(String) - 缩略图
    + enabled (int) - 0禁用 1启用
    + creator (Long) - 创建人
    + modifier (Long) - 修改人
    + created (date) - 创建时间
    + modified (date) - 修改时间

### 增加[POST] /admin/activitys
+ Description
    + [MUST] authenticated
    + [MUST] ROLE_ADMIN | ROLE_SUPER_ADMIN
    + attachmentIds - 为内容图片id（非必填）
+ Request (application/json)
    
      {
    	"data":{
    		"activityTitle":"月子线下活动001",
    		"description":"活动描述史蒂芬森001",
    		"content":"活动内容是的是的所多001",
    		"organizationId":2,
    		"stage":1,
    		"recommend":1,
    		"hasSign":1,
    		"attachmentIds":[1,2],
    		"thumbnail":"http://static.mifanxing.com/iyyren/image/201806/06/1638/000000.jpg"
    	}
      }

+ Response 200 (application/json)

      {
         "data": {
             "id": 15,
             "type": "activitys"
         }
      }


### 修改 [PUT] /admin/activitys/{id}
+ Description
    + [MUST] authenticated
    + [MUST] ROLE_ADMIN | ROLE_SUPER_ADMIN
    + attachmentIds - 为内容图片id（非必填）
+ Request (application/json)
        
      {
    	"data":{
    		"activityTitle":"月子线下活动002",
    		"description":"活动描述史蒂芬森001",
    		"content":"活动内容是的是的所多001",
    		"organizationId":2,
    		"stage":1,
    		"recommend":1,
    		"hasSign":1,
    		"attachmentIds":[1,2],
    		"thumbnail":"http://static.mifanxing.com/iyyren/image/201806/06/1638/000000.jpg"
    	}
      }
      
+ Response 200 (application/json)

### 详情 [GET] /admin/activitys/details/{id}

+ Response 200 (application/json)
    
      {
        "data": {
            "id": 15,
            "enabled": 1,
            "creator": 0,
            "modifier": 0,
            "created": "2019-05-08 13:38:15",
            "modified": "2019-05-08 13:41:55",
            "activityTitle": "月子线下活动1234",
            "description": "活动描述史蒂芬森1234",
            "content": "活动内容是的是的所多1234",
            "postDate": "2019-05-08 13:38",
            "organizationId": 2,
            "stage": 1,
            "recommend": 1,
            "hasSign": 1,
            "thumbnail": "http://static.mifanxing.com/iyyren/image/201806/06/1638/000000.jpg",
            "organizationTitle": "月子会所"
        }
      }

### 删除 [DELETE] /admin/activitys/{id}
+ Description
    + [MUST] authenticated
    + [MUST] ROLE_ADMIN | ROLE_SUPER_ADMIN
+ Response 204

### 列表 [GET] /admin/activitys
+ Parameters
  + filter[activityTitle:like]=%25活动%25 （'%25'为'%'的转义）
  + page[number]=1&page[size]=10
  + sort -modified(从新到旧) | modified(从旧到新)

+ Response 200 (application/json)

      {
        "meta": {
            "totalPages": 1,
            "totalElements": 5,
            "size": 10,
            "number": 1,
            "numberOfElements": 5,
            "first": true,
            "last": true,
            "sort": null
        },
        "links": {
            "self": "/admin/activitys?page[number]=1&page[size]=10",
            "first": "/admin/activitys?page[number]=1&page[size]=10",
            "last": "/admin/activitys?page[number]=1&page[size]=10"
        },
        "data": [
            {
                "id": 1,
                "created": "2019-04-11 11:41:01",
                "modified": "2019-04-11 11:41:04",
                "activityTitle": "孕妇一日游活动",
                "hasSign": 1,
                "hasSignName": "是"
            },
            {
                "id": 2,
                "created": "2019-04-11 11:41:09",
                "modified": "2019-04-11 11:41:06",
                "activityTitle": "别的地方活动",
                "hasSign": 1,
                "hasSignName": "是"
            },
            {
                "id": 3,
                "created": "2019-04-11 11:41:14",
                "modified": "2019-04-11 11:41:12",
                "activityTitle": "某某活动",
                "hasSign": 0,
                "hasSignName": "否"
            },
            {
                "id": 4,
                "created": "2019-04-11 11:41:22",
                "modified": "2019-04-11 11:41:18",
                "activityTitle": "哈哈活动",
                "hasSign": 1,
                "hasSignName": "是"
            },
            {
                "id": 5,
                "created": "2019-04-11 11:47:34",
                "modified": "2019-04-11 11:47:31",
                "activityTitle": "风儿活动",
                "hasSign": 1,
                "hasSignName": "是"
            }
        ]
      }

## 合作机构管理
+ Data
  + OrganizationCategory - 合作机构分类表 
    + categoryTitle (String) - 标题
    + description (String) - 描述
    + enabled (int) - 0禁用 1启用
    + creator (Long) - 创建人
    + modifier (Long) - 修改人
    + created (date) - 创建时间
    + modified (date) - 修改时间
  + Organization - 合作机构表 
    + categoryId (int) - 分类id
    + organizationTitle (String) - 机构名称
    + logo (String) - 机构LOGO
    + description (String) - 描述
    + regionId (int) - 区域id
    + address (String) -  详细地址
    + enabled (int) - 0禁用 1启用
    + creator (Long) - 创建人
    + modifier (Long) - 修改人
    + created (date) - 创建时间
    + modified (date) - 修改时间

### 合作机构分类增加[POST] /admin/organizationCategories
+ Description
    + [MUST] authenticated
    + [MUST] ROLE_ADMIN | ROLE_SUPER_ADMIN
+ Request (application/json)
    
      {
    	  "data":{
    	 	 "categoryTitle":"医院",
    		 "description":"内容巴巴多斯岛"
    	 }
      }

+ Response 200 (application/json)

      {
        "data": {
            "id": 3,
            "type": "OrganizationCategory"
        }
      }
### 合作机构分类修改 [PUT] /admin/organizationCategories/{id}
+ Description
    + [MUST] authenticated
    + [MUST] ROLE_ADMIN | ROLE_SUPER_ADMIN
+ Request (application/json)
    
       {
    	  "data":{
    	 	 "categoryTitle":"医院1",
    		 "description":"内容巴巴多斯岛"
    	 }
      }
+ Response 200 (application/json)

### 合作机构分类列表 [GET] /admin/organizationCategories
+ Parameters
  + filter[categoryTitle:like]=%25合作%25 （'%25'为'%'的转义）
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
            "sort": null
        },
        "links": {
            "self": "/admin/organizationCategories?page[number]=1&page[size]=10",
            "first": "/admin/organizationCategories?page[number]=1&page[size]=10",
            "last": "/admin/organizationCategories?page[number]=1&page[size]=10"
        },
        "data": [
            {
                "id": 1,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "categoryTitle": "合作机构分类1"
            },
            {
                "id": 2,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-05-06 20:09:38",
                "modified": "2019-05-06 20:09:38",
                "categoryTitle": "会所",
                "description": "内容巴巴多斯岛"
            },
            {
                "id": 3,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-05-06 20:09:45",
                "modified": "2019-05-08 14:00:59",
                "categoryTitle": "医院1",
                "description": "内容巴巴多斯岛"
            }
        ]
      }

### 合作机构分类删除 [DELETE] /admin/organizationCategories/{id}
+ Description
    + [MUST] authenticated
    + [MUST] ROLE_ADMIN | ROLE_SUPER_ADMIN
+ Response 204

### 合作机构增加[POST] /admin/Organization
+ Description
    + [MUST] authenticated
    + [MUST] ROLE_ADMIN | ROLE_SUPER_ADMIN
+ Request (application/json)
    
      {
    	 "data":{
    		 "categoryId":3,
    		 "organizationTitle":"上海妇幼保健院",
    		 "logo":"http://static.mifanxing.com/iyyren/image/201806/06/1638/1111111111.jpg",
    		 "description":"腿部锻炼将会缓解肿胀1",
    		 "regionId":3,
    		 "address":"黄浦区苏州路3号"
    	 }
      }

+ Response 200 (application/json)

      {
        "data": {
            "id": 3,
            "type": "Organization"
        }
      }


### 合作机构修改 [PUT] /admin/organizations/{id}
+ Description
    + [MUST] authenticated
    + [MUST] ROLE_ADMIN | ROLE_SUPER_ADMIN
+ Request (application/json)
    
      {
    	 "data":{
    		 "categoryId":3,
    		 "organizationTitle":"上海妇幼保健院1",
    		 "logo":"http://static.mifanxing.com/iyyren/image/201806/06/1638/1111111111.jpg",
    		 "description":"腿部锻炼将会缓解肿胀1",
    		 "regionId":3,
    		 "address":"黄浦区苏州路3号"
    	 }
      }
+ Response 200 (application/json)

### 合作机构详情 [GET] /admin/organizations/{id}

+ Response 200 (application/json)

      {
        "data": {
            "id": 3,
            "enabled": 1,
            "creator": 0,
            "modifier": 0,
            "created": "2019-05-06 20:16:10",
            "modified": "2019-05-08 14:09:28",
            "categoryId": 3,
            "organizationTitle": "上海妇幼保健院1",
            "logo": "http://static.mifanxing.com/iyyren/image/201806/06/1638/1111111111.jpg",
            "description": "腿部锻炼将会缓解肿胀1",
            "regionId": 3,
            "address": "黄浦区苏州路3号"
        }
      }

### 合作机构删除 [DELETE] /admin/organizations/{id}
+ Description
    + [MUST] authenticated
    + [MUST] ROLE_ADMIN | ROLE_SUPER_ADMIN
+ Response 204

### 合作机构列表 [GET] /admin/organizations
+ Parameters
  + filter[categoryId]=2（套餐分类查询）
  + filter[organizationTitle:like]=%25会所%25 （'%25'为'%'的转义）
  + page[number]=1&page[size]=10
  + sort -modified(从新到旧) | modified(从旧到新)

+ Response 200 (application/json)

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
            "self": "/admin/organizations?page[number]=1&page[size]=10",
            "first": "/admin/organizations?page[number]=1&page[size]=10",
            "last": "/admin/organizations?page[number]=1&page[size]=10"
        },
        "data": [
            {
                "id": 1,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "modified": "2019-05-07 15:22:01",
                "categoryId": 1,
                "organizationTitle": "北京月子会所",
                "categoryTitle": "合作机构分类1"
            },
            {
                "id": 2,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-05-06 20:15:34",
                "modified": "2019-05-08 13:41:55",
                "categoryId": 2,
                "organizationTitle": "月子会所",
                "logo": "http://static.mifanxing.com/iyyren/image/201806/06/1638/1111111111.jpg",
                "description": "腿部锻炼将会缓解肿胀1",
                "regionId": 3,
                "address": "黄浦区苏州路1号",
                "categoryTitle": "会所"
            },
            {
                "id": 3,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-05-06 20:16:10",
                "modified": "2019-05-08 14:09:28",
                "categoryId": 3,
                "organizationTitle": "上海妇幼保健院1",
                "logo": "http://static.mifanxing.com/iyyren/image/201806/06/1638/1111111111.jpg",
                "description": "腿部锻炼将会缓解肿胀1",
                "regionId": 3,
                "address": "黄浦区苏州路3号",
                "categoryTitle": "医院1"
            },
            {
                "id": 4,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-05-07 13:38:15",
                "modified": "2019-05-07 15:06:02",
                "categoryId": 1,
                "organizationTitle": "方庄妇幼保健院",
                "logo": "https://pics7.baidu.com/feed/0d338744ebf81a4c6746890429f2a85d272da6e0.jpeg?token=3f289d2b9406a768d35",
                "description": "孕妇调养",
                "regionId": 3,
                "address": "北京市丰台区南方庄99号院",
                "categoryTitle": "合作机构分类1"
            }
        ]
      }

## 轮播图管理
+ Data
  + Banner - 轮播图表 
    + attUrl (String) - 图片链接 
    + bannerTitle (String) - banner标题
    + bannerUrl (String) - banner访问路径
    + modular (int) - 模块，0：活动，1：孕产知识，2：课程
    + targetId (Long) - 目标标识
    + enabled (int) - 0禁用 1启用
    + creator (Long) - 创建人
    + modifier (Long) - 修改人
    + created (date) - 创建时间
    + modified (date) - 修改时间

### 增加[POST] /admin/banners
+ Description
    + [MUST] authenticated
    + [MUST] ROLE_ADMIN | ROLE_SUPER_ADMIN
+ Request (application/json)
    
      {
    	 "data":{
    		 "attUrl":"http://static.mifanxing.com/iyyren/image/20 1806/06/1638/00000000000.jpg",
    		 "bannerTitle":"活动开始啦",
    		 "bannerUrl":"localhost:8398/activitys/",
    		 "modular":0,
    		 "targetId":15
    	 }
      }

+ Response 200 (application/json)

      {
        "data": {
            "id": 4,
            "type": "Banner"
        }
      }


### 修改 [PUT] /admin/banners/{id}
+ Description
    + [MUST] authenticated
    + [MUST] ROLE_ADMIN | ROLE_SUPER_ADMIN
+ Request (application/json)
        
      {
    	 "data":{
    		 "attUrl":"http://static.mifanxing.com/iyyren/image/201806/06/1638/00000000000.jpg",
    		 "bannerTitle":"活动开始啦1",
    		 "bannerUrl":"localhost:8398/activitys/",
    		 "modular":0,
    		 "targetId":15
     	 }
      }
      
+ Response 200 (application/json)

### 详情 [GET] /admin/banners/{id}

+ Response 200 (application/json)
    
      {
        "data": {
            "id": 4,
            "enabled": 1,
            "creator": 0,
            "modifier": 0,
            "created": "2019-05-08 14:44:23",
            "modified": "2019-05-08 14:47:53",
            "attUrl": "http://static.mifanxing.com/iyyren/image/201806/06/1638/00000000000.jpg",
            "bannerTitle": "活动开始啦1",
            "bannerUrl": "localhost:8398/activitys/",
            "modular": 0,
            "targetId": 15
        }
      }

### 删除 [DELETE] /admin/banners/{id}
+ Description
    + [MUST] authenticated
    + [MUST] ROLE_ADMIN | ROLE_SUPER_ADMIN
+ Response 204

### 列表 [GET] /admin/banners
+ Parameters
  + filter[modular]=id（所属模块查询,id为模块值）
  + page[number]=1&page[size]=10
  + sort -modified(从新到旧) | modified(从旧到新)

+ Response 200 (application/json)

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
            "self": "/admin/banners?page[number]=1&page[size]=10",
            "first": "/admin/banners?page[number]=1&page[size]=10",
            "last": "/admin/banners?page[number]=1&page[size]=10"
        },
        "data": [
            {
                "id": 1,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-04-28 18:47:10",
                "modified": "2019-04-28 18:46:59",
                "attUrl": "http://static.mifanxing.com/iyyren/image/201806/06/1638/347865732702420992.jpg",
                "bannerTitle": "最新课程",
                "bannerUrl": "localhost:8398/courses/",
                "modular": 2,
                "targetId": 1
            },
            {
                "id": 2,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-04-28 18:47:13",
                "modified": "2019-04-28 18:47:02",
                "attUrl": "http://static.mifanxing.com/iyyren/image/201806/06/1638/347865732702420992.jpg",
                "bannerTitle": "最新活动",
                "bannerUrl": "localhost:8398/activitys/",
                "modular": 0,
                "targetId": 1
            },
            {
                "id": 3,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-04-28 18:47:16",
                "modified": "2019-04-28 18:47:07",
                "attUrl": "http://static.mifanxing.com/iyyren/image/201806/06/1638/347865732702420992.jpg",
                "bannerTitle": "最新孕产知识",
                "bannerUrl": "localhost:8398/knowledges/",
                "modular": 1,
                "targetId": 1
            },
            {
                "id": 4,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-05-08 14:44:23",
                "modified": "2019-05-08 14:47:53",
                "attUrl": "http://static.mifanxing.com/iyyren/image/201806/06/1638/00000000000.jpg",
                "bannerTitle": "活动开始啦1",
                "bannerUrl": "localhost:8398/activitys/",
                "modular": 0,
                "targetId": 15
            }
        ]
      }

## 课表管理
+ Data
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



### 增加[POST] /admin/attendClass
+ Description
    + [MUST] authenticated
    + [MUST] ROLE_ADMIN | ROLE_SUPER_ADMIN
+ Request (application/json)（私教课）
    
      {
    	 "data":{
    		 "categoryId":1,
    		 "mianCoachId":2,
    		 "place":1,
    		 "attendDate":"2019-05-20",
    		 "beginTime":"2019-05-20 14:51:11",
    		 "timeLength":15,
    		 "courseLevelId":3,
    		 "studentId":[25],
    		 "cardId":[41]
    	 }
      }

+ Request (application/json)（公开课）

      {
    	 "data":{
    		 "categoryId":1,
    		 "mianCoachId":2,
    		 "assistCoachId":"4",
    		 "place":1,
    		 "shopId":2,
    		 "attendDate":"2019-05-25",
    		 "beginTime":"2019-05-25 14:51:11",
    		 "timeLength":15,
    		 "courseLevelId":3,
    		 "studentId":[25,27],
    		 "cardId":[41,42]
    	 }
      }

+ Response 200 (application/json)

      {
        "data": 1
      }


### 修改 [PUT] /admin/attendClass/{id}
+ Description
    + [MUST] authenticated
    + [MUST] ROLE_ADMIN | ROLE_SUPER_ADMIN
+ Request (application/json)
        
      {
    	 "data":{
    		"categoryId":1,
    		"mianCoachId":2,
    		"place":1,
    		"attendDate":"2019-05-20",
    		"beginTime":"2019-05-20 14:51:11",
    		"timeLength":15,
    		"courseLevelId":3,
    		"studentId":[25],
    		"cardId":[41]
    	 }
      }
      
+ Response 200 (application/json)

### 详情 [GET] /admin/attendClass/{id}

+ Response 200 (application/json)
    
      {
        "data": {
            "categoryId": 2,
            "mianCoachId": 2,
            "courseLevelId": 3,
            "nature": 1,
            "category": "私教课",
            "mianCoach": "白求恩",
            "place": "上门",
            "attendDate": "2019-05-09",
            "beginTime": "21:51",
            "endTime": "22:06",
            "timeLength": 15,
            "courseLevel": "高级",
            "student": [
                {
                    "userId": 25,
                    "userName": "李白",
                    "phoneNumber": "17085145711",
                    "cardNumber": "20190425000001"
                }
            ]
        }
      }

### 删除 [DELETE] /admin/attendClass/{id} 
+ Description
    + [MUST] authenticated
    + [MUST] ROLE_ADMIN | ROLE_SUPER_ADMIN
+ Response 204

### 列表 [GET] /admin/attendClass
+ Parameters
  + page[number]=1&page[size]=10
  + sort -modified(从新到旧) | modified(从旧到新)

+ Response 200 (application/json)

      {
        "meta": {
            "totalPages": 3,
            "totalElements": 22,
            "size": 10,
            "number": 1,
            "numberOfElements": 10,
            "first": true,
            "last": false,
            "sort": null
        },
        "links": {
            "self": "/admin/attendClass?page[number]=1&page[size]=10",
            "first": "/admin/attendClass?page[number]=1&page[size]=10",
            "next": "/admin/attendClass?page[number]=2&page[size]=10",
            "last": "/admin/attendClass?page[number]=3&page[size]=10"
        },
        "data": [
            {
                "id": 4,
                "created": "2019-04-16 14:02:57",
                "modified": "2019-04-16 14:02:54",
                "state": 0,
                "categoryId": 2,
                "attendDate": "2019-04-16",
                "beginTime": "18:10",
                "endTime": "16:30",
                "attendTimeBucket": "2019.04.16 18:10-16:30",
                "mianCoachName": "白求恩",
                "attendClassStateName": "已预约",
                "categoryTitle": "私教课",
                "showSign": false
            },
            {
                "id": 5,
                "created": "2019-04-23 14:03:01",
                "modified": "2019-04-23 14:02:59",
                "state": 0,
                "categoryId": 4,
                "attendDate": "2019-04-17",
                "beginTime": "16:34",
                "endTime": "16:44",
                "attendTimeBucket": "2019.04.17 16:34-16:44",
                "mianCoachName": "张三1",
                "attendClassStateName": "已预约",
                "categoryTitle": "小班课",
                "showSign": false
            },
            {
                "id": 6,
                "state": 0,
                "categoryId": 5,
                "attendDate": "2019-04-18",
                "beginTime": "16:35",
                "endTime": "16:45",
                "attendTimeBucket": "2019.04.18 16:35-16:45",
                "mianCoachName": "张三1",
                "attendClassStateName": "已预约",
                "categoryTitle": "查房",
                "showSign": false
            },
            {
                "id": 7,
                "state": 0,
                "categoryId": 2,
                "attendDate": "2019-04-19",
                "beginTime": "16:40",
                "endTime": "16:50",
                "attendTimeBucket": "2019.04.19 16:40-16:50",
                "mianCoachName": "白求恩",
                "attendClassStateName": "已预约",
                "categoryTitle": "私教课",
                "showSign": false
            },
            {
                "id": 8,
                "state": 0,
                "categoryId": 4,
                "attendDate": "2019-04-25",
                "beginTime": "17:13",
                "endTime": "17:53",
                "attendTimeBucket": "2019.04.25 17:13-17:53",
                "mianCoachName": "白求恩",
                "attendClassStateName": "已预约",
                "categoryTitle": "小班课",
                "showSign": false
            },
            {
                "id": 11,
                "state": 0,
                "categoryId": 5,
                "attendDate": "2019-04-25",
                "beginTime": "17:49",
                "endTime": "18:19",
                "attendTimeBucket": "2019.04.25 17:49-18:19",
                "mianCoachName": "白求恩",
                "attendClassStateName": "已预约",
                "categoryTitle": "查房",
                "showSign": false
            },
            {
                "id": 14,
                "created": "2019-04-28 13:32:59",
                "modified": "2019-04-28 13:32:59",
                "state": 2,
                "categoryId": 3,
                "attendDate": "2019-05-02",
                "beginTime": "09:20",
                "endTime": "18:50",
                "attendTimeBucket": "2019.05.02 09:20-18:50",
                "mianCoachName": "白求恩",
                "attendClassStateName": "已完结",
                "categoryTitle": "助教课",
                "showSign": false
            },
            {
                "id": 16,
                "state": 0,
                "categoryId": 2,
                "attendDate": "2019-04-25",
                "beginTime": "18:31",
                "endTime": "18:51",
                "attendTimeBucket": "2019.04.25 18:31-18:51",
                "mianCoachName": "白求恩",
                "attendClassStateName": "已预约",
                "categoryTitle": "私教课",
                "showSign": false
            },
            {
                "id": 17,
                "state": 0,
                "categoryId": 4,
                "attendDate": "2019-05-02",
                "beginTime": "11:15",
                "endTime": "18:55",
                "attendTimeBucket": "2019.05.02 11:15-18:55",
                "mianCoachName": "白求恩",
                "attendClassStateName": "已预约",
                "categoryTitle": "小班课",
                "showSign": false
            },
            {
                "id": 18,
                "created": "2019-05-07 13:45:13",
                "modified": "2019-05-07 13:45:15",
                "state": 0,
                "categoryId": 2,
                "attendDate": "2019-05-07",
                "beginTime": "12:51",
                "endTime": "14:51",
                "attendTimeBucket": "2019.05.07 12:51-14:51",
                "mianCoachName": "ycl",
                "attendClassStateName": "已预约",
                "categoryTitle": "私教课",
                "showSign": false
            }
        ]
      }
### 获取客户会员卡号 [GET] /admin/cards/{studentUserId}

+ Response 200 (application/json)

      {
        "data": [
            {
                "id": 4,
                "cardNumber": "20190414000000"
            },
            {
                "id": 24,
                "cardNumber": "20190418000000"
            }
        ]
      }

## 统计管理
+ Description
+ studentInfo - 用户统计
    +  studentTotal (Long) - 用户总数
    +  HaveCardNumber (Long) - 持卡会员数
    +  purposeCardNumber (Long) - 意向会员数
    +  percentConversion (String) - 转化率
    +  addStudent (Long) - 前一天新增用户
+ dealInfo - 赢收统计
    + dealTotal (BigDecimal) - 交易总额
    + yesterdaySell (BigDecimal) - 昨日销售
    + plastMonthSell (BigDecimal) - 上月销售
    + avgdaySell (BigDecimal) - 日均销售
+ coachInfo - 教练统计
    + coachTotal (Long) - 教练总数
    + yesterdaySell (BigDecimal) - 昨日销售
    + addCoach (Long) - 前一天新增教练
+ ttendClassInfo - 上课统计
    +  attendClassTotal (Long) - 上课总数
    +  dayAttendClass (Long) - 今日课程数
    +  attendClassNumber (Long) - 上课人数
    +  avgdayNumber (Long) - 日均课数
+ cardExamineNumber - 会员卡审核数
+ studentLeaveApplyNumber - 用户请假申请数
+ salesVolumeTrends - 销售额趋势
    + monthSalesVolume (BigDecimal) - 月销售额
    + month (String) - 销售月份
+ CourseStatistics - 课程统计
    +  monthCourseNum (Long) - 月课程数
    +  month (String) - 月份

### 首页统计接口[GET] /admin/data
    
+ Response 200 (application/json)

      {
        "data": {
            "studentInfo": {
                "studentTotal": 7,
                "purposeCardNumber": -1,
                "percentConversion": "114.29",
                "addStudent": 0,
                "haveCardNumber": 8
            },
            "dealInfo": {
                "dealTotal": 20709,
                "yesterdaySell": 0,
                "plastMonthSell": 19006,
                "avgdaySell": 0
            },
            "coachInfo": {
                "coachTotal": 14,
                "addCoach": 0
            },
            "ttendClassInfo": {
                "attendClassTotal": 12,
                "dayAttendClass": 1,
                "attendClassNumber": 3,
                "avgdayNumber": 10
            },
            "cardExamineNumber": 11,
            "studentLeaveApplyNumber": 2,
            "salesVolumeTrends": [
                {
                    "monthSalesVolume": 19006,
                    "month": "2019-04"
                },
                {
                    "monthSalesVolume": 3,
                    "month": "2019-03"
                },
                {
                    "monthSalesVolume": 0,
                    "month": "2019-02"
                },
                {
                    "monthSalesVolume": 0,
                    "month": "2019-01"
                },
                {
                    "monthSalesVolume": 0,
                    "month": "2018-12"
                },
                {
                    "monthSalesVolume": 0,
                    "month": "2018-11"
                },
                {
                    "monthSalesVolume": 0,
                    "month": "2018-10"
                },
                {
                    "monthSalesVolume": 0,
                    "month": "2018-09"
                },
                {
                    "monthSalesVolume": 0,
                    "month": "2018-08"
                },
                {
                    "monthSalesVolume": 0,
                    "month": "2018-07"
                },
                {
                    "monthSalesVolume": 0,
                    "month": "2018-06"
                },
                {
                    "monthSalesVolume": 0,
                    "month": "2018-05"
                }
            ],
            "courseStatistics": {
                "openClass": [
                    {
                        "monthCourseNum": 0,
                        "month": "2019-04"
                    },
                    {
                        "monthCourseNum": 0,
                        "month": "2019-03"
                    },
                    {
                        "monthCourseNum": 0,
                        "month": "2019-02"
                    },
                    {
                        "monthCourseNum": 0,
                        "month": "2019-01"
                    },
                    {
                        "monthCourseNum": 0,
                        "month": "2018-12"
                    },
                    {
                        "monthCourseNum": 0,
                        "month": "2018-11"
                    },
                    {
                        "monthCourseNum": 0,
                        "month": "2018-10"
                    },
                    {
                        "monthCourseNum": 0,
                        "month": "2018-09"
                    },
                    {
                        "monthCourseNum": 0,
                        "month": "2018-08"
                    },
                    {
                        "monthCourseNum": 0,
                        "month": "2018-07"
                    },
                    {
                        "monthCourseNum": 0,
                        "month": "2018-06"
                    },
                    {
                        "monthCourseNum": 0,
                        "month": "2018-05"
                    }
                ],
                "privateClass": [
                    {
                        "monthCourseNum": 0,
                        "month": "2019-04"
                    },
                    {
                        "monthCourseNum": 0,
                        "month": "2019-03"
                    },
                    {
                        "monthCourseNum": 0,
                        "month": "2019-02"
                    },
                    {
                        "monthCourseNum": 0,
                        "month": "2019-01"
                    },
                    {
                        "monthCourseNum": 0,
                        "month": "2018-12"
                    },
                    {
                        "monthCourseNum": 0,
                        "month": "2018-11"
                    },
                    {
                        "monthCourseNum": 0,
                        "month": "2018-10"
                    },
                    {
                        "monthCourseNum": 0,
                        "month": "2018-09"
                    },
                    {
                        "monthCourseNum": 0,
                        "month": "2018-08"
                    },
                    {
                        "monthCourseNum": 0,
                        "month": "2018-07"
                    },
                    {
                        "monthCourseNum": 0,
                        "month": "2018-06"
                    },
                    {
                        "monthCourseNum": 0,
                        "month": "2018-05"
                    }
                ]
            }
         }
       }

### 销售教练排名 [GET] /admin/cardOrders/coachSalesRank
+ Parameters
  + packageType(0:新买卡，1：续课，2：套餐升级)
  + 不填packageType统计页销售教练排名
+ Description
  + coachId - 教练ID
  + coachName - 教练名称
  + phoneNumber - 手机号
  + packageType - 销售卡状态
  + salesNum - 销售个数
  + ranking - 排名
  
+ Response 200 (application/json)

      {
        "data": {
            "content": [
                {
                    "packageType": 0,
                    "packageTypeName": "新买课",
                    "salesNum": 9,
                    "coachId": 24,
                    "coachName": "江小白",
                    "phoneNumber": "17600261644",
                    "ranking": 1
                },
                {
                    "packageType": 0,
                    "packageTypeName": "新买课",
                    "salesNum": 6,
                    "coachId": 5,
                    "coachName": "ycl",
                    "phoneNumber": "17085145710",
                    "ranking": 2
                },
                {
                    "packageType": 0,
                    "packageTypeName": "新买课",
                    "salesNum": 3,
                    "coachId": 3,
                    "coachName": "张三1",
                    "phoneNumber": "18810649832",
                    "ranking": 3
                },
                {
                    "packageType": 1,
                    "packageTypeName": "续课",
                    "salesNum": 2,
                    "coachId": 2,
                    "coachName": "白求恩",
                    "phoneNumber": "18331931950",
                    "ranking": 4
                },
                {
                    "packageType": 0,
                    "packageTypeName": "新买课",
                    "salesNum": 1,
                    "coachId": 28,
                    "phoneNumber": "13051638531",
                    "ranking": 5
                }
            ],
            "totalElements": 5,
            "totalPages": 1,
            "last": true,
            "number": 0,
            "size": 10,
            "sort": null,
            "numberOfElements": 5,
            "first": true
        }
      }

### 动作库使用排名 [GET] /admin/actions/actionRank?sort=0
+ Parameters
  + sort必填项,0：默认全部排序
  + 1：上课记录排序，2：课后作业排序
+ Description
  + actionId - 动作ID
  + actionTitle - 动作名称
  + categoryTitle - 分类名称
  + frequency - 次数
  + ranking - 排名
  
+ Response 200 (application/json)

      {
        "data": {
            "content": [
                {
                    "id": 1,
                    "actionTitle": "俯卧撑",
                    "categoryTitle": "室内",
                    "actionId": 1,
                    "frequency": 6,
                    "ranking": 1
                },
                {
                    "id": 2,
                    "actionTitle": "仰卧起坐",
                    "categoryTitle": "室内",
                    "actionId": 2,
                    "frequency": 5,
                    "ranking": 2
                },
                {
                    "id": 4,
                    "actionTitle": "腿部按摩1",
                    "categoryTitle": "有氧室",
                    "actionId": 4,
                    "frequency": 4,
                    "ranking": 3
                },
                {
                    "id": 5,
                    "actionTitle": "腿部按摩1111",
                    "categoryTitle": "有氧室",
                    "actionId": 5,
                    "frequency": 4,
                    "ranking": 4
                },
                {
                    "id": 9,
                    "actionTitle": "测试动作11133",
                    "categoryTitle": "室内",
                    "actionId": 9,
                    "frequency": 3,
                    "ranking": 5
                },
                {
                    "id": 3,
                    "actionTitle": "瑜伽锻炼",
                    "categoryTitle": "室内",
                    "actionId": 3,
                    "frequency": 2,
                    "ranking": 6
                },
                {
                    "id": 10,
                    "actionTitle": "测试动作222",
                    "categoryTitle": "室内",
                    "actionId": 10,
                    "frequency": 1,
                    "ranking": 7
                }
            ],
            "totalElements": 7,
            "totalPages": 1,
            "last": true,
            "number": 0,
            "size": 10,
            "sort": null,
            "numberOfElements": 7,
            "first": true
        }
      }

### 教练上课记录排名 [GET] /admin/coachAttendClass/coachAttendClassRank
+ Parameters
  + categoryId(非必填) 分类ID
+ Description
  + actionId - 动作ID
  + actionTitle - 动作名称
  + categoryTitle - 分类名称
  + frequency - 次数
  + ranking - 排名
  
+ Response 200 (application/json)
    
      {
        "data": {
            "content": [
                {
                    "userId": 2,
                    "realName": "白求恩",
                    "phoneNumber": "18331931950",
                    "frequency": 10,
                    "ranking": 1
                },
                {
                    "userId": 4,
                    "realName": "小高",
                    "phoneNumber": "18611194890",
                    "frequency": 6,
                    "ranking": 2
                },
                {
                    "userId": 22,
                    "realName": "张老师",
                    "phoneNumber": "13000000000",
                    "frequency": 5,
                    "ranking": 3
                },
                {
                    "userId": 26,
                    "realName": "李四",
                    "phoneNumber": "17085145712",
                    "frequency": 4,
                    "ranking": 4
                },
                {
                    "userId": 3,
                    "realName": "张三1",
                    "phoneNumber": "18810649832",
                    "frequency": 2,
                    "ranking": 5
                },
                {
                    "userId": 5,
                    "realName": "ycl",
                    "phoneNumber": "17085145710",
                    "frequency": 1,
                    "ranking": 6
                }
            ],
            "totalElements": 6,
            "totalPages": 1,
            "last": true,
            "number": 0,
            "size": 10,
            "sort": null,
            "numberOfElements": 6,
            "first": true
        }
      }


## 活动报名统计
### 列表 [GET] /admin/activitySigns
+ Parameters
  + activityId= 11
  + filter[activityTitle]=月子
  + page[number]=1&page[size]=10
+ Description
    + id - 活动报名ID
    + created - 创建时间
    + modified - 修改时间
    + activityId - 活动ID
    + realName - 报名人姓名
    + phoneNumber - 报名手机号
    + activityTitle - 活动名称 

+ Response 200 (application/json)

       {
        "data": {
            "content": [
                {
                    "id": 15,
                    "created": "2019-05-10 17:51:01",
                    "modified": "2019-05-10 17:51:01",
                    "activityId": 16,
                    "realName": "白求恩",
                    "phoneNumber": "18331931950",
                    "activityTitle": "ffffasdf"
                },
                {
                    "id": 14,
                    "created": "2019-05-10 15:00:05",
                    "modified": "2019-05-10 15:00:05",
                    "activityId": 1,
                    "realName": "白求恩",
                    "phoneNumber": "18331931950",
                    "activityTitle": "孕妇一日游活动"
                },
                {
                    "id": 13,
                    "created": "2019-05-09 16:20:24",
                    "modified": "2019-05-09 16:20:24",
                    "activityId": 6,
                    "realName": "白求恩",
                    "phoneNumber": "18331931950",
                    "activityTitle": "月子线下活动1"
                },
                {
                    "id": 12,
                    "created": "2019-05-09 16:18:39",
                    "modified": "2019-05-09 16:18:39",
                    "activityId": 11,
                    "realName": "白求恩",
                    "phoneNumber": "18331931950",
                    "activityTitle": "月子线下活动4"
                },
                {
                    "id": 11,
                    "created": "2019-05-09 16:15:52",
                    "modified": "2019-05-09 16:15:52",
                    "activityId": 12,
                    "realName": "白求恩",
                    "phoneNumber": "18331931950",
                    "activityTitle": "月子线下活动5"
                }
            ],
            "totalPages": 3,
            "totalElements": 15,
            "last": false,
            "number": 0,
            "size": 5,
            "sort": null,
            "numberOfElements": 5,
            "first": true
        }
      }

## 用户管理
### 用户详情描述 [GET] /users/userCardInfo?userId={id}
+ Parameters
  + userId - 用户ID（必填）
  + cardId - 卡ID（非必填）
  + userId=25（示例）
+ Description
    + userName - 用户名称
    + phoneNumber - 用户手机号
    + SalespersonName - 销售教练
    + sexName - 性别名称
    + region - 用户所在地区
    + address - 详细地址
    + isShow - 用户是否有卡
+ Response 200 (application/json)

      {
        "data": {
            "userName": "李白",
            "phoneNumber": "17085145711",
            "sexName": "男",
            "region": {
                "id": 17,
                "parentId": 13,
                "regionTitle": "丰台区",
                "parent": {
                    "id": 13,
                    "parentId": 0,
                    "regionTitle": "北京市"
                }
            },
            "address": "北京市丰台区北大地",
            "avatar": "https://wx.qlogo.cn/mmopen/vi_32/Q0j4TwGTfTKFASdZ7SWviaHbqlp6tEVO5lLkaic3TIs8BBuczkQsWp7Hf1DvW9vyias1owNlEtrEEV45pl84k94gw/0",
            "salespersonName": "ycl",
            "show": true
        }
      }

### 会员卡列表 [GET] /v1/teacher/cards
+ Parameters
  + filter[userId]=1&sort=-created（示例）
  + page[number]=1&page[size]=10
+ Description
    + id - 卡ID
    + cardNumber - 卡号
    + projectcategoryTitle - 项目类型（卡类型）
    + salespersonName - 销售教练
    + packageTypeName - 套餐类型（卡状态）
    + classTimesNum - 总课时
    + remainingClassTime - 剩余次数
    + created - 发卡时间
    + effectiveDate - 有效日期

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
                    "property": "created",
                    "ignoreCase": false,
                    "nullHandling": "NATIVE",
                    "descending": true,
                    "ascending": false
                }
            ]
        },
        "links": {
            "self": "/v1/teacher/cards?filter[userId]=1&sort=-created&page[number]=1&page[size]=10",
            "first": "/v1/teacher/cards?filter[userId]=1&sort=-created&page[number]=1&page[size]=10",
            "last": "/v1/teacher/cards?filter[userId]=1&sort=-created&page[number]=1&page[size]=10"
        },
        "data": [
            {
                "id": 4,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-05-19 12:04:58",
                "modified": "2019-05-19 12:04:58",
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
                "effectiveDate": "2021-03-01",
                "payMethod": 1,
                "inside": 1,
                "dtd": 1,
                "dtdFee": 200,
                "remarks": "你是听你说打发布到封神榜备注信息",
                "leaveRemainingNum": 1,
                "leaveRemainingDays": 18,
                "projectName": "12节孕期瑜伽小班课",
                "packageTypeName": "新买课",
                "classTimesNum": 18,
                "stateName": "正常",
                "projectcategoryTitle": "测试",
                "salespersonName": "张三1"
            },
            {
                "id": 24,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2019-05-17 15:13:28",
                "modified": "2019-05-17 15:13:28",
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
                "effectiveDate": "2020-05-13",
                "payMethod": 3,
                "inside": 1,
                "dtd": 1,
                "dtdFee": 0,
                "remarks": "高耗能高好难过",
                "leaveRemainingNum": 1,
                "leaveRemainingDays": 18,
                "projectName": "孕期瑜伽小班课",
                "packageTypeName": "新买课",
                "classTimesNum": 15,
                "stateName": "请假中",
                "projectcategoryTitle": "孕期瑜伽小班课",
                "salespersonName": "白求恩"
            }
        ]
      }



### 会员卡上课记录列表 [GET] /admin/attendClass/cardAttendClass
+ Parameters
  + studentUserId - 用户ID（必填）
  + cardId -  卡ID（必填）
  + attendDate - 日期（非必填；2019-05-10）
  + state - 状态（非必填；状态，0：审核中，1：正常，2：请假中，3：审核未通过）
  + cardAttendClass?studentUserId=1&cardId=4（示例）
+ Description
    + id - 课程ID
    + attendTimeBucket - 上课时间段
    + salespersonName - 销售教练
    + mianCoachName - 上课教练
    + timeLength - 本课时
    + attendClassStateName - 上课状态
    + created - 创建时间
    + modified - 修改时间

+ Response 200 (application/json)

      {
        "data": {
            "content": [
                {
                    "id": 34,
                    "created": "2019-05-09 20:14:32",
                    "modified": "2019-05-09 20:14:32",
                    "state": 2,
                    "attendDate": "2019-05-15",
                    "beginTime": "10:51",
                    "endTime": "11:06",
                    "timeLength": 15,
                    "attendTimeBucket": "2019.05.15 10:51-11:06",
                    "mianCoachName": "李四",
                    "attendClassStateName": "已完结",
                    "studentUserId": 26,
                    "salespersonName": "张三1",
                    "showSign": false
                },
                {
                    "id": 28,
                    "created": "2019-05-09 17:56:03",
                    "modified": "2019-05-09 17:56:03",
                    "state": 2,
                    "attendDate": "2019-05-10",
                    "beginTime": "20:51",
                    "endTime": "21:21",
                    "timeLength": 30,
                    "attendTimeBucket": "2019.05.10 20:51-21:21",
                    "mianCoachName": "张老师",
                    "attendClassStateName": "已完结",
                    "studentUserId": 22,
                    "salespersonName": "张三1",
                    "showSign": false
                },
                {
                    "id": 27,
                    "created": "2019-05-09 17:50:23",
                    "modified": "2019-05-09 17:50:23",
                    "state": 2,
                    "attendDate": "2019-05-10",
                    "beginTime": "20:51",
                    "endTime": "21:21",
                    "timeLength": 30,
                    "attendTimeBucket": "2019.05.10 20:51-21:21",
                    "mianCoachName": "张老师",
                    "attendClassStateName": "已完结",
                    "studentUserId": 22,
                    "salespersonName": "张三1",
                    "showSign": false
                },
                {
                    "id": 4,
                    "created": "2019-04-16 14:02:57",
                    "modified": "2019-04-16 14:02:54",
                    "state": 0,
                    "attendDate": "2019-04-16",
                    "beginTime": "18:10",
                    "endTime": "16:30",
                    "timeLength": 2,
                    "attendTimeBucket": "2019.04.16 18:10-16:30",
                    "mianCoachName": "白求恩",
                    "attendClassStateName": "已预约",
                    "studentUserId": 2,
                    "salespersonName": "张三1",
                    "showSign": false
                },
                {
                    "id": 7,
                    "created": "2019-05-16 09:16:59",
                    "state": 0,
                    "attendDate": "2019-04-19",
                    "beginTime": "16:40",
                    "endTime": "16:50",
                    "timeLength": 2,
                    "attendTimeBucket": "2019.04.19 16:40-16:50",
                    "mianCoachName": "白求恩",
                    "attendClassStateName": "已预约",
                    "studentUserId": 2,
                    "salespersonName": "张三1",
                    "showSign": false
                }
            ],
            "totalPages": 1,
            "totalElements": 5,
            "last": true,
            "number": 0,
            "size": 10,
            "numberOfElements": 5,
            "sort": null,
            "first": true
        }
      }

### 会员卡阶段评估列表 [GET] admin/evaluations/cardEvaluation
+ Parameters
  + cardId - 卡ID
  + filter[cardId]=4（示例）
+ Description
    + id - 评估ID
    + attendTimeBucket - 评估时间段
    + mianCoachName - 评估教练
    + created - 创建时间
    + modified - 修改时间

+ Response 200 (application/json)

      {
        "data": {
            "content": [
                {
                    "id": 7,
                    "created": "2019-04-19 11:28:47",
                    "modified": "2019-04-19 11:28:43",
                    "mianCoachName": "白求恩",
                    "attendDate": "2019-04-19",
                    "beginTime": "16:40",
                    "endTime": "16:50",
                    "attendTimeBucket": "2019.04.19 16:40-16:50",
                    "coachId": 2
                },
                {
                    "id": 4,
                    "created": "2019-04-19 11:28:32",
                    "modified": "2019-04-19 11:28:35",
                    "mianCoachName": "白求恩",
                    "attendDate": "2019-04-16",
                    "beginTime": "18:10",
                    "endTime": "16:30",
                    "attendTimeBucket": "2019.04.16 18:10-16:30",
                    "coachId": 2
                }
            ],
            "totalPages": 1,
            "totalElements": 2,
            "last": true,
            "number": 0,
            "size": 10,
            "numberOfElements": 2,
            "sort": null,
            "first": true
        }
      }


### 会员卡服务教练列表 [GET] /admin/coachAttendClass/cardCoach
+ Parameters
  + cardId - 卡ID
  + cardId=4（示例）
  + filter[userId]=22（示例）
  + filter[realName]=小（示例）
  + filter[phoneNumber]=18（示例）
  + page[number]=1&page[size]=10
+ Description
    + id - 教练ID
    + realName - 教练名称
    + phoneNumber - 手机号
    + created - 创建时间
    + modified - 修改时间

+ Response 200 (application/json)

      {
        "data": {
            "content": [
                {
                    "id": 31,
                    "created": "2019-05-10 10:29:40",
                    "modified": "2019-05-10 10:29:40",
                    "userId": 26,
                    "realName": "李四",
                    "phoneNumber": "17085145712",
                    "ranking": 0
                },
                {
                    "id": 20,
                    "created": "2019-05-09 17:50:23",
                    "modified": "2019-05-09 17:50:23",
                    "userId": 22,
                    "realName": "张老师",
                    "phoneNumber": "13000000000",
                    "ranking": 0
                },
                {
                    "id": 2,
                    "created": "2019-04-16 18:33:31",
                    "modified": "2019-04-16 18:33:28",
                    "userId": 4,
                    "realName": "小高",
                    "phoneNumber": "18611194890",
                    "ranking": 0
                },
                {
                    "id": 1,
                    "created": "2019-04-16 17:04:39",
                    "modified": "2019-04-16 17:04:36",
                    "userId": 2,
                    "realName": "白求恩",
                    "phoneNumber": "18331931950",
                    "ranking": 0
                }
            ],
            "totalPages": 1,
            "totalElements": 4,
            "last": true,
            "number": 0,
            "size": 10,
            "numberOfElements": 4,
            "sort": null,
            "first": true
        }
      }


### 用户生日提醒列表 [GET] /admin/users/weekBirthdayRemind
+ Description
    + id - 用户ID
    + realName - 名称
    + phoneNumber - 手机号
    + organizationTitle - 用户来源
    + birthday - 生日
    + created - 创建时间
    + modified - 修改时间

+ Response 200 (application/json)

      {
        "data": {
            "content": [
                {
                    "id": 3,
                    "created": "2019-04-11 19:43:49",
                    "modified": "2019-04-30 16:37:32",
                    "phoneNumber": "18810649832",
                    "realName": "张三1",
                    "birthday": "2019-05-21",
                    "organizationTitle": "北京月子会所",
                    "hasCard": false
                },
                {
                    "id": 18,
                    "created": "2019-04-27 15:49:50",
                    "modified": "2019-04-27 18:24:25",
                    "phoneNumber": "13000000002",
                    "realName": "生日快了",
                    "birthday": "2019-05-23",
                    "organizationTitle": "北京月子会所",
                    "hasCard": false
                },
                {
                    "id": 2,
                    "created": "2019-04-10 17:46:41",
                    "modified": "2019-04-10 17:46:37",
                    "phoneNumber": "18331931950",
                    "realName": "白求恩",
                    "birthday": "2019-05-20",
                    "organizationTitle": "北京月子会所",
                    "hasCard": false
                }
            ],
            "totalPages": 1,
            "totalElements": 3,
            "last": true,
            "number": 0,
            "size": 10,
            "numberOfElements": 3,
            "sort": null,
            "first": true
        }
      }

## 会员卡管理
### 已开卡列表[GET] /admin/cards
+ Parameters
  + cardId - 卡ID
  + cardId=4（示例）
  + filter[state]=1&sort=-modified（开卡示例）
  + [GET]admin/cards/projectCategories?projectcategoryId=1(参数为卡类型id)
  + filter[salesperson]=5（销售教练搜索）
  + filter[packageType]=0（套餐类型（卡状态）搜索）
  + filter[state]=0&filter[state]=3&sort=state（会员卡审核列表）
  + filter[remainingClassTime:le]=5&sort=-remainingClassTime&sort=-modified（会员卡到期提醒列表）
  + page[number]=1&page[size]=10
+ Description
    + id - 会员卡ID
    + cardNumber - 卡号
    + projectcategoryTitle - 卡类型
    + salespersonName - 销售教练
    + packageTypeName - 卡状态名称
    + realName - 用户名
    + classTimesNum - 总课时
    + remainingClassTime - 剩余课时
    + effectiveDate - 有效期
    + modified - 修改时间
    + state - 状态，0：审核中，1：正常，2：请假中，3：审核未通过  

+ Response 200 (application/json) （开卡列表）

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
                    "ascending": false,
                    "descending": true
                }
            ]
        },
        "links": {
            "self": "/admin/cards?filter[state]=1&sort=-modified&page[number]=1&page[size]=10",
            "first": "/admin/cards?filter[state]=1&sort=-modified&page[number]=1&page[size]=10",
            "last": "/admin/cards?filter[state]=1&sort=-modified&page[number]=1&page[size]=10"
        },
        "data": [
            {
                "id": 4,
                "created": "2019-05-19 12:04:58",
                "modified": "2019-05-19 12:04:58",
                "cardNumber": "20190414000000",
                "state": 1,
                "realName": "海燕",
                "packageType": 0,
                "projectId": 9,
                "classTime": 18,
                "giftClassTime": 0,
                "remainingClassTime": 10,
                "salesperson": 3,
                "effectiveDate": "2021-03-01",
                "projectName": "12节孕期瑜伽小班课",
                "packageTypeName": "新买课",
                "classTimesNum": 18,
                "stateName": "正常",
                "projectcategoryTitle": "测试",
                "salespersonName": "张三1"
            },
            {
                "id": 48,
                "created": "2019-05-17 18:20:21",
                "modified": "2019-05-18 12:13:56",
                "cardNumber": "20190517000007",
                "state": 1,
                "realName": "货的话",
                "packageType": 0,
                "projectId": 1,
                "classTime": 0,
                "giftClassTime": 0,
                "remainingClassTime": 1,
                "salesperson": 24,
                "effectiveDate": "2019-05-17",
                "projectName": "免费体验课33",
                "packageTypeName": "新买课",
                "classTimesNum": 0,
                "stateName": "正常",
                "projectcategoryTitle": "免费体验课",
                "salespersonName": "江小白"
            },
            {
                "id": 37,
                "cardNumber": "20190425000000",
                "state": 1,
                "realName": "周芷若",
                "packageType": 0,
                "projectId": 3,
                "classTime": 45,
                "giftClassTime": 0,
                "remainingClassTime": 10,
                "salesperson": 0,
                "effectiveDate": "2020-10-01",
                "projectName": "孕期瑜伽小班课",
                "packageTypeName": "新买课",
                "classTimesNum": 45,
                "stateName": "正常",
                "projectcategoryTitle": "孕期瑜伽小班课",
                "salespersonName": "未添加真实姓名"
            }
        ]
      }


+ Response 200 (application/json) （审核列表）

      {
        "meta": {
            "totalPages": 4,
            "totalElements": 11,
            "size": 3,
            "number": 1,
            "numberOfElements": 3,
            "first": true,
            "last": false,
            "sort": [
                {
                    "direction": "ASC",
                    "property": "state",
                    "ignoreCase": false,
                    "nullHandling": "NATIVE",
                    "descending": false,
                    "ascending": true
                }
            ]
        },
        "links": {
            "self": "/admin/cards?filter[state]=0&filter[state]=3&sort=state&page[number]=1&page[size]=3",
            "first": "/admin/cards?filter[state]=0&filter[state]=3&sort=state&page[number]=1&page[size]=3",
            "next": "/admin/cards?filter[state]=0&filter[state]=3&sort=state&page[number]=2&page[size]=3",
            "last": "/admin/cards?filter[state]=0&filter[state]=3&sort=state&page[number]=4&page[size]=3"
        },
        "data": [
            {
                "id": 5,
                "created": "2019-02-15 13:48:51",
                "modified": "2019-02-15 13:48:51",
                "cardNumber": "20190414000001",
                "state": 0,
                "realName": "李四",
                "packageType": 0,
                "projectId": 11,
                "classTime": 1,
                "giftClassTime": 0,
                "remainingClassTime": 8,
                "salesperson": 2,
                "effectiveDate": "2020-02-02",
                "projectName": "1节免费体验课",
                "packageTypeName": "新买课",
                "classTimesNum": 1,
                "stateName": "审核中",
                "projectcategoryTitle": "孕产套课",
                "salespersonName": "白求恩"
            },
            {
                "id": 7,
                "created": "2019-03-15 13:48:53",
                "modified": "2019-03-15 13:48:53",
                "cardNumber": "20190414000002",
                "state": 0,
                "realName": "王五",
                "packageType": 0,
                "projectId": 12,
                "classTime": 25,
                "giftClassTime": 0,
                "remainingClassTime": 15,
                "salesperson": 3,
                "effectiveDate": "2020-03-03",
                "projectName": "25节孕产套课",
                "packageTypeName": "新买课",
                "classTimesNum": 25,
                "stateName": "审核中",
                "projectcategoryTitle": "测试",
                "salespersonName": "张三1"
            },
            {
                "id": 12,
                "created": "2019-04-15 13:48:55",
                "modified": "2019-04-15 13:48:55",
                "cardNumber": "20190415000001",
                "state": 0,
                "realName": "阿斯达",
                "packageType": 0,
                "projectId": 12,
                "classTime": 14,
                "giftClassTime": 0,
                "remainingClassTime": 11,
                "salesperson": 2,
                "effectiveDate": "2020-05-15",
                "projectName": "25节孕产套课",
                "packageTypeName": "新买课",
                "classTimesNum": 14,
                "stateName": "审核中",
                "projectcategoryTitle": "测试",
                "salespersonName": "白求恩"
            }
        ]
      }

+ Response 200 (application/json) （会员卡到期提醒列表）
    
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
                    "property": "remaining_class_time",
                    "ignoreCase": false,
                    "nullHandling": "NATIVE",
                    "descending": true,
                    "ascending": false
                },
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
            "self": "/admin/cards?filter[remainingClassTime:le]=5&sort=-remainingClassTime&sort=-modified&page[number]=1&page[size]=10",
            "first": "/admin/cards?filter[remainingClassTime:le]=5&sort=-remainingClassTime&sort=-modified&page[number]=1&page[size]=10",
            "last": "/admin/cards?filter[remainingClassTime:le]=5&sort=-remainingClassTime&sort=-modified&page[number]=1&page[size]=10"
        },
        "data": [
            {
                "id": 43,
                "created": "2019-05-14 16:13:53",
                "modified": "2019-05-18 12:14:41",
                "cardNumber": "20190514000003",
                "state": 0,
                "realName": "黄蓉2",
                "packageType": 0,
                "projectId": 1,
                "classTime": 0,
                "giftClassTime": 0,
                "remainingClassTime": 2,
                "salesperson": 24,
                "effectiveDate": "1980-01-01",
                "projectName": "免费体验课33",
                "packageTypeName": "新买课",
                "classTimesNum": 0,
                "stateName": "审核中",
                "projectcategoryTitle": "免费体验课",
                "salespersonName": "江小白"
            },
            {
                "id": 48,
                "created": "2019-05-17 18:20:21",
                "modified": "2019-05-18 12:13:56",
                "cardNumber": "20190517000007",
                "state": 1,
                "realName": "货的话",
                "packageType": 0,
                "projectId": 1,
                "classTime": 0,
                "giftClassTime": 0,
                "remainingClassTime": 1,
                "salesperson": 24,
                "effectiveDate": "2019-05-17",
                "projectName": "免费体验课33",
                "packageTypeName": "新买课",
                "classTimesNum": 0,
                "stateName": "正常",
                "projectcategoryTitle": "免费体验课",
                "salespersonName": "江小白"
            },
            {
                "id": 44,
                "created": "2019-05-14 16:13:55",
                "modified": "2019-05-18 12:14:41",
                "cardNumber": "20190514000004",
                "state": 0,
                "realName": "黄蓉2",
                "packageType": 0,
                "projectId": 1,
                "classTime": 0,
                "giftClassTime": 0,
                "remainingClassTime": 0,
                "salesperson": 24,
                "effectiveDate": "1980-01-01",
                "projectName": "免费体验课33",
                "packageTypeName": "新买课",
                "classTimesNum": 0,
                "stateName": "审核中",
                "projectcategoryTitle": "免费体验课",
                "salespersonName": "江小白"
            }
        ]
      }

### 请假管理
### 请假管理列表[GET] /admin/cardLeaves
+ Parameters
  + sort=state&sort=-modified（请假列表示例）
  + page[number]=1&page[size]=10
+ Description
    + cardId - 会员卡ID
    + cardNumber - 卡号
    + studentName - 用户
    + leaveDays - 请假天数
    + leaveRemainingNum - 剩余请假次数
    + leaveRemainingDays - 剩余请假天数
    + leaveReason - 请假理由
    + leaveStateName - 状态

+ Response 200 (application/json) 

      {
        "meta": {
            "totalPages": 6,
            "totalElements": 18,
            "size": 3,
            "number": 1,
            "numberOfElements": 3,
            "first": true,
            "last": false,
            "sort": [
                {
                    "direction": "ASC",
                    "property": "state",
                    "ignoreCase": false,
                    "nullHandling": "NATIVE",
                    "descending": false,
                    "ascending": true
                },
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
            "self": "/admin/cardLeaves?sort=state&sort=-modified&page[number]=1&page[size]=3",
            "first": "/admin/cardLeaves?sort=state&sort=-modified&page[number]=1&page[size]=3",
            "next": "/admin/cardLeaves?sort=state&sort=-modified&page[number]=2&page[size]=3",
            "last": "/admin/cardLeaves?sort=state&sort=-modified&page[number]=6&page[size]=3"
        },
        "data": [
            {
                "id": 22,
                "created": "2019-05-17 15:13:28",
                "modified": "2019-05-17 15:13:28",
                "cardId": 24,
                "state": 0,
                "leaveDays": 12,
                "leaveReason": "没有理由！",
                "leaveStateName": "审核中",
                "cardNumber": "20190418000000",
                "studentName": "小雨",
                "phoneNumber": "13051638532",
                "leaveRemainingNum": 1,
                "leaveRemainingDays": 18
            },
            {
                "id": 21,
                "created": "2019-05-07 17:38:05",
                "modified": "2019-05-07 17:38:05",
                "cardId": 4,
                "state": 0,
                "leaveDays": 10,
                "leaveReason": "由于近期出差，不能上课，希望予以批注，谢谢~",
                "leaveStateName": "审核中",
                "cardNumber": "20190414000000",
                "studentName": "小雨",
                "phoneNumber": "13051638532",
                "leaveRemainingNum": 1,
                "leaveRemainingDays": 18
            },
            {
                "id": 19,
                "created": "2019-04-25 12:38:45",
                "modified": "2019-04-25 12:38:45",
                "cardId": 4,
                "state": 0,
                "leaveDays": 8,
                "leaveStateName": "审核中",
                "cardNumber": "20190414000000",
                "studentName": "小雨",
                "phoneNumber": "13051638532",
                "leaveRemainingNum": 1,
                "leaveRemainingDays": 18
            }
        ]
      }
### 审核请假 [PUT]/admin/cardLeaves/{id}
+ Parameters
  + id=20（示例）
+ Description
    + [MUST] authenticated
    + [MUST] ROLE_ADMIN | ROLE_SUPER_ADMIN
    + state - 状态，0：待批准，1：已批准，2：未允许
+ Request (application/json)
    
      {
    	 "data":{
    		 "state":1,
    		 "leaveDays":10, // 弃用该字段
    		 "leaveRemainingNum":"1", // 弃用该字段 
    		 "leaveRemainingDays":"18", // 弃用该字段
    		 "leaveReason":"后台教练安排请假!" // 弃用该字段
    	  }
      }

+ Response 200
    
      {
        "data": 1
       }

### 请假详情 [GET]/admin/cardLeaves/{id}
+ Parameters
  + id=20（示例）
+ Response 200 (application/json)

      {
        "data": {
            "id": 20,
            "enabled": 1,
            "creator": 0,
            "modifier": 0,
            "created": "2019-05-19 12:04:58",
            "modified": "2019-05-19 12:04:58",
            "cardId": 4,
            "state": 1,
            "leaveDays": 10,
            "beginDate": "2019-05-01",
            "endDate": "2019-05-10",
            "leaveReason": "后台教练安排请假!",
            "leaveStateName": "正常",
            "cardNumber": "20190414000000",
            "studentName": "小雨",
            "phoneNumber": "13051638532",
            "leaveRemainingNum": 1,
            "leaveRemainingDays": 18
        }
      }

### 个人中心修改信息[PUT] /admin/users/updateOrUserCenter/{id}
+ Parameters
  + id=22（示例）
+ Description
    + [MUST] authenticated
    + [MUST] ROLE_ADMIN | ROLE_SUPER_ADMIN
    + realName - 姓名
    + phoneNumber - 手机号
    + password - 更换密码
    + oldPassword - 登录密码（之前密码）
    + avatar - 头像
+ Request (application/json)
    
      {
    	"data":{
    		"realName":"张老师",
    		"phoneNumber":"13000000000",
    		"password":"78910",
    		"oldPassword":"123456",
    		"avatar":"https://wx.qlogo.cn/mmopen/vi_32/vib6CNBXrDLZcicF9cZsC7uLFwclnN7RXAgVnOYr9Ipfn6gT9QR8m8IMFx5UicPxniboHtVhty8aib29BDazXNL5ssw/132"
    	}
      }

+ Response 204 (application/json)
    
### 后台管理登录 [GET] /admin/users/adminLogin
+ Parameters
  + phoneNumber - 手机号（必填）
  + password - 密码（必填）
  + phoneNumber=18810649831&password=123456（示例）

+ Response 200 (application/json) (登录成功)

       {
        "data": {
            "token": "d8d7a5d6-cd78-4e41-ace6-e1a262933f0c"
        }
       }
+ Response 200 (application/json) (登录失败)

       {
        "errors": [
            {
                "status": "400",
                "title": "Bad Request",
                "detail": "密码不符合要求!"
            }
        ]
       }

### 用户详情 [GET] /users/details
+ Parameters
  + phoneNumber - 手机号（必填）注意：本接口适用手机号获取用户信息
  + phoneNumber=17085145711（示例）

+ Response 200 (application/json)

      {
        "data": {
            "id": 25,
            "nickname": "小芳",
            "realName": "李白",
            "sex": 1,
            "birthday": "2001-04-20",
            "avatar": "https://wx.qlogo.cn/mmopen/vi_32/Q0j4TwGTfTKFASdZ7SWviaHbqlp6tEVO5lLkaic3TIs8BBuczkQsWp7Hf1DvW9vyias1owNlEtrEEV45pl84k94gw/0",
            "photo": "https://wx.qlogo.cn/mmopen/vi_32/Q0j4TwGTfTKFASdZ7SWviaHbqlp6tEVO5lLkaic3TIs8BBuczkQsWp7Hf1DvW9vyias1owNlEtrEEV45pl84k94gw/0",
            "sexName": "男",
            "hasCard": false
        }
      }
    

### 地区查询 [GET] /admin/regions
+ Parameters
  + filter[parentId]=0&filter[regionTitle:like]=%25河%25（查询所有省以及模糊匹配）
  + filter[parentId]=47（查询河北省所有市示例）
  + filter[parentId]=161（查询张家口所有区县示例）
  
+ Response 200 (application/json) （查询河北省所有市）
       
       {
        "meta": {
            "totalPages": 2,
            "totalElements": 11,
            "size": 10,
            "number": 1,
            "numberOfElements": 10,
            "first": true,
            "last": false,
            "sort": null
        },
        "links": {
            "self": "/admin/regions?filter[parentId]=47&page[number]=1&page[size]=10",
            "first": "/admin/regions?filter[parentId]=47&page[number]=1&page[size]=10",
            "next": "/admin/regions?filter[parentId]=47&page[number]=2&page[size]=10",
            "last": "/admin/regions?filter[parentId]=47&page[number]=2&page[size]=10"
        },
        "data": [
            {
                "id": 48,
                "enabled": 1,
                "parentId": 47,
                "regionTitle": "石家庄市"
            },
            {
                "id": 72,
                "enabled": 1,
                "parentId": 47,
                "regionTitle": "唐山市"
            },
            {
                "id": 87,
                "enabled": 1,
                "parentId": 47,
                "regionTitle": "秦皇岛市"
            },
            {
                "id": 95,
                "enabled": 1,
                "parentId": 47,
                "regionTitle": "邯郸市"
            },
            {
                "id": 115,
                "enabled": 1,
                "parentId": 47,
                "regionTitle": "邢台市"
            },
            {
                "id": 135,
                "enabled": 1,
                "parentId": 47,
                "regionTitle": "保定市"
            },
            {
                "id": 161,
                "enabled": 1,
                "parentId": 47,
                "regionTitle": "张家口市"
            },
            {
                "id": 179,
                "enabled": 1,
                "parentId": 47,
                "regionTitle": "承德市"
            },
            {
                "id": 191,
                "enabled": 1,
                "parentId": 47,
                "regionTitle": "沧州市"
            },
            {
                "id": 208,
                "enabled": 1,
                "parentId": 47,
                "regionTitle": "廊坊市"
            }
        ]
      }

+ Response 200 (application/json) （查询张家口所有区县）

      {
        "meta": {
            "totalPages": 2,
            "totalElements": 17,
            "size": 10,
            "number": 1,
            "numberOfElements": 10,
            "first": true,
            "last": false,
            "sort": null
        },
        "links": {
            "self": "/admin/regions?filter[parentId]=161&page[number]=1&page[size]=10",
            "first": "/admin/regions?filter[parentId]=161&page[number]=1&page[size]=10",
            "next": "/admin/regions?filter[parentId]=161&page[number]=2&page[size]=10",
            "last": "/admin/regions?filter[parentId]=161&page[number]=2&page[size]=10"
        },
        "data": [
            {
                "id": 162,
                "enabled": 1,
                "parentId": 161,
                "regionTitle": "桥东区"
            },
            {
                "id": 163,
                "enabled": 1,
                "parentId": 161,
                "regionTitle": "桥西区"
            },
            {
                "id": 164,
                "enabled": 1,
                "parentId": 161,
                "regionTitle": "宣化区"
            },
            {
                "id": 165,
                "enabled": 1,
                "parentId": 161,
                "regionTitle": "下花园区"
            },
            {
                "id": 166,
                "enabled": 1,
                "parentId": 161,
                "regionTitle": "宣化县"
            },
            {
                "id": 167,
                "enabled": 1,
                "parentId": 161,
                "regionTitle": "张北县"
            },
            {
                "id": 168,
                "enabled": 1,
                "parentId": 161,
                "regionTitle": "康保县"
            },
            {
                "id": 169,
                "enabled": 1,
                "parentId": 161,
                "regionTitle": "沽源县"
            },
            {
                "id": 170,
                "enabled": 1,
                "parentId": 161,
                "regionTitle": "尚义县"
            },
            {
                "id": 171,
                "enabled": 1,
                "parentId": 161,
                "regionTitle": "蔚　县"
            }
        ]
      }

