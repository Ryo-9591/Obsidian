# Oracle Net Serviceとは・・・
クライアントからOracleデータベースに接続する仕組み
## 役割
・データベース接続の確立
・名前解決
# Oracle Net Service設定に使用するツール３つ
## Oracle Enterprise Manager Cloud Control
GUI、一元管理
## Oracle Net Manager
GUI、ローカルのデータベースサーバーのネーミングメソッドを管理する
## Oracle Net Configuration Assistant
GUI、tnsnames.ora、リスナー、ネーミングメソッド、ネットサービス名、ディレクトリ使用を設定できる
# 接続要求の際の全体図
![[Pasted image 20250531154320.png]]
> [! ]
> クライアント側にもデータベースサーバ側にもOracle Net Serviceの設定が必要！！
# クライアント側でのOracle Net Serviceの設定
## ローカルネーミング
クライアント側にtnsnames.oraを置き、接続情報を得る方法
ファイルパス：`<ORACLE_HOME>/network/admin/tnsnames.ora`
Oracle Net Manager、NetCAで編集できる

tnsnames.ora例：
ORCL =
　(DESCRIPTION = 
　　(ADDRESS = (PROTOCOL =TCP)(HOST = db.oracle.com)(PORT = 1521))
　　(CONNECT_DATA = 
　　　(SERVICE_NAME = orcl.world)
　　)
　)
## SQL Plusでリモート接続
`sqlplus <ユーザ名>/<パスワード>@<接続識別子>`で接続
※ローカルだと`sqlplus <ユーザ名>/<パスワード>`
## 簡易接続ネーミング
接続識別子に接続情報を直接記入する
`sqlplus system/Password123@db.oracle.com:1521/orcl.world`

system・・・ユーザ名
Password123・・・パスワード
db.oracle.com・・・ホスト名
1521・・・ポート
orcl.world・・・サービス名
# データベースサーバー側のOracle Net Serviceの設定
## 動的サービス登録
インスタンスの内部プロセス「LREG」によって行われ「LOCAL＿LISTENER初期化パラメータ」に設定されたアドレスに対して定期的にサービス登録を行い、データベースサービス名とSIDを登録する
→インスタンスが停止したらサービス登録ができない！

LOCAL_LISTENER初期化パラメータ例：
`LOCAL_LISTENER=(ADDRESS = (PROTOCOL=TCP)(HOST=db.oracle.com)(PORT=1521))`
※ポート=1521の場合、LOCAL_LISTENER初期化パラメータを明示的に設定しないでいい
### リスナーにインスタンス情報が登録されているか確認
`lsnrctl services`
・・・
status=READY　←成功なら「READY」と出る！
・・・
## 静的サービス登録
「listener.ora」にあらかじめ「SID_LIST_<リスナー名>」というパラメータに記述しておく
→インスタンスが停止してもサービス登録状態は続く

listener.ora例：
LISTENER =
  (DESCRIPTION =
      (ADDRESS = (PROTOCOL = TCP)(HOST = db.oracle.com)(PORT = 1521))
    )
   )
SID_LIST_LISTENER=
   (SID_LIST=
     (SID_DESC=
        (GLOBAL_DBNAME=orcl.world)
        (SID_NAME=orcl)
     )
   )
  )
### リスナーにインスタンス情報が登録されているか確認
`lsnctl services`
・・・
status=UNKNOWN　←成功していると「UNKNOWN」と出る！
・・・
# 接続失敗時のトラブルシューティング
![[IMG_0070 1.jpg]]
## ①ORA-12154:TSN could not resolve service name
→クライアント側に設定しているtnsnames.oraの問題で名前解決に失敗

・tnsnames.oraにサービス名をちゃんと書いてるか？
・正しいパスに置いているか？
## ②TNS-12541:TNS:no listener
→クライアント側とデータベースサーバー側の問題、tnsnames.oraかリスナーが悪く通信に失敗

・tnsnames.oraに記載してIP、ポートがあっているか
・リスナーが起動しているか？記載したポートで待ち受けているか
## ③ORA-12514:TNS:listener could not resolve SERVICE_NAME given in connect descriptor
→データベースサーバ側でサービスが登録されていないので通信に失敗

・tnsnames.oraに記載したグローバルデータベース名があっているか？
・サービス登録しているか？
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
# データベースリンク
Oracleデータベースと別のOracleデータベースを連携させる仕組み

①接続元データベースにOracle Net Service(tsnnames.ora)の設定
②「CREATE DATABASE LINK文」を発行してデータベースリンクを作成
→「CREATE DATABASE LINK権限」が必要

CREATE DATABASE LINK文例：
`CREATE DATABASE LINK リンク名`
`CONNECT TO ユーザ名 IDENTIFIED BY パスワード`
`USING '接続記述子';`
# Oracle Database Gateway
Oracleデータベースと別のサービス間でデータベースリンクを確立する機能
→異機種間サービスという



