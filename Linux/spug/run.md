### Spug - 轻量级自动化运维平台
Spug 面向中小型企业设计的轻量级无 Agent 的自动化运维平台，整合了主机管理、主机批量执行、主机在线终端、文件在线上传下载、应用发布部署、在线任务计划、配置中心、监控、报警等一系列功能。
官网：https://spug.cc/

```shell
docker-compose -f docker-compose-spug.yml -p spug up -d
```

访问地址：[`ip地址:80`](http://www.zhengqingya.com:80)
以下操作会创建一个用户名为 admin 密码为 spug.cc 的管理员账户，可自行替换管理员账户/密码。
```shell
docker exec spug init_spug admin spug.cc
```
### 部署 Maven 项目
安装 jdk / maven
如果已安装可跳过该步骤，这里以安装 jdk-11 和 maven-3.9.6 为例，这里就只说明使用 Docker 部署的 Spug 的方式进行安装。
```shell
# 自行至 https://download.oracle.com/otn/java/jdk/11.0.22+9/8662aac2120442c2a89b1ee9c67d7069/jdk-11.0.22_linux-x64_bin.tar.gz 下载jdk
# 把已下载的压缩包拷贝进容器
docker cp jdk-11.0.22_linux-x64_bin.tar.gz spug:/
docker exec -it spug bash
tar xf jdk-11.0.22_linux-x64_bin.tar.gz -C /opt

# 安装maven
curl -o apache-maven-3.9.6-bin.tar.gz http://apache.mirrors.pair.com/maven/maven-3/3.9.6/binaries/apache-maven-3.9.6-bin.tar.gz
tar xf apache-maven-3.9.6-bin.tar.gz -C /opt/
echo -e 'export JAVA_HOME=/opt/jdk-11.0.22\nexport PATH=$PATH:$JAVA_HOME/bin:/opt/apache-maven-3.9.6/bin' > /etc/profile.d/java.sh

# [可选]配置阿里云镜像加速下载，在159-164行（<mirrors\>标签内）添加以下内容
vi /opt/apache-maven-3.9.6/conf/settings.xml

    159     <mirror>
    160       <id>aliyunmaven</id>
    161       <mirrorOf>*</mirrorOf>
    162       <name>阿里云公共仓库</name>
    163       <url>https://maven.aliyun.com/repository/public</url>
    164     </mirror>

# 退出并重启容器
exit
docker restart spug
```