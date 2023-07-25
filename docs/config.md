## 配置项

| 变量名 | 非空 | 描述 |
| :-----| :----: | :---- |
| mj.accounts | 否 | 参考 [账号池配置](./config.md#%E8%B4%A6%E5%8F%B7%E6%B1%A0%E9%85%8D%E7%BD%AE%E5%8F%82%E8%80%83)，配置后不需要额外设置mj.discord |
| mj.discord.guild-id | 是 | discord服务器ID |
| mj.discord.channel-id | 是 | discord频道ID |
| mj.discord.user-token | 是 | discord用户Token |
| mj.discord.session-id | 否 | discord用户SessionId，建议从interactions请求中复制替换掉 |
| mj.discord.user-agent | 否 | 调用discord接口、连接wss时的user-agent，建议从浏览器network复制 |
| mj.discord.remix | 否 | 是否启用了remix，默认false。与账号的Remix模式开关保持一致 |
| mj.api-secret | 否 | 接口密钥，为空不启用鉴权；调用接口时需要加请求头 mj-api-secret |
| mj.notify-hook | 否 | 全局的任务状态变更回调地址 |
| mj.notify-notify-pool-size | 否 | 通知回调线程池大小，默认10 |
| mj.task-store.type | 否 | 任务存储方式，默认in_memory(内存\重启后丢失)，可选redis |
| mj.task-store.timeout | 否 | 任务过期时间，过期后删除，默认30天 |
| mj.queue.core-size | 否 | 并发数，默认为3 |
| mj.queue.queue-size | 否 | 等待队列，默认长度10 |
| mj.queue.timeout-minutes | 否 | 任务超时时间，默认为5分钟 |
| mj.proxy.host | 否 | 代理host，全局代理不生效时设置 |
| mj.proxy.port | 否 | 代理port，全局代理不生效时设置 |
| mj.ng-discord.server | 否 | https://discord.com 反代地址 |
| mj.ng-discord.cdn | 否 | https://cdn.discordapp.com 反代地址 |
| mj.ng-discord.wss | 否 | wss://gateway.discord.gg 反代地址 |
| mj.translate-way | 否 | 中文prompt翻译成英文的方式，可选null(默认)、baidu、gpt、deepl |
| mj.translate-zh-way | 否 | describe、shorten等结果转中文的方式，可选null(默认)、baidu、gpt、deepl |
| mj.baidu-translate.appid | 否 | 百度翻译的appid |
| mj.baidu-translate.app-secret | 否 | 百度翻译的app-secret |
| mj.openai.gpt-api-url | 否 | 自定义gpt的接口地址，默认不需要配置 |
| mj.openai.gpt-api-key | 否 | gpt的api-key |
| mj.openai.timeout | 否 | openai调用的超时时间，默认30秒 |
| mj.openai.model | 否 | openai的模型，默认gpt-3.5-turbo |
| mj.openai.max-tokens | 否 | 返回结果的最大分词数，默认2048 |
| mj.openai.temperature | 否 | 相似度(0-2.0)，默认0 |
| mj.deepl-translate.auth-key | 否 | DEEPL翻译的鉴权密钥 |
| mj.error-desc | 否 | 任务错误原因转换，默认使用mj提供的英文描述 |
| spring.redis | 否 | 任务存储方式设置为redis，需配置redis相关属性 |

### 账号池配置参考
设置账号池后，调整`mj.queue`以实现更多任务并发
```yaml
mj:
  accounts:
    - guild-id: xxx
      channel-id: xxx
      user-token: xxxx
      session-id: xxxx
      user-agent: xxxx
      remix: false
    - guild-id: xxx
      channel-id: xxx
      user-token: xxxx
      session-id: xxxx
      user-agent: xxxx
      remix: false
```

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
