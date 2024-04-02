# shopware-docker











## Deploy the varnish container

```
docker run -d \
--name=varnish \
-i \
-t \
--net bridge \
-p [public IP]:80:80 \
--restart=always \
--privileged \
shopware_varnish:latest
```


