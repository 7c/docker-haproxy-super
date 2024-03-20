## HAProxy 2.9 Docker with super ports privileges
this version is able to bind ports <1024 and with `--net=host` enabled. In `--net=host` mode `--sysctl net.ipv4.ip_unprivileged_port_start=0` is not allowed. also `-privileged` seems not to work. For now the only solution is to have custom Dockerfile with `cap_net_bind_service` 


```
docker build . -t haproxy29-super

## run it with host enabled and ports binding < 1024 
docker run -it --net=host \
    -v /root/docker/haproxy/etc:/usr/local/etc/haproxy:ro \
    -v /opt/mycerts:/opt/mycerts:ro \
    -v /dev/log:/dev/log \
    haproxy29-super
```
