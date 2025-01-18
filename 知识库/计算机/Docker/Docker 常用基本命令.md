---
tags:
  - Docker
  - Docker命令
---
## 1、Docker 版本与信息

### 1.1 查看 Docker 版本

```bash
docker --version
```

或者：

```bash
docker version
```
### 1.2 查看 Docker 系统信息

```bash
docker info
```

---
## 2. 镜像操作

### 2.1 列出所有本地镜像

```bash
docker images
```
### 2.2 从 Docker Hub 拉取镜像

```bash
docker pull <image_name>:<tag>
```

示例：拉取最新的 Ubuntu 镜像

```bash
docker pull ubuntu:latest
```
### 2.3 删除本地镜像

```bash
docker rmi <image_name_or_id>
```
### 2.4 构建镜像

```bash
docker build -f <dockerfile_location> -t <image_name>:<tag> .
```

示例：从当前目录的 Dockerfile 构建镜像

```bash
docker build -t myapp:latest .
```

---
## 3. 容器操作

### 3.1 创建并运行容器

```bash
docker run -d --name <container_name> <image_name>
```

示例：运行一个 Nginx 容器

```bash
docker run -d --name my-nginx nginx:latest
```

示例：更多参数

```bash
docker run \  
	# 给容器命名
    --name postgresql \  
    # 映射端口： 宿主机端口:容器内端口
    -p 5432:5432 \  
    # 映射目录 宿主机目录:容器内目录 
    -v ~/data/postgresql/data:/var/lib/postgresql/data \ 
    # 环境变量 
    -e POSTGRES_USER=root \  
    -e POSTGRES_PASSWORD=abcd123456 \  
    # 加入网络
    --network stock-manage-service-network \  
    # 自动重启
    --restart=always \  
    # 后台运行 镜像名
    -d postgres:16.3
```
### 3.2 列出所有正在运行的容器

```bash
docker ps
```

### 3.3 列出所有容器（包括停止的容器）

```bash
docker ps -a
```

### 3.4 启动一个已停止的容器

```bash
docker start <container_name_or_id>
```

### 3.5 停止一个运行中的容器

```bash
docker stop <container_name_or_id>
```

### 3.6 进入运行中的容器（使用交互式终端）

```bash
docker exec -it <container_name_or_id> /bin/bash
```

示例：进入一个 Ubuntu 容器

```bash
docker exec -it my-ubuntu /bin/bash
```

### 3.7 查看容器的日志

```bash
docker logs <container_name_or_id>
```

### 3.8 删除容器

```bash
docker rm <container_name_or_id>
```

### 3.9 删除所有已停止的容器

```bash
docker container prune
```

---
## 4. 网络操作

### 4.1 列出所有网络

```bash
docker network ls
```

### 4.2 创建一个网络

```bash
docker network create <network_name>
```

### 4.3 将容器连接到网络

```bash
docker network connect <network_name> <container_name_or_id>
```
### 4.4 将容器从网络中断开

```bash
docker network disconnect <network_name> <container_name_or_id>
```

### 4.5 删除网络

```bash
docker network rm <network_name>
```

---

## 5. 卷操作

### 5.1 列出所有卷

```bash
docker volume ls
```

### 5.2 创建卷

```bash
docker volume create <volume_name>
```

### 5.3 挂载卷到容器

```bash
docker run -d --name <container_name> -v <volume_name>:/path/in/container <image_name>
```

示例：使用卷 `my-volume` 并挂载到容器的 `/data` 目录

```bash
docker run -d --name my-app -v my-volume:/data myapp:latest
```

### 5.4 删除卷

```bash
docker volume rm <volume_name>
```

### 5.5 删除所有未使用的卷

```bash
docker volume prune
```

---
## 6. Docker Compose

### 6.1 启动服务（根据 docker-compose.yml 文件）

```bash
# -p为命名 -d为后台运行
docker-compose -p <my_project_name> up -d
```

### 6.2 停止服务

```bash
docker-compose down
```

### 6.3 查看服务日志

```bash
docker-compose logs
```

### 6.4 查看服务状态

```bash
docker-compose ps
```

---
## 7. 其他常用命令

### 7.1 查看 Docker 系统资源使用情况

```bash
docker stats
```

### 7.2 清理未使用的 Docker 资源（镜像、容器、卷、网络）

```bash
docker system prune
```

### 7.3 查看容器的详细信息

```bash
docker inspect <container_name_or_id>
```

### 7.4、查看容器的IP

```bash
docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' <container_name_or_id>
```
