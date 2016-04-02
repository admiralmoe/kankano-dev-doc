# 服务器端的API

## 客户端与服务器端的通讯

### POST `/api_v1/get/last_update`
用于查询服务器端有无新的数据更新。已经考虑到多帐号的情况。

#### 请求
``` json
{
  "api_key": "API_KEY"
}

```
`api_key`：由服务器分发的鉴权 key。

#### 响应
``` json
{
  "0":
  {
    "player_id": 452156470,
    "last_update": 1458743944006
  }
}
```
不管是否多个帐号，最外层都使用数字进行编号，编号从 0 开始

`player_id`：由娇喘服务器返回的玩家 `api_nickname_id`，用于区分多帐号。

`last_update`：epoch/unix 时间，精确到毫秒。[访问此处](http://currentmillis.com/)了解更多信息。

### POST `/api_v1/get/port`
用于获取港口信息，包括舰队，远征，建造，入渠。
#### 请求
``` json
{
  "api_key": "API_KEY"
}
```
`api_key`：由服务器分发的鉴权 key。
#### 响应
```json
{
  "0":
  {
    "fleets":
    {
      "0":
      {
        "enable": 1,
        "name": "admiralmoe",
        "ships": [0,1,2,3,4,5],
        "mission":
        {
          "id":37,
          "complete_time": 1458743944006
        }
      },
      "1": {},
      "2": {},
      "3": {},
    },
    "ships":{},
    "items":{},
    "constructions":
    {
      "0":
      {
        "enable": 1,
        "ship": 1,
        "complete_time": 1458743944006
      },
      "1":{},
      "2":{},
      "3":{}
    },
    "repairs":{
      "0":
      {
        "enable": 1,
        "ship": 1,
        "complete_time": 1458743944006
      }
    }
  }
}
```
`fleets`：舰队及其编成，远征信息包含在其中。舰队编号从 0 开始，`enable` 为启用标志，启用为1，未启用为 -1。`name` 为舰队命名，`ships` 为舰队下属舰娘列表。目前暂时使用全局船列表编号。提督舰娘列表实装后，切换为提督舰娘列表编号。`mission` 为舰队远征信息，`id` 为远征编号，不在远征状态则数值为 -1。`complete_time` 为完成时间，格式为 epoch/unix，精确到毫秒。

`ships`：提督所有舰娘列表，实装预定。

`items`：提督所有装备列表，实装预定。

`constructions`：提督的建造信息。建造位编号从 0 开始，`enable` 为启用标志，启用为1，未启用为 -1。`ship` 为出货舰娘在全局船列表中的编号。`complete_time` 为完成时间，格式为 epoch/unix，精确到毫秒。

`repairs`：提督的入渠信息。澡堂编号从 0 开始。`enable` 为启用标志，启用为1，未启用为 -1。`ship` 为洗澡舰娘在全局船列表中的编号。提督舰娘列表实装后，切换为提督舰娘列表编号。`complete_time` 为完成时间，格式为 epoch/unix，精确到毫秒。
