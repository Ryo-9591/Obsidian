# 前処理
## ①欠損値への対応
### ①-1　欠測値を除去する

```
import pandas as pd

df = pd.read_csv('data/src/sample.csv')

df.dropna() # 欠測値の行を削除
df.dropna(how='all')  # 全ての列が欠損値である行を削除します
df.dropna(subset=['A']) # 'A'列に欠損値がある行を削除
```
### ①-2 　欠測値を補完する

```
import pandas as pd

df = pd.read_csv('data/src/sample.csv')

df.fillna(0) # 欠測値に0を代入
df.ffill() # 直前の値を使って代入
df.fillna(df.mean()) # 全ての列の欠損値を各列の平均値で代入
```

```

```

## ③