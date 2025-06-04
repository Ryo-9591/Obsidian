# DBCA(Database Configuration Assistant)
データベースを作成するツール、作成以外にもいろいろできる
![[Pasted image 20250605080624.png]]
## 標準構成か拡張構成を選ぶ
![[Pasted image 20250605081147.png]]
## 標準構成を用いたデータベースの作成

①グローバルデータベース名
②記憶域タイプ　　　　　　　
③データファイルの位置　　　
④高速リカバリ領域
⑤データベース文字セットは選択可能だが、キャラクタセットの選択は不可
⑥管理者パスワード
⑥コンテナ・データベースとしても作成
※OMFは自動的に有効化
## 拡張構成を用いたデータベースの作成

1. デプロイタイプ　　　　データベースの作成時のテンプレートを指定
2. データベース識別情報　グローバルデータベース名とSIDを指定
3. 記憶域オプション　　　ファイルシステム or 自動ストレージ管理、OMFを使用するかも
4. 高速リカバリ　　　　　リカバリのサイズの指定、アーカイブログモードにするかどうか
5. ネットワーク　　　　　リスナーを指定
6. Oracle Data Vault　　　 Oracle Data Vault、Oracle Label Securityを使用するか
7. 構成オプション　　　　メモリー領域のサイズ、データブロックのサイズ、起動プロセスの最大数、キャラクタセット、サンプルスキーマ
8. 管理オプション　　　　Em Expressを構成するか、Enterprise Manager Cloud Controlの管理対象に登録するか
9. ユーザ資格証明　　　　SYS,SYSTEMのパスワードを入力する
10. OMF（Oracle Managed Files）を明示的にON/OFFできる

## ③既存データベースの構成変更　
1. 専用サーバ構成から共有サーバ構成への変更
2. データベースを複製するためのテンプレートを作成

④データベース削除
⑤テンプレの作成と削除
⑥PDBの管理
## Enterprise Manager Cloud Controlへの登録の条件
利用可能なEnterprise Manager Management サーバーが存在し、
ホストにOracle Management Agentもインストールされている場合
