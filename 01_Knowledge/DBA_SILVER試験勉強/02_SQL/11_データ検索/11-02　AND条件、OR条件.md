# 条件の評価順序
① =, != ,< , > , <=
② IS NULL , LIKE , BETWEEN
③ NOT
④ AND
⑤ OR
## 例：
`where dep_id>30 AND job_id IN ('1' , '2' , '#') OR salaly>4000`
だと、
`dep_id>30 AND job_job_id IN ('1' , '2' , '#')`
が評価された後に
`OR salaly>4000`
が評価される