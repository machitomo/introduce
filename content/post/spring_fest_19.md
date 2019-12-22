
---
title: "Spring Fest 19 に初めて行ってみた。"
date: 2019-12-18T05:21:56+09:00
draft: false
---

#### Spring Fest とは？
>https://springfest2019.springframework.jp/

>Spring FrameworkはJavaの代表的なアプリケーションフレームワークであり、世界中の多くのJavaアプリケーションで利用されています。ユーザ間での情報交換・交流の場を提供し、さらなるSpring Frameworkの認知度の向上、普及促進を図るため、本カンファレンスを開催いたします。

だそうです。
ですので、Spring つよつよエンジニアの人から知見をGETするいい機会です。

#### 注意事項
- 筆者は自分がより知らない情報を取りに行っているため、誤っている情報を記載している可能性がある。
- あとで調べよう精神で箇条書きにキーワードだけ記載しているため、文章がまとまっていない。
- 登壇者の方々には知識の乏しい人間が聞いて、適当に書いていることに大変申し訳なく思っている。

#### 聞きたいセッション
- Spring Boot アプリの運用が楽になる？ Pivotal と Microsoft が共同開発した専用 PaaS「Azure Spring Cloud」のご紹介 !!
- LINE公式アカウントのチャットシステムにおけるSpringおよびWebFluxの活用事例
- 実践 Spring Boot Actuator + Micrometer
- Spring Developer のための コンテナ入門
- RSocket徹底入門 ~Spring 5.2の目玉機能であるRSocket対応とは~
- Spring Social でソーシャルログインを実装する

---
#### Spring Boot アプリの運用が楽になる？ Pivotal と Microsoft が共同開発した専用 PaaS「Azure Spring Cloud」のご紹介 !!

| 時間 | 登壇者 | 場所 |
|:-----------:|:------------:|:------------:|
| 11:00 - 11:45 | 寺田 佳央 | sola city Hall (WEST) |


- 知りたいこと
    - Azure Spring Cloud ってなに？
    - どれくらい楽になるの？
    - なにができるの？

- 知れたこと
    - > Azure Spring Cloud  
    フルマネージドのSpring Cloud サービスでアプリを簡単にデプロイ、操作、スケーリングができる。  
    https://azure.microsoft.com/ja-jp/services/spring-cloud/
    - Q2にGA（一般提供開始）
    - AzureでSpringを動かす為のリファレンス  
    - Blue-Green Deploymentに対応している。
    http://aka.ms/spring-java-jp
    - Cognitive Services は自然言語系が強いらしい。こういう系はGCP一択かと思っていたが、もう少し周りを見たほうが良いのかもしれない。 
    - Azure　DevOps & Jenkins で　CI/CDを実現する。
    - GCPやAWSへのデプロイもできる。
    - Azure Linux VMにJenkinsサーバをたてて、ビルドをして、Azure　DevOpsでデプロイする。  
    - オンプレでJenkinsを使用しているノウハウを生かすには良い選択かもしれない。
    - Azure Kubernetes Service(AKS)
    -  アプリ開発者が開発に専念できるように、k8sの機能の制御権に制限をかけているらしい。
    - Azureでspring cloud functionを動かせる。  
    http://aka.ms/Spring-Function-Azure-jp

- 感想  
正直、GCPかAWSを使用することが自分の中でのスタンダードだったけど、Azureっていう選択肢もちゃんと見ないけないという意識が芽生えた。

---

#### LINE公式アカウントのチャットシステムにおけるSpringおよびWebFluxの活用事例

| 時間 | 登壇者 | 場所 |
|:-----------:|:------------:|:------------:|
| 13:00 - 13:45 | 長谷部 良輔 | sola city Hall (EAST) |

- 知りたいこと
    - LINE社ではどんな使い方をしてるの？

