We are given the following cipher

```
cvpbPGS{abg_gbb_onq_bs_n_ceboyrz}
```

We are also given a clue that it is ROT13.

So using this simple python script

```
ct = 'cvpbPGS{abg_gbb_onq_bs_n_ceboyrz}'

for c in ct:
  if c.isalpha():
    if c.islower():
      print(chr((ord(c)-ord('a')-13)%26+ord('a')),end='')
    elif c.isupper():
      print(chr((ord(c)-ord('A')-13)%26+ord('A')),end='')
    else:
      print(c,end='')
```

We obtain the flag.
```
picoCTFnottoobadofaproblem
```