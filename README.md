[linuxserverurl]: https://linuxserver.io
[forumurl]: https://forum.linuxserver.io
[ircurl]: https://www.linuxserver.io/index.php/irc/
[podcasturl]: https://www.linuxserver.io/index.php/category/podcast/

[![linuxserver.io](https://www.linuxserver.io/wp-content/uploads/2015/06/linuxserver_medium.png)][linuxserverurl]

The [LinuxServer.io][linuxserverurl] team brings you another container release featuring easy user mapping and community support. Find us for support at:
* [forum.linuxserver.io][forumurl]
* [IRC][ircurl] on freenode at `#linuxserver.io`
* [Podcast][podcasturl] covers everything to do with getting the most from your Linux Server plus a focus on all things Docker and containerisation!

# lsioarmhf/daapd
[![](https://images.microbadger.com/badges/image/lsioarmhf/daapd.svg)](https://microbadger.com/images/lsioarmhf/daapd "Get your own image badge on microbadger.com")[![Docker Pulls](https://img.shields.io/docker/pulls/lsioarmhf/daapd.svg)][hub][![Docker Stars](https://img.shields.io/docker/stars/lsioarmhf/daapd.svg)][hub][![Build Status](http://jenkins.linuxserver.io:8080/buildStatus/icon?job=Dockers/LinuxServer.io-armhf/lsioarmhf-daapd)](http://jenkins.linuxserver.io:8080/job/Dockers/job/LinuxServer.io-armhf/job/lsioarmhf-daapd/)
[hub]: https://hub.docker.com/r/lsioarmhf/daapd/

[Forked-Daapd][daapdurl] (iTunes) media server with support for AirPlay devices, Apple Remote (and compatibles), Chromecast, MPD and internet radio.

[![daapd](https://raw.githubusercontent.com/linuxserver/beta-templates/master/lsiodev/img/daapd-git.png)][daapdurl]
[daapdurl]: https://ejurgensen.github.io/forked-daapd/

## Usage

```
docker create \
--name=daapd \
-v <path to data>:/config \
-v <path to music>:/music \
-e PGID=<gid> -e PUID=<uid>  \
--net=host \
lsioarmhf/daapd
```

**Parameters**

* `--net=host` - must be run in host mode
* `-v /config` - Where daapd server stores its config and dbase files.
* `-v /music` - map to your music folder
* `-e PGID` for GroupID - see below for explanation
* `-e PUID` for UserID - see below for explanation

It is based on alpine linux with s6 overlay, for shell access whilst the container is running do `docker exec -it daapd /bin/bash`.

### User / Group Identifiers

Sometimes when using data volumes (`-v` flags) permissions issues can arise between the host OS and the container. We avoid this issue by allowing you to specify the user `PUID` and group `PGID`. Ensure the data volume directory on the host is owned by the same user you specify and it will "just work" ™.

In this instance `PUID=1001` and `PGID=1001`. To find yours use `id user` as below:

```
  $ id <dockeruser>
    uid=1001(dockeruser) gid=1001(dockergroup) groups=1001(dockergroup)
```

## Setting up the application 
`IMPORTANT... THIS IS THE ARMHF VERSION`

Map your music folder, open up itunes on the same LAN to see your music there.
For further setup options of remotes etc, check out the daapd website, [Forked-daapd][daapdurl].

## Logs and shell
* To monitor the logs of the container in realtime `docker logs -f daapd`.
* Shell access whilst the container is running: `docker exec -it daapd /bin/bash`


## Versions
+ **17.09.16:** Initial Release.
