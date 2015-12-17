api/props/add-user-props  购买完成后为用户添加道具   //废弃该方法
	参数 store_id 道具所属store_id  获取道具时候会返回

api/props/get-user-props 获取用户道具  
	参数 page_no  默认1 
		page_size 默认20
	返回 {"code":600,"result":[{
				"up_id":"1",			主键
				"user_id":"10001",		所有者id
				"props_id":"1",			道具id
				"quantity":"99",		拥有数量
				"create_time":"2015-11-19 00:00:00",	初次购买时间
				"modify_time":null,		
				"props":{			对应道具
					"props_id":"1",		主键
					"props_name":"插队卡",			道具名		
					"type_id":"1",					道具类型
					"description_info":"立即前进5名队列",描述
					"create_time":"2015-11-20 22:31:54"
					}
			}]}

api/props/get-props 获取商城所有道具 
	参数 int null page_no 默认1
		int null page_size 默认20
	返回 {"code":600,"result":[{
				"store_id":"1",  主键
				"props_id":"1",  道具id
				"props_count":"5",  该商品包含道具数量
				"props_price":"5",	暂时不用  价格
				"reserve_price":"5",	一口价  使用这个价格
				"price_start_time":null,	活动时间 暂时废弃
				"price_end_time":null,
				"create_time":"2015-11-20 00:00:00",
				"props":{	对应道具
					"props_id":"1",
					"props_name":"插队卡",
					"type_id":"1", 类别id 
					"description_info":"立即前进5名队列",
					"create_time":"2015-11-20 22:31:54"
				}}
			}]}