#### Docker + Alpine + Aria2 + Aria2 WebUI


#### build

```
$ docker build -t="leafney/alpine-aria2-webui" .
```

#### run aria2 docker

```
$ docker run --name aria2ui -p 6800:6800 -p 6801:6801 -d -v /boxvalume/aria2pan:/aria2down leafney/alpine-aria2-webui
```

#### setting webui-aria2

open browser of `DOCKER_HOST:6801` , `Settings` -- `Connection Settings` , Enter the `host` , `port(default 6800)` and `secret token` .
