# Домашнее задание к занятию «Система мониторинга Zabbix»

## Задание 1
![Описание изображения](/screen_1.png)
[Cisco Packet Tracer](pkt/hsrp.pkt)

## Задание 2

```
# !/bin/bash

PORT=80
URL="/var/www/html/index.html"

nc -z 127.0.0.1 $PORT
if [ $? -ne 0 ]; then
    exit 1
fi

if [ ! -f "$URL" ]; then
    exit 1
fi

exit 0
```


```
vrrp_instance VI_1 {
    state MASTER
    interface eth0
    virtual_router_id 51
    priority 100
    advert_int 3

    authentication {
        auth_type PASS
        auth_pass 1234
    }

    virtual_ipaddress {
        192.168.1.100
    }

    track_script {
        check_web
    }
}

vrrp_script check_web {
    script "/etc/keepalived/check_web.sh"
    interval 3
    weight -10
}
```

![Описание изображения](/screen_2.png)
![Описание изображения](/screen_3.png)