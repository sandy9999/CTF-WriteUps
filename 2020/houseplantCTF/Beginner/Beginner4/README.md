We were given this ciphertext, `egpc{lnyy_orggre_cnegvpvcngr}`. Simple Caesar cipher. Used this script.

```
ciphertext = "egpc{lnyy_orggre_cnegvpvcngr}"
for i in range(1, 26):
  plaintext = ""
  for c in ciphertext:
    if c.isalpha():
      plaintext+=(chr((ord(c)-ord('a')-i)%26 + ord('a')))
    else:
      plaintext+=c
  print(plaintext)
```

```
rtcp{yall_better_participate}
```