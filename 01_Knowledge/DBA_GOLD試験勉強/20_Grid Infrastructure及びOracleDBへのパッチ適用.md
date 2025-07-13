# RU(Release Updates)
リリースに対しての修正(四半期に1度)
# RUR(Release Update Revisions)
RUに対しての修正(四半期に1度)
# Oracle Databaseへのパッチ適用手順
①My Oracle Supportからパッチをダウンロード
②Oracle Databaseとリスナーを停止
③opatch applyコマンドでパッチ適用(OracleDatabaseソフトウェアにパッチの適用)
④Oracle Databaseとリスナーを起動
⑤datapatchコマンドを実行してパッチ適用に伴う修正を適用(Oracle Databaseに対してパッチを適用)
# OPatchコマンド
・パッチ適用
→`$ORACLE_HOME/Opatch/opatch apply`
・パッチのロールバック
・コンフリクト
・パッチのレポート
# datapatchコマンド
`cd $ORACLE_HOME/OPatch`
`./database -verbose`
# opatchautoコマンド
`/u01/app/grid/product/19.0.0/grid/OPatch/opatchauto apply var/tmmp/32895426`

※
/u01/app/grid/product/19.0.0/grid/ → GIホームがあ
/var/tmmp/32895426 → パッチ展開済みファイル