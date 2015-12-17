所有接口如果返回的是User请参照以下说明	
	User={
			"user_tel":"13055005000",	注册手机号
			"user_picture":"1232313123", 头像地址
			"user_sexy":"1",			性别
			"user_name":"d123123",		用户昵称
			"account_name":"94096226",	logID
			"modify_time":"2015-11-19 13:49:22", 修改时间
			"create_time":"2015-11-19 13:49:22", 创建时间
			"user_id":10016,			
			"token":"nqXShTH965EN5BSv2JxqYFFMzv1Cwpe7e2x59a+o0FgRx+ffb3j941Rmez6aEr6c0vpH2VPKmrrhXFurCdxdxg==",荣云交互所用token
			"authority_time":"2050-12-30 00:00:00" token有效期
		}

api/user/register 注册 
	参数 string notnull user_tel 注册的手机号
		int notnull user_sexy 性别 1男 2女
		string notnull user_name 用户昵称
		string null account_name logID
		string notnull  user_picture 头像图片地址
		string notnull password 密码请MD5加密后传递
	返回 {"code":600,"result":User}
	
api/user/login  登陆  
	参数 string notnull user_tel  用户注册手机号
		string notnull password  密码请MD5加密后传递
	返回 {"code":600,"result":User}


api/user/get-user 获取符合条件的用户  不传任何参数获取当前登录用户
	参数 int null user_id 可选 用户id
		string null search_value 可选  user_name或者account_name
	返回 当search_value为空时返回 {"code":600,"result":User}  
		当search_value不为空时返回 {"code":600,"result":[User,User]}	
		当seach_value不为空时 返回User带有rela字段  rela:self 本用户 follow 我的关注  fans 我的粉丝  friend 我的好友  none 无关系
		
api/user/joinvip 加入vip 
	参数 int notnull vip_id 
	返回 {"code":600,"result":User}


api/user/getvips  获取vip列表
	返回 {"code":600,"result":[{
			"vip_id":"1",		会员id
			"vip_name":"普通会员", 名称
			"vip_ props":"1",	会员道具
			"join_ group_upper_limit":"50", 可加入群上限
			"create_group_upper_limit":"50", 可创建群上限
			"create_time":"2015-10-21 00:00:00",
			"modify_time":"2015-10-21 00:00:00"
			}]
		}

api/user/visit 访问其他用户统计  
	参数 int notnull landlord_id 被访问者user_id
	返回 {"code":600,"result":true}

api/user/visitors 获取最近访问用户 
	参数 int null page_no  默认1 
		int null page_size 默认20
	返回 {"code":600,"result":[{
				"id":"1",				主键
				"landlord_id":"10002",  被访问者id
				"visitor_id":"10016",	访问者id
				"visitor_time":"2015-11-19 14:33:04", 访问时间
				"modify_time":null,   无视。
				"visitor":User		访问者对象
				},
			"online":false			是否在线
		}]}	

api/user/upload-picture上传图片   
	参数 data notnull picture_data form/data格式post上传
	返回 {"code":600,
			"result":"12312312312312321"   图片服务器url
		}
	
api/user/update-user 更新用户资料  
	参数 User notnull user 用户对象 包含需要更新的字段名和字段值
	返回 {"code":600,"result":User}
	
api/user/update-password 重置密码 重置完成后默认登陆   这个功能设计因为安全暂停
	参数 string notnull user_tel 用户手机号
		string notnull validate_code 验证码
		string notnull post_type "android"或者"ios"
		string notnull password md5加密后的密码
	返回 {"code":600,"result":User}
	
api/user/create-lucky-flower 创建鲜花红包  返回鲜花id lf_id
	参数 int notnull total 鲜花总数
		int notnull quantity 发给多少人
		int notnull type 发送类型 0为随机人品模式  1为平均模式
		string null wish 祝福语
	返回 {"code":600,"result":{
					"lf_id":1   红包id
				}}
	
