# shopware-docker

## Create customer network
``` docker network create -d bridge dckr-bridge --subnet=119.77.69.0/24 --gateway=119.77.69.254 --attachable ```



## Deploy the varnish container

```
docker run -d \
--name=varnish \
-i \
-t \
--net dckr-bridge \
-p [public IP]:80:80 \
--restart=always \
--privileged \
shopware_varnish:latest
```

## Deploy the redis container

```
docker run -d \
--name=redis \
-i \
-t \
--net dckr-bridge \
-v redis_data:/data \
--restart=always \
--privileged \
shopware_redis:latest
```


## Deploy the shopware container

```
docker run -d \
--name=shopware_app \
-i \
-t \
--net dckr-bridge \
-v app:/var/www/html \
-v app_media:/var/www/html/public/media \
-v app_sitemap:/var/www/html/public/sitemap \
-v app_theme:/var/www/html/public/theme \
-v app_thumbnail:/var/www/html/public/theme \
-v app_bundles:/var/www/html/public/bundles \
-v app_files:/var/www/html/files \
--restart=always \
--privileged \
shopware_redis:latest
```
