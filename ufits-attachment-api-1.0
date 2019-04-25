+ 2019年4月23日
    + API初始化

## 文件

+ Data
    + attUrl (String) - 文件访问路径
    + attTitle (String) - 文件标题
    + extension (String) - 扩展名
    + filesize (int) - 文件大小，单位：KB
    + description (String) - 描述
    + enabled (Integer) - 是否可用 0：不可用 1：可用
    + modified (Date) - 修改时间
    + created (Date) - 创建时间
    + creator (Long) - 创建人
    + modifier (Long) - 修改人

### 文件上传 [POST] /attachments
+ Description
    + 【必须】登录
    + 修改时控制权限，只能上传文件的人和管理员有权限修改
+ Parameters
    + file [必填] 文件主体 
    + attTitle
    + description
    + id 不为空时修改，为空时则添加
+ Response 201|200 (application/json)

        {
            "data": {
                "type": "/attachments",
                "attUrl": "2019-04-23/8bc57f695f244ecaa07713906ba96530.jpg",
                "id": 20
            }
        }

### 文件删除 [DELETE] /attachments/{id}
+ Description
    + 【必须】登录
    + 修改时控制权限，只能上传文件的人和管理员有权限修改
+ Response 204

### 查看图片
+ Description
    + 138示例：http://static.ufits.com/{attUrl}
    + 前提条件，本机host文件配置：192.168.1.138 static.ufits.com
