# SQL*Plus

## 1. 概要
SQL*Plusは、Oracleデータベースに接続して操作を行うためのコマンドラインツールです。データベースがオープンしている必要があります。

## 2. 接続方法

### 2.1 データベース接続あり
```sql
-- SYSTEMユーザーでの接続
sqlplus system/Password123

-- SYSユーザーでの接続（SYSDBA権限）
sqlplus sys/Password123 as sysdba
```

### 2.2 データベース接続なし
```sql
-- 接続なしで起動
sqlplus /nolog

-- その後接続
CONNECT system/Password123
```

### 2.3 OS認証
```sql
-- SYSユーザーでOS認証
sqlplus / as sysdba
```

## 3. 主要コマンド

### 3.1 基本操作コマンド
| コマンド | 説明 | 使用例 |
|---------|------|--------|
| CONNECT | データベース接続 | `CONNECT user/pass` |
| EXIT | 終了 | `EXIT` |
| HOST | シェルコマンド実行 | `HOST dir *.sql` |

### 3.2 表示制御コマンド
| コマンド | 説明 | 使用例 |
|---------|------|--------|
| COLUMN | 列表示設定 | `COLUMN TYPE_NAME FORMAT A30` |
| DESCRIBE | オブジェクト仕様表示 | `DESCRIBE employee_list` |
| SHOW | 環境設定表示 | `SHOW REL` |

### 3.3 スクリプト関連コマンド
| コマンド | 説明 | 使用例 |
|---------|------|--------|
| @ | スクリプト実行 | `@PRINTRPT` |
| DEFINE | 変数定義 | `DEFINE ID = USER_NAME` |
| UNDEFINE | 変数削除 | `UNDEFINE USER_ID` |

### 3.4 インスタンス制御コマンド
| コマンド | 説明 | 使用例 |
|---------|------|--------|
| STARTUP | インスタンス起動 | `STARTUP` |
| SHUTDOWN | インスタンス停止 | `SHUTDOWN` |

### 3.5 PL/SQL実行コマンド
| コマンド | 説明 | 使用例 |
|---------|------|--------|
| EXECUTE | PL/SQL実行 | `EXECUTE dbms_output.put_line('実行')` |

## 4. 便利な機能

### 4.1 環境設定
```sql
-- システム変数の設定
SET DEFINE
SET LINESIZE 100
SET PAGESIZE 50
```

### 4.2 レポート作成
```sql
-- 列見出しの設定
COLUMN dept_name HEADING '部署名'
COLUMN emp_name HEADING '社員名'

-- 区切り線の表示
SET UNDERLINE =
```

## 5. ベストプラクティス

### 5.1 推奨事項
- 適切な権限での接続
- スクリプトの活用
- 環境設定の統一
- エラーハンドリング

### 5.2 注意点
- パスワードの取り扱い
- 権限の適切な使用
- スクリプトのバックアップ
- セッション管理
