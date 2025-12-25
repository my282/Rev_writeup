# reverse_cipher (Reverse Engineering / ~~Medium~~ -> Hard)
<img width="958" height="471" alt="image" src="https://github.com/user-attachments/assets/8b016ee0-2ee0-48e8-b95e-979ccb1a49d5" />

## 問題の概要
- **目的**:ELFファイルによって暗号化された文字列を復元しflagを取得
- **配布物**:ELFファイル, 暗号化された文字列
- **ヒント**:objdump and Gihdra are some tools that could assist with this

## 解法
1. ELFファイルをデコンパイル
2. 暗号化の方法を確認
3. 復号するソースコードを記述し、暗号化された文字列に対して実行
### 今回の暗号化方法
1. 0から7文字目までは暗号化せずにそのまま
2. 8文字目から22文字目までを暗号化
- 偶数文字目ならASCIIを+5ずらす
- 奇数文字目ならASCIIを-2ずらす
3. 23文字目はそのまま

## 実行ログ
暗号化された文字列
```
picoCTF{w1{1wq8cFF:7Rkr}
```
Ghidaで解析した疑似Cコード
(見やすいように変数名や数値の表記方法を一部変えています)
```C
void main(void)

{
  size_t sVar1;
  char input [23];
  char char_buffer1;
  int local_2c;
  FILE *file_pointer2;
  FILE *file_pointer1;
  uint j;
  int i;
  char char_buffer2;
  
  file_pointer1 = fopen("flag.txt","r");
  file_pointer2 = fopen("rev_this","a");
  if (file_pointer1 == NULL) {
    puts("No flag found, please make sure this is run on the server");
  }
  if (file_pointer2 == NULL) {
    puts("please run this on the server");
  }
  sVar1 = fread(input,0x18,1,file_pointer1);
  local_2c = (int)sVar1;
  if ((int)sVar1 < 1) {
                     /* WARNING: Subroutine does not return */
    exit(0);
  }
  for (i = 0; i < 8; i = i + 1) {
    char_buffer2 = input[i];
    fputc((int)char_buffer2,file_pointer2);
  }
  for (j = 8; (int)j < 0x17; j = j + 1) {
    if ((j & 1) == 0) {
      char_buffer2 = input[(int)j] + 5;
    }
    else {
      char_buffer2 = input[(int)j] + -2;
    }
    fputc((int)char_buffer2,file_pointer2);
  }
  char_buffer2 = char_buffer1;
  fputc((int)char_buffer1,file_pointer2);
  fclose(file_pointer2);
  fclose(file_pointer1);
  return;
}
```
解読に使用したソースコード
```C
#include <stdio.h>

int main(void) {
  char array[256] = "w1{1wq8cFF:7Rkr";
// 復号
  for (int i = 0; i < 15; i += 2) {
    array[i] -= 5;
  }
  for (int i = 1; i < 15; i += 2) {
    array[i] += 2;
  }

// 復号結果の表示
  for (int i = 0; i < 15; i += 1) {
    printf("%c", array[i]);
  }
  return 0;
}

```


## 使用したツール・コマンド
- Ghidra

## 学び・沼った所
- 暗号化方式が結構ややこしい。
