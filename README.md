#### Docker + Alpine + Aria2 + Aria2 WebUI

#### default ENV

* `WEBUI_PORT` `6801`
* `RPC_LISTEN_PORT` `6800`
* `BT_LISTEN_PORT` `51413`
* `DHT_LISTEN_PORT` `51415`

#### build

```
$ docker build -t="leafney/alpine-aria2-webui" .
```

#### run aria2 docker

```
$ docker run --name aria2ui --restart always -p 6800:6800 -p 6801:6801 -p 51413:51413 -p 51415:51415 -d -v /boxvalume/aria2pan:/aria2down leafney/alpine-aria2-webui
```

You can customize the parameters with `-e` whitch you set in the `aria2.conf` . 

eg : `$ docker run ... -e "BT_LISTEN_PORT=5000" ...` and the aria2.conf must set : `... listen-port=5000 ...` 

#### run aria2 docker with nginx

```
$ docker run --name aria2ui -p 127.0.0.1:6801:6801 -p 6800:6800 -p 51413:51413 -p 51415:51415 -d -v /boxvalume/aria2pan:/aria2down leafney/alpine-aria2-webui
```

nginx config 

```
server {
        server_name yourdoman.com;
        listen 80;

        location / {
                proxy_pass http://127.0.0.1:6801/;
        }
}
```

#### setting webui-aria2

open browser of `DOCKER_HOST:6801` , `Settings` -- `Connection Settings` , Enter the `host` , `port(default 6800)` and `secret token` .

#### aria2.conf Necessary Parameters

```
## 配置信息参考自 http://aria2c.com/usage.html ##

# These settings are the same as those at docker run
dir=/aria2down
rpc-listen-port=6800
listen-port=51413
dht-listen-port=51415
rpc-secret=leafney

continue=true

input-file=/etc/aria2/aria2.session
save-session=/etc/aria2/aria2.session
save-session-interval=60
max-concurrent-downloads=3

enable-rpc=true
rpc-allow-origin-all=true
rpc-listen-all=true

bt-enable-lpd=true
follow-torrent=true
enable-dht=true
bt-enable-lpd=true
enable-peer-exchange=true
peer-id-prefix=-TR2770-
user-agent=Transmission/2.77
bt-seed-unverified=true
bt-save-metadata=true
```
