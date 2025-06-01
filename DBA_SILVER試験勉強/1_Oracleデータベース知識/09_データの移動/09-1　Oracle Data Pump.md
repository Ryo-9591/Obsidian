# Oracle Data Pump
データをOracleデータベース外部にエクスポート/インポートするツール
## Oracle Data Pumpの操作インターフェース
### Oracle Data Pumpでのデータエクスポート





### Ctrl+cで対話型インターフェースへ遷移できる(処理はバックグラウンドで実行される)
`expdp system/Password123 FULL=y DUMPFILE=DATA_PUMP_DIR:full.dmp`　--ジョブ起動

`Ctrl + c`　--対話型インターフェースに遷移

実行中の処理は止まらない・・・

exit　→対話型インターフェース終了
## アタッチしたジョブを制御できる
[開始]

Export > expdp system/Password123 attach=SYS_EXPORT_FULL_01　→アタッチして対話型インターフェースへ

Export > STOP_JOB=IMMEDIATE　→アタッチしたジョブを即時停止
Export > START_JOB　→ジョブを再開
Export > STATUS
Export > EXECUTING　→実行中

[終了]