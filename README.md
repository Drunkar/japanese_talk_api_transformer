# japanese_talk_api_transformer


日本語の会話をtensor2tensorのtransformerモデルで学習させ、Q&Aサーバー化しました。
このリポジトリにはサンプルのモデル (`model/0`) が含まれていますが、これは学習の初期段階のモデルです。
学習されたモデルは、(gumroad)[https://gumroad.com/l/japanese_talk_api_transformer]にて販売していますのでお買い求めください。

Japanese conversation api learned by tensor2tensor's transformer model.
This repository contain a sample model (`model/0`) but it's a first checkpoint.
If you want a well-learned model, please buy it from my (mode)[https://gumroad.com/l/japanese_talk_api_transformer].



## Examples (selling model)

- 質問: GET localhost:5000?input=ウザめの顔文字

答え

```
{
   "outputs":[      {
         "score":"[ -7.4247966  -7.469062   -8.157035   -9.544703  -10.399394 ]",
         "val":[
            "( ˘ω˘ )",
            "( ´ ∵ )",
            "( ˘ω˘)",
            "( ´ ` )",
            "( ˘ω˘ )💓"
         ]
      }
   ]
}
```

- 質問: GET localhost:5000?input=毎日の通勤時間どれぐらい？

答え

```
{  
   "outputs":[  
      {  
         "score":"[-6.4501634 -6.6337633 -7.048634  -7.1006274 -8.481556 ]",
         "val":[  
            "4時間",
            "4時間くらい",
            "1時間",
            "1時間くらい",
            "4時間くらい？"
         ]
      }
   ]
}
```

- 質問: GET localhost:5000?input=昼飯はなんにしよう

答え

```
{  
   "outputs":[  
      {  
         "score":"[ -9.761208 -10.215987 -11.521189 -11.924395 -12.078274]",
         "val":[  
            "お昼寝",
            "お昼寝です",
            "お昼寝です。",
            "お昼寝です！",
            "お昼寝。"
         ]
      }
   ]
}
```


- 質問: GET localhost:5000?input=オイオイ死ぬわアイツ

答え

```
{  
   "outputs":[  
      {  
         "score":"[ -8.22032    -8.5791445  -8.779987   -8.898018  -10.033653 ]",
         "val":[  
            "うるせぇ",
            "そんなもん",
            "うるせ",
            "そんなこと言ってる",
            "うるせぇぇ"
         ]
      }
   ]
}
```


## Requirements
- docker
- docker-compose
- model


## Usage

```
git clone git@github.com:Drunkar/japanese_talk_api_transformer.git
```

---

**If you bought my pre-trained data**

After cloning the repository, please put `1552717118` directory into model directory.
The model directory will be like this:

```
japanese_talk_api_transformer
  |- model
      |- vocab.conversation_ja.8192.subwords
      |- 0: sample model
      |- 1552717118
          |- saved_model
          |- variables
              |- variables.data-00000-of-00001
              |- variables
```

---

Then, please start services:

```
cd japanese_talk_api_transformer
docker-compose up -d
```

By GET request with "input" parameter, you will get the answers.

```
curl localhost:5000?input=hello%20men
{"outputs":[{"score":"[-5.048567  -5.2183614 -6.455683  -7.121113  -7.4721427]","val":["Haha","Hahahaha","Hahahahaha","Hahahh","Hoo"]}]}
```

The higher score means more suitable to the question.