api/user/draws-lucky-flower 抢红包 
	参数 int notnull lf_id 红包id
	返回 {"code":600,"result":{
			"luckyFlower":{  
				"lf_id":"3", 红包id
				"quantity":"5", 			 包的数量
				"total":"50", 				总金额
				"best_wishes":"23123123",  	祝福语
				"expiryd_date":"2015-12-01 23:03:29", 过期时间
				"present_id":"10001",		发送者user_id
				"lf_type":"0",				红包类型 0:随机分配  1:平均分配
				"create_time":"2015-11-30 23:03:29",
				"present_user":User,  发送红包者 User基本字段 参考model.md
				"consigneeList":[{		收红包者
					"id":"3", 		主键
					"user_id":"10002",	抢红包者user_id
					"lf_id":"3",		红包id、
					"total":"1",		抢到金额
					"luckiest":"0",		是否最幸运  暂时无效
					"create_time":"2015-11-30 23:03:38",  时间
					"user_name":"本拉登",		抢夺者user_name
					"user_picture":"http://img2.imgtn.bdimg.com/it/u=740539823,2850729651&fm=21&gp=0.jpg"  头像
					}]
			}}

api/user/get-luckyflower 获取红包详情
	参数 int notnull lf_id 红包id
	返回  {"code":600,"result":{
			"luckyFlower":{  
				"lf_id":"3", 红包id
				"quantity":"5", 			 包的数量
				"total":"50", 				总金额
				"best_wishes":"23123123",  	祝福语
				"expiryd_date":"2015-12-01 23:03:29", 过期时间
				"present_id":"10001",		发送者user_id
				"lf_type":"0",				红包类型 0:随机分配  1:平均分配
				"create_time":"2015-11-30 23:03:29",
				"present_user":User,  发送红包者 User基本字段 参考model.md
				"consigneeList":[{		收红包者
					"id":"3", 		主键
					"user_id":"10002",	抢红包者user_id
					"lf_id":"3",		红包id、
					"total":"1",		抢到金额
					"luckiest":"0",		是否最幸运  暂时无效
					"create_time":"2015-11-30 23:03:38",  时间
					"user_name":"本拉登",		抢夺者user_name
					"user_picture":"http://img2.imgtn.bdimg.com/it/u=740539823,2850729651&fm=21&gp=0.jpg"  头像
					}]
			}}

api/user/get-user-luckyflower 获取所有我发送的红包
	参数 int null page_no 默认1 
		int null page_size 默认20
	返回	{"code":600,"result":[{  参考上个接口的返回  但是要注意这里返回的是红包list  上个接口是单个红包
				"lf_id":"1",
				"quantity":"3",
				"total":"20",
				"best_wishes":"",
				"expiryd_date":"201",
				"present_id":"10002",
				"lf_type":"0",
				"create_time":"2015-11-19 15:24:18",
					"consignee":[{"id":"1","user_id":"10001","lf_id":"1","total":"1","luckiest":"0","create_time":"2015-11-19 15:35:42"}]}]}

api/user/online  更新当前用户在线状态
	无参数
	返回 {"code":600,"result":true}

api/user/get-user-message 接受未读信息  并把所有消息标记为已读
	无参数
	返回 {"code":600,"result":[{
			"msg_id":"23", 消息主键
			"receive_user_id":"10002",  收信人user_id
			"trigger_user_id":"10001",	触发者user_id
			"outer_id":"9",				关联对象主键id 详情往下看msg_type 
			"msg_content":"12312312313123",
			"msg_type":"2",				消息触发类型 1:朋友券评论 2:朋友圈点赞 3:获赠鲜花    根据类型不同返回outer_id不同   比如点赞 返回的是点赞表的like_id   评论返回的是评论的fc_id（参考api/friend/showfr） 
			"msg_picture":null,			消息关联图片
			"about_content":"as123231a" 消息关联内容
			"create_time":"2015-11-16 12:56:45",  消息创建时间
			"if_read":"0",				是否已读   
			"trigger":                  触发者user对象
				{"user_id":"10001","user_name":"卡扎菲","user_age":"55","user_address":null,"user_tel":"13354281000","account_name":"卡扎菲大本营1","password":"ab1d012254dc8b35ec8bb7e8468c3c78","user_email":"kazhafei@163.com","user_sign":null,"user_picture":"2312323123213","home_picture":null,"user_sexy":"2","birthday":null,"profession_id":null,"school_id":null,"vip_id":null,"user_type":"2","token":"1111","authority_time":"2050-12-30 00:00:00","visit_count":"0","create_time":"2015-11-05 17:57:19","modify_time":null}
			}]}
			
api/user/get-userinfo 获取我的群组总数和我的好友总数
	无参数
	返回 {"code":600,"result":{
				"friend_count":2,	我的好友总数
				"group_count":"3"	我的群组总数
			}}
	
<h2>获取我的收益</h2>
描述:
接口: /api/user/my_revenues   [get]
参数:
示例:
	{
		"code":600,
		"result":{
			"flower_msg_amount":null,
			"group_msg_amount":0,
			"microblog_browse_amount":0,
			"microblog_like_amount":0,
			"visit_amount":0
		}
	}

<h2>添加收益计数</h2>
描述:
接口: /api/user/add_revenues_record  [get]
参数:
	type_id   int   必须    "收益计数的id类型 1:玫瑰花收益,2:群主的群消息收益,3:身边事浏览量,4:身边事点赞量,5:首页访问量"
示例:
	{
    	"code":600,
    	"result":{
        	"flower_msg_amount":"3",
        	"group_msg_amount":0.0002,
        	"microblog_browse_amount":0.0015,
        	"microblog_like_amount":0.004,
        	"visit_amount":0.002
    	}
	}

