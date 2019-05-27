### 2019年05月27日
> ufits,创建action
```sql
   CREATE TABLE `action` (
  `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT,
  `category_id` bigint(20) unsigned NOT NULL COMMENT '动作分类',
  `action_title` varchar(255) COLLATE utf8mb4_unicode_ci NOT NULL COMMENT '动作名',
  `thumbnail` varchar(100) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '缩略图',
  `description` varchar(512) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '描述',
  `content` text COLLATE utf8mb4_unicode_ci COMMENT '动作详情',
  `enabled` tinyint(1) unsigned NOT NULL DEFAULT '1',
  `modifier` bigint(20) unsigned NOT NULL DEFAULT '0',
  `creator` bigint(20) unsigned NOT NULL DEFAULT '0',
  `modified` datetime NOT NULL,
  `created` datetime NOT NULL,
  PRIMARY KEY (`id`),
  KEY `idx_enabled` (`enabled`) USING BTREE
) ENGINE=InnoDB AUTO_INCREMENT=13 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci COMMENT='动作表';
```
> ufits,创建action_attachment
```sql
CREATE TABLE `action_attachment` (
  `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT,
  `action_id` bigint(20) unsigned NOT NULL COMMENT '动作标识',
  `attachment_id` bigint(20) unsigned NOT NULL,
  `enabled` tinyint(1) unsigned NOT NULL DEFAULT '1',
  `modified` datetime NOT NULL,
  `created` datetime NOT NULL,
  PRIMARY KEY (`id`),
  UNIQUE KEY `action_attachment_unique` (`action_id`,`attachment_id`) USING BTREE,
  KEY `action_id_fk` (`action_id`) USING BTREE,
  KEY `attachment_id_fk` (`attachment_id`) USING BTREE,
  KEY `idx_enabled` (`enabled`) USING BTREE
) ENGINE=InnoDB AUTO_INCREMENT=14 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;
```
> ufits,创建action_category
```sql
CREATE TABLE `action_category` (
  `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT,
  `category_title` varchar(255) COLLATE utf8mb4_unicode_ci NOT NULL COMMENT '类别名',
  `description` varchar(255) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '描述',
  `enabled` tinyint(1) unsigned NOT NULL DEFAULT '1',
  `modifier` bigint(20) unsigned NOT NULL DEFAULT '0',
  `creator` bigint(20) unsigned NOT NULL DEFAULT '0',
  `modified` datetime NOT NULL,
  `created` datetime NOT NULL,
  PRIMARY KEY (`id`),
  KEY `idx_enabled` (`enabled`) USING BTREE
) ENGINE=InnoDB AUTO_INCREMENT=6 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci COMMENT='动作分类';
```
> ufits,创建activity
```sql
CREATE TABLE `activity` (
  `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT,
  `activity_title` varchar(255) COLLATE utf8mb4_unicode_ci NOT NULL COMMENT '活动标题',
  `description` varchar(255) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '活动描述',
  `content` text COLLATE utf8mb4_unicode_ci NOT NULL COMMENT '活动内容',
  `post_date` datetime NOT NULL COMMENT '发布时间',
  `organization_id` bigint(20) unsigned DEFAULT NULL COMMENT '合作机构id',
  `stage` tinyint(1) unsigned NOT NULL DEFAULT '0' COMMENT '活动阶段：0：无限制，1：备孕，2：孕期，3：产后，4：早教',
  `recommend` tinyint(3) unsigned NOT NULL DEFAULT '0' COMMENT '是否推荐，0：否，1：是',
  `has_sign` tinyint(1) unsigned NOT NULL DEFAULT '1' COMMENT '是否可以报名，0：否，1：是',
  `thumbnail` varchar(100) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '缩略图',
  `enabled` tinyint(1) unsigned NOT NULL DEFAULT '1',
  `modifier` bigint(20) unsigned NOT NULL DEFAULT '0',
  `creator` bigint(20) unsigned NOT NULL DEFAULT '0',
  `modified` datetime NOT NULL,
  `created` datetime NOT NULL,
  PRIMARY KEY (`id`),
  KEY `fk_activity_organization_id` (`organization_id`),
  KEY `idx_enabled` (`enabled`) USING BTREE,
  CONSTRAINT `fk_activity_organization_id` FOREIGN KEY (`organization_id`) REFERENCES `organization` (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=27 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci COMMENT='活动';
```
> ufits,创建activity_attachment
```sql
CREATE TABLE `activity_attachment` (
  `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT,
  `activity_id` bigint(20) unsigned NOT NULL COMMENT '活动id',
  `attachment_id` bigint(20) unsigned NOT NULL COMMENT '图片id',
  `enabled` tinyint(1) unsigned NOT NULL DEFAULT '1',
  `modified` datetime NOT NULL,
  `created` datetime NOT NULL,
  PRIMARY KEY (`id`),
  UNIQUE KEY `activity_attachment__unique` (`activity_id`,`attachment_id`) USING BTREE,
  KEY `activity_id_fk` (`activity_id`),
  KEY `activity_attachment_id_fk` (`attachment_id`),
  KEY `idx_enabled` (`enabled`) USING BTREE,
  CONSTRAINT `activity_attachment_id_fk` FOREIGN KEY (`attachment_id`) REFERENCES `attachment` (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=18 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci COMMENT='活动图片';
```
> ufits,创建activity_sign
```sql
CREATE TABLE `activity_sign` (
  `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT,
  `activity_id` bigint(20) unsigned NOT NULL COMMENT '活动id',
  `user_id` bigint(20) unsigned NOT NULL COMMENT '用户id',
  `enabled` tinyint(1) unsigned NOT NULL DEFAULT '1',
  `modifier` bigint(20) unsigned NOT NULL DEFAULT '0',
  `creator` bigint(20) unsigned NOT NULL DEFAULT '0',
  `modified` datetime NOT NULL,
  `created` datetime NOT NULL,
  PRIMARY KEY (`id`),
  UNIQUE KEY `activity_user_unique_key` (`activity_id`,`user_id`),
  KEY `sign_user_id_fk` (`user_id`),
  KEY `idx_enabled` (`enabled`) USING BTREE,
  CONSTRAINT `sign_activity_id_fk` FOREIGN KEY (`activity_id`) REFERENCES `activity` (`id`),
  CONSTRAINT `sign_user_id_fk` FOREIGN KEY (`user_id`) REFERENCES `user` (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=25 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci COMMENT='活动报名';
```
> ufits,创建attachment
```sql
CREATE TABLE `attachment` (
  `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT,
  `att_url` varchar(255) COLLATE utf8mb4_unicode_ci NOT NULL COMMENT '图片访问地址',
  `att_title` varchar(255) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '图片名称',
  `extension` varchar(10) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '扩展名',
  `filesize` int(11) unsigned DEFAULT NULL,
  `description` varchar(255) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '图片描述',
  `enabled` tinyint(1) unsigned NOT NULL DEFAULT '1',
  `modifier` bigint(20) unsigned NOT NULL DEFAULT '0',
  `creator` bigint(20) unsigned NOT NULL DEFAULT '0',
  `modified` datetime NOT NULL,
  `created` datetime NOT NULL,
  PRIMARY KEY (`id`),
  KEY `idx_enabled` (`enabled`) USING BTREE
) ENGINE=InnoDB AUTO_INCREMENT=216 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci COMMENT='图片表';
```
> ufits,创建attend_class
```sql
CREATE TABLE `attend_class` (
  `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT,
  `state` tinyint(1) unsigned NOT NULL COMMENT '状态，0：已预约，1：进行中，2：已完结，3：预约失败',
  `category_id` bigint(20) unsigned NOT NULL COMMENT '上课类型标识',
  `attend_date` date NOT NULL COMMENT '上课日期',
  `begin_time` datetime NOT NULL COMMENT '上课时间',
  `end_time` datetime NOT NULL COMMENT '下课时间',
  `time_length` decimal(10,2) NOT NULL COMMENT '上课时长',
  `course_level_id` bigint(20) unsigned NOT NULL COMMENT '课程级别标识',
  `place` tinyint(1) unsigned NOT NULL COMMENT '场所，0：到店，1：上门',
  `organization_id` bigint(20) unsigned DEFAULT NULL COMMENT '合作机构标识',
  `shop_id` bigint(20) unsigned NOT NULL DEFAULT '0' COMMENT '门店标识',
  `region_id` bigint(20) unsigned DEFAULT NULL COMMENT '区域id',
  `address` varchar(512) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '上课详细地址',
  `longitude` decimal(10,5) DEFAULT NULL COMMENT '经度',
  `latitude` decimal(10,5) DEFAULT NULL COMMENT '纬度',
  `remarks` varchar(512) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '备注',
  `enabled` tinyint(1) unsigned NOT NULL DEFAULT '1',
  `modifier` bigint(20) unsigned NOT NULL DEFAULT '0',
  `creator` bigint(20) unsigned NOT NULL DEFAULT '0',
  `modified` datetime NOT NULL,
  `created` datetime NOT NULL,
  PRIMARY KEY (`id`),
  KEY `course_level_id_fk` (`course_level_id`),
  KEY `shop_id_fk` (`shop_id`),
  KEY `fk_category_id` (`category_id`),
  KEY `fk_attend_region_id` (`region_id`),
  KEY `fk_attend_organization_id` (`organization_id`),
  KEY `id_index` (`id`) USING BTREE,
  KEY `begin_time_index` (`begin_time`) USING BTREE,
  KEY `state_index` (`state`) USING BTREE,
  KEY `idx_attendDate` (`attend_date`) USING BTREE,
  KEY `idx_endTime` (`end_time`) USING BTREE,
  KEY `idx_enabled` (`enabled`) USING BTREE,
  CONSTRAINT `course_level_id_fk` FOREIGN KEY (`course_level_id`) REFERENCES `course_level` (`id`),
  CONSTRAINT `fk_attend_organization_id` FOREIGN KEY (`organization_id`) REFERENCES `organization` (`id`),
  CONSTRAINT `fk_attend_region_id` FOREIGN KEY (`region_id`) REFERENCES `region` (`id`),
  CONSTRAINT `fk_category_id` FOREIGN KEY (`category_id`) REFERENCES `attend_class_category` (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=93 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci COMMENT='预约/上课';
```
> ufits,创建attend_class_category
```sql
CREATE TABLE `attend_class_category` (
  `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT,
  `category_title` varchar(255) COLLATE utf8mb4_unicode_ci NOT NULL COMMENT '分类名称',
  `description` varchar(255) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '分类描述',
  `nature` tinyint(1) unsigned NOT NULL COMMENT '课程性质，0：公开，1：私教',
  `enabled` tinyint(1) unsigned NOT NULL DEFAULT '1',
  `modifier` bigint(20) unsigned NOT NULL DEFAULT '0',
  `creator` bigint(20) unsigned NOT NULL DEFAULT '0',
  `modified` datetime NOT NULL,
  `created` datetime NOT NULL,
  PRIMARY KEY (`id`),
  KEY `idx_nature` (`nature`) USING BTREE,
  KEY `idx_enabled` (`enabled`) USING BTREE
) ENGINE=InnoDB AUTO_INCREMENT=12 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;
```
> ufits,创建banner
```sql
CREATE TABLE `banner` (
  `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT,
  `att_url` varchar(255) COLLATE utf8mb4_unicode_ci NOT NULL,
  `banner_title` varchar(255) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT 'banner标题',
  `banner_url` varchar(100) COLLATE utf8mb4_unicode_ci NOT NULL COMMENT 'banner访问路径',
  `modular` tinyint(1) unsigned NOT NULL COMMENT '模块，0：活动，1：孕产知识，2：课程',
  `target_id` bigint(20) unsigned NOT NULL COMMENT '目标标识',
  `enabled` tinyint(1) unsigned NOT NULL DEFAULT '1',
  `modifier` bigint(20) unsigned NOT NULL DEFAULT '0',
  `creator` bigint(20) unsigned NOT NULL DEFAULT '0',
  `modified` datetime NOT NULL,
  `created` datetime NOT NULL,
  PRIMARY KEY (`id`),
  KEY `idx_enabled` (`enabled`) USING BTREE
) ENGINE=InnoDB AUTO_INCREMENT=7 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;
```
> ufits,创建card
```sql
CREATE TABLE `card` (
  `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT,
  `user_id` bigint(20) unsigned NOT NULL COMMENT '学生/用户id',
  `card_number` varchar(20) COLLATE utf8mb4_unicode_ci NOT NULL COMMENT '卡号',
  `state` tinyint(1) unsigned NOT NULL DEFAULT '0' COMMENT '状态，0：审核中，1：正常，2：请假中，3：审核未通过',
  `real_name` varchar(255) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '姓名',
  `birthday` datetime DEFAULT NULL COMMENT '生日',
  `pregnancy_stage` tinyint(1) unsigned NOT NULL DEFAULT '0' COMMENT '孕产阶段，0：未知，1：备孕，2：怀孕，3：产后',
  `pregnancy_date` date DEFAULT NULL COMMENT '孕产日期',
  `region_id` bigint(20) unsigned DEFAULT NULL COMMENT '区域id',
  `address` varchar(255) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '详细住址',
  `package_type` tinyint(1) unsigned NOT NULL COMMENT '套餐类型，0：新买课，1：续课，2，套餐升级',
  `project_id` bigint(20) unsigned NOT NULL COMMENT '项目标识',
  `money` decimal(10,2) NOT NULL COMMENT '金额',
  `class_time` decimal(10,2) NOT NULL COMMENT '课时数/购课数',
  `gift_class_time` decimal(10,2) NOT NULL DEFAULT '0.00' COMMENT '赠送课时/课数',
  `remaining_class_time` decimal(10,2) NOT NULL COMMENT '剩余课时',
  `salesperson` bigint(20) unsigned NOT NULL COMMENT '销售教练',
  `effective_date` date NOT NULL COMMENT '有效日期',
  `organization_id` bigint(20) unsigned DEFAULT NULL COMMENT '来源合作机构标识',
  `pay_method` tinyint(1) unsigned NOT NULL COMMENT '支付方式，0：大众点评，1：支付宝，2：微信，3：现金，4：刷卡，5：其他',
  `inside` tinyint(1) unsigned NOT NULL COMMENT '0：场外，1：场内',
  `dtd` tinyint(1) unsigned NOT NULL COMMENT '是否有上门，0：否，1：是',
  `dtd_fee` decimal(10,2) NOT NULL DEFAULT '0.00' COMMENT '上门费',
  `remarks` varchar(512) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '备注',
  `leave_remaining_num` int(11) unsigned NOT NULL COMMENT '请假剩余次数',
  `leave_remaining_days` int(11) unsigned NOT NULL COMMENT '请假剩余天数',
  `longitude` decimal(10,5) DEFAULT NULL COMMENT '经度',
  `latitude` decimal(10,5) DEFAULT NULL COMMENT '纬度',
  `enabled` tinyint(1) unsigned NOT NULL DEFAULT '1',
  `modifier` bigint(20) unsigned NOT NULL DEFAULT '0',
  `creator` bigint(20) unsigned NOT NULL DEFAULT '0',
  `modified` datetime NOT NULL,
  `created` datetime NOT NULL,
  PRIMARY KEY (`id`),
  UNIQUE KEY `idx_card_number` (`card_number`) USING BTREE,
  KEY `user_id_fk` (`user_id`),
  KEY `project_id_fk` (`project_id`),
  KEY `fk_card_organization_id` (`organization_id`),
  KEY `fk_card_region_id` (`region_id`),
  KEY `id_index` (`id`) USING BTREE,
  KEY `idx_enabled` (`enabled`) USING BTREE,
  CONSTRAINT `project_id_fk` FOREIGN KEY (`project_id`) REFERENCES `project` (`id`),
  CONSTRAINT `user_id_fk` FOREIGN KEY (`user_id`) REFERENCES `user` (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=59 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci COMMENT='会员卡';
```
> ufits,创建card_attend_class
```sql
CREATE TABLE `card_attend_class` (
  `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT,
  `card_id` bigint(20) unsigned NOT NULL COMMENT '卡id',
  `attend_class_id` bigint(20) unsigned NOT NULL COMMENT '上课id',
  PRIMARY KEY (`id`),
  UNIQUE KEY `classid_cardid_unique` (`attend_class_id`,`card_id`) USING BTREE,
  KEY `card_id_fk` (`card_id`),
  CONSTRAINT `attend_class_id_fkk` FOREIGN KEY (`attend_class_id`) REFERENCES `attend_class` (`id`),
  CONSTRAINT `card_id_fk` FOREIGN KEY (`card_id`) REFERENCES `card` (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=155 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci COMMENT='会员卡-上课/预约';
```
> ufits,创建card_attend_class
```sql
CREATE TABLE `card_attend_class` (
  `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT,
  `card_id` bigint(20) unsigned NOT NULL COMMENT '卡id',
  `attend_class_id` bigint(20) unsigned NOT NULL COMMENT '上课id',
  PRIMARY KEY (`id`),
  UNIQUE KEY `classid_cardid_unique` (`attend_class_id`,`card_id`) USING BTREE,
  KEY `card_id_fk` (`card_id`),
  CONSTRAINT `attend_class_id_fkk` FOREIGN KEY (`attend_class_id`) REFERENCES `attend_class` (`id`),
  CONSTRAINT `card_id_fk` FOREIGN KEY (`card_id`) REFERENCES `card` (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=155 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci COMMENT='会员卡-上课/预约';
```
> ufits,创建card_leave
```sql
CREATE TABLE `card_leave` (
  `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT,
  `card_id` bigint(20) unsigned NOT NULL COMMENT '卡id',
  `state` tinyint(1) unsigned NOT NULL COMMENT '状态，0：待批准，1：已批准，2：未允许',
  `leave_days` int(11) unsigned NOT NULL COMMENT '请假天数',
  `begin_date` date NOT NULL COMMENT '请假开始日期',
  `end_date` date NOT NULL COMMENT '请假结束日期',
  `leave_reason` varchar(512) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '请假理由',
  `enabled` tinyint(3) unsigned NOT NULL DEFAULT '1',
  `modifier` bigint(20) unsigned NOT NULL DEFAULT '0',
  `creator` bigint(20) unsigned NOT NULL DEFAULT '0',
  `modified` datetime NOT NULL,
  `created` datetime NOT NULL,
  PRIMARY KEY (`id`),
  KEY `idx_enabled` (`enabled`) USING BTREE
) ENGINE=InnoDB AUTO_INCREMENT=33 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci COMMENT='请假';
```
> ufits,创建card_order
```sql
CREATE TABLE `card_order` (
  `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT,
  `card_id` bigint(20) unsigned NOT NULL COMMENT '卡标识',
  `user_id` bigint(20) unsigned NOT NULL COMMENT '学生标识（冗余）',
  `package_type` tinyint(1) unsigned NOT NULL DEFAULT '0' COMMENT '套餐类型，0：新买课，1：续课，2，套餐升级',
  `project_title` varchar(255) COLLATE utf8mb4_unicode_ci NOT NULL COMMENT '项目名称',
  `card_number` varchar(20) COLLATE utf8mb4_unicode_ci NOT NULL COMMENT '卡号',
  `money` decimal(10,2) NOT NULL COMMENT '金额',
  `class_time` decimal(10,2) NOT NULL COMMENT '购课数',
  `pay_method` tinyint(1) unsigned NOT NULL DEFAULT '5' COMMENT '支付方式，0：大众点评，1：支付宝，2：微信，3：现金，4：刷卡，5：其他',
  `effective_date` date NOT NULL COMMENT '有效日期',
  `salesperson` bigint(20) unsigned NOT NULL COMMENT '销售教练',
  `remarks` varchar(512) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '备注',
  `enabled` tinyint(1) unsigned NOT NULL DEFAULT '1',
  `modifier` bigint(20) unsigned NOT NULL DEFAULT '0',
  `creator` bigint(20) unsigned NOT NULL DEFAULT '0',
  `modified` datetime NOT NULL,
  `created` datetime NOT NULL COMMENT '购课日期',
  PRIMARY KEY (`id`),
  KEY `user_id_index` (`user_id`) USING BTREE,
  KEY `idx_card_id` (`card_id`) USING BTREE,
  KEY `idx_package_type` (`package_type`) USING BTREE,
  KEY `idx_enabled` (`enabled`) USING BTREE,
  CONSTRAINT `card_id` FOREIGN KEY (`card_id`) REFERENCES `card` (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=38 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci COMMENT='订单';
```
> ufits,创建coach_attend_class
```sql
CREATE TABLE `coach_attend_class` (
  `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT,
  `attend_class_id` bigint(20) unsigned NOT NULL COMMENT '上课id',
  `user_id` bigint(20) unsigned NOT NULL COMMENT '教练/用户id',
  `head` tinyint(1) unsigned NOT NULL DEFAULT '1' COMMENT '是否主教练，0：否，1：是',
  `state` tinyint(1) unsigned NOT NULL COMMENT '状态：0：已预约，1：已签到，2：已签退，3：已总结，4：已结束，5：预约失败',
  `enabled` tinyint(1) unsigned NOT NULL DEFAULT '1',
  `modifier` bigint(20) unsigned NOT NULL DEFAULT '0',
  `creator` bigint(20) unsigned NOT NULL DEFAULT '0',
  `modified` datetime NOT NULL,
  `created` datetime NOT NULL,
  PRIMARY KEY (`id`),
  UNIQUE KEY `attend_class_id_userid_unique` (`attend_class_id`,`user_id`) USING BTREE,
  KEY `user_id_fkk` (`user_id`),
  KEY `idx_enabled` (`enabled`) USING BTREE,
  CONSTRAINT `attend_class_id_fk` FOREIGN KEY (`attend_class_id`) REFERENCES `attend_class` (`id`),
  CONSTRAINT `user_id_fkk` FOREIGN KEY (`user_id`) REFERENCES `user` (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=99 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci COMMENT='教师-上课/预约表';
```
> ufits,创建coach_card
```sql
CREATE TABLE `coach_card` (
  `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT,
  `coach_id` bigint(20) unsigned NOT NULL COMMENT '教练/用户id',
  `card_id` bigint(20) unsigned NOT NULL COMMENT '卡id',
  `head` tinyint(1) unsigned NOT NULL COMMENT '是否是主教练，0：否，1：是',
  `student_id` bigint(20) unsigned NOT NULL COMMENT '学生/用户id（冗余，方便查询）',
  `cooperation` tinyint(1) unsigned NOT NULL DEFAULT '0' COMMENT '是否是合作教练，0：否，1：是',
  `enabled` tinyint(1) unsigned NOT NULL DEFAULT '1',
  `modifier` bigint(20) unsigned NOT NULL DEFAULT '0',
  `creator` bigint(20) unsigned NOT NULL DEFAULT '0',
  `modified` datetime NOT NULL,
  `created` datetime NOT NULL,
  PRIMARY KEY (`id`),
  KEY `idx_coachId_cardId` (`coach_id`,`card_id`) USING BTREE,
  KEY `idx_enabled` (`enabled`) USING BTREE
) ENGINE=InnoDB AUTO_INCREMENT=71 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci COMMENT='教练-会员卡';
```
> ufits,创建comment
```sql
CREATE TABLE `comment` (
  `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT,
  `student_attend_class_id` bigint(20) unsigned NOT NULL COMMENT '学生上课id',
  `user_id` bigint(20) unsigned NOT NULL COMMENT '学生/用户id（冗余）',
  `attend_class_id` bigint(20) unsigned NOT NULL COMMENT '上课id（冗余）',
  `content` varchar(512) COLLATE utf8mb4_unicode_ci NOT NULL COMMENT '评论内容',
  `coach_score` tinyint(1) unsigned NOT NULL COMMENT '教练评分',
  `attend_class_score` tinyint(1) unsigned NOT NULL COMMENT '课程评分',
  `service_score` tinyint(1) unsigned NOT NULL COMMENT '服务评分',
  `enabled` tinyint(1) unsigned NOT NULL DEFAULT '1',
  `modifier` bigint(20) unsigned NOT NULL DEFAULT '0',
  `creator` bigint(20) unsigned NOT NULL DEFAULT '0',
  `modified` datetime NOT NULL,
  `created` datetime NOT NULL,
  PRIMARY KEY (`id`),
  KEY `student_attend_class_id_fk` (`student_attend_class_id`),
  KEY `idx_enabled` (`enabled`) USING BTREE,
  CONSTRAINT `student_attend_class_id_fk` FOREIGN KEY (`student_attend_class_id`) REFERENCES `student_attend_class` (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=24 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci COMMENT='评论';
```
> ufits,创建comment_attachment
```sql
CREATE TABLE `comment_attachment` (
  `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT,
  `comment_id` bigint(20) unsigned NOT NULL COMMENT '评论id',
  `attachment_id` bigint(20) unsigned NOT NULL COMMENT '图片id',
  `enabled` tinyint(1) unsigned NOT NULL DEFAULT '1',
  `modified` datetime NOT NULL,
  `created` datetime NOT NULL,
  PRIMARY KEY (`id`),
  UNIQUE KEY `comment_attachment_unique` (`comment_id`,`attachment_id`) USING BTREE,
  KEY `comment_attachment_id_fk` (`attachment_id`),
  KEY `comment_id_fk` (`comment_id`) USING BTREE,
  KEY `idx_enabled` (`enabled`) USING BTREE,
  CONSTRAINT `comment_attachment_id_fk` FOREIGN KEY (`attachment_id`) REFERENCES `attachment` (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=20 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci COMMENT='评论图片';
```
> ufits,创建course
```sql
CREATE TABLE `course` (
  `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT,
  `level_id` bigint(20) unsigned NOT NULL COMMENT '级别标识，外键',
  `course_title` varchar(255) COLLATE utf8mb4_unicode_ci NOT NULL COMMENT '课程名称',
  `thumbnail` varchar(100) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '缩略图',
  `description` varchar(512) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '课程描述',
  `content` text COLLATE utf8mb4_unicode_ci COMMENT '课程内容',
  `recommend` tinyint(1) unsigned NOT NULL DEFAULT '0' COMMENT '是否推荐',
  `enabled` tinyint(1) unsigned NOT NULL DEFAULT '1',
  `modifier` bigint(20) unsigned NOT NULL DEFAULT '0',
  `creator` bigint(20) unsigned NOT NULL DEFAULT '0',
  `modified` datetime NOT NULL,
  `created` datetime NOT NULL,
  PRIMARY KEY (`id`),
  KEY `level_id_fk` (`level_id`),
  KEY `idx_enabled` (`enabled`) USING BTREE,
  CONSTRAINT `level_id_fk` FOREIGN KEY (`level_id`) REFERENCES `course_level` (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=21 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci COMMENT='课程';
```
> ufits,创建course_attachment
```sql
CREATE TABLE `course_attachment` (
  `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT,
  `course_id` bigint(20) unsigned NOT NULL COMMENT '课程id',
  `attachment_id` bigint(20) unsigned NOT NULL COMMENT '图片id',
  `enabled` tinyint(1) unsigned NOT NULL DEFAULT '1',
  `modified` datetime NOT NULL,
  `created` datetime NOT NULL,
  PRIMARY KEY (`id`),
  UNIQUE KEY `course_attachment_unique` (`course_id`,`attachment_id`) USING BTREE,
  KEY `course_attachment_id_fk` (`attachment_id`),
  KEY `course_id_fk` (`course_id`) USING BTREE,
  KEY `idx_enabled` (`enabled`) USING BTREE,
  CONSTRAINT `course_attachment_id_fk` FOREIGN KEY (`attachment_id`) REFERENCES `attachment` (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=42 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci COMMENT='课程图片';
```
> ufits,创建course_level
```sql
CREATE TABLE `course_level` (
  `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT,
  `level_title` varchar(255) COLLATE utf8mb4_unicode_ci NOT NULL COMMENT '级别名称',
  `description` varchar(512) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '级别描述',
  `time_coefficient` decimal(10,2) NOT NULL DEFAULT '1.00' COMMENT '时长系数',
  `enabled` tinyint(1) unsigned NOT NULL DEFAULT '1',
  `modifier` bigint(20) unsigned NOT NULL DEFAULT '0',
  `creator` bigint(20) unsigned NOT NULL DEFAULT '0',
  `modified` datetime NOT NULL,
  `created` datetime NOT NULL,
  PRIMARY KEY (`id`),
  KEY `idx_enabled` (`enabled`) USING BTREE
) ENGINE=InnoDB AUTO_INCREMENT=20 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci COMMENT='课程级别';
```
> ufits,创建evaluation
```sql
CREATE TABLE `evaluation` (
  `id` bigint(20) unsigned NOT NULL COMMENT '主键，同预约/上课主键相同',
  `state` tinyint(1) unsigned NOT NULL DEFAULT '0' COMMENT '状态，0：草稿，1：提交',
  `user_id` bigint(20) unsigned NOT NULL COMMENT '学生/用户标识',
  `real_name` varchar(255) COLLATE utf8mb4_unicode_ci NOT NULL COMMENT '姓名',
  `age` int(11) unsigned NOT NULL DEFAULT '18' COMMENT '年龄',
  `gestation_num` int(10) unsigned DEFAULT NULL COMMENT '妊娠次数',
  `childbirth` date DEFAULT NULL COMMENT '分娩日期',
  `baby_birth_weight` varchar(10) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '宝宝出生体重',
  `gestation_ex` varchar(512) COLLATE utf8mb4_unicode_ci DEFAULT '0' COMMENT '妊娠特殊情况',
  `childbirth_mode` tinyint(1) unsigned DEFAULT NULL COMMENT '分娩方式，0：顺产，1：剖腹产',
  `spontaneous_labor_ex` varchar(50) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '顺产异常，0：无撕裂无侧切，1：有侧切，2：撕裂Ⅰ度，3：撕裂Ⅱ度，4：撕裂Ⅲ度，5：撕裂Ⅳ度；可多选，逗号隔开',
  `caesarean_ex` varchar(50) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '剖腹产异常，0：疤痕红肿、筋膜远端触痛，1：疤痕增生，2：陈旧疤痕；可多选，逗号隔开',
  `sleep_condition` tinyint(1) unsigned DEFAULT NULL COMMENT '睡眠情况，0：充足，1：一般，2：欠缺',
  `sleep_lack_reason` tinyint(1) unsigned DEFAULT NULL COMMENT '睡眠欠缺原因，0：入睡难，1：易惊醒，2：照顾宝宝',
  `sleep_time` varchar(10) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '睡眠时长',
  `mentality` tinyint(1) unsigned DEFAULT NULL COMMENT '精神状态，0：好，1：一般，2：不佳',
  `appetite` tinyint(1) unsigned DEFAULT NULL COMMENT '食欲，0：好，1：一般，2：不佳',
  `posture` varchar(50) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '体态评估，0：正常，1：上交叉综合证，2：下交叉综合证，3：膝外翻、X型腿，4：膝内翻、O型腿，5：扁平足，6：高弓足；可多选，逗号隔开',
  `neck` tinyint(1) unsigned DEFAULT NULL COMMENT '颈部评估，0：无不适，1：有不适',
  `neck_about` tinyint(1) unsigned DEFAULT NULL COMMENT '颈部不适位置，0：左，1：右',
  `neck_ex` varchar(50) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '颈部不适性质，0：僵硬，1：疼痛，2：酸痛，3：活动受限；可多选，逗号隔开',
  `arm` varchar(50) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '手臂评估，0：无不适，1：酸软，2：无力，3：疼痛，4：麻，5：胸廓出口综合征；可多选，逗号隔开',
  `shoulder` tinyint(1) unsigned DEFAULT NULL COMMENT '肩部评估，0：无不适，1：有不适',
  `shoulder_about` tinyint(1) unsigned DEFAULT NULL COMMENT '肩部不适位置，0：左，1：右',
  `shoulder_ex` varchar(50) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '肩部不适性质，0：僵硬，1：疼痛，2：酸痛，3：活动受限；可多选，逗号隔开',
  `wrist` varchar(50) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '手腕评估，0：无不适，1：腱鞘炎，2：腕管综合征；可多选，逗号隔开',
  `waist` tinyint(1) unsigned DEFAULT NULL COMMENT '腰部评估，0：无不适，1：有不适',
  `waist_about` tinyint(1) unsigned DEFAULT NULL COMMENT '腰不适位置，0：左腰，1：右腰，3：腰椎',
  `waist_ex` varchar(50) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '腰部不适性质，0：僵硬，1：疼痛，2：酸痛，3：活动受限；可多选，逗号隔开',
  `pelvis` tinyint(1) unsigned DEFAULT NULL COMMENT '骨盆评估，0：无不适，1：有不适',
  `pelvis_about` tinyint(1) unsigned DEFAULT NULL COMMENT '骨盆不适位置，0：左，1：右，2：前，3后',
  `pelvis_ex` varchar(50) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '骨盆不适性质，0：僵硬，1：疼痛，2：酸痛，3：下腹明显坠胀感，4：单侧耻骨牵拉感；可多选，逗号隔开',
  `sciatic_nerve` tinyint(1) unsigned DEFAULT NULL COMMENT '坐骨神经症状，0：无，1：有',
  `sciatic_nerve_ex` varchar(50) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '坐骨神经异常，0：伴随腰痛，1：同侧骨盆后侧痛，2：不伴随其他位置痛；可多选，逗号隔开',
  `leg` varchar(50) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '下肢评估，0：水肿，1：膝关节痛，2：足根痛；可多选，逗号隔开',
  `pelvic_floor` varchar(50) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '盆底功能评估，0：压力性尿失禁，1：急迫性尿失禁；可多选，逗号隔开',
  `abdomen_muscle` tinyint(1) unsigned DEFAULT NULL COMMENT '腹直肌，0：阴性，1：阳性',
  `abdomen_muscle_about` tinyint(1) unsigned DEFAULT NULL COMMENT '腹直肌位置，0：脐上，1：脐中，2：脐下',
  `abdomen_muscle_separate_len` varchar(10) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '腹直肌总分离长度',
  `abdomen_muscle_depth` varchar(10) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '腹直肌深度',
  `abdomen_wall` tinyint(1) unsigned DEFAULT NULL COMMENT '腹壁，正常弹性，1：松软无力，2：紧绷疼痛',
  `bust` varchar(10) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '胸围',
  `waistline` varchar(10) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '腰围',
  `abdomenling` varchar(10) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '腹围',
  `hipline` varchar(10) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '臀围',
  `height` varchar(10) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '身高',
  `weight` varchar(10) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '体重',
  `BMI` varchar(10) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT 'BMI指数',
  `others` varchar(1024) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '其他',
  `enabled` tinyint(1) unsigned NOT NULL DEFAULT '1',
  `modifier` bigint(20) unsigned NOT NULL DEFAULT '0',
  `creator` bigint(20) unsigned NOT NULL DEFAULT '0',
  `modified` datetime NOT NULL,
  `created` datetime NOT NULL,
  PRIMARY KEY (`id`),
  KEY `key_user_id` (`user_id`),
  KEY `idx_enabled` (`enabled`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci COMMENT='评估表';
```
> ufits,创建evaluation_attachment
```sql
CREATE TABLE `evaluation_attachment` (
  `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT,
  `evaluation_id` bigint(20) unsigned NOT NULL COMMENT '评估id',
  `attachment_id` bigint(20) unsigned NOT NULL COMMENT '图片id',
  `enabled` tinyint(1) unsigned NOT NULL DEFAULT '1',
  `modified` datetime NOT NULL,
  `created` datetime NOT NULL,
  PRIMARY KEY (`id`),
  KEY `key_evaluation_id` (`evaluation_id`),
  KEY `fk_evaluation_attachment_id` (`attachment_id`),
  KEY `idx_enabled` (`enabled`) USING BTREE,
  CONSTRAINT `fk_evaluation_attachment_id` FOREIGN KEY (`attachment_id`) REFERENCES `attachment` (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=15 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci COMMENT='评估-图片表';
```
> ufits,创建evaluation_course
```sql
CREATE TABLE `evaluation_course` (
  `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT,
  `evaluation_id` bigint(20) unsigned NOT NULL COMMENT '评估标识',
  `course_id` bigint(20) unsigned NOT NULL COMMENT '课程id',
  PRIMARY KEY (`id`),
  UNIQUE KEY `evaluationid_courseid_unique` (`evaluation_id`,`course_id`),
  KEY `fk_course_id` (`course_id`),
  CONSTRAINT `fk_course_id` FOREIGN KEY (`course_id`) REFERENCES `course` (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=42 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci COMMENT='评估-课程表';
```
> ufits,创建knowledge
```sql
CREATE TABLE `knowledge` (
  `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT,
  `knowledge_title` varchar(255) COLLATE utf8mb4_unicode_ci NOT NULL COMMENT '知识库标题',
  `description` varchar(255) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '描述',
  `content` text COLLATE utf8mb4_unicode_ci NOT NULL COMMENT '知识库内容',
  `post_user_name` varchar(255) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '作者',
  `post_date` datetime NOT NULL,
  `recommend` tinyint(1) unsigned NOT NULL DEFAULT '0' COMMENT '是否推荐，0：否，1：是',
  `thumbnail` varchar(100) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '缩略图',
  `enabled` tinyint(1) unsigned NOT NULL DEFAULT '1',
  `modifier` bigint(20) unsigned NOT NULL DEFAULT '0',
  `creator` bigint(20) unsigned NOT NULL DEFAULT '0',
  `modified` datetime NOT NULL,
  `created` datetime NOT NULL,
  PRIMARY KEY (`id`),
  KEY `idx_enabled` (`enabled`) USING BTREE,
  KEY `idx_modified` (`modified`) USING BTREE
) ENGINE=InnoDB AUTO_INCREMENT=12 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci COMMENT='知识库';
```
> ufits,创建knowledge_attachment
```sql
CREATE TABLE `knowledge_attachment` (
  `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT,
  `knowledge_id` bigint(20) unsigned NOT NULL COMMENT '知识库id',
  `attachment_id` bigint(20) unsigned NOT NULL COMMENT '图片id',
  `enabled` tinyint(1) unsigned NOT NULL DEFAULT '1',
  `modified` datetime NOT NULL,
  `created` datetime NOT NULL,
  PRIMARY KEY (`id`),
  UNIQUE KEY `knowledge_attachment_unique` (`knowledge_id`,`attachment_id`) USING BTREE,
  KEY `knowledge_id_fk` (`knowledge_id`),
  KEY `knowledge_attachment_id_fk` (`attachment_id`),
  KEY `idx_enabled` (`enabled`) USING BTREE,
  CONSTRAINT `knowledge_attachment_id_fk` FOREIGN KEY (`attachment_id`) REFERENCES `attachment` (`id`),
  CONSTRAINT `knowledge_id_fk` FOREIGN KEY (`knowledge_id`) REFERENCES `knowledge` (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=18 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci COMMENT='知识库图片';
```
> ufits,创建organization
```sql
CREATE TABLE `organization` (
  `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT,
  `category_id` bigint(20) unsigned NOT NULL COMMENT '分类id',
  `organization_title` varchar(100) COLLATE utf8mb4_unicode_ci NOT NULL COMMENT '机构名称',
  `logo` varchar(100) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '机构LOGO',
  `description` varchar(512) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '描述',
  `region_id` bigint(20) unsigned DEFAULT NULL COMMENT '区域id',
  `address` varchar(512) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '详细地址',
  `enabled` tinyint(1) unsigned NOT NULL DEFAULT '1',
  `modifier` bigint(20) unsigned NOT NULL DEFAULT '0',
  `creator` bigint(20) unsigned NOT NULL DEFAULT '0',
  `modified` datetime NOT NULL,
  `created` datetime NOT NULL,
  PRIMARY KEY (`id`),
  KEY `fk_organization_category_id` (`category_id`),
  KEY `fk_arganization_region_id` (`region_id`),
  KEY `idx_enabled` (`enabled`) USING BTREE,
  CONSTRAINT `fk_arganization_region_id` FOREIGN KEY (`region_id`) REFERENCES `region` (`id`),
  CONSTRAINT `fk_organization_category_id` FOREIGN KEY (`category_id`) REFERENCES `organization_category` (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=8 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci COMMENT='合作机构';
```
> ufits,创建organization_category
```sql
CREATE TABLE `organization_category` (
  `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT,
  `category_title` varchar(100) COLLATE utf8mb4_unicode_ci NOT NULL COMMENT '分类标识',
  `description` varchar(512) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '分类描述',
  `enabled` tinyint(1) unsigned NOT NULL DEFAULT '1',
  `modifier` bigint(20) unsigned NOT NULL DEFAULT '0',
  `creator` bigint(20) unsigned NOT NULL DEFAULT '0',
  `modified` datetime NOT NULL,
  `created` datetime NOT NULL,
  PRIMARY KEY (`id`),
  KEY `idx_enabled` (`enabled`) USING BTREE
) ENGINE=InnoDB AUTO_INCREMENT=15 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci COMMENT='机构分类';
```
> ufits,创建project
```sql
CREATE TABLE `project` (
  `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT,
  `category_id` bigint(20) unsigned NOT NULL COMMENT '项目分类',
  `project_title` varchar(255) COLLATE utf8mb4_unicode_ci NOT NULL COMMENT '项目名称',
  `class_time` decimal(10,2) NOT NULL COMMENT '课时数/购课数',
  `gift_class_time` decimal(10,2) NOT NULL COMMENT '赠送课时/课数',
  `money` decimal(10,2) NOT NULL COMMENT '金额',
  `unit_price` decimal(10,2) DEFAULT NULL COMMENT '单价',
  `effective_days` int(11) unsigned DEFAULT NULL COMMENT '有效时间（单位：天）',
  `leave_restrict` tinyint(3) unsigned DEFAULT NULL COMMENT '请假限制，0：不限制，1：不允许，2：有限制',
  `leave_permit_num` int(11) unsigned NOT NULL COMMENT '请假允许次数',
  `leave_permit_days` int(11) unsigned NOT NULL COMMENT '请假允许天数',
  `leave_min_days` int(11) unsigned NOT NULL COMMENT '一次请假最少天数',
  `enabled` tinyint(1) unsigned NOT NULL DEFAULT '1',
  `modifier` bigint(20) unsigned NOT NULL DEFAULT '0',
  `creator` bigint(20) unsigned NOT NULL DEFAULT '0',
  `modified` datetime NOT NULL,
  `created` datetime NOT NULL,
  PRIMARY KEY (`id`),
  KEY `idx_categoryId` (`category_id`) USING BTREE,
  KEY `idx_enabled` (`enabled`) USING BTREE
) ENGINE=InnoDB AUTO_INCREMENT=27 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci COMMENT='项目';
```
> ufits,创建project_category
```sql
CREATE TABLE `project_category` (
  `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT,
  `category_title` varchar(100) COLLATE utf8mb4_unicode_ci NOT NULL COMMENT '分类名',
  `enabled` tinyint(1) unsigned NOT NULL DEFAULT '1',
  `modifier` bigint(20) unsigned NOT NULL DEFAULT '0',
  `creator` bigint(20) unsigned NOT NULL DEFAULT '0',
  `modified` datetime NOT NULL,
  `created` datetime NOT NULL,
  PRIMARY KEY (`id`),
  KEY `idx_enabled` (`enabled`) USING BTREE
) ENGINE=InnoDB AUTO_INCREMENT=11 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;
```
> ufits,创建region
```sql
CREATE TABLE `region` (
  `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT,
  `parent_id` bigint(20) unsigned NOT NULL DEFAULT '0' COMMENT '父区域标识',
  `region_title` varchar(50) COLLATE utf8mb4_unicode_ci NOT NULL COMMENT '区域名',
  `enabled` tinyint(1) unsigned NOT NULL DEFAULT '1',
  PRIMARY KEY (`id`),
  KEY `idx_regionTitle` (`region_title`) USING BTREE,
  KEY `idx_enabled` (`enabled`) USING BTREE
) ENGINE=InnoDB AUTO_INCREMENT=3279 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci COMMENT='区域表';
```
> ufits,创建role
```sql
CREATE TABLE `role` (
  `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT COMMENT 'ID',
  `role_title` varchar(50) COLLATE utf8mb4_unicode_ci NOT NULL COMMENT '角色名称',
  `description` varchar(255) COLLATE utf8mb4_unicode_ci NOT NULL COMMENT '角色描述',
  `enabled` tinyint(1) NOT NULL DEFAULT '1' COMMENT '是否允许 0:否 1:是',
  `modifier` bigint(20) unsigned NOT NULL DEFAULT '0',
  `creator` bigint(20) unsigned NOT NULL DEFAULT '0',
  `created` datetime NOT NULL COMMENT '创建时间',
  `modified` datetime NOT NULL COMMENT '修改时间',
  PRIMARY KEY (`id`),
  UNIQUE KEY `role_title_unique` (`role_title`),
  KEY `idx_enabled` (`enabled`) USING BTREE
) ENGINE=InnoDB AUTO_INCREMENT=4 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci COMMENT='角色表';
```
> ufits,创建shop
```sql
CREATE TABLE `shop` (
  `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT,
  `shop_title` varchar(255) COLLATE utf8mb4_unicode_ci NOT NULL COMMENT '店名',
  `address` varchar(512) COLLATE utf8mb4_unicode_ci NOT NULL COMMENT '门店地址',
  `longitude` decimal(10,5) DEFAULT NULL COMMENT '经度',
  `latitude` decimal(10,5) DEFAULT NULL COMMENT '纬度',
  `enabled` tinyint(1) unsigned NOT NULL DEFAULT '1',
  `modifier` bigint(20) unsigned NOT NULL DEFAULT '0',
  `creator` bigint(20) unsigned NOT NULL DEFAULT '0',
  `modified` datetime NOT NULL,
  `created` datetime NOT NULL,
  PRIMARY KEY (`id`),
  KEY `idx_enabled` (`enabled`) USING BTREE
) ENGINE=InnoDB AUTO_INCREMENT=4 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci COMMENT='门店';
```
> ufits,创建student_attend_class
```sql
CREATE TABLE `student_attend_class` (
  `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT,
  `attend_class_id` bigint(20) unsigned NOT NULL COMMENT '上课id',
  `user_id` bigint(20) unsigned NOT NULL COMMENT '学生/用户id',
  `state` tinyint(1) unsigned NOT NULL DEFAULT '0' COMMENT '状态：0：已预约，1：已签到，2：已评论，3：已完结，4：已取消',
  `enabled` tinyint(1) unsigned NOT NULL DEFAULT '1',
  `modifier` bigint(20) unsigned NOT NULL DEFAULT '0',
  `creator` bigint(20) unsigned NOT NULL DEFAULT '0',
  `modified` datetime NOT NULL,
  `created` datetime NOT NULL,
  PRIMARY KEY (`id`),
  UNIQUE KEY `attendid_userid_unique` (`attend_class_id`,`user_id`) USING BTREE,
  KEY `userid_fkkk` (`user_id`) USING BTREE,
  KEY `idx_enabled` (`enabled`) USING BTREE,
  CONSTRAINT `attend_class_id_fkkk` FOREIGN KEY (`attend_class_id`) REFERENCES `attend_class` (`id`),
  CONSTRAINT `user_id_fkkk` FOREIGN KEY (`user_id`) REFERENCES `user` (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=128 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci COMMENT='学生-上课/预约';
```
> ufits,创建summary
```sql
CREATE TABLE `summary` (
  `id` bigint(20) unsigned NOT NULL COMMENT '主键，同预约上课id',
  `student_num` int(11) unsigned NOT NULL DEFAULT '1' COMMENT '到场上课人数',
  `student_remarks` varchar(512) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '给客户的备注',
  `coach_remarks` varchar(512) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '给教练/销售的备注',
  `attend_class_content` varchar(1024) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '上课内容',
  `has_dtd_fee` tinyint(1) unsigned NOT NULL DEFAULT '0' COMMENT '是否收取上门费，0：否，1：是',
  `key_user` varchar(1024) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '重点用户记录',
  `enabled` tinyint(1) unsigned NOT NULL DEFAULT '1',
  `modifier` bigint(20) unsigned NOT NULL DEFAULT '0',
  `creator` bigint(20) unsigned NOT NULL DEFAULT '0',
  `modified` datetime NOT NULL,
  `created` datetime NOT NULL,
  PRIMARY KEY (`id`),
  KEY `idx_enabled` (`enabled`) USING BTREE,
  CONSTRAINT `summary_class_id_fk` FOREIGN KEY (`id`) REFERENCES `attend_class` (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci COMMENT='小结';
```
> ufits,创建summary_action
```sql
CREATE TABLE `summary_action` (
  `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT,
  `summary_id` bigint(20) unsigned NOT NULL COMMENT '小结id',
  `action_id` bigint(20) unsigned NOT NULL COMMENT '动作标识',
  `groups_count` int(11) unsigned NOT NULL DEFAULT '1' COMMENT '做了几组',
  `group_action_count` int(11) unsigned NOT NULL COMMENT '每组几个',
  `enabled` tinyint(1) NOT NULL DEFAULT '1',
  `modifier` bigint(20) NOT NULL DEFAULT '0',
  `creator` bigint(20) NOT NULL DEFAULT '0',
  `modified` datetime NOT NULL,
  `created` datetime NOT NULL,
  PRIMARY KEY (`id`),
  KEY `summary_id_fk` (`summary_id`),
  KEY `action_id_fk` (`action_id`),
  CONSTRAINT `action_id_fk` FOREIGN KEY (`action_id`) REFERENCES `action` (`id`),
  CONSTRAINT `summary_id_fk` FOREIGN KEY (`summary_id`) REFERENCES `summary` (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=41 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci COMMENT='小结-动作';
```
> ufits,创建summary_attachment
```sql
CREATE TABLE `summary_attachment` (
  `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT,
  `summary_id` bigint(20) unsigned NOT NULL COMMENT '小结id',
  `attachment_id` bigint(20) unsigned NOT NULL,
  `enabled` tinyint(1) unsigned NOT NULL DEFAULT '1',
  `modified` datetime NOT NULL,
  `created` datetime NOT NULL,
  PRIMARY KEY (`id`),
  KEY `comment_summary_id_fk` (`summary_id`),
  KEY `attachment_id_fk` (`attachment_id`),
  KEY `idx_enabled` (`enabled`) USING BTREE,
  CONSTRAINT `attachment_id_fk` FOREIGN KEY (`attachment_id`) REFERENCES `attachment` (`id`),
  CONSTRAINT `comment_summary_id_fk` FOREIGN KEY (`summary_id`) REFERENCES `summary` (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=5 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci COMMENT='小结图片';
```
> ufits,创建task
```sql
CREATE TABLE `task` (
  `id` bigint(20) unsigned NOT NULL COMMENT '主键，同预约/上课id',
  `user_id` bigint(20) unsigned NOT NULL DEFAULT '0' COMMENT '给谁的作业（冗余）',
  `enabled` tinyint(1) unsigned NOT NULL DEFAULT '1',
  `modifier` bigint(20) unsigned NOT NULL DEFAULT '0',
  `creator` bigint(20) unsigned NOT NULL DEFAULT '0',
  `modified` datetime NOT NULL,
  `created` datetime NOT NULL,
  PRIMARY KEY (`id`),
  KEY `key_user_id` (`user_id`),
  KEY `idx_enabled` (`enabled`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci COMMENT='作业';
```
> ufits,创建task_action
```sql
CREATE TABLE `task_action` (
  `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT,
  `task_id` bigint(20) unsigned NOT NULL COMMENT '作业id',
  `action_id` bigint(20) unsigned NOT NULL COMMENT '动作id',
  `groups_count` int(11) unsigned NOT NULL DEFAULT '1' COMMENT '做了几组',
  `group_action_count` int(11) unsigned NOT NULL COMMENT '每组几个',
  `enabled` tinyint(1) unsigned NOT NULL DEFAULT '1',
  `modifier` bigint(20) unsigned NOT NULL DEFAULT '0',
  `creator` bigint(20) unsigned NOT NULL DEFAULT '0',
  `modified` datetime NOT NULL,
  `created` datetime NOT NULL,
  PRIMARY KEY (`id`),
  KEY `fk_task_id` (`task_id`) USING BTREE,
  KEY `fk_action_id` (`action_id`) USING BTREE,
  KEY `idx_enabled` (`enabled`) USING BTREE,
  CONSTRAINT `fk_action_id` FOREIGN KEY (`action_id`) REFERENCES `action` (`id`),
  CONSTRAINT `fk_task_id` FOREIGN KEY (`task_id`) REFERENCES `task` (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=37 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci COMMENT='作业-动作表';
```
> ufits,创建user
```sql
CREATE TABLE `user` (
  `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT,
  `wechat_id` varchar(50) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '微信标识',
  `phone_number` varchar(11) COLLATE utf8mb4_unicode_ci NOT NULL COMMENT '注册号码',
  `pwd_log_in` tinyint(1) unsigned NOT NULL DEFAULT '0' COMMENT '允许密码登录，0：否，1：是',
  `password` varchar(100) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '登录密码',
  `identity` tinyint(1) unsigned NOT NULL DEFAULT '0' COMMENT '0：学生，1：教练',
  `is_admin` tinyint(1) unsigned NOT NULL DEFAULT '0' COMMENT '是否是管理员：0：否，1：是',
  `nickname` varchar(255) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '昵称',
  `real_name` varchar(255) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '真实姓名',
  `sex` tinyint(1) unsigned NOT NULL DEFAULT '0' COMMENT '性别：0：女，1：男',
  `birthday` date DEFAULT NULL COMMENT '生日',
  `organization_id` bigint(20) unsigned NOT NULL DEFAULT '0' COMMENT '用户来源合作机构标识',
  `pregnancy_stage` tinyint(1) unsigned NOT NULL DEFAULT '0' COMMENT '孕产阶段，0：未知，1：备孕，2：怀孕，3：产后',
  `pregnancy_date` date DEFAULT NULL COMMENT '孕产日期',
  `region_id` bigint(20) unsigned DEFAULT NULL COMMENT '区域id',
  `address` varchar(512) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '详细住址',
  `avatar` varchar(255) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '头像',
  `wechat_number` varchar(100) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '微信号',
  `job_title` varchar(255) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '职称认证',
  `description` varchar(255) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '教师简单介绍',
  `remarks` varchar(512) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '备注',
  `coach_content` text COLLATE utf8mb4_unicode_ci COMMENT '教师详细介绍',
  `photo` varchar(255) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '照片',
  `entry_date` date DEFAULT NULL COMMENT '入职时间',
  `enabled` tinyint(1) unsigned NOT NULL DEFAULT '1',
  `modifier` bigint(20) unsigned NOT NULL DEFAULT '0',
  `creator` bigint(20) unsigned NOT NULL DEFAULT '0',
  `modified` datetime NOT NULL,
  `created` datetime NOT NULL,
  PRIMARY KEY (`id`),
  UNIQUE KEY `phone_num_key` (`phone_number`),
  UNIQUE KEY `wechat_id_key` (`wechat_id`),
  KEY `fk_user_region_id` (`region_id`),
  KEY `idx_realName` (`real_name`(191)) USING BTREE,
  KEY `idx_enabled` (`enabled`) USING BTREE,
  CONSTRAINT `fk_user_region_id` FOREIGN KEY (`region_id`) REFERENCES `region` (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=50 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci COMMENT='用户';
```
> ufits,创建user_role
```sql
CREATE TABLE `user_role` (
  `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT COMMENT 'ID',
  `user_id` bigint(20) unsigned NOT NULL COMMENT 'FK 用户ID',
  `role_id` bigint(20) unsigned NOT NULL COMMENT 'FK 角色ID',
  `enabled` tinyint(1) unsigned NOT NULL DEFAULT '1',
  `modifier` bigint(20) unsigned NOT NULL DEFAULT '0',
  `creator` bigint(20) unsigned NOT NULL DEFAULT '0',
  `modified` datetime NOT NULL,
  `created` datetime NOT NULL,
  PRIMARY KEY (`id`),
  UNIQUE KEY `user_id_role_id_unique` (`user_id`,`role_id`),
  KEY `user_role_roleid_fk` (`role_id`),
  KEY `idx_enabled` (`enabled`) USING BTREE,
  CONSTRAINT `user_role_roleid_fk` FOREIGN KEY (`role_id`) REFERENCES `role` (`id`),
  CONSTRAINT `user_role_userid_fk` FOREIGN KEY (`user_id`) REFERENCES `user` (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=53 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci COMMENT='用户与角色关联表';
```
