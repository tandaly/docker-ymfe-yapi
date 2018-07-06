
## 官网

https://yapi.ymfe.org

## docker镜像下载

https://dev.aliyun.com/list.html?namePrefix=tandaly/yapi

## docker-compose.yml
```yml
version: "2"
services:
  mongo:
    image: mongo:3
    container_name: mongo
    privileged: true
    restart: always
    networks:
      - yapi
    environment:
      - MONGO_INITDB_ROOT_USERNAME=yapi
      - MONGO_INITDB_ROOT_PASSWORD=yapi
      - MONGO_INITDB_DATABASE=yapi
    volumes:
      - ./mongo-data:/data/db
  yapi:
    image: registry.cn-hangzhou.aliyuncs.com/tandaly/yapi
    container_name: yapi
    privileged: true
    restart: always
    depends_on:
      - mongo
    ports:
      - "8000:3000"
    networks:
      - yapi
    volumes:
      - ./config.json:/app/config.json
      - ./yapi-runtime:/app/runtime
networks:
  yapi:
```

## config.json

```yml
{
  "port": "3000",
  "adminAccount": "admin@yapi.com",
  "db": {
    "servername": "mongo",
    "DATABASE": "yapi",
    "port": 27017,
    "user": "yapi",
    "pass": "yapi",
    "authSource": "admin"
  }
}
```

## 操作

### 启动

```shell
docker-compose up -d
```

### 停止

```shell
docker-compose down
```

### 登录信息

访问地址：http://主机IP:8000

用户名：admin@yapi.com

密码： ymfe.org
