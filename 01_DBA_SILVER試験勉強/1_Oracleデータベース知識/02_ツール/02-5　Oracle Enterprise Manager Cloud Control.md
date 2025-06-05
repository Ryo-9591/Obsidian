# Oracle Enterprise Manager Cloud Control
複数のサーバーに配置された複数のデータベースを一元管理できるツール
![[Pasted image 20250605215829.png]]
## 構成要素
### OMS(Oracle Management Service)
Webベースで管理コンソールを提供するwebアプリ
### OMR(Oracle Management)
管理情報や、収集したデータを管理するデータベース
### OMA(Oracle Management Agent)
管理対象サーバ上の管理ターゲットの制御および情報の収集


DBCAから条件(OMS（Oracle Management Service）とOMA（Agent）)ありで登録可能
外部ツール(データベースオープンじゃなくてもいい)
管理対象は、OMA、OMS、リポジトリデータベース

1. ﻿インスタンス （データベース）の起動／停止
2. ﻿﻿Oracle Net Services の設定
3. ﻿スキーマ（表／素引など）の管理
4. ﻿ジョブの管理および実行
5. ﻿バックアップ／リカバリ
6. ﻿データベースリソースマネージャ
7. ﻿パッチ推奨（My Oracle Support パッチ取得）