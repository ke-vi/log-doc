api/friends/friend  添加或者删除好友   
	参数  int notnull friend_id  需要添加或者删除的好友 如好友已存在则删除
	返回  {"code":600,"result":"add"}添加成功 或者{"code":600,"result":"remove"}添加失败
	
api/friends/addfr 发表朋友圈  
	参数 string notnull com_content  发表的内容
		string null com_content_picture 附加图片 可为空
		string notnull address  所属位置
	返回 {"code":600,"result":57	}  返回com_id  
		
api/friends/deletefr 删除本人朋友圈  
	参数 int notnull com_id  朋友圈id  获取朋友圈时候可获取
	返回	{"code":600,"result":true}
	
api/friends/showfr 分页获取朋友圈 
	参数 int null page_no  默认 1
		int null page_size  默认 20
		int null show_user_id  要显示朋友圈的用户id   如果为空则显示当前用户及所有朋友
		string notnull create_time 截止时间点
	返回 {"code":600,"result":[{
				"com_id":"9",	主键
				"com_user_id":"10002",  发表者user_id
				"like_count":"76",		总点赞数
				"com_content":"坐上了火车去拉萨，啊哈哈哈哈哈",	发表内容
				"com_content_picture":"ad12313,4231231",	 发表图片串  客户端统一下格式 用半角的逗号隔开多个图片链接
				"type_id":"1",	1 普通内容  2 邀请加群或者创建群邀请
				"address":"新疆拉萨",  地址
				"create_time":"2015-11-04 10:33:19",
				"modify_time":null,
				"author":User,		参考user.md文档的说明
				"like":[{	点赞着内容表
					"like_id":"62",	 主键
					"user_id":"10001",  点赞者user_id
					"fr_id":"9",	上面的com_id
					"like_count":"21",	点赞数
					"create_time":null,
					"modify_time":null
				}],
				"comment":[{	前三条评论
					"fc_id":"5",	主键
					"fc_content":"12312312313123",	评论内容
					"user_id":"10001",	评论者user_id
					"fr_id":"9",	上面的com_id
					"address":null,  评论者所在地址
					"create_time":"2015-11-16 12:56:45",
					"modify_time":null,
					"user_name":"卡扎菲"	评论者user_name
				}
			]}]}
		
api/friends/get-frcomment  分页获取某条朋友圈的评论  注意返回是个page对象{totalResult:20,pageNo:2,pageSize:2,data:frconmentlist}
	参数 int null page_no  默认 1
		int null page_size  默认 20
		int notnull com_id  朋友圈的com_id
	返回 {"code":600,"result":{
				"pageNo":1,
				"pageSize":"1",
				"totalResult":5, 总数
				"data":[{	返回的评论  参考showfr的评论
					"fc_id":"5",
					"fc_content":"12312312313123",
					"user_id":"10001",
					"fr_id":"9",
					"address":null,
					"create_time":"2015-11-16 12:56:45",
					"modify_time":null,
					"user_name":"卡扎菲"
				}]}}
		
api/friends/like  无限次点赞！
	参数 int notnull fr_id(朋友圈id)
		int null count 本次点赞次数  默认为1
	返回	{"code":600,"result":"like success"}
	
api/friends/comment 发表评论
	参数 int notnull fr_id 用户朋友圈的com_id
		string notnull fc_content 评论内容
	返回 {"code":600,"result":13} 返回主键
	
api/friends/find-telephone-friends 根据电话号码查询好友
	参数 string null user_tels  多个电话号码用,隔开
	返回 {"code":600,"result":{
				"isfriends":[User,User], 是你的好友的列表
				"nofriends":[User,User], 不是你好友但是是平台用户的列表
				"nouser":["1231231234"]	不是平台用户的电话号码
				}}
				
api/friends/get-friends 获取好友
	参数 int null page_no 默认1
		int null page_size 默认20
		string null user_name 好友的昵称或者logid  用户搜索
	返回 {"code":600,"result":{
			"pageNo":1,	当前页码
			"pageSize":20,	页面大小
			"totalResult":"2", 总条数
			"data":[User,User] 好友列表  
		}}

api/friends/get-fans 获取粉丝
	参数 int null page_no 默认1
		int null page_size 默认20
		string null user_name 粉丝的昵称或者logid  可为空
	返回 {"code":600,"result":{
			"pageNo":1,	当前页码
			"pageSize":20,	页面大小
			"totalResult":"2", 总条数
			"data":[User,User] 好友列表  
		}}

api/friends/get-follows 获取我的关注
	参数 int null page_no 默认1
		int null page_size 默认20
		string null user_name 关注的昵称或者logid 可为空
	返回 {"code":600,"result":{
			"pageNo":1,	当前页码
			"pageSize":20,	页面大小
			"totalResult":"2", 总条数
			"data":[User,User] 好友列表  
		}}
		
api/friends/get-recommend 获取不是我的关注的推荐好友
	参数 num  随机取出的数量  不传默认5个
	返回 {"code":600,"result":[User,User]} 
