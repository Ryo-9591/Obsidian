# UNDO表領域
変更前の過去データ(UNDOデータ)をUNDOセグメントの格納して管理
## UNDOデータの用途
①トランザクションのロールバック
②読み取り一貫性
③インスタンスリカバリの際のロールバック
④フラッシュバック機能


# UNDO表領域として表領域を使いたいときの手順

①UNDO_MANAGEMET初期化パラメータ=AUTOに設定
②CREATE UNDO TABLESPACE文を実行してUNDO表領域を作成
③UNDO_TABLESPACE初期化パラメータ=UNDO表領域の名前に設定
# UNDO管理問題

CREATE UNDO TABLESPACE undotbs03
DATAFILE 'ファイルパス' SIZE 100M
AUTOEXTEND OFF
RETENTION GUARANTEE ;

ALTER SYSTEM SET UNDO_TABLESPACE=undotbs03 ;
ALTER SYSTEM SET UNDO_RETENTION=900 ;

UNDO表領域が埋まっているときに新しいトランザクションが発行されると・・・

①ORA-30036エラーが出る
なんで？

1. RETENTION GUARANTEEが設定されている
　　→UNDO保存期間(UNDO_RETENTION)に設定した秒数だけ必ず保存されるので、
　　　新しくUNDO表領域が上書きできない！
NOGUARANTEEだと・・・
保存期間内でも古いUNDOを上書きできる

2. AUTOEXTEND OFFが設定されている
　　→UNDO表領域の自動拡張ができない
ONだと・・・
自動拡張になるのでエラーは起きない

---
# 一時UNDO表領域の有効化

TEMP_UNDO_ENABLED=trueに設定
設定すると・・・
一時表領域に格納したデータを変更した際にUNDOの出力先をUNDO表領域から一時表領域に変更できる
→
REDOが生成されず(そもそも一時表領域に格納されているデータ変更にはREDOが生成されない)
UNDOのみ生成(一時表領域に)

---
## UNDOセグメント
・UNDOセグメントには１つまたは複数のトランザクションが対応する
・最後のエクステントがトランザクションで埋まったら・・・
①追加でエクステントが割り当てられる
②最初のエクステントに上書きされる
上記２つの動作をする


上記２つが常にその表領域に格納されるわけではない・・・
例外がある・・・

・一時UNDO機能を使用したときに、UNDOセグメントが一時表領域に格納される
・一時表領域を作成中、一時セグメントが永続表領域に作成される