<div align="center">

<h1 align="center">midjourney-proxy-plus</h1>

English | [中文](./README_CN.md)

[![GitHub release](https://img.shields.io/static/v1?label=release&message=v3.8.2&color=blue)](https://github.com/litter-coder/midjourney-proxy-plus)
[![License](https://img.shields.io/badge/license-Apache%202-4EB1BA.svg)](https://www.apache.org/licenses/LICENSE-2.0.html)

</div>

The plus version of [midjourney-proxy](https://github.com/novicezk/midjourney-proxy) adopts a brand new mode. It supports all MidJourney commands and related operations, and accurately matches all submitted tasks.

## Open Source Version Features
- [x] Supports Imagine instructions and related actions
- [x] Supports adding image base64 as a placeholder when using the Imagine command
- [x] Supports Blend (image blending) and Describe (image to text) commands
- [x] Supports real-time progress tracking of tasks
- [x] Supports translation of Chinese prompts, requires configuration of Baidu Translate or GPT
- [x] Prompt sensitive word pre-detection, supports override adjustment
- [x] User-token connects to WSS (WebSocket Secure), allowing access to error messages and full functionality
- [x] Supports multi-account configuration, with each account able to set up corresponding task queues

## Plus Version Features
- [x] Supports all the features of the open-source version
- [x] Supports Shorten (prompt analysis) command
- [x] Supports focus shifting: Pan ⬅️ ➡️ ⬆️ ⬇️
- [x] Supports image zooming: Zoom 🔍
- [x] Supports local redrawing: Vary (Region) 🖌
- [x] Supports nearly all associated button actions and the 🎛️ Remix mode
- [x] Supports retrieving the seed value of images
- [x] Account pool persistence, dynamic maintenance
- [x] Account and task storage support for in-memory, Redis, MySQL
- [x] Supports retrieving account /info and /settings information, and changing settings configurations
- [x] Supports canceling tasks that are waiting or in progress
- [x] Embedded management dashboard page: Supports account maintenance, task viewing, drawing tests, etc
- [x] Supports MJ V6.0 and other latest parameter operations such as 'cerf'
- [x] Automatically disable when the MJ account subscription expires or is banned
- [x] Automatically switch to relax mode after the quick duration of the MJ account is consumed
- [x] Supports [niji・journey Bot](https://discord.com/invite/nijijourney), must be added to your own server
- [x] Supports [InsightFace Bot](https://discord.com/api/oauth2/authorize?client_id=1090660574196674713&permissions=274877945856&scope=bot)

## Acquisition Method

Obtain by scanning WeChat QR code, remark with ‘mj plus’.

 <img src="https://raw.githubusercontent.com/litter-coder/midjourney-proxy-plus/main/docs/manager-qrcode.jpeg" width="240" alt="WeChat QR Code"/>

Telegram

 <img src="https://raw.githubusercontent.com/litter-coder/midjourney-proxy-plus/main/docs/telegram-qrcode.png" width="240" alt="Telegram QR Code"/>

Join us to receive

- The latest version of midjourney-proxy
- [The latest version of the WeChat bot](https://github.com/litter-coder/wechat-ai)
- Timely maintenance with priority given to fixing issues as they arise
- Your opinions and suggestions will be given priority consideration by us

## Application Project
- [wechat-ai](https://github.com/litter-coder/wechat-ai) : A WeChat smart bot based on chatgpt-on-wechat and midjourney-proxy-plus
- [chatgpt-web-midjourney-proxy](https://github.com/Dooy/chatgpt-web-midjourney-proxy) : chatgpt web, midjourney, gpts,tts, whisper A complete UI solution

## Prerequisites for use
1. Register and subscribe to MidJourney, create your own channel, refer to https://docs.midjourney.com/docs/quick-start
2. Obtain user Token, server ID, channel ID: [Method of acquisition](./docs/discord-params.md)

## Others
If you find this project helpful, please consider giving it a star

[![Star History Chart](https://api.star-history.com/svg?repos=litter-coder/midjourney-proxy-plus&type=Date)](https://star-history.com/#litter-coder/midjourney-proxy-plus&Date)
