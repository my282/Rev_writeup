# [Picker II] (Reverse Engineering / Medium)
![alt text](<images/スクリーンショット 2026-01-23 130432.png>)
## 問題の概要
- **目的**: プログラムにflagを表示させる
- **配布物**: pythonソースコード

## 解法
1. pythonソースコードの内にflagを表示するwin()を確認
2. filter()関数によってwinを直接実行できない
3. win()関数の内容を直接exec()関数で実行
## 実行ログ
### win()
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
### filter(user_input)
```python
def filter(user_input):
  if 'win' in user_input:
    return False
  return True
```
### exec()実行
```
==> exec("print(' '.join([hex(ord(c)) for c in open('flag.txt').read().strip()]))")
0x70 0x69 0x63 0x6f 0x43 0x54 0x46 0x7b 0x66 0x31 0x6c 0x37 0x33 0x72 0x35 0x5f 0x66 0x34 0x31 0x6c 0x5f 0x63 0x30 0x64 0x33 0x5f 0x72 0x33 0x66 0x34 0x63 0x37 0x30 0x72 0x5f 0x6d 0x31 0x67 0x68 0x37 0x5f 0x35 0x75 0x63 0x63 0x33 0x33 0x64 0x5f 0x39 0x35 0x64 0x34 0x34 0x35 0x39 0x30 0x7d
```
## 使用したツール・コマンド
- VScode
- Dencode
## 学び・沼った所
- pythonが書けないせいでAI頼りになってしまった。無念。
