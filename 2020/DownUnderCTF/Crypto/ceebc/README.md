It's CBC again! Let's first take a sneak peak into how the verification process works. Given a message, signature and an IV, it computes the signature using the given IV on the message and verifies if the signature that you provided matches. Best part though, you can give whatever IV you want!

If b'cashcashcashcash' xor IV1 = b'flagflagflagflag' xor IV2, we are going to get the same signature! We know IV1, which means finding IV2 is easy. So, we can give b'flagflagflagflag' as the input pessage, the same signature as that of b'cashcashcash' and IV2 as input and we get the flag. Here's the script

```
from pwn import *

r = remote('chal.duc.tf', 30202)
sig_hex = r.recvline().split()[-1][:-1].decode()

sig = binascii.unhexlify(sig_hex)
iv = sig[16:32]
p1 = b"cashcashcashcash"
p2 = b"flagflagflagflag"
ans = sig[0:16].hex() + xor(xor(p1,p2),iv).hex()
r.recvuntil(b': ')
r.send(p2+ b'\n')
r.recvuntil(b': ')
r.send(ans.encode()+b'\n')
print(r.recvline())
print(r.recvline())

```

```
Flag: DUCTF{WAT_I_THOUGHT_IV_IZ_G00D}
```