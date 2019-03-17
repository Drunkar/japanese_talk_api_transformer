# japanese_talk_api_transformer


日本語の会話をtensor2tensorのtransformerモデルで学習させ、Q&Aサーバー化しました。
このリポジトリにはサンプルのモデル (`model/0`) が含まれていますが、これは学習の初期段階のモデルです。
学習されたモデルは、[gumroad](https://gumroad.com/l/japanese_talk_api_transformer) にて販売していますのでお買い求めください。

Japanese conversation api learned by tensor2tensor's transformer model.
This repository contain a sample model (`model/0`) but it's a first checkpoint.
If you want a well-learned model, please buy it from my [gumroad](https://gumroad.com/l/japanese_talk_api_transformer) .



## Examples (selling model)

- 質問: GET localhost:5000?input=ウザめの顔文字

答え

```
{  
   "outputs":[  
      {  
         "score":[  
            -7.4247965812683105,
            -7.469061851501465,
            -8.157034873962402,
            -9.544702529907227,
            -10.399394035339355
         ],
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
         "score":[  
            -6.4501633644104,
            -6.633763313293457,
            -7.048634052276611,
            -7.100627422332764,
            -8.481555938720703
         ],
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
         "score":[  
            -9.761207580566406,
            -10.215987205505371,
            -11.521188735961914,
            -11.924394607543945,
            -12.07827377319336
         ],
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
         "score":[  
            -8.220319747924805,
            -8.579144477844238,
            -8.779987335205078,
            -8.898017883300781,
            -10.033653259277344
         ],
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

