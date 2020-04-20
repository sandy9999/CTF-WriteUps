We are given the following ciphertext

```
picoCTF{rgdhhxcviwtgjqxrdcdydkefyh}
```

It's mentioned that we need to use Caesar cipher. So let's write a short script.

```
ciphertext = "rgdhhxcviwtgjqxrdcdydkefyh"

for i in range(1, 26):
  plaintext = ""
  for c in ciphertext:
    plaintext+=(chr((ord(c)-ord('a')-i)%26 + ord('a')))
  print(plaintext)
```

We get 25 possibilities of plaintexts. Only one of them comes close to making sense. And we get our flag.
```
picoCTF{crossingtherubiconojovpqjs}
```