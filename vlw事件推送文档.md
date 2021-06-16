## 事件消息推送格式
```json
{
    "event":"事件类型",
    "data":"事件相关数据" 
}
```
#### header传送的信息包括
- Authorization 通信鉴权密钥
- Name 插件名称
- Ver 插件版本
- Udid 设备标识


#### 事件类型包括
- Enable   插件启用时，运行一次这里（启动完成后也会调用一次这里，便于初始化，其他时候，只有用户点击启用插件时才会调用）
- StopUsing 插件被停用，运行一次这里
- Uninstall 插件被卸载，运行一次这里
- Login 新的账号登录成功/下线，运行一次这里
- EventGroupChat 群消息事件（收到群消息时，运行这里）
- EventPrivateChat 私聊消息事件（收到私聊消息时，运行这里）
- EventDeviceCallback 设备回调事件
- EventFrieneVerify 好友请求事件
- EventGroupNameChange 群名称变动事件
- EventGroupMemberAdd 群成员增加事件（新人进群）
- EventGroupMemberDecrease 群成员减少事件（群成员退出）
- EventInvitedInGroup 被邀请入群事件，运行这里（企业微信不传递此事件
- EventQRcodePayment 面对面收款事件（二维码收款时，运行这里）（企业微信不传递此事件）


#### 事件消息推送data 相关数据格式
    Enable，StopUsing，Uninstall 这三个data 为空字符串
###### Login 

```
{
    "login_type":0,  // 0 登录成功 / 1 即将离线
    "Wxid":"", //登录/离线 的Wxid
    "robot_type":0 // 来源微信类型 0 正常微信 / 1 企业微信
}
```
###### EventGroupChat

```
{
    "robot_wxid": "happylittlestone", //机器人Wxid
    "type": 1, //1/文本消息 3/图片消息 34/语音消息  42/名片消息  43/视频 47/动态表情 48/地理位置  49/分享链接  2001/红包  2002/小程序  2003/群邀请 更多请参考sdk模块常量值
    "from_group": "17195401988@chatroom", // 来源群号
    "from_group_name": "测试群2", //来源群名称
    "from_wxid": "wxid_vmdz32uhtcdy22", //具体发消息的群成员id
    "from_name": "老张", //具体发消息的群成员昵称
    "msg": "%E7%BE%A4%E6%B6%88%E6%81%AF", // 消息内容 注意：所有消息都进行了urlencode编码
    "msg_source": "", //可选，附带属性（群消息有艾特人员时，返回被艾特数组）
    "clientid": 0, //企业微信可用
    "robot_type": 0 //来源微信类型 0 正常微信 / 1 企业微信
} 
```

###### EventPrivateChat

```
{
    "robot_wxid": "happylittlestone", //机器人Wxid
    "type": 1, //1/文本消息 3/图片消息 34/语音消息  42/名片消息  43/视频 47/动态表情 48/地理位置  49/分享链接  2001/红包  2002/小程序  2003/群邀请
    "from_wxid": "wxid_vmdz32uhtcdy22", //来源用户ID
    "from_name": "老张", //来源用户昵称
    "msg": "123", //消息内容
    "clientid": 0, //企业微信可用
    "robot_type": 0 //来源微信类型 0 正常微信 / 1 企业微信
}
```
###### EventDeviceCallback

```
{
    "robot_wxid": "happylittlestone", //机器人Wxid
    "type":0, //消息类型
    "msg": "123", //消息内容
    "to_wxid":"", //接收用户ID
    "to_name":"", //接收用户昵称
    "clientid": 0, //企业微信可用
    "robot_type": 0 //来源微信类型 0 正常微信 / 1 企业微信
}
```

###### EventFrieneVerify

```
{
    "robot_wxid": "",  // 机器人账号id
    "type": 1,  // 添加方式 3/微信号,手机搜索添加 12/QQ号 13/通讯录 14/群内添加 17/名片推荐 18/附近 29/摇一摇 30/扫一扫
    "from_wxid": "",  // 请求者wxid
    "from_name": "",  // 请求者昵称
    "v1": "",
    "v2": "",
    "json_msg": "",
    "robot_type": 0 //来源微信类型 0 正常微信 / 1 企业微信
    
}
```
###### EventGroupNameChange
```
{
    "robot_wxid": "",  // 机器人账号id
    "from_group": "",  // 群号
    "new_name": "",  // 新群名
    "old_name": "",  // 旧群名
    "from_name": "",  // 操作者昵称
    "clientid": 0, //企业微信可用
    "robot_type": 0 //来源微信类型 0 正常微信 / 1 企业微信
}
```

###### EventGroupMemberAdd
```
{
    "robot_wxid": "",  // 机器人账号id
    "from_group": "",  // 群号
    "from_group_name": "",  // 群名
    "guest": "",  // 新人（可以调用api分析或自己分析）
    "inviter": "",  // 邀请者（可以调用api分析或自己分析）
    "clientid": 0, //企业微信可用
    "robot_type": 0 //来源微信类型 0 正常微信 / 1 企业微信
}
```

###### EventGroupMemberDecrease

```
{
    "robot_wxid": "",  // 机器人账号id
    "from_group": "",  // 群号
    "from_group_name": "",  // 群名
    "to_wxid": "",  // 被操作者wxid
    "to_name": "",  // 被操作者昵称
    "time": "",  // 操作时间
    "clientid": 0, //企业微信可用
    "robot_type": 0 //来源微信类型 0 正常微信 / 1 企业微信
}
```
###### EventInvitedInGroup

```
{
    "robot_wxid": "",  // 机器人账号id
    "from_wxid": "",  // 邀请机器人入群的id
    "msg": "",  // 内容
    "robot_type": 0 //来源微信类型 0 正常微信 / 1 企业微信
}
```
###### EventQRcodePayment
```
{
    "robot_wxid": "",  // 机器人账号id
    "to_wxid": "",  // 收款者wxid
    "payer_wxid": "",  // 付款者wxid
    "payer_nickname": "",  // 付款者昵称
    "payer_pay_id": "",
    "received_money_index": "",
    "money": "",  // 金额
    "total_money": "",
    "remark": "",  // 备注
    "scene_desc": "",
    "scene": "",  // -1 扫码后退出 / 1 已扫码，未付款 / 2 付款完成 / 3 付款完成后的日志 / 4 付款完成后的日志（商家版），这里重点说明一下，如要做收款播报，只需要判断等于2或者等3的时候就可以了
    "time": ""
}
```