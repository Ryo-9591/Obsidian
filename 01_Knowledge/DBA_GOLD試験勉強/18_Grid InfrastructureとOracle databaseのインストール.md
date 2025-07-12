## Oracle restart
シングルインスタンスのoracle databaseの可用性を高める機能
**OracleソフトウェアにGIを導入したサーバーの構成**
## Oracle Clusterware
GIに含まれるコンポーネント(インスタンス、リスナー)の管理をするクラスタソフトウェア
## GI管理でのクラスタリソースのふるまい
### リスナー
通常：Oracleホームから起動
GI管理：Gridホームから起動
### データベースサービス
通常：SERVICE_NAMESにサービス名を指定してDBMS_SERVICEパッケージのプロシージャで管理する
GI管理：SRVCTLコマンドで構成管理
## crsctl status resorceコマンド
クラスタリソースの起動状態の表示
`crsctl status resource -t`
## Oracle ASM
複数の物理ストレージ(**ASMディスク**)をまとめて単一の仮想ストレージ(**ASMディスクグループ**)として扱うことができる仕組み
### ストライピング
### 