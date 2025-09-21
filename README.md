---
description: 会話型の人工知能をあなたの側に
---

# Noby APIについて

![](.gitbook/assets/cotogoto-dev-title.png)

## 目的

NOBY APIはCotoGoto(コトゴト)内で利用している人工知能のAPIです。

NOBY APIを利用することで、CotoGoto(コトゴト)に対しても会話を通して、様々な操作をすることができます。\
CotoGoto(コトゴト)はFacebook、Twitter、Googleカレンダー、Trelloなどのサービスとも連携していますので、NOBY APIを通して、連動させることも可能となります。

※会話内容の例はこちらのサイトの「[AIとの会話のコツ](https://docs.cotogoto.ai/talk)」を参考にしてください。

## 会話する

下記の YOUR\_API\_KEY の部分をメールで届いた API キーに置き換えて下記のコマンドをターミナル上で実行すると、会話結果のJsonが返却されます。

```
$ curl 'https://app.cotogoto.ai/webapi/noby.json' \
--verbose \
--get \
--data 'text=おはようございます' \
--data 'appkey=YOUR_API_KEY'
```

『地名』と『天気』という単語が含まれた場合、天気を教えてくれます。

```
$ curl 'https://app.cotogoto.ai/webapi/noby.json' \
--verbose \
--get \
--data 'text=今日の名古屋の天気は？' \
--data 'appkey=YOUR_API_KEY'
```

『おみくじ』と『引きたい』という単語が含まれるとおみくじが引けます。

```
$ curl 'https://app.cotogoto.ai/webapi/noby.json' \
--verbose \
--get \
--data 'text=おみくじ引きたいな。' \
--data 'appkey=YOUR_API_KEY'
```

『じゃんけん』と『グー』『チョキ』『パー』という単語が含まれるとじゃんけんができます。

```
$ curl 'https://app.cotogoto.ai/webapi/noby.json' \
--verbose \
--get \
--data 'text=じゃんけんグー' \
--data 'appkey=YOUR_API_KEY'
```

## 文章中の単語と機能を連動

### **会話から動作を取得する**

会話の中に複数のキーワードを設定することにより、動作(コマンド機能)を設定することができます。

### **取得した動作を様々なデバイスへ連携する**

取得した動作(コマンド機能)は一意の動作キーを発行します。\
動作キーからプログラム実行やデバイスへの指示などを送ったり、様々な連携を可能とします。
