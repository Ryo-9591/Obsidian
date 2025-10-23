# 前処理
## ①欠損値への対応
### ①-1　欠測値を除去する

```
import pandas as pd
df = pd.read_csv('data/src/sample_pandas_normal_nan.csv')
df.dropna() # 欠測値の行を削除
df.

```



### ①-2 　欠測値を補完する

## ③