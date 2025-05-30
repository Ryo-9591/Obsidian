# Oracle Net ServiceとOracle Net Configuration Assistant
## Oracle Net Service
幅広い範囲のOracle Net Servicesの設定を実行できるGUIツール
ローカルのデータベースサーバーのネーミングメソッドを管理できる
## Oracle Net Configuration Assistant
tnsnames.ora、リスナー、ネーミングメソッド、ネットサービス名、ディレクトリ使用を設定できるGUIツール

---
# クライアントサーバーとデータベースサーバーの接続方法２種

## ①クライアントサーバー側で設定する方法

### ローカルネーミング

クライアント側にtnsnames.oraを置き、接続情報を得る方法
ファイルパス：`<ORACLE_HOME>/network/admin/tnsnames.ora`

Oracle Net Managerで編集できる

### SQL Plusでリモート接続

sqlplus <ユーザ名>/<パスワード>@<接続識別子>

で接続

※ローカルだと
sqlplus <ユーザ名>/<パスワード>

### 簡易接続ネーミング

接続識別子に接続情報を直接記入する

`sql plus system/Password123@db.oracle.com:1521/orcl.world`

## ② データベースサーバー側でサービスを登録しておく方法

###  インスタンスのサービス登録

リスナーはデータベースの接続要求を中継するために、データベースの構成情報、起動状態をリスナーに登録しておく必要がある

### 動的サービス登録

インスタンスが自分の情報をリスナーに登録する
→インスタンスが停止するとサービスの登録状態が切れる

LREGによって行われLOCAL＿LISTENER初期化パラメータにせってされたアドレスに対して定期的にサービス登録を行い、データベースサービス名とSIDを登録する。

| データベース名(データベースの識別子) | インスタンスSID(インスタンスの識別子) |
| ------------------- | --------------------- |
| orcl.world          | orcl                  |
PORTが1521の場合、LOCAL_LISTENERを明示的に設定しないでいい
サービスの登録確認をすると、`status=ready`になる

### 静的サービス登録

listener.oraにあらかじめ「SID_LIST_<リスナー名>」というパラメータに記述しておく
→インスタンスが停止してもサービス登録状態は続く

サービスの登録確認をすると、`status=UNKNOWN`になる

# 接続失敗時のトラブルシューティング

## ①ORA-12154:TSN could not resolve service name
→サービス名の解決ができない
### 原因
クライアント側の名前解決に失敗している
→tnsnames.oraに接続識別子がちゃんと書かれているか？
→tnsnames.oraを正しいファイルパスに置いているか？
## ②TNS-12541:TNS:no listener
→リスナーがない
### 原因
リスナーとの通信に失敗する
→tnsnames.oraに記載してIP、ポートがあっているか
→リスナーが起動しているか？記載したポートで待ち受けているか
## ③ORA-12514:TNS:listener could not resolve SERVICE_NAME given in connect descriptor
→接続識別子で記載されているサービスを認識できない
### 原因
データベースサーバ側でサービスが登録されていない
→tnsnames.oraに記載したグローバルデータベース名があっているか？
→サービス登録しているか？

## 接続確認
tnsping ユーティリティ

`tnsping ORCL`
# TNS_ADMIN環境変数

tnsnames.ora、listener.ora、sqlnet.oraをデフォルト以外の場所に置きたいときに使用
# 接続時フェイルオーバーと接続時ロードバランシング

## 接続時フェイルオーバー

上から接続してだめなら2番目

tnsnames.oraの内容：

ORCL2 =
  (DESCRIPTION =
    (FAILOVER = ON)
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = db.oracle.com)(PORT = 1521))
      (ADDRESS = (PROTOCOL = TCP)(HOST = db.oracle.com)(PORT = 1522))
    )
    (CONNECT_DATA =
      (SERVER = DEDICATED)
      (SERVICE_NAME = orcl.world)
    )
  )
## 接続時ロードバランシング

負荷分散のためランダムに接続

tnsnames.oraの内容：

ORCL2 =
  (DESCRIPTION =
    (LOAD_BALANCE = ON)
    (FAILOVER = OFF)
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = db.oracle.com)(PORT = 1521))
      (ADDRESS = (PROTOCOL = TCP)(HOST = db.oracle.com)(PORT = 1522))
    )
    (CONNECT_DATA =
      (SERVER = DEDICATED)
      (SERVICE_NAME = orcl.world)
    )
  )
## 接続時フェイルオーバーと接続時ロードバランシングの併用

ランダムに選んで接続

tnsnames.oraの内容：

ORCL2 =
  (DESCRIPTION =
    (FAILOVER = ON)
    (LOAD_BALANCE = ON)
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = db.oracle.com)(PORT = 1521))
      (ADDRESS = (PROTOCOL = TCP)(HOST = db.oracle.com)(PORT = 1522))
    )
    (CONNECT_DATA =
      (SERVER = DEDICATED)
      (SERVICE_NAME = orcl.world)
    )
  )

# 共有サーバでのそれぞれのパーツの役割

![[Pasted image 20250527221634.png]]

①ディスパッチャ　接続要求応答
②共有サーバプロセス　SQLと要求キューから取り出し、実行結果を応答キューに詰める

# データベースリンク

プライベートデータベースリンク
→CREATE DATABASE LINK権限が必要

記述例：
基本的には名前解決できる方のユーザがあるサーバ上で実行する

CREATE DATABASE LINK リンク名
CONNECT TO ユーザ名 IDENTIFIED BY パスワード
USING '接続記述子';

※Oracle Database Gatewayを使えば異機種間でのデータリンクができる



