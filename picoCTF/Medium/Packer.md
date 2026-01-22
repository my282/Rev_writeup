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
hexeditorでファイルを直接確認
```
000000E0  10 00 00 00  00 00 00 00   8B 25 67 AE  55 50 58 21                   .........%g.UPX!
```
これにより圧縮方式がUPXであることを確認 \
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
GhidraでELFの中身を確認 \
<img width="322" height="718" alt="image" src="https://github.com/user-attachments/assets/2f0f1e81-80c7-414a-95d0-b0e57ef5a3db" /> \
symbol treeのディレクトリの数がすごい \
<img width="282" height="127" alt="image" src="https://github.com/user-attachments/assets/c6b2f6d6-f876-40d1-a27e-2166fba5b82a" /> \
main関数発見
```C

undefined8 main(void)

{
  size_t sVar1;
  char *pcVar2;
  int iVar3;
  undefined1 *puVar4;
  long in_FS_OFFSET;
  undefined1 auStack_a8 [8];
  size_t local_a0;
  undefined8 local_98;
  char *local_90;
  char local_88 [104];
  long local_20;
  
  local_20 = *(long *)(in_FS_OFFSET + 0x28);
  local_a0 = 100;
  local_98 = 99;
  for (puVar4 = auStack_a8; puVar4 != auStack_a8; puVar4 = puVar4 + -0x1000) {
    *(undefined8 *)(puVar4 + -8) = *(undefined8 *)(puVar4 + -8);
  }
  *(undefined8 *)(puVar4 + -8) = *(undefined8 *)(puVar4 + -8);
  builtin_strncpy(local_88,
                  "7069636f4354467b5539585f556e5034636b314e365f42316e34526933535f31613561336633397d"
                  ,0x51);
  local_88[0x51] = '\0';
  local_88[0x52] = '\0';
  local_88[0x53] = '\0';
  local_88[0x54] = '\0';
  local_88[0x55] = '\0';
  local_88[0x56] = '\0';
  local_88[0x57] = '\0';
  local_88[0x58] = '\0';
  local_88[0x59] = '\0';
  local_88[0x5a] = '\0';
  local_88[0x5b] = '\0';
  local_88[0x5c] = '\0';
  local_88[0x5d] = '\0';
  local_88[0x5e] = '\0';
  local_88[0x5f] = '\0';
  local_88[0x60] = '\0';
  local_88[0x61] = '\0';
  local_88[0x62] = '\0';
  local_88[99] = '\0';
  local_90 = puVar4 + -0x70;
  *(undefined8 *)(puVar4 + -0x78) = 0x401eee;
  printf("Enter the password to unlock this file: ");
  pcVar2 = local_90;
  sVar1 = local_a0;
  *(undefined8 *)(puVar4 + -0x78) = 0x401f0f;
  fgets(pcVar2,(int)sVar1,(FILE *)stdin);
  pcVar2 = local_90;
  *(undefined8 *)(puVar4 + -0x78) = 0x401f2a;
  printf("You entered: %s\n",pcVar2);
  pcVar2 = local_90;
  sVar1 = local_a0;
  *(undefined8 *)(puVar4 + -0x78) = 0x401f47;
  iVar3 = strncmp(pcVar2,local_88,sVar1);
  if (iVar3 == 0) {
    *(undefined8 *)(puVar4 + -0x78) = 0x401f57;
    puts(
        "Password correct, please see flag: 7069636f4354467b5539585f556e5034636b314e365f42316e345269 33535f31613561336633397d"
        );
    *(undefined8 *)(puVar4 + -0x78) = 0x401f63;
    puts(local_88);
  }
  else {
    *(undefined8 *)(puVar4 + -0x78) = 0x401f71;
    puts("Access denied");
  }
  if (local_20 == *(long *)(in_FS_OFFSET + 0x28)) {
    return 0;
  }
                    /* WARNING: Subroutine does not return */
  __stack_chk_fail();
}
```
なぜかhexになってますが直接flagを表示するコードを確認
```C
  puts(
        "Password correct, please see flag: 7069636f4354467b5539585f556e5034636b314e365f42316e345269 33535f31613561336633397d"
        );
```
これをdencodeで変換して
```
picoCTF{U9X_UnP4ck1N6_B1n4Ri3S_1a5a3f39}
```

## 使用したツール・コマンド
- file,binwalk,stringsコマンド
- UPX(Ultimate Packer for eXecutables)
- Ghidra
- dencode

## 学び・沼った所
- バイナリファイルが圧縮されていると、Ghidraが関数の情報を取得できない(IDAだとよくわからない関数群を表示する)
