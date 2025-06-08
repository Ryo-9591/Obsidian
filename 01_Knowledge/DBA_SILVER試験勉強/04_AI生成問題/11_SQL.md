# SQL

## 問題1
SQLについて、以下の選択肢から正しいものを1つ選びなさい。

1. SELECT文は、データを取得する
2. SELECT文は、データを更新する
3. SELECT文は、データを削除する
4. SELECT文は、データを挿入する

<details>
<summary>答えと解説</summary>

### 答え
1. SELECT文は、データを取得する

### 解説
SQLの基本文について：
- SELECT：データの取得（検索）
- INSERT：データの挿入
- UPDATE：データの更新
- DELETE：データの削除
- CREATE：オブジェクトの作成
- ALTER：オブジェクトの変更
- DROP：オブジェクトの削除

</details>

## 問題2
SQLについて、以下の記述のうち正しいものを2つ選びなさい。

1. WHERE句は、条件を指定する
2. ORDER BY句は、並び替えを指定する
3. GROUP BY句は、条件を指定する
4. HAVING句は、並び替えを指定する
5. FROM句は、条件を指定する

<details>
<summary>答えと解説</summary>

### 答え
1. WHERE句は、条件を指定する
2. ORDER BY句は、並び替えを指定する

### 解説
SQLの主要な句について：
- WHERE：行の選択条件を指定
- ORDER BY：結果の並び替えを指定
- GROUP BY：グループ化を指定
- HAVING：グループ化後の条件を指定
- FROM：対象テーブルを指定

</details>

## 問題3
SQLについて、以下の選択肢から正しいものを1つ選びなさい。

1. JOINは、複数のテーブルを結合する
2. JOINは、データを更新する
3. JOINは、データを削除する
4. JOINは、データを挿入する

<details>
<summary>答えと解説</summary>

### 答え
1. JOINは、複数のテーブルを結合する

### 解説
JOINの種類と特徴：
- INNER JOIN：両方のテーブルに一致する行を結合
- LEFT OUTER JOIN：左テーブルの全行と右テーブルの一致する行を結合
- RIGHT OUTER JOIN：右テーブルの全行と左テーブルの一致する行を結合
- FULL OUTER JOIN：両方のテーブルの全行を結合
- CROSS JOIN：両方のテーブルの直積を生成

</details>

## 問題4
INSERT文について、以下の記述のうち正しいものを2つ選びなさい。

1. INSERT文は、データを挿入する
2. INSERT文は、データを更新する
3. INSERT文は、データを削除する
4. INSERT文は、データを検索する
5. INSERT文は、データをコピーする

<details>
<summary>答えと解説</summary>

### 答え
1. INSERT文は、データを挿入する
5. INSERT文は、データをコピーする

### 解説
INSERT文の機能：
- 新しい行をテーブルに追加
- SELECT文の結果をテーブルにコピー
- 単一行の挿入と複数行の挿入が可能
- VALUES句とSELECT文の両方を使用可能
- 列名の指定が省略可能

</details>

## 問題5
UPDATE文について、以下の選択肢から正しいものを1つ選びなさい。

1. UPDATE文は、データを挿入する
2. UPDATE文は、データを更新する
3. UPDATE文は、データを削除する
4. UPDATE文は、データを検索する

<details>
<summary>答えと解説</summary>

### 答え
2. UPDATE文は、データを更新する

### 解説
UPDATE文の機能：
- 既存の行のデータを更新
- WHERE句で更新対象を指定
- 複数列の同時更新が可能
- サブクエリを使用した更新が可能
- 条件に合致する行のみを更新

</details>

## 問題6
DELETE文について、以下の記述のうち正しいものを2つ選びなさい。

1. DELETE文は、データを挿入する
2. DELETE文は、データを更新する
3. DELETE文は、データを削除する
4. DELETE文は、データを検索する
5. DELETE文は、データをコピーする

<details>
<summary>答えと解説</summary>

### 答え
3. DELETE文は、データを削除する
4. DELETE文は、データを検索する

### 解説
DELETE文の機能：
- テーブルから行を削除
- WHERE句で削除対象を指定
- 条件に合致する行のみを削除
- 削除前にデータの存在確認が可能
- トランザクション内で実行可能

</details>

## 問題7
CREATE TABLE文について、以下の選択肢から正しいものを1つ選びなさい。

1. CREATE TABLE文は、テーブルを作成する
2. CREATE TABLE文は、テーブルを更新する
3. CREATE TABLE文は、テーブルを削除する
4. CREATE TABLE文は、テーブルを検索する

<details>
<summary>答えと解説</summary>

### 答え
1. CREATE TABLE文は、テーブルを作成する

### 解説
CREATE TABLE文の機能：
- 新しいテーブルを作成
- 列名とデータ型を指定
- 制約（主キー、外部キーなど）を定義
- デフォルト値の設定
- ストレージパラメータの指定

</details> 