---
layout: page
title: "Docker Notes"
description: ""
header-img: "img/avatar.jpg"
type: "note"
---

# Docker

The problem solved by **Docker**:

>My program can run on my PC, but failed on others' PC.

Docker packed:

- program
- dependencies
- environments

into a **container**.

For example, assume we have a **python repo**, it contains `app.py`, and its dependency contains `numpy, pandas` ... also the environment is `Python 3.12`.

## prework

1. download Docker Desktop.
2. For windows OS, download **WSL** and **ubuntu** to simulate the linux environment.

>sidenotes:
>
>WSL is a frame in Windows to run Linux.
>
>Ubuntu is a concrete Linux version run in WSL. 

## Docker images and container management

### Basic commands

```bash
docker images
docker ps -a
docker ps
docker start container's ID
docker stop container's ID
docker rm container's ID
docker rmi image's ID
```

You can try all the codes above to see what happened and I will explain all the commands below.

1. `docker image` list all the images in the docker engine now.
2. `docker ps -a` list all the containers in the docker engine now.
3. `docker ps` will only list the containers that are running now.
4. rm = remove.
5. rmi = remove image

### What is image?

An **image** can be understand as a read-only template used to create container. It usually contains:

- OS
- runtime(interpreter)
- dependencies
- scripts
- default startup command

```
Image → docker run → Container
```

### What is container?

A container is created from images, which is the real running environment(instance).

## Dockerfile

A **Dockerfile** is the “recipe” used to build an image:

```text
Dockerfile (recipe)
        |
        | docker build
        ↓
Image (template)
        |
        | docker run
        ↓
Container (running instance)
```

Example of a Dockerfile:
```dockerfile
FROM python:3.12
COPY app.py .
CMD ["python3","app.py"]
```

1. Set `python:3.12` as the base image.
2. copy `app.py` into the working directory.
3. when the container is ran, execute `python3 app.py` by default.

## implement the pipeline

After learning the whole process, let's create a container! Try the commands below!

```bash
mkdir docker_demos
cd docker_demos
nano app.py
```

1. mkdir = make directory
2. nano = create a script named `app.py` and enter the editor.

```python
print("Hello from Docker!")
```

Exit and save the python script. Follow the instruction given by the nano editor.

```bash
nano Dockerfile
```

```dockerfile
FROM python:3.12
COPY app.py .
CMD ["python3", "app.py"]
```

```bash
docker build -t docker-demo .
docker images
```

Here is the summary:

```
Dockerfile → docker build → Image
```

# Not arranged

## volume

```
docker volume create mydata
```

To create a Docker data storage named mydata. Volume is different from container, since it can store data even the container is deleted.

```
docker volume ls
docker run -it -v mydata:/data ubuntu bash
echo "hello" > /data/test.txt
cat /data/test.txt
```

ubuntu is a image format, which can be understand as template now.

```
exit
```

To exit a container.

```
docker ps -a
```

check the existing container.

## bind mount

```
docker run -it -v ~/project:/app ubuntu bash
```

map the folder `~/project` to `/app`. i.e. share the folder `~/project`.

## port mapping

```
docker run -p 8080:80 nginx
```

then when you enter localhost:8080 in browser, you can see the 80 port of the container, now is the nginx.

## docker compose

manage multi container one time!

eg:

```
services:
  web:
    image: nginx
  db:
    image: mysql
```

in wsl:

```
mkdir compose_test
cd compose_test
nano compose.yaml
```

```yaml
services:
  web:
    image: nginx
    ports:
      - "8080:80"
```

```bash
docker compose up
```

then also type `localhost:8080` in the browser.

Next add the second service.

```
services:
  web:
    image: nginx
    ports:
      - "8080:80"

  db:
    image: redis
```

```
docker compose up
```

And open another terminal:

```
docker compose ps
```

then you can see two container `web` and `db`.

## compose stop and clear

前台：```Ctrl + C```

后台启动：
```
docker compose up -d
```

查看:

```
docker compose ps
```

stop and delete:

```
docker compose down
```

## compose + volume

<!-- ## 把 Python 自动机脚本变成真正的软件

### 测试（pytest）

### Dockerfile

### README

1. 项目简介：说清楚这个项目做了什么
2. 输入与输出：如果有必要，可以详细解释相应文件的格式
3. 快速开始：支持的版本（如python）以及使用的命令行命令
4. Docker：如何用docker运行这个项目
5. 运行测试

### 做一次最终验证

```powershell
python -m pytest
docker run --rm -v "${PWD}:/data" observer `
  /data/data/models/Example27_G.json `
  /data/data/agents/Example27_A1.json `
  /data/data/agents/Example27_A2.json `
  /data/output.json
```

### 配置自动测试 CI

每次提交代码后，GitHub会自动运行`pytest`，如果测试失败会发出提示，同时禁止代码进入仓库。

### 版本发布（release）+ 项目展示

先做 Release：

1. 确认测试与 CI 通过  
2. GitHub → **Releases** → **Create new release**  
3. click Tag to 创建标签 `v1.0.0`  
4. Release title `v0.1.0 - Initial Release`  
5. 描述功能、运行方式、限制  
6. 点击 **Publish release**

目的：生成可引用、可下载的稳定版本。发布后再做 README 展示。 -->
