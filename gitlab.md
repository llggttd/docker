#### gitlab
```bash
docker run --detach --hostname gitlab.local.com --publish 443:443 --publish 8888:80 --publish 22:22 --name gitlab --restart always --volume gitlab-config:/etc/gitlab --volume gitlab-logs:/var/log/gitlab --volume gitlab-data:/var/opt/gitlab gitlab/gitlab-ce
```

#### gitlab-runner
```bash
docker run --detach --name gitlab-runner --restart always --link gitlab:gitlab gitlab/gitlab-runner
```

#### gitlab-ci.yml
``` yml
# 定义变量，引用形式$VAR
variables:
  OPTS: ""
  DATE_FORMAT: "+%Y/%m/%d-%H:%M:%S"


# 定义stages, 默认为build->test->deploy
stages:
  - build
  - test
  - deploy
  - production


# 在每个job执行之前执行
before_script:
  - echo before_script

# 在每个job执行之后执行
after_script:
  - echo before_script

compile:
  stage: build
  script:
    - date $DATE_FORMAT
    - echo build

# 合并显示相同命令前缀的job
JUnit 1:
  stage: test
  script:
    - date $DATE_FORMAT
    - echo junit 1

JUnit 2:
  stage: test
  script:
    - date $DATE_FORMAT
    - echo junit 2

JUnit 3:
  stage: test
  script:
    - date $DATE_FORMAT
    - echo junit 3

JUnit 4:
  stage: test
  script:
    - date $DATE_FORMAT
    - echo junit 4

DOC:
  stage: deploy
  script:
    - date $DATE_FORMAT
    - echo deploy

WAR:
  stage: deploy
  script:
    - date $DATE_FORMAT
    - echo war

Backup:
  stage: production
  script:
    - date $DATE_FORMAT
    - echo backup
  when: manual
  dependencies:
    - DOC
    - WAR
```