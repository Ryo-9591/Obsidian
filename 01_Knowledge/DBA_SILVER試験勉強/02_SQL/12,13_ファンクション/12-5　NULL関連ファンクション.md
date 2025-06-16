# NVL
## 例：
`NVL(in , replace)`
→
inがnullの場合replaceに置き換える
inがnullでなければin返す
inとreplaceのデータ型は暗黙的に変換する
# NVL2
## 例：
`NVL2(in , out1 , out2)`
→
inがnullでない場合、out1を返す
inがnullであるなら、out2を返す
out1とout2のデータ型は暗黙的に変換する
# NULLIF
## 例：
`NULLIF(in , check)`
→
inがcheckに等しいならNULLを返す
inがcheckに等しくないならinを返す
inにNULLを指定できない
※inとcheckは同じデータ型である必要がある
# COALENSE
## 例：
`COALENCE(in1 , in2 , ... , inN)`
→
in1からinNまでで最初に見つかったNULLでない値を返す
すべてnullの場合nullを返す
※in1からinNまではデータ型は同じである必要がある
