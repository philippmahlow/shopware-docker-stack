

# 1. Installation:
## 1.1 Build mittwald/shopware-image
```bash
~$ docker build -t mittwald/shopware Docker/Shop_PHP7/
```
## 1.2 Start docker containers
```bash
~$ docker-sync-stack start
```
### Troubleshooting:
#### "Unable to find image 'mittwald/shopware' locally"
Please build the image. see **1.1**

#### "port already in use" on dockerhost
U can change the public port in **~/docker-compose.yml**

```bash
...
mittwald_shopware_nginx_proxy:
  container_name: mittwald_shopware_nginx_proxy
  restart: always
  image: jwilder/nginx-proxy:latest
  ports:
    - 8080:80  # <--- HTTP PORT default(80)
    - 8043:443 # <--- HTTPS PORT default(433)
  volumes:
    - /var/run/docker.sock:/tmp/docker.sock:ro
...
```
## 1.4 Edit /etc/hosts
change the following line in **/etc/hosts**:

```bash
127.0.0.1	localhost
```

to:

```bash
127.0.0.1	localhost www.mittwald-shopware.dev mail.mittwald-shopware.dev db.mittwald-shopware.dev
```


## 2. PHPMyAdmin:
URL: http://db.mittwald-shopware.dev

Username/Password (default): **swuser**/**swpassword**


This is based on work of my friend Sebastian (anoxGH). Thanks dude. 
