## 构建arm64架构镜像
docker build -f Dockerfile-arm64 -t java/jre:arm64-openjre11 .

## 构建amd64架构镜像
docker build -f Dockerfile-amd64 -t java/jre:amd64-openjre11 .

## 同时构建arm64/amd64架构镜像
docker buildx build --platform linux/amd64,linux/arm64 -t java/jre:open11 . --push


> 上面命令会将镜像构建到本地，如果需要构建到指定镜像库，需要加前缀，如：docker.io/java/jre:{tag}