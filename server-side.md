# 服务器端的API

我们的口号是，向娇喘程序员学习！

## POST `/api_v1/get/last_update`
用于查询服务器端有无新的数据更新。已经考虑到多帐号的情况。

### 请求
``` json
{
  "api_key": "API_KEY"
}

```
`api_key`：由服务器分发的鉴权 key。

### 响应
``` json
{
  "0":
  {
    "player_id": "000000000",
    "last_update": "1458743944006"
  }
}
```
不管是否多个帐号，最外层都使用数字进行编号，编号从 0 开始

`player_id`：由娇喘服务器返回的玩家 `api_nickname_id`，用于区分多帐号。

`last_update`：epoch /unix 时间，精确到毫秒。[访问此处](http://currentmillis.com/)了解更多信息。

## POST `/api_v1/get/port`
用于获取港口信息，包括舰队，远征，建造，入渠。
### 请求
``` json
{
  "api_key": "API_KEY"
}
```
`api_key`：由服务器分发的鉴权 key。
### 响应
```json
{
  "0":
  {

  }
}
```
