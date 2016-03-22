title: Cloud9 运行 Telegram Bot
date: 2016-03-22 15:38:36
tags: [telegram, python, py]
---

[Telegram](https://telegram.org/) 是俄罗斯人开发的一款即时聊天工具, 详细的介绍请看 Rei 的 [介绍Telegram](http://chloerei.com/2015/02/05/telegram/).

[Cloud9](https://c9.io/) 是什么呢?
Cloud9 provides a development environment in the cloud that allows developers to get started with coding immediately and collaborate with their peers.

### 申请 Telegram Bot
添加 机器老爹-[BotFather](https://telegram.me/BotFather)
输入指令 `/newbot`, 选好 `name` 和 `username` 之后, 老爹会返回一串 Token:

```
Use this token to access the HTTP API:
161xxxx:xxxx_xxxx-xxxxxx

For a description of the Bot API, see this page: https://core.telegram.org/bots/api
```

### Flask 运行 server

1 安装 Flask, `pip install Flask`, pip 类似于 gem

2 来个 hello world

```python

from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello():
    return "Hello World!"

if __name__ == "__main__":
    app.run()
```
运行 `python hello.py`, 访问 http://localhost:5000/, 修改端口 `app.run(port='xxxx')`

### 使用 telegram python sdk
用[python-telegram-bot](https://github.com/python-telegram-bot/python-telegram-bot) 简化开发.

代码如下, 适用于py 2.7

```python

#coding=utf-8

import os
import logging
import telegram
import urlparse
from flask import Flask, render_template, request

HOST = "<Host>"
app = Flask(__name__)
logging.basicConfig(level=logging.DEBUG,
                    format='%(asctime)s - %(name)s - %(levelname)s - %(message)s')

global bot
bot = telegram.Bot(token = "<Token>")

botName = "@MustangBot"

@app.route("/", methods=["POST", "GET"])
def setWebhook():
    if request.method == "GET":
        logging.info("Hello, Telegram!")
        return "OK, Telegram Bot!"

@app.route("/set_webhook", methods=['GET'])
def setWebHook():
    result = bot.setWebhook("{}/bot_talk".format(HOST))
    if result:
        return "{} WebHook Setup OK!".format(botName)
    else:
        return "{} WebHook Setup Failed!".format(botName)

@app.route("/bot_talk", methods=["POST"])
def bot_talk():
    if request.method == "POST":
        update = telegram.Update.de_json(request.get_json(force=True))

        if update is None:
            return "Show me your TOKEN please!"
        logging.info("Calling {}".format(update.message))
        handdle_message(update.message)
        return "ok"

def handdle_message(msg):
    text = msg.text
    if "/echo" in text:
      bot.sendMessage(chat_id=msg.chat.id, text="Hello, I am a nerd")
    if "/photo" in text:
        bot.sendPhoto(chat_id=msg.chat.id, photo="<photo-url>")
    elif "/help" in text:
        helpInfo(msg)
    else:
        helpInfo(msg)

def helpInfo(msg):
    text ="""
/echo  - echo
/photo - photo
/help  - Help Info

--------------------------
在cloud9上跑了个telegram_bot
"""
    sendTxtMsg(msg, text)

########

def sendTxtMsg(msg, text):
    bot.sendMessage(chat_id=msg.chat.id, text=text)

if __name__ == "__main__":
  app.run(host=os.getenv('IP'),port=int(os.getenv('PORT')))

```

#### NOTICE

必须把应用设为 public, 获取cloud9的 IP 和 Port

``` python
os.getenv('IP')
os.getenv('PORT')

# 修改Flask
app.run(host=os.getenv('IP'), port=int(os.getenv('PORT')))
```

### 享用 Robot

访问 `<cloud9-url>/set_webhook`, 初始化bot, 添加机器人为好友, 发送 `/echo /help /photo` 试试哦.