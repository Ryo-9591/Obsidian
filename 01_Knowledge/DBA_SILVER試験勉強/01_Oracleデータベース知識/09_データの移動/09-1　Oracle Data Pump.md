# Oracle Data Pump
データをOracleデータベース外部にエクスポート/インポートするツール
## Oracle Data Pumpの操作インターフェース
### コマンドライン
`expdp user0/Pass123 SCHEMAS=user0 DUMPFILE=dmp_dir:test1.dmp LOGFILE=dmp_dir:test1.log`
### パラメータファイル
`expdp user0/Pass123 PARFILE=exp.par`
### 対話型
`expdp system/Password123 FULL=y DUMPFILE=DATA_PUMP_DIR:full.dmp`--エクスポート開始
`Ctrl + c`　--対話型インターフェースに遷移(バックグラウンドでエクスポート実行中)
`exit`　--対話型インターフェース終了

`expdp system/Password123 attach=SYS_EXPORT_FULL_01`　--アタッチして対話型インターフェースへ
`STOP_JOB=IMMEDIATE`　→アタッチしたジョブを即時停止
`START_JOB`　→ジョブを再開
`STATUS`　--ステートタス表示(EXECUTING(実行中))

