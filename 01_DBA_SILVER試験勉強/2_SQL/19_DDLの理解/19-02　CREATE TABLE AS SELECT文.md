# CREATE TABLE AS SELECT文
問い合わせ結果をもとに表を作成してデータを移行する文
## 表定義とデータをコピーする
`CREATE TABLE emp_copy AS SELECT * FROM employee ;`

①employee表のすべてがコピーされる
②NOT NULL制約のみがコピーされる
## 表定義だけコピーする
`CREATE TABLE emp_copy AS SELECT * FROM employee where 1=0`

①employee表の表定義のみでデータはコピーされない
②制約はNOT NULLのみがコピーされる