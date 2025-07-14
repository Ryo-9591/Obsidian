# Oracle Databaseアップグレード手順
①新しいリリースのOracle Databaseソフトウェアをインストールする
②データベース外部のファイル(Oracle Net Servicesの設定ファイルなど)を新しい環境に引き継ぐ
③古いリリースのOracleデータベースに格納されたデータを引き継ぐ
## パターン①
DBUA(Database Upgrade Assistant), AutoUpgradeかアップグレードスクリプトを実行
→データベースそのものを変換するから直接アップグレードという
※現行と新サーバーは同じOS,CPU種別である必要がある
## パターン②
Data Pumpなどを用いて新しいリリースにデータを転送する
