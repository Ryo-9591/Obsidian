# ALTER TABLE ADD(列の追加)
`ALTER TABLE employees ADD hire_date DATE;`
# ALTER TABLE MODIFY(列の定義の変更)
`ALTER TABLE employees MODIFY salary NUMBER(10, 2);`
# ALTER TABLE DROP(列の削除)
`ALTER TABLE employees DROP COLUMN hire_date;`
# ALTER TABLE SET UNUSED(列の未使用化)
列を削除には時間がかかる
→未使用にするのはすぐなので未使用→消すがいい
`ALTER TABLE emp2 SET UNUSED COLUMN sal;`
`ALTER TABLE emp2 DROP UNUSED COLUMNS;`
