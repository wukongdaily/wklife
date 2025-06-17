## 你可以根据视频id搜索
 [![Bilibili](https://img.shields.io/badge/Bilibili-123456?logo=bilibili&logoColor=fff&labelColor=fb7299)](https://www.bilibili.com/video/BV1J4J3zAEDz) [![YouTube](https://img.shields.io/badge/YouTube-123456?logo=youtube&labelColor=ff0000)](https://youtu.be/WhtPERoU7PY)
 
 举例来说 https://www.bilibili.com/video/BV1gCTYzmEnA
 <br>该视频的id=`BV1gCTYzmEnA`
 <br>再比如说 https://youtu.be/TcwQHtVOVXA
 <br>该视频的id=`TcwQHtVOVXA`


==============【快捷会员合租：戳下边】================

[ChatGPT Plus | Netflix | Disney+ | Spotify | HBO |](https://naifei.pro/m/?rid=1p5c6/)

## BV1gCTYzmEnA|TcwQHtVOVXA
该视频主要是讲如何利用群晖NAS 给索尼电视安装xapk格式的流媒体软件。
<br>视频里提到的docker镜像名称:`wukongdaily/box`
- 盒子助手docker版 离线包
[国内下载地址(x86-64)](https://slink.ltd/https://github.com/wukongdaily/DockerTarBuilder/releases/download/DockerTarBuilder-AMD64/wukongdaily_box-amd64.tar.gz)

## 威联通NAS使用盒子助手docker版
```
version: '3.8'

services:
  tvhelper:
    image: wukongdaily/box:latest
    container_name: tvhelper
    restart: unless-stopped
    ports:
      - "10022:22"
      - "10080:80"
    volumes:
      - /share/Public/xapks:/data:ro
    environment:
      - PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/lib/android-sdk/platform-tools
```