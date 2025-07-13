# Oracle restart
シングルインスタンスのoracle databaseの可用性を高める機能
**OracleソフトウェアにGIを導入したサーバーの構成**
# Oracle Clusterware
GIに含まれるコンポーネント(インスタンス、リスナー)の管理をするクラスタソフトウェア
# GI管理でのクラスタリソースのふるまい
## リスナー
通常：Oracleホームから起動
GI管理：Gridホームから起動
## データベースサービス
通常：SERVICE_NAMESにサービス名を指定してDBMS_SERVICEパッケージのプロシージャで管理する
GI管理：SRVCTLコマンドで構成管理
# crsctl status resorceコマンド
クラスタリソースの起動状態の表示
`crsctl status resource -t`
# Oracle ASM
複数の物理ストレージ(**ASMディスク**)をまとめて単一の仮想ストレージ(**ASMディスクグループ(ASMCAで作成可能)**)として扱うことができる仕組み
※I/O動作はOracle DBの方でやるのでDBWnとかは使うただそれ以下はASM(OSデータファイルを使わないでAMSディスクにデータを格納)
# インストール時のASM
GIインストール後に自動的に導入される。
インストール時のディスクグループは1つ
ASMを使用するOSユーザにはセカンダリグループとして、OSASM,OSDBAをに所属させる必要がある
### ストライピング
AU(Allocation Unit)単位で異なるASMディスクに分散保存しI/O性能を高めることできる
### ミラーリング
多重化し可用性を向上させることできる
# スタンドアロンサーバ用Grid Infrastractureの構成

# Oracle Resatrtの起動停止
※gridユーザで使用
## 起動
`crsctl start has` 
## 自動起動設定
`crsctl enable has`
## 停止
`crsctl stop has`
## 自動停止設定
`crsctl disable has`
