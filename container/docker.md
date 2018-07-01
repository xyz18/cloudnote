## Docker

虚拟机是在操作系统上虚拟一套硬件，然后在其上运行一套完整的操作系统．而操作系统是在内核的基础上挂载了第三方软件，方便用户友好操作．真正和硬件打交道的是内核，它提供了访问硬件设备和进行资源管理等的一些基础模块．

容器是对进程进行了封装，在进程的基础上加了隔离和限制，使得容器独立于宿主，并与其它容器隔离．并且容器直接运行于宿主的内核，没有进行硬件虚拟，因此容器要比传统虚拟机更为轻便．

Docker 在容器的基础上进一步封装，使用的核心技术包括：
* 命名空间（Namespaces）：保证容器独立于宿主，并与其它容器彼此互不影响．这时的容器不仅包括进程，还有内核、文件系统、网络、PID、UID、IPC、内存、硬盘、CPU 等等
* 控制组（Control groups）：对主机资源进行分配，避免多个容器运行时对系统资源的竞争
* Union 文件系统（Union file systems）：多层文件系统分层构建镜像，使得镜像可以被复用，并且镜像之间还可以共享文件系统层，节约存储空间
* 容器格式（Container format）
* 网络：在本地主机和容器内分别创建一个虚拟接口（veth pair），并让它们彼此连通

### Docker 基本概念

#### 镜像

Docker 镜像是一组文件系统，既可以作为其他镜像构建的基础．也可以用于容器的启动．提供了启动容器的所有资源和配置．

#### 容器

容器是镜像启动时的实体，拥有独立的命名空间．

#### Docker Registry

Docker Registry 是集中的存储、分发镜像的服务．一个 Docker Registry 中可以包含多个仓库（Repository）；每个仓库可以包含多个标签（Tag）；每个标签对应一个镜像．例如：Docker Hub


### Docker Compose

Docker Compose 是 Docker 官方编排（Orchestration）项目之一，负责实现对 Docker 容器集群的快速编排.

#### Compose 模板文件
```yaml
version: "3"
services:
  python3:
    container_name: ide
    image: python:alpine
    tty: true
    ports:
      - 80:80
    volumes:
      - ./:/root
    restart: unless-stopped
```
