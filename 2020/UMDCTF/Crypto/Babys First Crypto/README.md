This was a ROT13 mod 128.

```
text  = open('ciphertext').read()
for t in text:
  print(chr((ord(t)-13)%128),end='')
```