# huffman-codec

Very simple 8 bits huffman encoder/decoder.

## Build
```make```

## Usage
Encoder a file:
```
./huffman e filename
```
Output is "out.he"

Decode a file:
```
./huffman d filename
```
Output is "out.hd"



例子
==================================
james@james-OptiPlex-380:~/huffmantest/test$ hexdump -C 1.txt
00000000  31 0a                                             |1.|
00000002


james@james-OptiPlex-380:~/huffmantest/test$ ../huffman e 1.txt
        [49:1]
R:2
        [10:1]
value = 10, length = 1 code = 0
value = 49, length = 1 code = 1
File size = 2
Table size = 2


james@james-OptiPlex-380:~/huffmantest/test$ ../huffman d out.he
        [49:1]
R:2
        [10:1]

james@james-OptiPlex-380:~/huffmantest/test$ hexdump  out.he -C
00000000  48 55 46 46 4d 41 4e 00  02 00 00 00 00 00 00 00  |HUFFMAN.........|
00000010  02 00 00 00 00 00 00 00  0a 01 00 00 00 00 00 00  |................|
00000020  31 01 00 00 00 00 00 00  80                       |1........|


编码后的数据包含3部分

文件头
==================================

struct huffman_file_header {
    char magic[8];
    uint64_t file_size;
    uint32_t table_size;
};


printf("sizeof(huffman_file_header)=%d\n", sizeof(struct huffman_file_header));

总共24字节长

8字节文件头  8字节文件长度
8字节表格长度（结构体对齐）


huffman表格
==================================

表格，每个占用8字节，总共8*表格长度


编码数据区
==================================

80 的二进制是 1000 0000  对应 49 10（即十六进制的 31 0a ）
*/
