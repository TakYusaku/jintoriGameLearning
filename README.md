# Jintori GAME 
unfinished...
## directory structure
```
.
├── README.md
├── api
│   └── [source code (python)]
├── docker
│   ├── aws
│   │   └── Dockerfile
│   ├── go_server
│   │   └── [Dockerfile]
│   ├── memo.txt
│   └── ubuntu
│       └── [Dockerfile]
├── jinGame
│   ├── [source code (python)]
│   ├── log
│   ├── save
│   │   ├── history
│   │   │   ├── eval
│   │   │   │   ├── [csv file]
│   │   │   └── learn
│   │   │       └── [csv file]
│   │   ├── parameter
│   │   │   └── [date(directory)]
│   │   │       └── [pt file (network parameter)]
│   │   └── replay_memory
│   │       └── [binary file]
│   └── tmp
├── other
├── rule-jintori.txt
└── server-field
    ├── [go file]
    └── memo.txt
```

* api (directory)  
フィールド情報を取得したり，エージェントを操作するapiを実装したソースコード(python)  
* docker (directory)  
    * go_server(directory)  
    server-field(directory)にあるgo-langファイルを実行できる環境を構築するDockerfile  
    * ubuntu(directory)  
    エージェントの学習のための環境を構築するDockerfile  
* jinGame(directory)  
エージェントを学習させるソースコードと，logデータを保存するdirectory  
    * log(directory)  
    学習開始時刻と終了時刻を記録する  
    * save(directory)  
    学習のログ，ネットワークパラメータ，replaymemoryの保存  
        * history(directory)  
        学習時(learn)と評価時(eval)のログを保存する  
        * parameter(directory)  
        ネットワークパラメータの保存  
        * replay_memory(directory)  
        replay memoryのバイナリデータ
* server-field(diectory)  
    フィールドを構成するgo-langファイル  

## dockerfile
DQN学習は, (cpu環境では)docker/ubuntu/ にあるDockerfileを使ってください  
(gpu環境では)docker/aws/ にあるDockerfileを使ってください  

## docker を立ち上げる時の注意
### localで作業をする場合
> docker run -it -d -p 8001:8000 -v [host側の作業ディレクトリ(このjintoriGameのディレクトリ)]:/home/develop --name [image名] [container名] bash  

でrunしてください.

### awsで作業をする場合
* ローカル(ホスト)のディレクトリにコンテナのディレクトリをマウントできるなら，'localで作業をする場合'と同じ操作をしてください．  
* ローカル(ホスト)のディレクトリにコンテナのディレクトリをマウントできないなら，このようにportだけ通してください．
> docker run -it -d -p 8001:8000 --name [image名] [container名] bash 
  

## dqnの実行の仕方
1.server-field/jintori-field.go を 'go run jintori-field.go'で実行する  
(1.5 jinGame/jin_parameter.py で学習回数を変更する)  
2.jinGame/jin_execute.py を 'python3 jin_execute.py'で実行する.
## jinGameのソースコードについて  
* jin_NN.py  
ネットワークの構成  
* jin_agent.py  
学習，評価に関する処理を記述したソース  
* jin_consts.py  
データ・ログの保存先を記したファイル  
* jin_execute.py  
学習・評価を実行する  
* jin_init_parameter_optim.py  
楽観的初期化のためのソース  
* jin_jinGame.py  
陣取りゲームを行うために必要な機能集  
* jin_parameter.py    
Epoch, Evaluation, Set 数を記したファイル  
* jin_replayMemory.py  
replay memory を構成するソース  
* jin_util.py  
現在時刻等を取得し，変換するソース

## 'save' directory の中身について
