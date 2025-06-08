# SQL *Plus

外部ツールだけど、データベースがオープンしてないと使用できない
## ①起動、ログイン
### systemユーザ(データベース接続あり)
sqlplus system/Password123
### systemユーザ(データベースなし)
sqlplus /nolog
CONNECT system/Password123
### sysユーザ
sqlplus sys/Password123 ==as sysdba==
sysユーザは権限を持ちすぎるのであえてsysdbsで入る
### sysユーザ(OS認証)
sqlplus / as sysdba
## ②コマンド集
覚え方：Hu-Desc 
HU1 DE2 S4 C2

| SQL*Plusコマンド | コマンド説明                     | 使用例                                            |
| ------------ | -------------------------- | ---------------------------------------------- |
| @(アットマーク)    | 指定したスクリプトのSQL*Plus文を実行     | @PRINTRPT  <br>@WKRPT.QRY                      |
| COLUMN       | 特定列の表示設定を指定                | COLUMN TYPE_NAME  <br>FORMAT A30               |
| CONNECT      | 指定したユーザー名でデータベースへ接続        | CONNECT user/user_pass                         |
| DEFINE       | ユーザー変数または定義定数の設定と表示        | DEFINE ID = USER_NAME                          |
| DESCRIBE     | 指定したファンクションまたはプロシージャの仕様を表示 | DESCRIBE employee_list                         |
| EXECUTE      | PL/SQLサブプログラムを実行           | EXECUTE dbms_output.  <br>put_line(‘プロシージャ実行’) |
| EXIT         | SQL*Plusを終了                | EXIT                                           |
| HOST         | シェルでコマンドの実行                | HOST dir *.sql                                 |
| SET          | システム変数を設定                  | SET DEFINE                                     |
| SHOW         | 現行のSQL*Plus環境や値を表示         | SHOW REL                                       |
| SHUTDOWN     | Oracle Databaseインスタンスを停止   | SHUTDOWN                                       |
| STARTUP      | Oracle Databaseインスタンスを起動   | STARTUP                                        |
| UNDEFINE     | ユーザー定義定数の削除                | UNDEFINE USER_ID                               |
