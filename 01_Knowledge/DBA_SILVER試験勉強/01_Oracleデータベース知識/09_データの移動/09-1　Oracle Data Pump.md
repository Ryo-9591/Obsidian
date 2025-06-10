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

# エクスポート例

`expdp scott/tiger　--動作モードの指定がないためスキーマモード`
`DUMFILE=directory01:exp_%U.dmp`　
`FILESIZE=1G　--ダンプファイルの最大サイズは1G`
`PARALLEL=2　--パラレル処理のスレッド数`
`LOGFILE=directory01:/exp_01.log`　
`JOB_NAME=exp_01　--ジョブ名を指定、しないと「SYS_EXPORT」から始まるジョブ名が自動でつく`

# インポート例

impdp system/oracle
SCHEMAS=hr,oe　
REMAP_SCHEMA=hr_dev:hr　--
DUMPFILE=orcl.dmp
EXCLUDE=FUNCTION
TABLE_EXISTS_ACTION=APPEND
LOGFILE=impdp01.log