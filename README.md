# japanese_talk_api_transformer


日本語の会話をtensor2tensorのtransformerモデルで学習させ、Q&Aサーバー化しました。
このリポジトリにはサンプルのモデル (`model/0`) が含まれていますが、これは学習の初期段階のモデルです。
学習されたモデルは、[gumroad](https://gumroad.com/l/japanese_talk_api_transformer) にて販売していますのでお買い求めください。

Japanese conversation api learned by tensor2tensor's transformer model.
This repository contain a sample model (`model/0`) but it's a first checkpoint.
If you want a well-learned model, please buy it from my [gumroad](https://gumroad.com/l/japanese_talk_api_transformer) .


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

リポジトリをクローンした後、購入したzipファイル内の`1553675918` フォルダと `vocab.conversation_ja.8192.subwords` をmodel以下に配置して下さい。
modelディレクトリは以下のようになります。`vocab.conversation_ja.8192.subwords` は購入したものに置き換えられています。

After cloning the repository, please put `1553675918` directory and `vocab.conversation_ja.8192.subwords` into model directory.
The model directory will be like this. `vocab.conversation_ja.8192.subwords` should be replaced by bought one.:

```
japanese_talk_api_transformer
  |- model
      |- vocab.conversation_ja.8192.subwords
      |- 0: sample model
      |- 1553675918
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



## Examples (selling model)

- 質問: GET localhost:5000?input=プログラミングは得意？

答え

```
{  
   "outputs":[  
      {  
         "score":[  
            -4.312653541564941,
            -5.427693843841553,
            -5.809759140014648,
            -6.852217197418213,
            -7.029977798461914
         ],
         "val":[  
            "仕事は得意ですね",
            "プログラミングは楽しいですね",
            "同時ネットは楽しいですね",
            "どんなプログラミングを使いますか？",
            "どんなプログラミングを使いますか?"
         ]
      }
   ]
}
```

- 質問: GET localhost:5000?input=なんか面白いこと言って

答え

```
{  
   "outputs":[  
      {  
         "score":[  
            -1.4691219329833984,
            -1.4737167358398438,
            -2.6456146240234375,
            -3.069878578186035,
            -4.23007345199585
         ],
         "val":[  
            "退屈になりがちよねえ",
            "退屈になりがちか",
            "楽しそうですね",
            "スイカは大好きですね",
            "大好きですね"
         ]
      }
   ]
}
```

- 質問: GET localhost:5000?input=今日は何の日？

答え

```
{  
   "outputs":[  
      {  
         "score":[  
            -1.0922307968139648,
            -4.318934440612793,
            -4.448232173919678,
            -4.468869209289551,
            -4.474625587463379
         ],
         "val":[  
            "淫夢の日",
            "淫夢の日！",
            "淫夢の日だYo",
            "淫夢の日!",
            "淫夢の日だY"
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
            -2.9464476108551025,
            -3.4061570167541504,
            -3.543358325958252,
            -4.417332172393799,
            -4.759749889373779
         ],
         "val":[  
            "産んでない",
            "死ね",
            "死ぬ",
            "産んでくれてるよ",
            "産んでないね"
         ]
      }
   ]
}
```


