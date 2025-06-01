# AS SELECT FROM文

CREATE TABLE emp_copy AS SELECT * FROM employee ;

この情報からわかることは・・・
①employee表のすべてがコピーされる
②NOT NULL制約のみがコピーされる

---
