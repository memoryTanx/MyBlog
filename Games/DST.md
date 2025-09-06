# DST

### TREE

```txt
MyDediServer
|   adminlist.txt
|   cluster.ini
|   cluster_token.txt
|
+---Master
|       modoverrides.lua
|       server.ini
|       worldgenoverride.lua
|
\---Caves
        modoverrides.lua
        server.ini
        worldgenoverride.lua
```

### MyDediServer

```ini

[GAMEPLAY]
game_mode = survival
max_players = 6
pvp = false
pause_when_empty = true

[NETWORK]
cluster_description = DST
cluster_name = DST
cluster_password = 
cluster_language = zh
tick_rate = 15

[MISC]
console_enabled = true

[SHARD]
shard_enabled = true
bind_ip = 127.0.0.1
master_ip = 127.0.0.1
master_port = 10889
cluster_key = supersecretkey


```

### Master


```ini
[NETWORK]
server_port = 11000

c_connect("127.0.0.1", 11000)

[SHARD]
is_master = true


[STEAM]
master_server_port = 27018
authentication_port = 8768


[ACCOUNT]
encode_user_path = true

```
### Caves

```ini
[NETWORK]
server_port = 11001


[SHARD]
is_master = false
name = Caves
id = 3534808791


[STEAM]
master_server_port = 27019
authentication_port = 8769


[ACCOUNT]
encode_user_path = true
```

##### D:\steamcmd\steamapps\common\Don't Starve Together Dedicated Server\mods\dedicated_server_mods_setup.lua

```lua
-- 全图定位（完全同步）
ServerModSetup("3138571948")

-- 防卡两招_新
ServerModSetup("3044756151")

-- 史诗血量条 (Epic Healthbar)
ServerModSetup("1185229307")




```
##### modoverrides.lua

```lua
return {
["workshop-3138571948"] = { enabled = true },
["workshop-3044756151"] = { enabled = true },
["workshop-1185229307"] = { enabled = true }
}

```

### 参考：

- https://blog.ttionya.com/article-1235.html
- https://leanote.zzzmh.cn/blog/post/admin/63e46785da7405001301c7f5
- https://forums.kleientertainment.com/forums/forum/83-dont-starve-together-dedicated-server-discussion/

