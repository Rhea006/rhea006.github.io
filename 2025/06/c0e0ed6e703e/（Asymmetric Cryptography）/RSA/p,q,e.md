---
title: p,q,e
date: '2025-6-14 22:00'
categories:
  - Crypto
  - 非对称加密（Asymmetric Cryptography）
  - RSA
---
在一次RSA密钥对生成中，假设p=473398607161，q=4511491，e=17
求解出d作为flga提交
```
p=473398607161
q=4511491
e=17
z=(p-1)*(q-1) #欧拉函数
d = pow(e, -1, z) #(e * d) % z == 1 
#m = pow(c, d, n)
print(d)
```
or
```
import gmpy2
p = 473398607161 
q = 4511491 
e = 17 
z = (p - 1) * (q - 1) 
d = gmpy2.invert(e, z) # e*d mod z = 1
print(d)
```
![](/images/{398FE444-FE62-474E-8333-9D51EDA83FEB}.png)
右键
![](/images/Pastedimage20250603090548.png)
125631357777427553

