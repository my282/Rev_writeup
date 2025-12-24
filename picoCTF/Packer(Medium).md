# Packer (Reverse Engineering / Medium)
<img width="712" height="549" alt="image" src="https://github.com/user-attachments/assets/777a9445-6754-440d-b38d-524f99da4e16" />

## 問題の概要
- **目的**:バイナリファイルの解凍
- **配布物**:passwordつきELFファイル
- **ヒント**:What can we do to reduce the size of a binary after compiling it.

## 解法
1. UPXを使ってELFファイルを解凍
2. デコンパイルして中身を見る
3. flagを表示するputsを直接発見
## 実行ログ
```
file binwalk strings | head 
```
実行結果(一部)
```
000000E0  10 00 00 00  00 00 00 00   8B 25 67 AE  55 50 58 21                   .........%g.UPX!
```
これにより圧縮方式がUPXであることを確認
UPXで解凍
```
upx -d (ファイル名)
```
実行結果
```
                      Ultimate Packer for eXecutables
                          Copyright (C) 1996 - 2024
UPX 4.2.2       Markus Oberhumer, Laszlo Molnar & John Reiser    Jan 3rd 2024

        File size         Ratio      Format      Name
   --------------------   ------   -----------   -----------
[WARNING] bad b_info at 0x4b718

[WARNING] ... recovery at 0x4b714

    877724 <-    336520   38.34%   linux/amd64   out

```



## 使用したツール・コマンド
- fileコマンド
- UPX(Ultimate Packer for eXecutables)
- Ghidra

## 学び・沼った所**
- バイナリファイルが圧縮されていると、Ghidraが関数の情報を取得できない(IDAだとよくわからない関数群を表示する)
