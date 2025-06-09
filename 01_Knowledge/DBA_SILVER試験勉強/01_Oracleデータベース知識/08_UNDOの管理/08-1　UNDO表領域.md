# UNDO表領域
変更前の過去データ(UNDOデータ)をUNDOセグメントの格納して管理
デフォルトで「UNDOTBS1」が作成される
## UNDOデータの用途
①トランザクションのロールバック
②読み取り一貫性
③インスタンスリカバリの際のロールバック
④フラッシュバック機能
## UNDOセグメント
1つまたは複数のトランザクションに対して1つのUNDOセグメントが対応し、変更前のデータ(UNDOデータ)がそのUNDOセグメントに格納

※最後のエクステントがトランザクションで埋まったら、追加でエクステントが割り当てられるか、最初のエクステントに上書きされる
# UNDO表領域の作成
## ①「UNDO_MANAGEMET初期化パラメータ」をAUTOに設定
`ALTER SYSTEM SET UNDO_MANAGEMENT=AUTO;`
## ②CREATE UNDO TABLESPACE文を実行してUNDO表領域を作成

UNDO表領域作成例：
`CREATE UNDO TABLESPACE undotbs03`
`DATAFILE 'ファイルパス' SIZE 100M`
`AUTOEXTEND OFF`　--エクステントの自動拡張OFF
`RETENTION GUARANTEE ;`　--UNDO保存期間の保証
`ALTER SYSTEM SET UNDO_RETENTION=900 ;`　--UNDOの保存期間900秒

※UNDO表領域が埋まっているときに新しいトランザクションが発行されるとORA-30036エラーが出る
→「RETENTION GUARANTEE」が設定されている
### UNDO保存期間の保証
#### RETEMTION GUARANTEE
「UNDO_RETENTION初期化パラメータ」に設置した秒数「UNDO保存期間」の保証をする
コミットされてからUNDO_RETENTION初期化パラメータ分だけ保存されそのあとは
#### RETENTION NOGUARANTEE
保存期間内でも古いUNDOを上書きできる
## ③「UNDO_TABLESPACE初期化パラメータ」をUNDO表領域の名前に設定
`ALTER SYSTEM SET UNDO_TABLESPACE=undotbs03 ;`

※有効化できるUNDO表領域は1つ
