## 配置项

| 变量名                           | 非空 | 描述 |
|:------------------------------| :----: | :---- |
| mj.accounts                   | 是 | 参考 [账号池配置](./config.md#%E8%B4%A6%E5%8F%B7%E6%B1%A0%E9%85%8D%E7%BD%AE%E5%8F%82%E8%80%83)，配置后不需要额外设置mj.discord |
| mj.account-store-type         | 否 | 账号存储方式，默认in_memory(内存\重启后丢失)，可选redis |
| mj.account-choose-rule        | 否 | 账号选择策略：默认 BestWaitIdleRule(最少等待空闲)、RoundRobinRule(轮循) |
| mj.api-secret                 | 否 | 接口密钥，为空不启用鉴权；调用接口时需要加请求头 mj-api-secret |
| mj.username                   | 否 | 后台管理登录的用户名 |
| mj.password                   | 否 | 后台管理登录的密码，默认为接口密钥(两者均未设置默认admin) |
| mj.task-store.type            | 否 | 任务存储方式，默认in_memory(内存\重启后丢失)，可选redis |
| mj.task-store.timeout         | 否 | 任务存储过期时间，过期后删除，默认30天 |
| mj.notify-hook                | 否 | 全局的任务状态变更回调地址 |
| mj.notify-notify-pool-size    | 否 | 通知回调线程池大小，默认10 |
| mj.proxy.host                 | 否 | 代理host，全局代理不生效时设置 |
| mj.proxy.port                 | 否 | 代理port，全局代理不生效时设置 |
| mj.ng-discord.server          | 否 | https://discord.com 反代地址 |
| mj.ng-discord.cdn             | 否 | https://cdn.discordapp.com 反代地址 |
| mj.ng-discord.wss             | 否 | wss://gateway.discord.gg 反代地址 |
| mj.ng-discord.resume-wss      | 否 | wss://gateway-us-east1-b.discord.gg 反代地址 |
| mj.translate-way              | 否 | 中文prompt翻译成英文的方式，可选null(默认)、baidu、gpt、deepl |
| mj.translate-zh-way           | 否 | describe、shorten等结果转中文的方式，可选null(默认)、baidu、gpt、deepl |
| mj.baidu-translate.appid      | 否 | 百度翻译的appid |
| mj.baidu-translate.app-secret | 否 | 百度翻译的app-secret |
| mj.openai.gpt-api-url         | 否 | 自定义gpt的接口地址，默认不需要配置 |
| mj.openai.gpt-api-key         | 否 | gpt的api-key |
| mj.openai.timeout             | 否 | openai调用的超时时间，默认30秒 |
| mj.openai.model               | 否 | openai的模型，默认gpt-3.5-turbo |
| mj.openai.max-tokens          | 否 | 返回结果的最大分词数，默认2048 |
| mj.openai.temperature         | 否 | 相似度(0-2.0)，默认0 |
| mj.deepl-translate.auth-key   | 否 | DEEPL翻译的鉴权密钥 |
| mj.error-desc                 | 否 | 任务错误原因转换，默认使用mj提供的英文描述 |
| spring.redis                  | 否 | 存储方式设置为redis，需配置redis相关属性 |

### 账号池配置参考
```yaml
mj:
  accounts:
    - guild-id: xxx
      channel-id: xxx
      user-token: xxxx
      mj-bot-channel-id: xxxx
      user-agent: xxxx
    - guild-id: xxx
      channel-id: xxx
      user-token: xxxx
      mj-bot-channel-id: xxxx
      user-agent: xxxx
```
账号字段说明

| 名称                | 非空 | 描述                                                                  |
|:------------------| :----: |:--------------------------------------------------------------------|
| guild-id          | 是 | discord服务器ID                                                        |
| channel-id        | 是 | discord频道ID                                                         |
| user-token        | 是 | discord用户Token                                                      |
| mj-bot-channel-id | 否 | Midjourney Bot私信ID                                                  |
| user-agent        | 否 | 调用discord接口、连接wss时的user-agent，建议从浏览器network复制                       |
| enable            | 否 | 是否可用，默认true                                                         |
| remix-auto-submit | 否 | remix自动提交(默认false)，共享账号无法自主控制remix模式时使用，自动提交reroll、variation、pan的弹框 |
| core-size         | 否 | 并发数，默认3                                                             |
| queue-size        | 否 | 等待队列长度，默认10                                                         |
| timeout-minutes   | 否 | 任务超时时间(分钟)，默认5                                                      |
| remark            | 否 | 备注说明                                                                |

### spring.redis配置参考
```yaml
spring:
  redis:
    host: 10.107.xxx.xxx
    port: 6379
    password: xxx
```

### mj.error-desc配置参考
```yaml
mj:
  error-desc:
    - en: "against our community standards"
      zh: "可能包含违规信息"
    - en: "Invalid parameter"
      zh: "无效的参数"
```
