Let's consider the mapping, m(A) = 0, m(B) = 1, ... , m(Y) = 24, m(Z) = 25

From the table, we can notice that the encryption of 2 letters is nothing but (map(plaintext_letter) + map(key_letter))%26 = m(our ciphertext_letter)

Which means, (map(ciphertext_letter) - map(key_letter))%26 = m(our plaintext_letter). I wrote a small script for this.

```
ciphertext = 'UFJKXQZQUNB'
key = 'SOLVECRYPTO'

plaintext = ''
for i in range(len(ciphertext)):
  plaintext+=chr((ord(ciphertext[i])-ord(key[i]))%26 + ord('A'))

print(plaintext)
```

Anddd we get our flag!
```
CRYPTOISFUN
```

