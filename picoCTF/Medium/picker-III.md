# [Picker-III] (Reverse Engineering / Medium)
![alt text](images/image.png)
## 問題の概要
- **目的**: プログラムにflagを表示させる
- **配布物**: pythonソースコード

## 解法
1. pythonソースコードよりwin関数がflagを表示することを確認
2. write_variableによって関数名を変更できることを確認
3. アクセスできる関数テーブル内の4関数のいずれかの名称をwinに変更
4. 変更した関数を数値で指定して実行
## 実行ログ
### win関数(picker-III.py)
```python
def win():
  # This line will not work locally unless you create your own 'flag.txt' in
  #   the same directory as this script
  flag = open('flag.txt', 'r').read()
  #flag = flag[:-1]
  flag = flag.strip()
  str_flag = ''
  for c in flag:
    str_flag += str(hex(ord(c))) + ' '
  print(str_flag)
```
### win関数実行
```
❯  nc saturn.picoctf.net 60020
==> 1
1: print_table
2: read_variable
3: write_variable
4: getRandomNumber
==> 2
Please enter variable name to read: filter_value
<function filter_value at 0x7408922d4940>
==> 3
Please enter variable name to write: write_variable
Please enter new value of variable: win
==> 3
0x70 0x69 0x63 0x6f 0x43 0x54 0x46 0x7b 0x37 0x68 0x31 0x35 0x5f 0x31 0x35 0x5f 0x77 0x68 0x34 0x37 0x5f 0x77 0x33 0x5f 0x67 0x33 0x37 0x5f 0x77 0x31 0x37 0x68 0x5f 0x75 0x35 0x33 0x72 0x35 0x5f 0x31 0x6e 0x5f 0x63 0x68 0x34 0x72 0x67 0x33 0x5f 0x61 0x31 0x38 0x36 0x66 0x39 0x61 0x63 0x7d
```
### flag
```
picoCTF{7h15_15_wh47_w3_g37_w17h_u53r5_1n_ch4rg3_a186f9ac}
```
## 使用したツール・コマンド
- VSCode
- Dencode
## 学び・沼った所
2,3の関数名に"variable"とついていたので変えられるのは変数のみだと勘違いしていた。
