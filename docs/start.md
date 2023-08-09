## 部署教程

### Docker

1. 创建/xxx/xxx/config，docker用户需要有读写权限，目录文件如下
   > 注意: /xxx/xxx是 服务器目录示例，需自行修改
   - `app.jar` 项目jar包，https://github.com/litter-coder/midjourney-proxy-plus/releases 下找到最新的jar包，下载并命名为app.jar
   - `application.yml` mj配置项，参考 https://github.com/litter-coder/midjourney-proxy-plus/blob/main/resources/application.yml
   - `banned-words.txt` 非必须，覆盖默认的敏感词文件，参考 https://github.com/litter-coder/midjourney-proxy-plus/blob/main/resources/banned-words.txt

2. 启动容器，映射config目录
    ```shell
    docker run -d --name midjourney-proxy-plus \
     -p 8080:8080 \
     -v /xxx/xxx/config:/home/spring/config \
     novicezk/plus-jdk17:latest
    ```

3. 在API文档页 `http://ip:port/doc` 服务激活 -> 获取机器码，联系作者获取激活码，激活服务
4. 访问 `http://ip:port` 查看管理页面，用户名是admin，密码是设置的接口密钥（未设置默认密码是admin）
5. 后续升级版本，直接替换config目录下的app.jar，重启容器即可，不需要重新激活
    ```shell
    docker restart midjourney-proxy-plus
    ```
