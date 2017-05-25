# 生成nginx的运行容器

FROM nginx:latest

MAINTAINER 0z0ne lgt_livezone@live.com

LABEL description="Image for nginx exec"

COPY html /usr/share/nginx/html

COPY conf /etc/nginx/conf.d

# 每条run指令在当前基础镜像执行，并且提交新镜像
RUN ["rm", "/var/log/nginx/access.log"]
RUN ["rm", "/var/log/nginx/error.log"]

# 需要暴露出去的端口，如：EXPOSE 22 80 443
EXPOSE 80

# 每个容器只能执行一条CMD命令，多个CMD命令时，只最后一条被执行
# CMD ["executable", "Param1", "param2"]
