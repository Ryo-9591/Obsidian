# 条件の評価順序

① =, != ,< , > , <=
② IS NULL , LIKE , BETWEEN
③ NOT
④ AND
⑤ OR

where dep_id>30 AND job_id IN ('1' , '2' , '#') OR salaly>4000

だと、
dep_id