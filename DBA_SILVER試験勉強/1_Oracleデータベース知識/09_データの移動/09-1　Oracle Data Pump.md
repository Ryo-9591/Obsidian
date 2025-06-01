# Oracle Data Pump
データをOracleデータベース外部にエクスポート/インポートするツール
## Oracle Data Pumpの操作インターフェース
### コマンドライン
### パラメータファイル
### 対話型
`expdp system/Password123 FULL=y DUMPFILE=DATA_PUMP_DIR:full.dmp`--エクスポート開始
`Ctrl + c`　--対話型インターフェースに遷移(バックグラウンドでエクスポート実行中)
`exit`　--対話型インターフェース終了

Export > expdp system/Password123 attach=SYS_EXPORT_FULL_01　→アタッチして対話型インターフェースへ

Export > STOP_JOB=IMMEDIATE　→アタッチしたジョブを即時停止
Export > START_JOB　→ジョブを再開
Export > STATUS
Export > EXECUTING　→実行中

[終了]