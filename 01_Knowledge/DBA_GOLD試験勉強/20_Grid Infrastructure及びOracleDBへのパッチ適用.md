# RU(Release Updates)
リリースに対しての修正(四半期に1度)
# RUR(Release Update Revisions)
RUに対しての修正(四半期に1度)
# Oracle Databaseへのパッチ適用手順
①My Oracle Supportからパッチをダウンロード
②Oracle Databaseとリスナーを停止
③opatch applyコマンドでパッチ適用
④Oracle Databaseとリスナーを起動
⑤datapatchコマンドを実行してパッチ適用に伴う修正を適用
# OPatchコマンド
・パッチ適用
→$ORACLE_HOME/Opat
・パッチのロールバック
・コンフリクト
・パッチのレポート