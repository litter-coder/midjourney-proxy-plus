<div align="center">

<h1 align="center">midjourney-proxy-plus</h1>

[English](./README.md) | 中文

[![GitHub release](https://img.shields.io/static/v1?label=release&message=v3.8.2&color=blue)](https://github.com/litter-coder/midjourney-proxy-plus)
[![License](https://img.shields.io/badge/license-Apache%202-4EB1BA.svg)](https://www.apache.org/licenses/LICENSE-2.0.html)

</div>

[midjourney-proxy](https://github.com/novicezk/midjourney-proxy) 的plus版本，采用了全新模式。支持mj所有的指令和相关操作，精准匹配所有提交的任务。

## 开源版功能
- [x] 支持 Imagine 指令和相关动作
- [x] Imagine 时支持添加图片base64，作为垫图
- [x] 支持 Blend(图片混合)、Describe(图生文) 指令
- [x] 支持任务实时进度
- [x] 支持中文prompt翻译，需配置百度翻译或gpt
- [x] prompt 敏感词预检测，支持覆盖调整
- [x] user-token 连接 wss，可以获取错误信息和完整功能
- [x] 支持多账号配置，每个账号可设置对应的任务队列

## 先行版功能
- [x] 支持开源版的所有功能
- [x] 支持 Shorten(prompt分析) 指令
- [x] 支持焦点移动: Pan ⬅️ ➡️ ⬆️ ⬇️
- [x] 支持图片变焦: Zoom 🔍
- [x] 支持局部重绘: Vary (Region) 🖌
- [x] 支持几乎所有的关联按钮动作和🎛️ Remix模式
- [x] 支持获取图片的seed值
- [x] 账号池持久化，动态维护
- [x] 账号、任务存储支持内存、Redis、MySQL
- [x] 支持获取账号/info、/settings信息，更改settings设置
- [x] 支持取消等待、进行中的任务
- [x] 内嵌 [管理后台](https://github.com/litter-coder/midjourney-proxy-admin): 支持账号维护、任务查看、绘图测试等
- [x] 支持MJ V6.0以及cerf等最新参数操作
- [x] mj账号订阅过期或被封后，自动禁用
- [x] mj账号快速时长消耗完后，自动切换为relax模式
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

## 应用项目
- [wechat-ai](https://github.com/litter-coder/wechat-ai) : 基于 chatgpt-on-wechat 和 midjourney-proxy-plus 的微信智能机器人
- [chatgpt-web-midjourney-proxy](https://github.com/Dooy/chatgpt-web-midjourney-proxy) : chatgpt web, midjourney, gpts,tts, whisper 一套ui全搞定
- [new-api](https://github.com/Calcium-Ion/new-api) : 接入Midjourney Proxy (Plus)的接口管理 & 分发系统
- [midjourney-captcha-bot](https://github.com/ye4241/midjourney-captcha-bot) : 绕过Midjourney验证码

## 使用前提
1. 注册并订阅 MidJourney，创建自己的频道，参考 https://docs.midjourney.com/docs/quick-start
2. 获取用户Token、服务器ID、频道ID等：[获取方式](./docs/discord-params.md)

## 其它
如果觉得这个项目对您有所帮助，请帮忙点个star

[![Star History Chart](https://api.star-history.com/svg?repos=litter-coder/midjourney-proxy-plus&type=Date)](https://star-history.com/#litter-coder/midjourney-proxy-plus&Date)
