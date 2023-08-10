# API接口说明

`http://ip:port/doc` 已有api文档，此处仅作补充

## 1. 数据结构

### 任务
| 字段 | 类型 | 示例 | 描述 |
|:-----:|:----:|:----|:----|
| id | string | 1689231405853400 | 任务ID |
| action | string | IMAGINE | 任务类型: IMAGINE（绘图）、UPSCALE（选中放大）、VARIATION（选中变换）、ZOOM（图片变焦）、PAN（焦点移动）、DESCRIBE（图生文）、BLEAND（图片混合）、SHORTEN（prompt分析） |
| status | string | SUCCESS | 任务状态: NOT_START（未启动）、SUBMITTED（已提交处理）、MODAL（窗口等待）、IN_PROGRESS（执行中）、FAILURE（失败）、SUCCESS（成功） |
| prompt | string | 猫猫 | 提示词 |
| promptEn | string | Cat | 英文提示词 |
| description | string | /imagine 猫猫 | 任务描述 |
| submitTime | number | 1689231405854 | 提交时间 |
| startTime | number | 1689231442755 | 开始执行时间 |
| finishTime | number | 1689231544312 | 结束时间 |
| progress | string | 100% | 任务进度 |
| imageUrl | string | https://cdn.discordapp.com/attachments/xxx/xxx/xxxx.png | 生成图片的url, 成功或执行中时有值，可能为png或webp |
| failReason | string | [Invalid parameter] Invalid value | 失败原因, 失败时有值 |
| properties | object | {"finalPrompt": "Cat"} | 任务的扩展属性，系统内部使用 |
| buttons | Button[] | [] | 任务完成后的可执行按钮 |

### Button
| 字段 | 类型 | 示例 | 描述 |
|:-----:|:----:|:----|:----|
| customId | string | MJ::JOB::upsample::1::85a4b4c1-8835-46c5-a15c-aea34fad1862 | 动作标识 |
| emoji | string | 🪄 | 图标 |
| label | string | Make Variations | 文本 |
| type | number | 2 | 类型，系统内部使用 |
| style | number | 2 | 样式: 2（Primary）、3（Green） |

## 2. 任务提交返回
- code=1: 提交成功，result为任务ID
    ```json
    {
      "code": 1,
      "description": "提交成功",
      "result": "14001929738841620",
      "properties": {
          "discordInstanceId": "1118138338562560102"
      }
    }
    ```
- code=22: 提交成功，进入队列等待
    ```json
    {
        "code": 22,
        "description": "排队中，前面还有1个任务",
        "result": "14001929738841620",
        "properties": {
            "numberOfQueues": 1,
            "discordInstanceId": "1118138338562560102"
         }
    }
    ```
- code=23: 队列已满，请稍后尝试
    ```json
    {
        "code": 23,
        "description": "队列已满，请稍后尝试",
        "result": "14001929738841620",
        "properties": {
            "discordInstanceId": "1118138338562560102"
         }
    }
    ```
- code=24: prompt包含敏感词
    ```json
    {
        "code": 24,
        "description": "可能包含敏感词",
        "properties": {
            "promptEn": "nude body",
            "bannedWord": "nude"
         }
    }
    ```
- other: 提交错误，description为错误描述

## 3. 执行任务的关联动作
调用 `/mj/submit/action`，几乎所有的button都做了支持，除了以下情况:
- 图生文结果的 `🎉Imagine all`
- 图片放大后的 `❤️`

```json
{
  // 关联任务的ID
  "taskId": "1689216801333574",
  // 动作标识
  "customId": "MJ::JOB::reroll::0::1c6dff5e-5632-40c6-9d4c-afb261705313::SOLO"
}
```
⚠️ 注意: 某些场景需要modal弹框确认
- 执行CustomZoom(自定义变焦)
- 执行PicReader(Describe后选择生图)
- 执行PromptAnalyzer(Shorten后选择生图)
- 账号开启了Remix & 执行Reroll、Variation、Pan

这时返回的code为 21，示例:
```json
{
  "code": 21,
  "description": "窗口等待",
  "result": "14001929738841620"
}
```
该任务状态为MODAL，但不会进队列影响并发。需调用`/mj/submit/modal`提交最终任务
```json
{
  // 需确认的任务ID
  "taskId": "1689228047868174",
  // prompt: 为空时使用原任务的prompt
  "prompt": "Cat"
}
```
CustomZoom的prompt需要设置`--zoom`(1到2之间)，例如: `Cat --zoom 1.5`

## 4. `/mj/submit/describe` 图生文
```json
{
    // 图片的base64字符串
    "base64": "data:image/png;base64,xxx"
}
```

后续任务完成后，properties中finalPrompt即为图片生成的prompt，finalZhPrompt为翻译的中文
```json
{
  "id":"14001929738841620",
  "action":"DESCRIBE",
  "status": "SUCCESS",
  "description":"/describe 14001929738841620.png",
  "imageUrl":"https://cdn.discordapp.com/attachments/xxx/xxx/14001929738841620.png",
  "properties": {
    "finalPrompt": "1️⃣ Cat --ar 5:4\n\n2️⃣ Cat2 --ar 5:4\n\n3️⃣ Cat3 --ar 5:4\n\n4️⃣ Cat4 --ar 5:4",
    "finalZhPrompt": "1️⃣ 猫 --ar 5:4\n\n2️⃣ 猫2 --ar 5:4\n\n3️⃣ 猫3 --ar 5:4\n\n4️⃣ 猫4 --ar 5:4"
  }
  // ...
}
```

