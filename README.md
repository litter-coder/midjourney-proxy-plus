# midjourney-proxy-plus

[midjourney-proxy](https://github.com/novicezk/midjourney-proxy) 的plus版本，采用了全新模式。支持mj所有的指令和相关操作，精准匹配所有提交的任务。

## 开源版功能
- [x] 支持 Imagine 指令和相关动作
- [x] Imagine 时支持添加图片base64，作为垫图
- [x] 支持 Blend(图片混合)、Describe(图生文) 指令
- [x] 支持任务实时进度
- [x] 支持中文prompt翻译，需配置百度翻译或gpt
- [x] prompt 敏感词预检测，支持覆盖调整
- [x] user-token 连接 wss，可以获取错误信息和完整功能
- [x] 支持多账号配置，每个账号可设置对应的任务队列（参考 [MidJourney订阅级别](https://docs.midjourney.com/docs/plans) 调整）
- [x] 任务存储支持内存、Redis

## 先行版功能
- [x] 支持开源版的所有功能
- [x] 支持 Shorten(prompt分析) 指令
- [x] 支持焦点移动: Pan ⬅️ ➡️ ⬆️ ⬇️
- [x] 支持图片变焦: Zoom 🔍
- [x] 支持局部重绘: Vary (Region) 🖌
- [x] 支持所有的关联按钮动作和 🎛️Remix模式，参考 [API接口说明-执行动作](./docs/api.md#3-%E6%89%A7%E8%A1%8C%E4%BB%BB%E5%8A%A1%E7%9A%84%E5%85%B3%E8%81%94%E5%8A%A8%E4%BD%9C)
- [x] 支持获取图片的seed值
- [x] 账号池持久化，动态维护
- [x] 账号、任务存储支持内存、Redis、MySQL
- [x] 支持获取账号/info、/settings信息，更改settings设置
- [x] 支持取消等待、进行中的任务
- [x] 内嵌管理后台页面: 支持账号维护、任务查看、绘图测试等
- [x] 支持 [niji・journey Bot](https://discord.com/invite/nijijourney)，需加入自己的服务器
- [x] 支持 [InsightFace 人脸服务](https://discord.com/api/oauth2/authorize?client_id=1090660574196674713&permissions=274877945856&scope=bot)

## 获取方式

微信扫码获取，备注mj先行版

 <img src="https://raw.githubusercontent.com/litter-coder/midjourney-proxy-plus/main/docs/manager-qrcode.jpeg" width="240" alt="微信二维码"/>

Telegram

 <img src="https://raw.githubusercontent.com/litter-coder/midjourney-proxy-plus/main/docs/telegram-qrcode.png" width="240" alt="Telegram二维码"/>

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
- mj.account-store-type: 账号存储方式，默认in_memory(内存\重启后丢失)，可选redis、mysql
- mj.task-store.type: 任务存储方式，默认in_memory(内存\重启后丢失)，可选redis、mysql
- mj.task-store.timeout: 任务存储过期时间，过期后删除，默认30天。mysql存储不生效
- mj.api-secret: 接口密钥，为空不启用鉴权；调用接口时需要加请求头 mj-api-secret
- mj.translate-way: 中文prompt翻译成英文的方式，可选null(默认)、baidu、gpt、deepl
- mj.translate-zh-way: describe、shorten等结果翻译成中文的方式，可选null(默认)、baidu、gpt、deepl
- redis、mysql、翻译或更多配置查看 [配置项](./docs/config.md)
