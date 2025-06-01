# Oracle Data Pump
データをOracleデータベース外部にエクスポート/インポートするツール


# Oracle Data Pumpの操作インターフェース

## Ctrl+cで対話型インターフェースへ遷移できる(処理はバックグラウンドで実行される)
[開始]

Export > expdp system/Password123 FULL=y DUMPFILE=DATA_PUMP_DIR:full.dmp　→ジョブ起動
Export > [Ctrl + c]　→対話型インターフェースに遷移

実行中の処理は止まらない・・・

Export > exit　→対話型インターフェース終了

[終了]
## アタッチしたジョブを制御できる
[開始]

Export > expdp system/Password123 attach=SYS_EXPORT_FULL_01　→アタッチして対話型インターフェースへ

Export > STOP_JOB=IMMEDIATE　→アタッチしたジョブを即時停止
Export > START_JOB　→ジョブを再開
Export > STATUS
Export > EXECUTING　→実行中

[終了]

---
# SQL* Loaderとは

OSファイルシステム上のデータをOracleデータベースの表にロードするツール

概念図：
![[Pasted image 20250517084154.png]]
　　
| 対象      | 説明                    |
| ------- | --------------------- |
| データファイル | ロード対象のデータを含むファイル      |
| 制御ファイル  | データをロードする表やデータファイルの設定 |
| ログファイル  | ログを出力                 |
| 廃棄ファイル  | ロード対象外のレコードを出力        |
| 不良ファイル  | エラーによりロードされなかったデータを出力 |

---
# 制御ファイルの記述例

LOAD DATA
INFILE 'data.csv'　　データファイル
INFO TABLE tbl01　ロード先
APPEND　追加ロード
FIELDS TERMINATED BY ' , '　カンマ区切りでフィールドを分割
(no , name)　フィールドのデータをno列,name列にロード

---
# SQL* Loaderによるcsvファイルのロード

`sqlldr user1/pass1 control=csv.ctl`

---
# SQL* Loaderエクスプレスモードによるcsvファイルのロード

`sqlldr user1/pass1 TABLE=data`
## 特徴

・制御ファイルを使用しない
・TABLEで指定したテーブル名.datでロードされる
・自動的にAPPENDモード
・ロードの並列度も自動で設定

## ログファイルに生成される内容

・実行した処理に対応する制御ファイルの内容
→エキスプレスモードでない場合の実行をしたときに使えるように出力される
・内部で実行されるSQLの内容
→SQLスクリプトではない

---
# 外部表

外部ファイルを表のように扱うことができる仕組み
csvファイルにSELECT文が実行できる
## ORACLE_LOADERアクセスドライバ

サーバ内の外部ファイルをデータベースの表にロードすることなくSELECT文で問い合わせることができる

## ORACLE_DATAPUMPアクセスドライバ

複雑な問い合わせ結果をダンプファイルとしてアンロードして別のデータベースに転送してロードできる