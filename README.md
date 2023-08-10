# midjourney-proxy-plus

[midjourney-proxy](https://github.com/novicezk/midjourney-proxy) 的先行版，采用了全新模式。支持mj所有的指令和相关操作，精准匹配所有提交的任务。

## 开源版功能
- [x] 支持 Imagine 指令和相关U、V、R动作
- [x] Imagine 时支持添加图片base64，作为垫图
- [x] 支持 Blend(图片混合)、Describe(图生文) 指令
- [x] 支持任务实时进度
- [x] 支持中英文翻译，需配置百度翻译或gpt
- [x] prompt 敏感词判断，支持覆盖调整
- [x] 任务队列，默认队列10，并发3
- [x] user-token 连接 wss，可以获取错误信息和完整功能
- [x] 支持 discord域名(server、cdn、wss)反代，配置 mj.ng-discord

## 先行版功能
- [x] 支持开源版的所有功能
- [x] 支持U之后的所有相关动作：Zoom(图片变焦)、Pan(焦点移动) 等
- [x] 支持 Blend(图片混合) 指令和相关动作
- [x] 支持 Describe(图生文) 指令和相关动作
- [x] 支持 Shorten 指令和相关动作
- [x] 支持 Remix 模式，参考 [API接口说明](./docs/api.md) 的`/mj/submit/action`
- [x] 支持获取图片的seed值
- [x] 中英文翻译额外支持deepl
- [x] 账号池持久化，动态维护
- [x] 每个账号可设置对应的任务队列（参考 [MidJourney订阅级别](https://docs.midjourney.com/docs/plans) 调整）
- [x] 支持获取账号/info、/settings信息
- [x] 内嵌 [管理后台页面](https://github.com/litter-coder/midjourney-proxy-admin)

## 后续计划

- [ ] 任务、账号存储支持MySQL
- [ ] settings设置

## 获取方式

扫码获取，备注mj先行版

 <img src="https://raw.githubusercontent.com/litter-coder/midjourney-proxy-plus/main/docs/manager-qrcode.jpeg" width="240" alt="微信二维码"/>

加入我们即可获得

- midjourney-proxy的最新版本
- [微信机器人最新版本](https://github.com/litter-coder/wechat-ai)
- 及时维护，出问题优先修复
- 您的意见和建议会被我们重点采纳

## 使用前提
1. 注册并订阅 MidJourney，创建自己的频道，参考 https://docs.midjourney.com/docs/quick-start
2. 获取用户Token、服务器ID、频道ID等：[获取方式](./docs/discord-params.md)

## 配置项
- mj.accounts: 参考 [账号池配置](./docs/config.md#%E8%B4%A6%E5%8F%B7%E6%B1%A0%E9%85%8D%E7%BD%AE%E5%8F%82%E8%80%83)
- mj.account-store-type: 账号存储方式，默认in_memory(内存\重启后丢失)，可选redis
- mj.task-store.type: 任务存储方式，默认in_memory(内存\重启后丢失)，可选redis
- mj.task-store.timeout: 任务存储过期时间，过期后删除，默认30天
- mj.api-secret: 接口密钥，为空不启用鉴权；调用接口时需要加请求头 mj-api-secret
- mj.translate-way: 中文prompt翻译成英文的方式，可选null(默认)、baidu、gpt、deepl
- mj.translate-zh-way: describe、shorten等结果翻译成中文的方式，可选null(默认)、baidu、gpt、deepl
- redis、翻译或更多配置查看 [配置项](./docs/config.md)

## 相关文档
- [部署教程](./docs/start.md)
- [全部配置项](./docs/config.md)
- [API接口说明](./docs/api.md)
- [Release版本jar包地址](https://github.com/litter-coder/midjourney-proxy-plus/releases)