- 知れたこと
    - SpringFWを使っているprojectは5000くらいある？

    - Event Receiverがメッセージ受信Event等を受け取ったらKafkaに記載している。その際にもWebFluxを使用してる。

    - Kafkaについて
      スケーラビリティに優れた分散メッセージジューらしいです。  
    https://qiita.com/sigmalist/items/5a26ab519cbdf1e07af3

    - WebFluxとは  
    Netty（NonBlockingFW）を使用した、非同期なノンブロッキング通信を実現するフレームワーク  

    - WebFlux以前の問題点  
    Tomcatでは1つのリクエストに対して、1スレッドを割り当てているため、多くのスレッドが必要になる。

    - 使用されたスライド(これ読んだほうが早い)  
    https://speakerdeck.com/line_developers/examples-of-using-spring-and-webflux-in-the-chat-system-for-line-official-accounts?slide=28

- 感想  
  率直に言うと自分には早かった。（知識不足で全然理解できなかった。）
  けど、Tomcatでの問題点を知ったので、今後システムを組むときの選定ができる。

---
#### 実践 Spring Boot Actuator + Micrometer

| 時間 | 登壇者 | 場所 |
|:-----------:|:------------:|:------------:|
| 14:00 - 14:45 | Tommy Luiwd | Room B |

- 知りたいこと
    - そもそもActuatorを理解してない。
    - >開発に使うだけではもったいない、Actuatorの活用方法をお伝えできればと思います。

- 知れたこと
    - Spring Boot Actuator  
    システムの状態やメトリクスを確認できるため、ヘルスチェックとかで使う。
    - Micrometerって？
        - メトリクスを取得できるようにするライブラリ(であってるかな？)
            https://micrometer.io/
        - Spring に依存しているわけではないが、依存を書くだけで色々なモニタリングサービスにデータを渡せる。
        - メトリクスはカスタマイズして、独自の値が作れる。  
    - Metric Types
        - Gauge（ゲージ）
            - 増減する値
            - 例：CPU使用率とか
        - Counter（カウンター）
            - 増加する値（カウンターでもの足りるものでGaugesは使わない。）
            - 例：リクエスト数とか？
        - Timer（タイマー）
            - 時間
            - 例：HTTPエンドポイントとか、レスポンス時間とか
        - Distribution summary（ヒストグラム）
            - 離散値のようやく
            - リクエストボディサイズの分布
            
    - 使用されたスライド  
    https://docs.google.com/presentation/d/1ChFvgyxoqlA2eX4bwse1VC9vcFpiFYtFSVV1YqbBzt4/edit#slide=id.p
- 感想  
自分は上っ面のアプリ開発しかしていなかったので、こういう世界があることが知れたことが最大の成果。もっと下層を意識するいい機会になった。
---
#### Spring Developer のための コンテナ入門

| 時間 | 登壇者 | 場所 |
|:-----------:|:------------:|:------------:|
| 15:00 - 15:45 | 塚越 啓介 | sola city Hall (EAST) |

- 知りたいこと
    - Kubernetes使った事ないから見てみたい。
    - コンテナ使って何がらくになるのか？

- 知れたこと
    - Jibでdockerイメージが簡単にできる（ここ重要）
    - コンテナの本番環境への問題点
        - コンテナをホストする場所
        - コンテナ障害時のリカバリープラン（クラッシュ前提で考える）
        - スケーリング
    - k8sのコンテナオーケストレータが優秀
    　　- コンテナを管理する技術のこと
    　　- ノードが壊れたら、別の空いてるノードに元の環境を復元してくれたりもする。
- 感想  
Jibだけはすぐに使ってみようと思った。k8sは正直、難しそうだと思って、嫌煙してたけどからこの機会に触ってみる。
---
#### RSocket徹底入門 ~Spring 5.2の目玉機能であるRSocket対応とは~

| 時間 | 登壇者 | 場所 |
|:-----------:|:------------:|:------------:|
| 16:15 - 17:00 | 槙 俊明 | sola city Hall (WEST) |

