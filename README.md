# Custom 1Panel App Store

自用自定义 1Panel 应用商店

[官方文档](https://github.com/1Panel-dev/appstore?tab=readme-ov-file)

## 添加本地应用

```shell
TMP_DIR="/tmp/appstore_tmp"
TARGET_DIR="/opt/1panel/resource/apps/local"
sudo git clone --depth 1 https://github.com/nyable/appstore-mirai.git "$TMP_DIR"
sudo cp -r "$TMP_DIR/apps/." "$TARGET_DIR/"
# 清理临时文件
sudo rm -rf "$TMP_DIR"
```


## 自动获取新版本

[renovate.json](renovate.json)中配置`matchPackagePatterns`，加入需要匹配的镜像名称。

执行GitHub Actions中的renovate.yml，如果有更新会自动PR并且触发renovate-app-version.yml。