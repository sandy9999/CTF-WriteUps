We were given this ciphertext, `00110 01110 00100 00000 10011 00101 01110 01110 00011 00011 01110 01101 10011 10010 10011 00000 10001 10101 00100`. Just convert the indidivual binary numbers into decimals and apply A0Z25 cipher. Script here.

```
cipher = "00110 01110 00100 00000 10011 00101 01110 01110 00011 00011 01110 01101 10011 10010 10011 00000 10001 10101 00100"

cipher = cipher.split(' ')
for c in cipher:
  print(chr(ord('a')+int(c,2)),end='')
```

```
rtcp{goeatfooddontstarve}
```