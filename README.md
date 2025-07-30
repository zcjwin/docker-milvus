# Milvus 向量数据库部署

本项目使用 Docker Compose 部署 Milvus 向量数据库及其相关组件。

## 组件介绍

### 1. etcd
- 用于存储 Milvus 的元数据
- 版本: v3.5.5
- 配置了自动压缩和存储配额

### 2. minio
- 对象存储服务，用于存储 Milvus 的数据文件
- 版本: RELEASE.2023-03-20T20-16-18Z
- 默认访问密钥和密码均为 `minioadmin`
- 提供两个端口访问:
  - 9000: S3 API 端口
  - 9001: Web 控制台端口

### 3. milvus-standalone
- Milvus 单机版服务
- 版本: v2.4.1
- 使用 etcd 存储元数据
- 使用 minio 作为对象存储
- 提供两个端口:
  - 19530: Milvus 主服务端口
  - 9091: 健康检查端口

### 4. attu
- Milvus 的 Web 管理界面
- 版本: v2.3.10
- 可通过浏览器访问管理 Milvus 数据库
- 运行在 8000 端口

## 部署方式

1. 确保已安装 Docker 和 Docker Compose

2. 在 docker-compose.yml 文件所在目录执行以下命令：

   ```bash
   docker compose up -d
   ```

3. 等待所有服务启动完成（可能需要几分钟时间）

## 访问方式

- **Attu 管理界面**: http://localhost:8000
- **Milvus 服务端口**: 19530
- **MinIO 控制台**: http://localhost:9001
  - 用户名: minioadmin
  - 密码: minioadmin

## 数据持久化

所有服务的数据都存储在 `volumes` 目录下：
- etcd 数据: ./volumes/etcd
- minio 数据: ./volumes/minio
- milvus 数据: ./volumes/milvus

## 停止服务

在 docker-compose.yml 文件所在目录执行：

```bash
docker compose down
```

## 注意事项

1. 首次启动可能需要较长时间，请耐心等待
2. 所有数据都会持久化存储，删除容器不会丢失数据
3. 如需重新初始化，请删除 `volumes` 目录后重新启动
4. 生产环境请修改默认的访问密钥和密码







