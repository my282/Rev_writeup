# [Bit-O-Asm-3] (Reverse Engineering / Medium)
## 問題の概要
- **目的**:アセンブリ命令実行後のeaxレジスタ内の数値を特定
- **配布物**:txtファイル

## 解法
1. 配布されたアセンブリコードを読む。
## 実行ログ
配布ファイルの中身 + 筆者の解説コメントアウト
```asm
<+0>:     endbr64 
<+4>:     push   rbp
<+5>:     mov    rbp,rsp
<+8>:     mov    DWORD PTR [rbp-0x14],edi
<+11>:    mov    QWORD PTR [rbp-0x20],rsi
<+15>:    mov    DWORD PTR [rbp-0xc],0x9fe1a
<+22>:    mov    DWORD PTR [rbp-0x8],0x4
<+29>:    mov    eax,DWORD PTR [rbp-0xc]
<+32>:    imul   eax,DWORD PTR [rbp-0x8]
<+36>:    add    eax,0x1f5
<+41>:    mov    DWORD PTR [rbp-0x4],eax
<+44>:    mov    eax,DWORD PTR [rbp-0x4]
<+47>:    pop    rbp
<+48>:    ret

```
```asm
<+0>:     endbr64 ; セキュリティチェック

; 関数プロローグ
<+4>:     push   rbp
<+5>:     mov    rbp,rsp

<+8>:     mov    DWORD PTR [rbp-0x14],edi
<+11>:    mov    QWORD PTR [rbp-0x20],rsi

; eaxレジスタに関係があるのはここから
<+15>:    mov    DWORD PTR [rbp-0xc],0x9fe1a
<+22>:    mov    DWORD PTR [rbp-0x8],0x4
<+29>:    mov    eax,DWORD PTR [rbp-0xc]
; eax = 0x9fe1a
<+32>:    imul   eax,DWORD PTR [rbp-0x8]
; eax *= 0x4
<+36>:    add    eax,0x1f5
; eax += 0x1f5

; 下に行はおそらく最適化オプションがない影響
<+41>:    mov    DWORD PTR [rbp-0x4],eax
; 計算結果をメモリに保存
<+44>:    mov    eax,DWORD PTR [rbp-0x4]
; 戻り値としてeaxに保存

;関数エピローグ
<+47>:    pop    rbp
<+48>:    ret
```
## 使用したツール・コマンド
- エディタ
## 学び・沼った所
今回のコードはスタックを使ってないので関数プロローグとエピローグがなくても成立するっぽい。 \
CTFの難易度としては割と優しい方。