## ②UNDO表領域
変更前の過去データをUNDOセグメントに格納し管理
・１つ以上のデータファイルからなる
# データファイルのブロックサイズについて

特に指定なし
デフォルトのブロックサイズ→「DB_BLOCK_SIZE初期化パラメータ」で指定

指定する
「DB_nK_CACHE_SIZE 初期化パラメータ」で指定したサイズ

---
# bigfile / smallfile 表領域

| 種類        | 説明                              |
| --------- | ------------------------------- |
| smallfile | ✅ デフォルト。複数のデータファイルを持てる。         |
| bigfile   | 1つの超巨大データファイル（最大32TB）を持つ。管理が簡便。 |

---
# データ移動のやり方２選

## オフライン移動
- ALTER TABLE 表領域名 OFFLINE;
- mvなどで移動
- ALETR TABLE 表領域名 RENAME DATAFILEでデータファイルが移動したことを認識させる 
- ALTER TABLE 表領域名 ONLINE

## オンライン移動
- ALTER **DATABASE** MOVE DATAFILE [ファイルパス(ID指定可)] TO [ファイルパス]  [REUSE];
REUSE・・・既存ファイルが存在する場合

# OMF(Oracle Managed Files)

- 初期化パラメータで格納先を設定しておけば、**ファイル名・サイズ指定不要**。
- `CREATE TABLESPACE` 時に `DATAFILE` 句を省略できる。
- 削除時は `DROP TABLESPACE` だけで**データファイルごと削除**（OMF管理なら）。

①初期化パラメータでOMF管理するデータファイルの格納先を指定(必須)
`ALTER SYSTEM SET DB_CREATE_FILE_DEST='/u01/app/oracle/omf';`


| 初期化パラメータ                               | 管理対象のファイル                                                                 |
| -------------------------------------- | ------------------------------------------------------------------------- |
| DB_CREATE_FILE_DEST                    | データファイル<br>一時ファイル<br>制御ファイルとREDOファイル<br>(DB_CREATE_ONLINE_LOG_DEST_nが未設定) |
| DB_CREATE_ONLINE_LOG_DEST_n(n=1,2,...) | 制御ファイルとREDOファイル                                                           |
| DB_RECOVERY_FILE_DEST                  | リカバリ関連ファイル<br>制御ファイルとREDOファイル                                             |

②データファイル名を指定せずに表領域作成
`CREATE TABLESPACE omf_tbs DATAFILE SIZE100M;`
→OMF管理となり、①で指定した'/u01/app/oracle/omf'に表領域が格納

`CREATE TABLESPACE omf_tbs;`
→OMF管理となり＋'/u01/app/oracle/omf'に表領域格納＋データファイルのAUTOEXTENDが有効

③表領域削除
`DROP TABLESPACE omf_tbs;`
→OMF管理された表領域は制御ファイルだけでなくデータファイルからも自動削除
