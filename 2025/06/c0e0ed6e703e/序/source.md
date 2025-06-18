---
title: source
date: '2025-6-14 22:00'
categories:
  - REVERSE
  - 直接给程序
---
```
#include <stdio.h> 
#include <string.h> 
int main(int argc, char *argv[]) { 
	if (argc != 4) { 
	printf("what?\n"); 
	exit(1); 
	} 
	
	unsigned int first = atoi(argv[1]);
	if (first != 0xcafe) { 
	printf("you are wrong, sorry.\n"); 
	exit(2);
	} 
	
	unsigned int second = atoi(argv[2]); 
	if (second % 5 == 3 || second % 17 != 8) { 
	printf("ha, you won't get it!\n"); 
	exit(3); 
	} 
	
	if (strcmp("h4cky0u", argv[3])) { 
	printf("so close, dude!\n"); 
	exit(4); 
	} 
	
	printf("Brr wrrr grr\n"); 
	
	unsigned int hash = first * 31337 + (second % 17) * 11 + strlen(argv[3]) - 1615810207; 
	printf("Get your key: "); 
	printf("%x\n", hash); 
	return 0; 
}
```
### 程序分析
这个程序需要三个命令行参数才能正常运行：
1. 第一个参数必须是整数`0xcafe`（即十进制的 51966）
2. 第二个参数必须满足两个条件：
    - 模 5 不等于 3
    - 模 17 等于 8
3. 第三个参数必须是字符串`h4cky0

**正确运行方法：**
./程序名 51966 25 h4cky0u

Brr wrrr grr
Get your key: c0ffee

OR
**直接算**
hash = 51966 * 31337 + 8 * 11 + 8 - 1615810207 = 1628468542 + 88 + 8 - 1615810207 = 1628468638 - 1615810207 = 12658431
转换为十六进制：`0xc0ffee`