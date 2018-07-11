## Nginx

### 实现静态资源服务器

* docker-compose.yml 文件
* default.conf 配置文件

创建文本文件, 命名为 docker-compose.yml :

```yaml
version: "3" 
services:
  python3:
    container_name: nginx
    image: nginx
    tty: true
    ports:
      - 8080:80
    volumes:
      - ./:/root
      - ./default.conf:/etc/nginx/conf.d/default.conf
    environment:
      TZ: Asia/Shanghai
    restart: unless-stopped
```

创建文本文件, 命名为 default.conf :

```conf
server {
    listen 80;
    server_name localhost;
    charset utf-8;

    root /root;
    location / { 
        autoindex on;
        autoindex_exact_size off;
        autoindex_localtime on;
    }
}
```

> *chatset utf-8: 用中文文件名时设置*

> *autoindex on: 启动目录索引*



