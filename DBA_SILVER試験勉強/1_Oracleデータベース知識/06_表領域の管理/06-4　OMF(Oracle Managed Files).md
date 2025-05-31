# OMF(Oracle Managed Files)

・「DB_CREATE_FILE_DEST初期化パラメータ」で格納先を設定しておけば、ファイル名・サイズ指定不要
・`CREATE TABLESPACE` 時に `DATAFILE` 句を省略できる
・削除時は `DROP TABLESPACE` だけでデータファイルごと削除

## ①初期化パラメータでOMF管理するデータファイルの格納先を指定(必須)
`ALTER SYSTEM SET DB_CREATE_FILE_DEST='/u01/app/oracle/omf';`

| 初期化パラメータ                               | 管理対象のファイル                                                                 |
| -------------------------------------- | ------------------------------------------------------------------------- |
| DB_CREATE_FILE_DEST                    | データファイル<br>一時ファイル<br>制御ファイルとREDOファイル<br>(DB_CREATE_ONLINE_LOG_DEST_nが未設定) |
| DB_CREATE_ONLINE_LOG_DEST_n(n=1,2,...) | 制御ファイルとREDOファイル                                                           |
| DB_RECOVERY_FILE_DEST                  | リカバリ関連ファイル<br>制御ファイルとREDOファイル                                             |

## OMF管理表領域の作成

前提






`CREATE TABLESPACE omf_tbs DATAFILE SIZE100M;`
→OMF管理となり、①で指定した'/u01/app/oracle/omf'に表領域が格納

`CREATE TABLESPACE omf_tbs;`
→OMF管理となり＋'/u01/app/oracle/omf'に表領域格納＋データファイルのAUTOEXTENDが有効

## 表領域削除
`DROP TABLESPACE omf_tbs;`
→OMF管理された表領域は制御ファイルだけでなくデータファイルからも自動削除
