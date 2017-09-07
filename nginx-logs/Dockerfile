# 生成nginx的日志存储容器

FROM nginx:latest

MAINTAINER 0z0ne lgt_livezone@live.com

 

# 每条run指令在当前基础镜像执行，并且提交新镜像
RUN ["rm", "/var/log/nginx/access.log"]
RUN ["rm", "/var/log/nginx/error.log"]

VOLUME /var/log/nginx

# 需要暴露出去的端口，如：EXPOSE 22 80 443
EXPOSE 80
