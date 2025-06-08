# Oracle Net Service

## 1. 概要
Oracle Net Serviceは、クライアントからOracleデータベースに接続するための仕組みです。

### 1.1 主な役割
- データベース接続の確立
- 名前解決
- ネットワーク通信の管理

## 2. 設定ツール

### 2.1 Oracle Enterprise Manager Cloud Control
- GUIベースの管理ツール
- 複数データベースの一元管理が可能

### 2.2 Oracle Net Manager
- GUIベースの設定ツール
- ローカルのデータベースサーバーのネーミングメソッドを管理

### 2.3 Oracle Net Configuration Assistant
- GUIベースの設定ツール
- 以下の設定が可能：
  - tnsnames.ora
  - リスナー
  - ネーミングメソッド
  - ネットサービス名
  - ディレクトリ使用

## 3. 接続設定

### 3.1 クライアント側の設定

#### 3.1.1 ローカルネーミング
- クライアント側にtnsnames.oraを配置
- ファイルパス：`<ORACLE_HOME>/network/admin/tnsnames.ora`
- 設定例：
```tnsnames
ORCL =
  (DESCRIPTION = 
    (ADDRESS = (PROTOCOL =TCP)(HOST = db.oracle.com)(PORT = 1521))
    (CONNECT_DATA = 
      (SERVICE_NAME = orcl.world)
    )
  )
```

#### 3.1.2 簡易接続ネーミング
- 接続識別子に直接接続情報を記述
- 形式：`sqlplus system/Password123@db.oracle.com:1521/orcl.world`
  - system：ユーザ名
  - Password123：パスワード
  - db.oracle.com：ホスト名
  - 1521：ポート
  - orcl.world：サービス名

### 3.2 サーバー側の設定

#### 3.2.1 動的サービス登録
- LREGプロセスによる自動登録
- LOCAL_LISTENER初期化パラメータで設定
- インスタンス停止時は登録不可
- 確認方法：`lsnrctl services`（status=READY）

#### 3.2.2 静的サービス登録
- listener.oraに手動で設定
- インスタンス停止時も登録状態を維持
- 確認方法：`lsnrctl services`（status=UNKNOWN）

## 4. トラブルシューティング

### 4.1 一般的なエラー

#### 4.1.1 ORA-12154
- 原因：tnsnames.oraの問題
- 確認事項：
  - サービス名の記述
  - ファイルの配置場所

#### 4.1.2 TNS-12541
- 原因：通信設定の問題
- 確認事項：
  - IPアドレスとポート番号
  - リスナーの起動状態

#### 4.1.3 ORA-12514
- 原因：サービス未登録
- 確認事項：
  - グローバルデータベース名
  - サービス登録状態

### 4.2 接続確認
- tnspingユーティリティの使用
- 例：`tnsping ORCL`

## 5. 高可用性機能

### 5.1 接続時フェイルオーバー
- プライマリ接続失敗時にセカンダリに接続
- FAILOVER = ONで設定

### 5.2 接続時ロードバランシング
- 負荷分散のためのランダム接続
- LOAD_BALANCE = ONで設定

### 5.3 透過的アプリケーションフェイルオーバー(TAF)
- 接続切断時の自動再接続
- 実行中のSELECT文を継続
- 接続時フェイルオーバーと併用可能

## 6. 環境変数
- TNS_ADMIN：設定ファイルの代替配置場所を指定
- 対象ファイル：
  - tnsnames.ora
  - listener.ora
  - sqlnet.ora

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
status=READY　←成功なら「<font color="#ffff00">READY</font>」と出る！
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
`lsnrctl services`
・・・
status=UNKNOWN　←成功していると「<font color="#ffff00">UNKNOWN</font>」と出る！
・・・
# 接続失敗時のトラブルシューティング
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
負荷分散のためランダムに接続し、失敗したら終わり

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
ランダムに選んで接続し、失敗したらランダムなアドレスに接続

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

# 透過的アプリケーションフェイルオーバー(TAF)
接続確立後、意図せずに接続が切断された際に、接続を再確立して実行中のSELECT文を接続後、シームレスに行う機能
接続時フェイルオーバーと併用できる

