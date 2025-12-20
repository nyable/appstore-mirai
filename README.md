# Custom 1Panel App Store

自用自定义 1Panel 应用商店

[官方文档](https://github.com/1Panel-dev/appstore?tab=readme-ov-file)

## 添加本地应用

```shell
TMP_DIR="/tmp/appstore_tmp"
TARGET_DIR="/opt/1panel/resource/apps/local"
sudo rm -rf "$TMP_DIR"
sudo git clone --depth 1 https://github.com/nyable/appstore-mirai.git "$TMP_DIR"
sudo cp -r "$TMP_DIR/apps/." "$TARGET_DIR/"
# 清理临时文件
sudo rm -rf "$TMP_DIR"
```

## 应用规划

应用本身相关的镜像尽量用 latest，只维护这个版本的配置。如果有跨版本不兼容又需要部署的情况，单独建个最新旧版本的固定版本号目录维护即可。
应用依赖的数据库等通用服务固定一个常用的版本，就不用重复下载不同版本的镜像了。
依赖的 Redis 不沿用现有的服务，单独在各自的 docker compose 中直接使用。
MySQL 等数据库看情况。

## 自动获取固定版本镜像的新版本

[renovate.json](renovate.json)中配置`matchPackagePatterns`，加入需要匹配的镜像名称。

执行 GitHub Actions 中的 renovate.yml，如果有更新会自动 PR 并且触发 renovate-app-version.yml。

[renovatebot 配置文档](https://docs.renovatebot.com/configuration-options/#matchpackagenames)

## 固定格式

```yml
services:
  homarr:
    container_name: ${CONTAINER_NAME}
    image: IMAGE_NAME
    # volumes:
    #   - ./data:/data
    # environment:
    #   - KEY=${VALUE}
    ports:
      - ${PANEL_APP_PORT_HTTP}:8080
    restart: unless-stopped
    networks:
      - 1panel-network
    labels:
      createdBy: "Apps"
networks:
  1panel-network:
    external: true
```
