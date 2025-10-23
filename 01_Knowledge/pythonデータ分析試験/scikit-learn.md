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
#### Pandasを使う方法
```
import pandas as pd

df = pd.read_csv('data/src/sample.csv')

df.fillna(0) # 欠測値に0を代入
df.ffill() # 直前の値を使って代入
df.fillna(df.mean()) # 全ての列の欠損値を各列の平均値で代入
```
#### scikit-learnを使う方法
```
from sklearn.impute import SimpleImputer
import pandas as pd

df = pd.read_csv('data/src/sample.csv')

imp = SimpleImputer(strategy='mean')
imp.fit(df) # 欠測していない値の平均値を計算して内部に記憶
imp.transform(df) # fitで記憶した平均値を使って欠測値を変換
```
## ②カテゴリ変数のエンコーディング

```
from sklearn.preprocessing import LabelEncoder

le = LabelEncoder() # ラベルエンコーダのインスタンス生成
le.fit(df.loc[:, "B"])  # 全てのユニークなカテゴリ値
le.transform(df.loc[:, "B"])　# カテゴリ値を、対応する整数値に置き換え
```
## ③One-hotエンコーディング
![One-Hot Encoding in Scikit-Learn with OneHotEncoder • datagy](https://datagy.io/wp-content/uploads/2022/01/One-Hot-Encoding-for-Scikit-Learn-in-Python-Explained-1024x576.png)

```
import pandas as pd

data = {
    '名前': ['田中', '佐藤', '鈴木', '高橋'],
    '性別': ['男性', '女性', '男性', '女性'],
    '職業': ['エンジニア', 'デザイナー', '営業', 'エンジニア']
}
df = pd.DataFrame(data)
```
#### 元のデータ
   名前  性別     職業
0  田中  男性  エンジニア
1  佐藤  女性  デザイナー
2  鈴木  男性     営業
3  高橋  女性  エンジニア
### Pandasを使う方法
```
df_pandas = pd.get_dummies(df, columns=['性別', '職業'])
```
Pandas:
   名前  性別_女性  性別_男性  職業_エンジニア  職業_デザイナー  職業_営業
0  田中  False   True      True     False  False
1  佐藤   True  False     False      True  False
2  鈴木  False   True     False     False   True
3  高橋   True  False      True     False  False
### scikit-learnを使う方法
```
from sklearn.preprocessing import OneHotEncoder
from sklearn.compose import ColumnTransformer

# ColumnTransformerの設定
preprocessor = ColumnTransformer(
    transformers=[
        ('onehot', OneHotEncoder(sparse_output=False), ['性別', '職業'])
    ],
    remainder='passthrough'  # 指定されていない列はそのまま残す
)

# データを変換
transformed_data = preprocessor.fit_transform(df) 
```
#### One Hot エンコーディング後
  onehot__性別_女性 onehot__性別_男性 onehot__職業_エンジニア onehot__職業_デザイナー onehot__職業_営業  \
0           0.0           1.0              1.0              0.0           0.0   
1           1.0           0.0              0.0              1.0           0.0   
2           0.0           1.0              0.0              0.0           1.0   
3           1.0           0.0              1.0              0.0           0.0   
## ④特徴量の正規化

```
import pandas as pd

df = pd.DataFrame(
    {
        "A": [1, 2, 3, 4, 5],
        "B": [100, 200, 300, 400, 500]
    }
)
```
### 分散正規化

```
from 
```

### 最小最大正規化
