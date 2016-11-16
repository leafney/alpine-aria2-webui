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
$ docker run --name aria2ui -p 6800:6800 -p 6801:6801 -p 51413:51413 -p 51415:51415 -d -v /boxvalume/aria2pan:/aria2down leafney/alpine-aria2-webui
```

#### run aria2 docker with nginx

```
$ docker run --name aria2ui -p 127.0.0.1:6800:6800 -p 127.0.0.1:6801:6801 -p 51413:51413 -p 51415:51415 -d -v /boxvalume/aria2pan:/aria2down leafney/alpine-aria2-webui
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

server {
        server_name yourdoman.com;
        listen yourdoman.com:6800;

        location / {
                proxy_pass http://127.0.0.1:6800/;
        }
}
```

#### setting webui-aria2

open browser of `DOCKER_HOST:6801` , `Settings` -- `Connection Settings` , Enter the `host` , `port(default 6800)` and `secret token` .
