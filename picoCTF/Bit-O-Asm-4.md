# [Bit-O-Asm-4] (Reverse Engineering / Medium)
## 問題の概要
- **目的**: 最終的にeaxレジスタに格納されている数値の特定
- **配布物**: x86-64ソースコード

## 解法
1. 読む。
## 実行ログ
```
<+0>:     endbr64 
<+4>:     push   rbp
<+5>:     mov    rbp,rsp
<+8>:     mov    DWORD PTR [rbp-0x14],edi
<+11>:    mov    QWORD PTR [rbp-0x20],rsi
<+15>:    mov    DWORD PTR [rbp-0x4],0x9fe1a
<+22>:    cmp    DWORD PTR [rbp-0x4],0x2710
<+29>:    jle    0x55555555514e <main+37>
<+31>:    sub    DWORD PTR [rbp-0x4],0x65
<+35>:    jmp    0x555555555152 <main+41>
<+37>:    add    DWORD PTR [rbp-0x4],0x65
<+41>:    mov    eax,DWORD PTR [rbp-0x4]
<+44>:    pop    rbp
<+45>:    ret

```
```
<+0>:     endbr64 
<+4>:     push   rbp
<+5>:     mov    rbp,rsp
<+8>:     mov    DWORD PTR [rbp-0x14],edi
<+11>:    mov    QWORD PTR [rbp-0x20],rsi

; ここからがeaxに関係するところ
<+15>:    mov    DWORD PTR [rbp-0x4],0x9fe1a
<+22>:    cmp    DWORD PTR [rbp-0x4],0x2710 ; 0x9fe1a と 0x2710で比較
<+29>:    jle    0x55555555514e <main+37> ; 0x9fe1a <= 0x2710ではないのでジャンプしない
<+31>:    sub    DWORD PTR [rbp-0x4],0x65 ; 0x9fe1a - 0x65
<+35>:    jmp    0x555555555152 <main+41> ; <+41>にジャンプ
<+37>:    add    DWORD PTR [rbp-0x4],0x65 ; ここは実行されない
<+41>:    mov    eax,DWORD PTR [rbp-0x4]  ; eaxに格納

<+44>:    pop    rbp
<+45>:    ret

```
### flag
```
picoCTF{654773}
```
## 使用したツール・コマンド
- VSCode
## 学び・沼った所
Bit-O-Asm-3と同様、基本文法がわかっているかどうかの問題。