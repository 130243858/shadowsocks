# CentOS-7 with shadowsocks supervisord launcher | Docker

#### - bootstrap.sh script

The container has an **ENTRYPOINT** set to `/config/bootstrap.sh`. It iterates through all `/config/init/*.sh` scripts and runs them, then launches supervisord. See [bootstrap.sh](container-files/config/bootstrap.sh) for details.


#### - supervisord

Supervisord is installed and loads services to run from `/etc/supervisor.d/` directory. Add your own files there to launch your services. For example in your `Dockerfile` you could put:
```ADD my-supervisord-service.conf /etc/supervisord.d/my-supervisord-service.conf```


#### - /data volume

The `/data` directory is meant to be used to simply and easily deploy web applications using a volume binding on `/data`, presumably using [data only containers](https://docs.docker.com/userguide/dockervolumes/) pattern.

Recommended structure:
```
/data/run/ # pid, sockets
/data/conf/ # extra configs for your services
/data/logs/ # logs
/data/www/ # your web application data
```

##### - shadowsock

```
COPY shadowsocks/shadowsocks.json /data/www/
```
