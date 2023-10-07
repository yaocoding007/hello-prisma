## 使用 [Prisma](https://www.prisma.io/docs/getting-started/quickstart) 链接数据库 

### prisma 介绍


```shell
mkdir hello-prisma
cd hello-prisma
npm init -y
pnpm install typescript ts-node @types/node --save-dev
npx tsc --init
pnpm install prisma --save-dev
## 初始化 prisma
npx prisma init --datasource-provider mysql
## 创建数据库和表
npx prisma migrate dev --name init

```

```yml
version: "3.7"
services:
  mysql: ## 定义了一个名为"mysql"的服务
    image: mysql:latest ##  最新版本的MySQL Docker镜像
    container_name: mysql ## 容器的名称
    restart: always ## 确保容器在任何情况下停止后都会重新启动
    ports:
      - 3306:3306 ## 将容器的端口3306映射到主机的端口3306，允许外部应用程序连接到运行在容器内部的MySQL服务器
    env_file:
      - .env ## 指定了一个名为".env"的文件，其中包含要传递给容器的环境变量
    volumes:
      - ./mysql:/var/lib/mysql ## 将主机机器上名为"mysql"的目录挂载到容器内部的"/var/lib/mysql"目录。这样，即使停止或删除容器，MySQL数据也可以持久化。****

```


```
docker-compose -f docker-compose.db.yml up -d
```
1. "docker-compose"是Docker Compose的命令行工具。
2. "-f"选项指定要使用的Docker Compose文件的名称。在这个例子中，文件名为"docker-compose.db.yml"。
3. "up"命令用于创建并启动Docker Compose应用程序。它会读取Docker Compose文件中定义的服务，并创建和启动相应的容器。
4. "-d"选项指定Docker Compose应用程序应该在后台运行。这意味着控制台不会显示容器的输出，而是将其发送到日志文件中。