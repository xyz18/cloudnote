## FTP + LDAP 实现用户访问

### 使用 Dockerfile 定制镜像

```Dockerfile
FROM ubuntu:xenial

RUN apt-get update \
    && apt-get install -y proftpd-basic proftpd-mod-ldap \
    && apt-get clean

RUN echo "/bin/false" >> /etc/shells

EXPOSE 21
EXPOSE 20
EXPOSE 49152-49252

CMD ["proftpd", "--nodaemon"]
```

### 使用 docker build 构建镜像

```bash
docker build -t ftp .
```

### 使用 docker build 构建镜像

* *modules.conf*
* *ldap.conf*
* *proftpd.conf*
* *docker-compose.yml*

modules.conf 文件中添加:
```conf
LoadModule mod_ldap.c
```

ldap.conf 文件:
```conf
<IfModule mod_ldap.c>

LDAPServer ldap://{IP/域名}/?mail?sub

LDAPAttr uid mail
LDAPBindDN "cn=admin,dc={公司名称},dc=cn" "{密码}"
LDAPUsers ou=R&D,dc={公司名称},dc=cn (mail=%u)

LDAPForceDefaultGID on
LDAPForceDefaultUID on
LDAPDefaultGID 65534
LDAPDefaultUID 500 

LDAPGenerateHomedir on
LDAPGenerateHomedirPrefix /root/data
LDAPForceGeneratedHomedir on
LDAPGenerateHomedirPrefixNoUsername on
CreateHome on

</IfModule>
```

修改 proftpd.conf 文件:
```conf
DefaultRoot         /root/data
RequireValidShell       off
PassivePorts                  49152 49252
MasqueradeAddress       1.2.3.4    # 外网访问ip
AllowStoreRestart       on
AllowRetrieveRestart    on

<Directory /root/data>
  Umask  022 022 
  <Limit READ DIRS>
    AllowAll
  </Limit>
  <Limit WRITE>
    DenyAll
  </Limit>
</Directory>

<Directory /root/data/one>
  Umask  022 022 
  <Limit READ DIRS>
    AllowAll
  </Limit>
  <Limit WRITE>
    AllowUser user-name
  </Limit>
</Directory>
```

docker-compose.yml 文件:
```yaml
version: "3" 
services:
  ftp:
    container_name: ftp
    image: ftp
    tty: true
    ports:
      - "20:20"
      - "21:21"
      - "49152-49252:49152-49252"
    volumes:
      - ./data:/root/data
      - ./modules.conf:/etc/proftpd/modules.conf
      - ./ldap.conf:/etc/proftpd/ldap.conf
      - ./proftpd.conf:/etc/proftpd/proftpd.conf
    #restart: unless-stopped
```

### FTP 访问

```ftp -p ip 21```
