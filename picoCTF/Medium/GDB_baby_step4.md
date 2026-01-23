# [GDB baby step 4] (Reverse Engineering / Medium)
![alt text](<images/スクリーンショット 2026-01-23 122258.png>)
## 問題の概要
- **目的**: main関数が呼び出す関数がeaxの値を何と乗算をおこなっているかを特定
- **配布物**: ELFファイル

## 解法
1. gdbにてmain関数を観察
2. main関数が"func1"という関数を呼び出していることを確認
3. gdbにてfunc1関数を観察
## 実行ログ
### main
```
(gdb) x/20i main
   0x40111c <main>:     endbr64
   0x401120 <main+4>:   push   %rbp
   0x401121 <main+5>:   mov    %rsp,%rbp
   0x401124 <main+8>:   sub    $0x20,%rsp
   0x401128 <main+12>:  mov    %edi,-0x14(%rbp)
   0x40112b <main+15>:  mov    %rsi,-0x20(%rbp)
   0x40112f <main+19>:  movl   $0x28e,-0x4(%rbp)
   0x401136 <main+26>:  movl   $0x0,-0x8(%rbp)
   0x40113d <main+33>:  mov    -0x4(%rbp),%eax
   0x401140 <main+36>:  mov    %eax,%edi
   0x401142 <main+38>:  call   0x401106 <func1>
   0x401147 <main+43>:  mov    %eax,-0x8(%rbp)
   0x40114a <main+46>:  mov    -0x4(%rbp),%eax
   0x40114d <main+49>:  leave
   0x40114e <main+50>:  ret
   (以下省略)
```
### func1
```
(gdb) x/20i func1
   0x401106 <func1>:    endbr64
   0x40110a <func1+4>:  push   %rbp
   0x40110b <func1+5>:  mov    %rsp,%rbp
   0x40110e <func1+8>:  mov    %edi,-0x4(%rbp)
   0x401111 <func1+11>: mov    -0x4(%rbp),%eax
   0x401114 <func1+14>: imul   $0x3269,%eax,%eax
   0x40111a <func1+20>: pop    %rbp
   0x40111b <func1+21>: ret
    (以下省略)
```
### flag
```
picoCTF{12905}
```

## 使用したツール・コマンド
- gdb

## 学び・沼った所
ブレークポイントをアドレスを直接指定して設置するには
```
b *0x40111a
```
のように*(アスタリスク)を付けないといけない(今回意味なかったけど)