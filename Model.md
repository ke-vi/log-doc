user 用户表
字段 
	user_id		
	user_name
	user_age
	user_address
	user_tel
	account_name 传说中的logID
	user_email
	user_sign 签名
	user_picture 头像链接
	user_sexy 
	profession_id 职业id
	school_id
	vip_id vip对应的id
	token 荣云token
	authority_time token有效期 现在默认好几年。。暂时忽略
	visit_count 被访问数
	create_time
	modify_time

User 用户表基本值
字段
	user_id
	user_name
	user_tel
	account_name
	user_picture
	user_sexy
	
microblog_comment 朋友圈
字段 
	com_id 朋友圈id
	com_user_id 用户id
	like_count 点赞数
	com_content 发表内容
	com_content_picture 发表的图片 
	address 所在地址
	create_time
	modify_time
	
microblog_friend_comment 朋友圈评论
字段 
	fc_id 主键
	fc_content 评论内容
	user_id 评论人id
	fr_id 朋友圈的com_id
	address
	create_time
	modify_time
	
microblog_like 朋友圈点赞
字段 
	like_id 主键
	user_id 点赞人id
	fr_id 朋友圈的com_id
	create_time
	modify_time

user_vip 会员表
字段 	
	vip_name  会员种类名称
	vip_props  会员道具
	join_group_upper_limit  可加入群上限
	create_group_upper_limit  可创建群上限
	create_time
	modify_time

user_visitor 用户访问表
字段
	landlord_id 受访者user_id
	visitor_id 访问者user_id
	visitor_time 
	modify_time

user_props  用户道具表
字段
	user_id 
	store_id 商城id
	buy_count 数量
	create_time
	modify_time

store  商城表
字段
	store_id 主键
	props_id 道具id
	props_count 购买数量
	props_price 价格
	reserve_price 一口价
	price_start_time 一口价开始时间
	price_end_time 一口价截止时间
	create_time
	
props 道具表
字段
	props_id
	props_name 道具名称
	type_id 类型id 参考props_type表
	description_info 道具描述
	create_time

props_type 道具类型
字段
	type_id
	type_name
	create_time
	
props_event 道具玩法关系表
字段
	pe_id 主键
	props_id 道具id
	event_id 玩法id
	create_time
	modify_time
 