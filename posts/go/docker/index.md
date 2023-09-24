# Docker-getting-started

## Get started tutorial

## 啥是docker

- is a runnable instance of an image. You can create, start, stop, move, or delete a container using the DockerAPI or CLI（命令行界面）.
- can be run on local machines, virtual machines or deployed to the cloud.
- is portable (can be run on any OS)
- Containers are isolated from each other and run their own software, binaries, and configurations.

## 1 The example of "Build the app’s container image"

### 1.1 Get app and Create a `Dockerfile`

1.1.1 [Download the App contents](https://github.com/docker/getting-started/tree/master/app)

1.1.2 Create a file named `Dockerfile` in the same folder as the file `package.json` with the following contents.

```dockerfile
# syntax=docker/dockerfile:1
FROM node:12-alpine
RUN apk add --no-cache python2 g++ make
WORKDIR /app
COPY . .
RUN yarn install --production
CMD ["node", "src/index.js"]
```

### 1.2 Build the container image

```CLI
 docker build -t getting-started .
```

- The `-t` flag tags our image. Named image `geting-started`
- The `.` means that Docker should look for the `Dockerfile` in the current directory

### 1.3 Start an app container

```CLI
 docker run -dp 8080:3000 getting-started
```

- `-d` - run the container in detached mode (in the background)
- `-p 8080:3000` - map port 8080 of the host to port 3000 in the container
- `docker/getting-started` - the image to use

### 1.4 use use 吧

Add some items 

If you take a quick look at the Docker Dashboard, you should see your two containers running now (this tutorial and your freshly launched app container).

## 2 Update the application

##### 直接改，删了原来的image，再创建

### Remove a container using the CLI

1. Get the ID of the container by using the `docker ps` command.

   ```
    $ docker ps
   ```

2. Use the `docker stop` command to stop the container.

   ```
    # Swap out <the-container-id> with the ID from docker ps
    $ docker stop <the-container-id>
   ```

3. Once the container has stopped, you can remove it by using the `docker rm` command.

   ```
    $ docker rm <the-container-id>
   ```

> **Note**
>
> You can stop and remove a container in a single command by adding the “force” flag to the `docker rm` command. For example: `docker rm -f <the-container-id>`

## 3 Push the image

```
docker tag getting-started hair2020/getting-started
docker push hair2020/getting-started
```

## 记录下文档的反人类缩写

###### 来自[Sample application | Docker Documentation](https://docs.docker.com/get-started/)

- MVP (minimum viable product 最小可行产品)
- CLI（command-line interface命令行界面）
- hub (是吧)

## 安装问题

- win10 已开启hyper-v所有服务

  打开报错：

  `System.InvalidOperationExceptionshell`

  `Failed to set version to docker-desktop: exit code: -1windows`

  解决：

  [Windows 10 Docker InvalidOperationException Failed to set version to docker-desktop: exit code: -1 - 尚码园 (shangmayuan.com)](https://www.shangmayuan.com/a/67b6aead43c5494d91ee2f8f.html)

  临时方案：cmd/shell下执行：`netsh winsock reset`

  重启docker

  永久方案：在网站消失的时间里，用上了win10企业版，完美运行。
