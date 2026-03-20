# 🔗 Docker主页
 
 https://hub.docker.com/r/wukongdaily/openwrt-istoreos/

# 支持2种架构 x86-64 和 arm64 的 iStoreOS的旁路由
- 建议在Linux内核较高（6.x）的系统上使用(比如飞牛、绿联、OMV、Armbian、Debian、Ubuntu等等) 
- 群晖内核版本（4.4）较低 对于macvlan支持和兼容性上不太好 不推荐在群晖部署哈
- ✅ 已测试 飞牛fnOS（x86-64 、arm64） 
- ✅ 已测试 openmediavault（x86-64 、arm64）
- ✅ 已测试 Armbian（x86-64 、arm64）

# 默认密码
root / password

# luci 版本 
24.10.5 iStoreOS 2025123110 
# 上网模式
默认是DHCP模式，在容器内输入quickstart ————> Show Interfaces 来查看具体ip

# docker compose 部署方式 x86-64为例

```bash
services:
  ios:
    image: wukongdaily/openwrt-istoreos:amd64-latest # 根据架构 如果是arm64 标签写arm64-latest
    container_name: istoreos
    privileged: true
    command: /sbin/init
    networks:
      - ios_macnet
        
networks:
  ios_macnet:
    name: ios_macnet
    driver: macvlan
    driver_opts:
      parent: enp2s0-ovs # 这里替换为你设备的网卡名称（比如eth0、end0、enp1s0、enp1s0-ovs等）
    ipam:
      config:
        - subnet: 192.168.66.0/24 # 这里换成你的NAS所在的网段(比如192.168.100.0/24)
          gateway: 192.168.66.1 # 这里换成你的NAS所在的网关（比如192.168.100.1）
```

# docker compose 部署方式 arm64 为例
```bash
services:
  ios:
    image: wukongdaily/openwrt-istoreos:arm64-latest # 根据架构 如果是x86-64 标签写amd64-latest
    container_name: istoreos
    privileged: true
    command: /sbin/init
    networks:
      - ios_macnet
        
networks:
  ios_macnet:
    name: ios_macnet
    driver: macvlan
    driver_opts:
      parent: end0 # 这里替换为你设备的网卡名称（比如eth0、end0、enp1s0、enp1s0-ovs等）
    ipam:
      config:
        - subnet: 192.168.66.0/24 # 这里换成你的NAS所在的网段(比如192.168.100.0/24)
          gateway: 192.168.66.1 # 这里换成你的NAS所在的网关（比如192.168.100.1）

```

# 进容器查看 
```bash
# 假设istoreos是容器名称
sudo docker exec -it istoreos /bin/bash 
```

<img width="50%" height="50%" alt="image" src="https://github.com/wukongdaily/pan/releases/download/img/111.jpg" />


# 镜像出处说明

🔗 项目地址：https://github.com/wukongdaily/istoreos-docker-builder

本镜像基于 iStoreOS（OpenWrt）使用 ImageBuilder 构建。

仅提供 Docker 镜像，构建方法与配置详见 GitHub 项目。

支持完全复现构建。