- 知りたいこと
    - RSocketってなに？
    - どうやって使うの？
    - 既存技術となにが違うの？

- 知れたこと
    - Rsocketとは
      DuplexでMultiplexなバイナリプロトコル（らしいスライド参照）
    - 様々な通信方法
        - Request Response  
        1メッセージを送ると、1メッセージが返却される。
        - Request Stream  
        1メッセージを送ると、メッセージをストリームで返却される。
        - Request Channel  
        メッセージをストリームで送ると、メッセージをストリームで返却する
        - Fire and Foget  
        1メッセージを送るが、返却はない。
    - Duplex 
        - 双方向通信に対応しており、従来のClient-Serverで考えると、どちらかからでも送信ができる。  
        送る側をRequester、受ける側をResponderと呼び、ClientとServerがそのどちらにでもなれる。
    - Reactive Stream
        - "Requester" が "Responder" に処理する分のリクエストを要求する。
    - Session Resumption
        - Streamの途中で切れた場合に再接続してStreamを再開させる。
    - Leasing
        - ”Responder” が ”Requester”に対してリクエストを制限する 
        - RequesterがRespinderに対して、何回のリクエストを送っていいかを制限する。
    - DBの使用条件
        - R2DBC使わないといけない。

    - 使用されたスライド  (正直、むちゃくちゃ詳しく書かれてるから読んだほうがはやい。)
    https://docs.google.com/presentation/d/1ygSM85-RQ3NZjCg6RaZ52mGzxbWiItVwzlCpr1vaWBw/edit#slide=id.g75f375afa0_0_0
- 感想  
このセッションも自分にはまだ早かった（知識不足）  
ただ、通信方法の選定方法によってここまで、システムに影響を与えることができるのは楽しい。
---
#### Spring Social でソーシャルログインを実装する

| 時間 | 登壇者 | 場所 |
|:-----------:|:------------:|:------------:|
| 17:15 - 18:00 | 田中 竜介 | sola city Hall (EAST) |

- 知りたいこと
    - Spring でソーシャルログインライブラリあんの！？
    - どうやって使うの？
    - なんのSNSのライブラリがあるの？
    - Firebaseとどっちが楽なんだろう？

- 知れたこと
    - 楽天さんでもMyBatisつかってるんだな
    - Spring SocialはEOLだが、内容はSpring Security OAuth2.0に継承している。
    - OpenID connect
    - 今までのOAuth2.0はクライアントがリソースサーバへアクセスするときに、ちゃんと認可サーバにて認可されているかを確認する仕組み。
    - OpenID connectはリソースオーナーが認可されてるかを確認する仕組み
    - クライアントはOpenIDプロバイダーを通して、IDトークンを発行してもらう。  
    そのIDトークンをリソースユーザーが認可することで、リソースサーバへのアクセスが可能となる。

    - CommonOAuth2Providerを使用することで下記のSNSログインは簡単に行える。
        - google
        - facebook
        - github
        - Okta

    - 使用されたスライド  
    https://www.slideshare.net/rakutentech/spring-social-206911643

- 感想  
ソーシャルログインって今ではかなり、必須項目だし、認証系はちゃんと理解しないといけない。あと、EOLには気をつけよう。

---
#### 総評
マジでわからん三昧だった。  
自分はプログラマーとして参加することが多くて、基盤とか、技術選定とか、解析とか  
全然業務ではしたことないので、将来的にはここを目指して学習しないといけないんだなと思えた。  
圧倒的にネットワーク技術に対する知識が足りない。それを実装する力はもっと足りない。  
最後に、スピーカーのみなさま、運営、スポンサーのみなさま。ありがとうございました。

--- 
#### 連絡先
ここ間違ってる。ここは消せ。情弱ざまぁwwwなどは 私のTwitter[ https://twitter.com/machin3010 ] までどしどしください。  
普通に凹むので。。。