## 5. `/mj/submit/shorten` prompt分析
```json
{
  "prompt": "️appdash appdash, in the style of expert draftsmanship, commission for, ethereal, dreamlike quality, dadaistic, toonami"
}
```

后续任务完成后，properties中finalPrompt即为分析结果，finalZhPrompt为翻译的中文
```json
{
  "id":"1689252749098647",
  "action":"SHORTEN",
  "status": "SUCCESS",
  "description":"/shorten appdash appdash, in the style of expert draftsmanship, commission for, ethereal, dreamlike quality, dadaistic, toonami",
  "properties": {
    "finalPrompt": "## Important tokens\n**appdash** **appdash**, in the ~~style~~ of ~~expert~~ **draftsmanship**, commission for, ethereal, dreamlike quality, ~~dadaistic~~, **toonami**\n## Shortened prompts\n1️⃣ appdash appdash, draftsmanship, commission for, ethereal, toonami\n\n2️⃣ appdash appdash, draftsmanship, commission, toonami\n\n3️⃣ appdash appdash, draftsmanship, toonami\n\n4️⃣ appdash appdash, toonami\n\n5️⃣ appdash appdash",
    "finalZhPrompt": "## 重要词汇\n**appdash** **appdash**，以专家的绘画风格，委托制作，飘渺的，梦幻般的质感，达达主义的，**toonami**\n## 简化提示\n1️⃣ appdash appdash，绘画风格，委托制作，飘渺的，toonami\n\n2️⃣ appdash appdash，绘画风格，委托制作，toonami\n\n3️⃣ appdash appdash，绘画风格，toonami\n\n4️⃣ appdash appdash，toonami\n\n5️⃣ appdash appdash"
  }
  // ...
}
```
对该任务执行 `Show Details` 动作，能获得进一步的分析结果
```json
{
  "id":"1689253263953453",
  "action":"SHORTEN",
  "status": "SUCCESS",
  "description":"/up 168925266642808397 Show Details",
  "properties": {
    "finalPrompt": "## Important tokens\n**appdash** (1.00) **appdash** (0.79), in the style (0.01) of expert (0.00) **draftsmanship** (0.09), commission (0.08) for, ethereal (0.05), dreamlike (0.02) quality (0.01), dadaistic (0.01), **toonami** (0.19)\n\n██████████ appdash\n████████░░ appdash\n██░░░░░░░░ toonami\n█░░░░░░░░░ draftsmanship\n█░░░░░░░░░ commission\n█░░░░░░░░░ ethereal\n## Shortened prompts\n1️⃣ appdash appdash, draftsmanship, commission for, ethereal, toonami\n\n2️⃣ appdash appdash, draftsmanship, commission, toonami\n\n3️⃣ appdash appdash, draftsmanship, toonami\n\n4️⃣ appdash appdash, toonami\n\n5️⃣ appdash app",
    "finalZhPrompt": "## 重要的词语\n**appdash** (1.00) **appdash** (0.79)，以专家级(0.01) **绘画技巧** (0.09) 的风格，委托(0.08) 制作，飘渺的(0.05)，梦幻般的(0.02) 质感(0.01)，达达主义的(0.01)，**toonami** (0.19)\n\n██████████ appdash\n████████░░ appdash\n██░░░░░░░░ toonami\n█░░░░░░░░░ draftsmanship\n█░░░░░░░░░ commission\n█░░░░░░░░░ ethereal\n## 简化的提示\n1️⃣ appdash appdash，绘画技巧，委托制作，飘渺，toonami\n\n2️⃣ appdash appdash，绘画技巧，委托制作，toonami\n\n3️⃣ appdash appdash，绘画技巧，toonami\n\n4️⃣ appdash appdash，toonami\n\n5️⃣ appdash appdash"
  }
  // ...
}
```

## 6. 获取任务图片的seed

绘图任务执行后，不会设置seed，如需获取seed，需要执行 `/mj/task/{id}/image-seed`

⚠️ 注意: 必须配置账号的Midjourney Bot私信ID，否则无法调用

- code=1: 获取成功，result为图片对应的seed
    ```json
    {
      "code": 1,
      "description": "成功",
      "result": "636646138"
    }
    ```
- other: 执行错误，description为错误描述

## 7. 任务变更回调
任务状态变化或进度改变时，会调用业务系统的接口
- 接口地址为配置的 mj.notify-hook，任务提交时支持传`notifyHook`以改变此任务的回调地址
- 两者都为空时，不触发回调

POST  application/json
```json
{
  "id": "14001929738841620",
  "action": "IMAGINE",
  "status": "SUCCESS",
  "prompt": "猫猫",
  "promptEn": "Cat",
  "description": "/imagine 猫猫",
  "submitTime": 1689231405854,
  "startTime": 1689231442755,
  "finishTime": 1689231544312,
  "progress": "100%",
  "imageUrl": "https://cdn.discordapp.com/attachments/xxx/xxx/xxxx.png",
  "failReason": null,
  "properties": {
    "finalPrompt": "Cat"
  },
  "buttons": []
}
```
