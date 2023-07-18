# midjourney-proxy-plus
midjourney-proxy的先行版，采用了全新架构，降低了封号的几率，解决了提示词匹配不准确的问题。

## 主要功能

- [x] 支持 Imagine 指令和相关动作
- [x] Imagine 时支持添加图片base64，作为垫图
- [x] 支持 Zoom(图片变焦)、Pan(焦点移动) 等功能
- [x] 支持 Remix 模式
- [x] 支持 Blend(图片混合) 指令和相关动作
- [x] 支持 Describe(图生文) 指令和相关动作
- [x] 支持任务实时进度
- [x] 支持中英文翻译，需配置百度翻译、deepl翻译或gpt
- [x] prompt 敏感词判断，支持覆盖调整
- [x] 任务队列，默认队列10，并发3。可参考 [MidJourney订阅级别](https://docs.midjourney.com/docs/plans) 调整mj.queue
- [x] user-token 连接 wss，可以获取错误信息和完整功能
- [x] 支持 discord域名(server、cdn、wss)反代，配置 mj.ng-discord
- [x] 支持配置账号池，分发绘图任务

## 后续计划

- [ ] 多种轮询机制
- [ ] mj管理后台
- [ ] ...

## 获取方式

扫码获取，备注mj先行版

 <img src="https://raw.githubusercontent.com/novicezk/midjourney-proxy/main/docs/manager-qrcode.png" width="220" alt="微信二维码"/>

加入我们即可获得

- midjourney-proxy的最新版本
- 微信机器人最新版本
- 及时维护，出问题优先修复
- 您的意见和建议会被我们重点采纳
