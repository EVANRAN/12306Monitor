
## 12306ByPass辅助程序

监控抢票状态，然后通过各种方式通知你，默认支持钉钉机器人，同时支持WebHook

### 安装

- `git clone`
- `pip install requests`
- `pip install pywin32`

### 配置

请注意配置文件格式为json，引号全部使用双引号，文件编码为UTF-8

#### 通用

- interval: 监控周期, 默认1秒一次

#### 简单版

- 创建一个钉钉群
- 添加自定义群机器人，获取WebHook地址
- 将access_token填入`config.json`中"dingTokenListImportant"字段

#### 进阶版

- 同`简单版`
- 如果你希望获取一些其他信息，可以修改"monitorWord"和"gohomeWord"字段，只要日志中包含该关键词，则会使用"dingTokenListVerbose"和"dingTokenListImportant"对应的钉钉机器人进行推送

#### 复杂版

- 支持WebHook方式
- 按照WebHook需要的请求类型，配置enableGetWebHook/enablePostWebHook为true即可
- 填写WebHook地址，分别对应getWebHook/postWebHook
    + 程序会自动替换其中对应的`$message`字段
    + 如果是POST类型，需要POST的数据请填写到`postWebHookData`
- postWebHookType
    + formdata/json

### 运行

- 修改配置后，执行`python main.py` 即可
- 另外可以执行`python test.py`测试通知是否正常，请修改`config.json`后测试

### 拓展

注意: 省略部分不代表不需要

#### Server酱配置

```JSON
{
    "...": "...",
    "getWebHook": "https://sc.ftqq.com/SCKEY.send?text=$message",
    "...": "..."
}

{
    "...": "...",
    "postWebHook": "https://sc.ftqq.com/SCKEY.send",
    "postWebHookData": {
        "text": "抢到票啦，快去付款吧",
        "desp": "Markdown"
    },
    "postWebHookType": "formdata",
    "...": "..."
}
```

#### 语音电话

- 注册[云片](https://www.yunpian.com)，新用户有10条语音短信的额度
    + 友情提醒，我注册后没隔多久就接到了客服打来的营销电话
- 获取APIKEY，填入`yunpianApiKey`字段
- 配置`enableMobile`为`true`
- 配置接收电话的手机号`notifyMobile`
- `python test.py`测试，你会接到一个验证码为12306的电话😊

```JSON
{
    "...": "...",
    "enableMobile": true,
    "yunpianApiKey": "APIKEY",
    "notifyMobile": "手机号",
    "...": "..."
}
```

---

### 讨论群

![微信群](./res/wechat_group.jpeg)
