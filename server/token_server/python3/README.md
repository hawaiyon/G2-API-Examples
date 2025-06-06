# 生成云信 RTC 鉴权的 token

* 基础 token：https://doc.yunxin.163.com/nertc/server-apis/TcxNDAxMTI?platform=server
* 高级 token：https://doc.yunxin.163.com/nertc/server-apis/DU3Mjk0MzQ?platform=server

## 代码目录

* 本目录下是一个完整的 Python3 项目。`./token_server.py`  文件包含了基础 token、高级 token 的完整代码

## 使用示例

```python
from . import token_server

# 建议项目初始化时候创建对象， 通过单例全局维护一个 TokenServer 对象
# appKey、appSecret 请替换成自己的，具体在云信管理后台查看。
# 7200 代表默认有效的时间，单位秒。不能超过 86400，即 24 小时
my_token_server = token_server.TokenServer(appKey, appSecret, 7200)

# 在需要的时候，提供 channel_name（房间名）、uid（用户标识）、ttlSec（有效时间，单位秒） 参数，生成 token
token = my_token_server.get_token(channel_name, uid, ttl_sec)

# perm_secret 见云信管理后台，具体见文档说明：https://doc.yunxin.163.com/nertc/server-apis/DU3Mjk0MzQ?platform=server
permission_key = my_token_server.get_permission_key(channel_name, perm_secret, uid, privilege, ttl_sec)
```

## 代码引入说明

1. 复制 `./token_server.py` 文件到你的项目中
2. 初始化时候调用 `TokenServer(appKey, appSecret, ttlSec)`，生成 token 时候调用 `get_token` 方法
3. 如果需要生成高级 token，调用 `get_permission_key` 方法

