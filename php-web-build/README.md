## 目录结构说明
├── docker-compose.yml          容器启动配置文件
├── dockerfiles                 构建配置文件目录
├── conf                        配置目录
│   ├── mysql                   MySQL配置文件目录
│   │   └── my.cnf              MySQL配置文件
│   ├── nginx                   Nginx配置文件目录
│   │   ├── conf.d              站点配置文件目录
│   │   │   ├── certs           SSL认证文件、密钥和加密文件目录
│   │   │   │   └── site2       站点2的认证文件目录
│   │   │   ├── site1.conf      站点1 Nginx配置文件
│   │   │   └── site2.conf      站点2 Nginx配置文件
│   │   └── nginx.conf          Nginx通用配置文件
│   └── php                     PHP配置目录
│       ├── php-fpm.d           PHP-FPM配置目录
│       │   └── www.conf        PHP-FPM配置文件
│       └── php.ini             PHP配置文件
├── logs                        日志目录
│   ├── mysql                   MySQL日志目录
│   ├── nginx                   Nginx日志目录
│   └── php-fpm                 PHP-FPM日志目录
├── data                        数据文件相关(Mysql数据文件、Redis数据文件)
└── wwwroot                     站点根目录


## 私有仓库操作

### 构建文件内容<./dockerfiles/nginx>
```
FROM nginx:1.15

# set timezome
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
```

### 生成镜像文件
`docker build -t nginx-1.15:zdy -f ./dockerfiles/nginx .`

### 镜像列表
`docker images`

### 镜像标记
`docker tag nginx-1.15:zdy 127.0.0.1:5000/nginx-1.15:zdy`

### 镜像上传到私有仓库
`docker push 127.0.0.1:5000/nginx-1.15:zdy`

### 查看上传到私有仓库的镜像文件
`curl 127.0.0.1:5000/v2/_catalog`

### 删除本地镜像
`docker rmi 127.0.0.1:5000/nginx-1.15:zdy`

### 从远端私有仓库拉取镜像文件到本地
`docker pull 127.0.0.1:5000/nginx-1.15:zdy`
