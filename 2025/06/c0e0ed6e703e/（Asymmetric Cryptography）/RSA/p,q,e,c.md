---
title: p,q,e,c
date: '2025-6-14 22:00'
sticky: 1
categories:
  - Crypto
  - 非对称加密（Asymmetric Cryptography）
  - RSA
tags:
---
p = 3487583947589437589237958723892346254777
q = 8767867843568934765983476584376578389
e = 65537
cipher = 26369494845903294944045520286034018329014599704760363106090278637665342700044

```
from sympy import mod_inverse
e = 65537
p = 3487583947589437589237958723892346254777
q = 8767867843568934765983476584376578389
cipher = 26369494845903294944045520286034018329014599704760363106090278637665342700044

n = p * q #计算模数
phi_n = (p - 1) * (q - 1) #计算欧拉函数

d = mod_inverse(e, phi_n) #计算私钥d=e^-1 mod ϕ(n)

m = pow(cipher, d, n) #m=cipher^d mod n使用 pow 函数进行模幂运算，效率更高

def num_to_ascii(m):
    # 将数字转换为字节流
	m_bytes = m.to_bytes((m.bit_length() + 7) // 8, byteorder='big')
    # 将字节流转换为 ASCII 字符串
    return m_bytes.decode('utf-8')

flag = num_to_ascii(m)
print(f"flag = {flag}")
```
 flag=TZCFlag{try_rsa}
![](/images/Pastedimage20250603143947.png)）