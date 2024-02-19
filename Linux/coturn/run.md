### Coturn TURN 服务器

```shell
docker-compose -f docker-compose-couchbase.yml -p couchbase up -d
```

TURN 服务器是 VoIP 媒体流量 NAT 遍历服务器和网关。它也可以用作通用网络流量 TURN 服务器和网关。

源码地址：https://github.com/coturn/coturn
