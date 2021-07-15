## 构建arm64架构镜像
docker build -f Dockerfile-arm64 -t docker.develop.huanweiyun.com/java/jre:arm64-openjre11 .

## 构建amd64架构镜像
docker build -f Dockerfile-amd64 -t docker.develop.huanweiyun.com/java/jre:amd64-openjre11 .