## Gitbook

### 使用 Dockerfile 定制镜像

* *Dockerfile* 文件
* *docker-entrypoint.sh* 依赖脚本文件

创建一个文本文件, 命名为 Dockerfile :

```dockerfile
From node:9-alpine

RUN apk add --no-cache tzdata \
    && npm install -g gitbook-cli \
    && rm -rf /root/.npm /tmp/*

ENV TZ=Asia/Shanghai

COPY docker-entrypoint.sh /usr/local/bin/

WORKDIR /root

EXPOSE 4000 35729

ENTRYPOINT ["docker-entrypoint.sh"]

CMD ["gitbook", "serve"]
```

创建 shell 脚本文件, 命名为 docker-entrypoint.sh :

```bash
#!/bin/sh

gitbook init

gitbook install

exec "$@"
```

> *docker-entrypoint.sh 文件需要拥有可执行权限*

### 使用 docker build 构建镜像

```bash
docker build -t gitbook .
```

### 使用 Docker Compose 启动容器

创建文本文件, 命名为 docker-compose.yml :

```yaml
version: "3" 
services:
  gitbook:
    image: gitbook
    tty: true
    ports:
      - 4000:4000
      - 35729:35729
    volumes:
      - ./:/root
    restart: unless-stopped
```

执行 `docker-compose up -d` 启动容器

### 启动多个GitBook

```bash
gitbook serve --lrport 35288 --port 4001
```
