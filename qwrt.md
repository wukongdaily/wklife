## 视频：https://www.bilibili.com/video/BV1tcwTzXEVB 

# Docker 离线包项目和下载 ：

https://github.com/wukongdaily/DockerTarBuilder/releases

# 芝麻开门
```bash
echo 0xDEADBEEF > /etc/config/google_fu_mode
```

# 查询网卡名称
```bash
ip link show
```
# Docker compose部署QWRT

# Arm64的群晖 （比如DS220J）

```bash
services:
  qwrt:
    image: coolsnowwolf/qwrt:arm64-latest
    container_name: qwrt
    privileged: true
    command: /sbin/init
    networks:
      - qwrt_macnet
        
        
networks:
  qwrt_macnet:
    name: qwrt_macnet
    driver: macvlan
    driver_opts:
      parent: eth0 # 这里替换为你设备的网卡名称（比如eth0、end0、enp1s0、enp1s0-ovs等）
    ipam:
      config:
        - subnet: 192.168.66.0/24 # 这里换成你的NAS所在的网段(比如192.168.100.0/24)
          gateway: 192.168.66.1
```


# x86-64的群晖 （比如DS1821+）

```bash
services:
  qwrt:
    image: coolsnowwolf/qwrt:amd64-latest
    container_name: qwrt
    privileged: true
    command: /sbin/init
    networks:
      - qwrt_macnet       
        
networks:
  qwrt_macnet:
    name: qwrt_macnet
    driver: macvlan
    driver_opts:
      parent: eth0 # 这里替换为你设备的网卡名称（比如eth0、end0、enp1s0、enp1s0-ovs等）
    ipam:
      config:
        - subnet: 192.168.66.0/24 # 这里换成你的NAS所在的网段(比如192.168.100.0/24)
          gateway: 192.168.66.1
```

# Armbian-arm64


```bash
services:
  qwrt:
    image: coolsnowwolf/qwrt:arm64-latest
    container_name: qwrt
    privileged: true
    command: /sbin/init
    networks:
      - qwrt_macnet
        
networks:
  qwrt_macnet:
    name: qwrt_macnet
    driver: macvlan
    driver_opts:
      parent: enp0s1 # 这里替换为你设备的网卡名称（比如eth0、end0、enp1s0、enp1s0-ovs等）
    ipam:
      config:
        - subnet: 192.168.66.0/24 # 这里换成你的NAS所在的网段(比如192.168.100.0/24)
          gateway: 192.168.66.1
```


# 旁路由是给谁用的

所谓旁路由 本质是一个网关。这个网关是给除了NAS以外的设备来用的。最好不要给NAS本身用。

原因很简单，是谁生了docker？是宿主机NAS。所以是先有的NAS，后有的docker，为了稳定性 我认为网关 应该给除了NAS以外的其他局域网设备来用。

