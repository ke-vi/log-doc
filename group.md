#群组

<h1>创建群</h1>

描述：创建一个新群。

接口：/api/group/addgroup    [post]

参数:

	open_status   int    not null "(0:私有群,1:公共群)"
	group_nick    string not null 
	group_address string not null
	school_name   string not null
	group_picture string not null
	event_id      int    not null


<h2>获取活动列表</h2>

描述：通过活动id来显示群组列表

接口：/api/group/get_group_event_list   [get]

参数:

	pageindex int  "当前页面索引"
	pagesize  int  "当前页面数据大小"
	
<h2>通过活动id来显示群组列表</h2>

接口: api/group/get_groups_by_evenid    [get]

    pageindex int  "当前页面索引"
    pagesize  int  "当前页面大小"
    evenid    int  not null  "每个频道的id"
 
<h2>通过event_id来加入随机某群组(首页)</h2>

接口: /api/group/join_group_by_event_id    [get]

    event_id    int  not null  "每个频道的id"
    is_msg_remind  int not null 0不提醒 或 1提醒
返回示例：

<pre>
	{
    	"code":600,
    	"result":{
            "group_id":"10005",                       //群组id
            "owner_id":"10003",                       //群所有者id
            "open_status":"0",                        //公开状态（私有群或公有群）
            "group_address":"北京宇宙中心 风云五道口",   //群地址
            "group_nick":"啪啪啪",                     //群昵称
            "school_name":null,                       //学校名
            "group_picture":"http://app.lognb._49_31--NbOy.png" //图片地址
            "event_id":"1",                           //活动id
            "gr_id":null,                             //群关系id
            "group_topic":null,                        //群话题
            "create_time":"2015-12-12 11:31:33",      //创建时间
            "modify_time":null,                       //修改时间
            "members":[
            			{"user_id":"10004","user_picture":"ccc.jpg"},
            			{"user_id":"10004","user_picture":"ddd.jpg"}
            		   ]
        }
	}
</pre>	


<h2>获得活动(玩法)</h2>

描述：玩法列表(例如：真心话、赛自拍、女神说、无玩法)，这里所说的玩法，等同于频道首页的频道。

接口：/api/group/get_event   [get]

	

<h2>随机群</h2>

描述：频道主页右上角，的即时开聊。(将在所有频道中随机抽选一组群的信息)

接口：/api/group/random_chat    [get]


<h2>通过群名称或者群号查找群</h2>

接口: /api/group/search_group     [get]

	group_val string  not null "为整数时候根据group_id查找，为非数字的时候根据group_nick进行查找"
	

<h2>返回群成员中随机的uid</h2>

描述: 如果想要根据玩法，来获取群成员中，随机的用户 使用这个接口可以返回随机的uid

接口: /api/group/random_uid    [get]

	group_id  int  not null  "群id"
	

<h2>访客进群</h2>

描述: 访问者进入群 并成为群的游客

接口: /api/group/visit_group  [post]

	group_id    not null  "群组id"
	event_id    not null  "频道id(玩法id)"
	group_name  not null  "频道名称，用于在RongCloud中显示"


<h2>加入群组</h2>

描述: 用户进入群后，申请成为群成员

接口: /api/group/join_group [post]

	group_id	  int not null	"群id"
	is_msg_remind int not null  "是否接受消息(0:不接收，1:接收)"
	group_name    not null      "频道名称，用于在RongCloud中显示"


<h2 id="meb_quit_group">成员退出群</h2>


接口:  /api/group/meb_quit_group [get]

	group_id   int  not null  "群id"
	event_id   int  not null  "频道id(玩法id)"


<h2 id="vor_quit_group">访客退出群</h2>

接口:  /api/group/meb_quit_group [get]

	group_id   int  not null  "群id"
	event_id   int  not null  "频道id(玩法id)"



<h2 id="get_my_group_list">获取我的群列表</h2>

描述: 

接口: /api/group/get_my_group_list [get]

返回示例：

<pre>
	{
    "code":600,
    "result":[
        {
            "group_id":"10005",                       //群组id
            "owner_id":"10003",                       //群所有者id
            "group_nick":"啪啪啪",                     //群昵称
            "group_address":"北京宇宙中心 风云五道口",   //群地址
            "open_status":"0",                        //公开状态（私有群或公有群）
            "user_id":"10002",                        //用户id
            "isowner":"false"                         //是否是群主
        },
        {
            "group_id":"10004",
            "owner_id":"10001",
            "group_nick":"砰此次",
            "group_address":"山东临淄",
            "user_id":"10002",
            "isowner":"false"
        }
    ]
}
</pre>


<h2>消息活动计数(除群主外，成员发送一跳消息就调用此接口)</h2>

描述

接口: /api/group/post-msg  [get]

	group_id   int not null "群组id"



<h2>随机获取真心话</h2>

描述

接口: /api/group/random_question  [get]


返回示例:

<pre>
	{
	    "code":600,
	    "result":[
	        {
	            "eid_id":"45",
	            "event_id":"2",
	            "content":"你身高多少？",
	            "create_time":"2015-11-27 17:30:18",
	            "status":"1"
	        }
	    ]
	}
</pre>



<h2>获取频道成员</h2>

描述

接口: /api/group/get_group_member  [get]


