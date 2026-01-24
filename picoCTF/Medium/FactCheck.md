# [FactCheck] (Reverse Engineering / Medium)
![alt text](images/image-2.png)
## 問題の概要
- **目的**: 実行ファイルをデコンパイルしてflagを発見する
- **配布物**: ELFファイル

## 解法
1. デコンパイラツールに通す
2. flagの前半部分はそのままソースコード内に明記
3. flagの後半部分はoperator+=で処理されている
4. 後半部分を読んで後半部分のフラグを組み立てる
## 実行ログ
### main関数
```cpp
undefined8 main(void)

{
  char cVar1;
  char *pcVar2;
  long in_FS_OFFSET;
  allocator local_249;
  string local_248 [32];
  string local_228 [32];
  string local_208 [32];
  string local_1e8 [32];
  string local_1c8 [32];
  string local_1a8 [32];
  string local_188 [32];
  string local_168 [32];
  string local_148 [32];
  string local_128 [32];
  string local_108 [32];
  string local_e8 [32];
  string local_c8 [32];
  string local_a8 [32];
  string local_88 [32];
  string local_68 [32];
  string local_48 [40];
  long local_20;
  
  local_20 = *(long *)(in_FS_OFFSET + 0x28);
  std::allocator<char>::allocator();
                    /* try { // try from 001012cf to 001012d3 has its CatchHandler @ 00101975 */
  std::__cxx11::string::string(local_248,"picoCTF{wELF_d0N3_mate_",&local_249);
  std::allocator<char>::~allocator((allocator<char> *)&local_249);
  std::allocator<char>::allocator();
                    /* try { // try from 0010130a to 0010130e has its CatchHandler @ 00101996 */
  std::__cxx11::string::string(local_228,"0",&local_249);
  std::allocator<char>::~allocator((allocator<char> *)&local_249);
  std::allocator<char>::allocator();
                    /* try { // try from 00101345 to 00101349 has its CatchHandler @ 001019b1 */
  std::__cxx11::string::string(local_208,"5",&local_249);
  std::allocator<char>::~allocator((allocator<char> *)&local_249);
  std::allocator<char>::allocator();
                    /* try { // try from 00101380 to 00101384 has its CatchHandler @ 001019cc */
  std::__cxx11::string::string(local_1e8,"d",&local_249);
  std::allocator<char>::~allocator((allocator<char> *)&local_249);
  std::allocator<char>::allocator();
                    /* try { // try from 001013bb to 001013bf has its CatchHandler @ 001019e7 */
  std::__cxx11::string::string(local_1c8,"3",&local_249);
  std::allocator<char>::~allocator((allocator<char> *)&local_249);
  std::allocator<char>::allocator();
                    /* try { // try from 001013f6 to 001013fa has its CatchHandler @ 00101a02 */
  std::__cxx11::string::string(local_1a8,"2",&local_249);
  std::allocator<char>::~allocator((allocator<char> *)&local_249);
  std::allocator<char>::allocator();
                    /* try { // try from 00101431 to 00101435 has its CatchHandler @ 00101a1d */
  std::__cxx11::string::string(local_188,"a",&local_249);
  std::allocator<char>::~allocator((allocator<char> *)&local_249);
  std::allocator<char>::allocator();
                    /* try { // try from 0010146c to 00101470 has its CatchHandler @ 00101a38 */
  std::__cxx11::string::string(local_168,"a",&local_249);
  std::allocator<char>::~allocator((allocator<char> *)&local_249);
  std::allocator<char>::allocator();
                    /* try { // try from 001014a7 to 001014ab has its CatchHandler @ 00101a53 */
  std::__cxx11::string::string(local_148,"e",&local_249);
  std::allocator<char>::~allocator((allocator<char> *)&local_249);
  std::allocator<char>::allocator();
                    /* try { // try from 001014e2 to 001014e6 has its CatchHandler @ 00101a6e */
  std::__cxx11::string::string(local_128,"e",&local_249);
  std::allocator<char>::~allocator((allocator<char> *)&local_249);
  std::allocator<char>::allocator();
                    /* try { // try from 0010151d to 00101521 has its CatchHandler @ 00101a89 */
  std::__cxx11::string::string(local_108,"d",&local_249);
  std::allocator<char>::~allocator((allocator<char> *)&local_249);
  std::allocator<char>::allocator();
                    /* try { // try from 00101558 to 0010155c has its CatchHandler @ 00101aa4 */
  std::__cxx11::string::string(local_e8,"b",&local_249);
  std::allocator<char>::~allocator((allocator<char> *)&local_249);
  std::allocator<char>::allocator();
                    /* try { // try from 00101593 to 00101597 has its CatchHandler @ 00101abf */
  std::__cxx11::string::string(local_c8,"e",&local_249);
  std::allocator<char>::~allocator((allocator<char> *)&local_249);
  std::allocator<char>::allocator();
                    /* try { // try from 001015ce to 001015d2 has its CatchHandler @ 00101ada */
  std::__cxx11::string::string(local_a8,"6",&local_249);
  std::allocator<char>::~allocator((allocator<char> *)&local_249);
  std::allocator<char>::allocator();
                    /* try { // try from 00101606 to 0010160a has its CatchHandler @ 00101af5 */
  std::__cxx11::string::string(local_88,"c",&local_249);
  std::allocator<char>::~allocator((allocator<char> *)&local_249);
  std::allocator<char>::allocator();
                    /* try { // try from 0010163e to 00101642 has its CatchHandler @ 00101b0d */
  std::__cxx11::string::string(local_68,"9",&local_249);
  std::allocator<char>::~allocator((allocator<char> *)&local_249);
  std::allocator<char>::allocator();
                    /* try { // try from 00101676 to 0010167a has its CatchHandler @ 00101b25 */
  std::__cxx11::string::string(local_48,"8",&local_249);
  std::allocator<char>::~allocator((allocator<char> *)&local_249);
                    /* try { // try from 00101699 to 0010185f has its CatchHandler @ 00101b3d */
  pcVar2 = (char *)std::__cxx11::string::operator[]((ulong)local_208);
  if (*pcVar2 < 'B') {
    std::__cxx11::string::operator+=(local_248,local_c8);
  }
  pcVar2 = (char *)std::__cxx11::string::operator[]((ulong)local_a8);
  if (*pcVar2 != 'A') {
    std::__cxx11::string::operator+=(local_248,local_68);
  }
  pcVar2 = (char *)std::__cxx11::string::operator[]((ulong)local_1c8);
  cVar1 = *pcVar2;
  pcVar2 = (char *)std::__cxx11::string::operator[]((ulong)local_148);
  if ((int)cVar1 - (int)*pcVar2 == 3) {
    std::__cxx11::string::operator+=(local_248,local_1c8);
  }
  std::__cxx11::string::operator+=(local_248,local_1e8);
  std::__cxx11::string::operator+=(local_248,local_188);
  pcVar2 = (char *)std::__cxx11::string::operator[]((ulong)local_168);
  if (*pcVar2 == 'G') {
    std::__cxx11::string::operator+=(local_248,local_168);
  }
  std::__cxx11::string::operator+=(local_248,local_1a8);
  std::__cxx11::string::operator+=(local_248,local_88);
  std::__cxx11::string::operator+=(local_248,local_228);
  std::__cxx11::string::operator+=(local_248,local_128);
  std::__cxx11::string::operator+=(local_248,'}');
  std::__cxx11::string::~string(local_48);
  std::__cxx11::string::~string(local_68);
  std::__cxx11::string::~string(local_88);
  std::__cxx11::string::~string(local_a8);
  std::__cxx11::string::~string(local_c8);
  std::__cxx11::string::~string(local_e8);
  std::__cxx11::string::~string(local_108);
  std::__cxx11::string::~string(local_128);
  std::__cxx11::string::~string(local_148);
  std::__cxx11::string::~string(local_168);
  std::__cxx11::string::~string(local_188);
  std::__cxx11::string::~string(local_1a8);
  std::__cxx11::string::~string(local_1c8);
  std::__cxx11::string::~string(local_1e8);
  std::__cxx11::string::~string(local_208);
  std::__cxx11::string::~string(local_228);
  std::__cxx11::string::~string(local_248);
  if (local_20 == *(long *)(in_FS_OFFSET + 0x28)) {
    return 0;
  }
                    /* WARNING: Subroutine does not return */
  __stack_chk_fail();
}
```
###
```cpp
 pcVar2 = (char *)std::__cxx11::string::operator[]((ulong)local_208);
 // local_208 = '5' 
 if (*pcVar2 < 'B') {
    // '5' < 'B'
   std::__cxx11::string::operator+=(local_248,local_c8);
   // local_c8 = 'e'
 }
 
 
 pcVar2 = (char *)std::__cxx11::string::operator[]((ulong)local_a8);
 // local_a8 = '6'
 if (*pcVar2 != 'A') {
    // '6' != 'A'
   std::__cxx11::string::operator+=(local_248,local_68);
   // local_68 = '9'
 }

 pcVar2 = (char *)std::__cxx11::string::operator[]((ulong)local_1c8);
 cVar1 = *pcVar2;
 // cVar1 = local_1c8 = '3'

 pcVar2 = (char *)std::__cxx11::string::operator[]((ulong)local_148);
 // *pcVar2 = local_148 = 'e'
 if ((int)cVar1 - (int)*pcVar2 == 3) {
    // '3' - 'e' != 3
   std::__cxx11::string::operator+=(local_248,local_1c8);
 }

 std::__cxx11::string::operator+=(local_248,local_1e8);
 // local_1e8 = 'd'

 std::__cxx11::string::operator+=(local_248,local_188);
 // local_188 ~ 'a'

 pcVar2 = (char *)std::__cxx11::string::operator[]((ulong)local_168);
 // local_168 = 'a'
 if (*pcVar2 == 'G') {
   std::__cxx11::string::operator+=(local_248,local_168);
 }
```cpp
 std::__cxx11::string::operator+=(local_248,local_1a8); 	//2
 std::__cxx11::string::operator+=(local_248,local_88);  	//c
 std::__cxx11::string::operator+=(local_248,local_228);	    //0
 std::__cxx11::string::operator+=(local_248,local_128);	    //e
 std::__cxx11::string::operator+=(local_248,'}');			//}
```
### flag
```
picoCTF{wELF_d0N3_mate_e9da2c0e}
```

## 使用したツール・コマンド
- ghidra
## 学び・沼った所
- 今思うとlocal_1a8などのstring型配列の名前をを格納している文字に置き換えた方が読みやすかった
- おそらくこの実行ファイルの元のソースコードはC++11。ghidraはC言語で疑似コードを表示するため、C++の組み込み関数を処理できなかったのだと思う。ものすごく読みづらかった。