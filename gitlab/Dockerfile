# 生成gitlab的运行容器

FROM gitlab/gitlab-ce:latest

MAINTAINER 0z0ne lgt_livezone@live.com

LABEL description="Image for nginx exec"

VOLUME /etc/gitlab
VOLUME /var/log/gitlab
VOLUME /var/opt/gitlab

# 需要暴露出去的端口，如：EXPOSE 22 80 443
EXPOSE 80

# 每个容器只能执行一条CMD命令，多个CMD命令时，只最后一条被执行
# CMD ["executable", "Param1", "param2"]
