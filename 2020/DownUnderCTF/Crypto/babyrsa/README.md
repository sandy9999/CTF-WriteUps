Let pos(c) represent the position of letter c in the key. Also, notice that the add function is nothing but the xor operation.

We are given a part of the plaintext, which only makes it easier to set up some Xor rules (Note that ^ here represents xor).

```
pos [5] ^ 7 = pos [8]
pos [4] ^ pos [5] = pos [5]
pos [6] ^ pos [4] = pos [6]
pos [8] ^ pos [6] = pos [7]
pos [6] ^ pos [8] = pos [7]
pos [5] ^ pos [6] = pos [b]
pos [2] ^ pos [5] = pos [c]
pos [0] ^ pos [2] = pos [8]
pos [7] ^ pos [0] = pos [3]
pos [3] ^ pos [7] = pos [0]
pos [6] ^ pos [3] = pos [2]
pos [5] ^ pos [6] = pos [b]
pos [6] ^ pos [5] = pos [b]
pos [3] ^ pos [6] = pos [2]
pos [7] ^ pos [3] = pos [0]
pos [2] ^ pos [7] = pos [f]
pos [6] ^ pos [2] = pos [3]
pos [5] ^ pos [6] = pos [b]
pos [7] ^ pos [5] = pos [e]
pos [4] ^ pos [7] = pos [7]
pos [2] ^ pos [4] = pos [2]
pos [0] ^ pos [2] = pos [8]
pos [6] ^ pos [0] = pos [f]
pos [d] ^ pos [6] = pos [9]
pos [6] ^ pos [d] = pos [9]
pos [5] ^ pos [6] = pos [b]
pos [7] ^ pos [5] = pos [e]
pos [3] ^ pos [7] = pos [0]
pos [7] ^ pos [3] = pos [0]
pos [3] ^ pos [7] = pos [0]
pos [6] ^ pos [3] = pos [2]
pos [1] ^ pos [6] = pos [e]
pos [6] ^ pos [1] = pos [e]
pos [7] ^ pos [6] = pos [8]
pos [6] ^ pos [7] = pos [8]
pos [5] ^ pos [6] = pos [b]
pos [2] ^ pos [5] = pos [c]
pos [0] ^ pos [2] = pos [8]
pos [6] ^ pos [0] = pos [f]
pos [9] ^ pos [6] = pos [d]
pos [7] ^ pos [9] = pos [c]
pos [3] ^ pos [7] = pos [0]
pos [3] ^ pos [3] = pos [4]
pos [a] ^ pos [3] = pos [5]
```

On drawing conclusions from the above,
```
pos[1] = 7
pos[4] = 0
On fixing, pos[5], pos[6], pos[2], pos[d] we can get,
pos[b] = pos[5]^pos[6]
pos[7] = pos[b]^7
pos[e] = pos[7]^pos[5]
pos[8] = pos[5]^7
pos[0] = pos[2]^pos[8]
pos[3] = pos[2]^pos[6]
pos[f] = pos[2]^pos[7]
pos[a] = pos[3]^pos[5]
pos[c] = pos[2]^pos[5]
pos[9] = pos[d]^pos[6]
```

We need brute force over 0-9a-f for pos[5], pos[6], pos[2], pos[d] and it's just 14 x 14 x 14 x 14 iterations! Here's a rather ugly script that does the job.

```
def decrypt(pos, key, ciphertext):
    m = ""
    s = 7
    for c_i in ciphertext:
        m+=key[pos[c_i]^s]
        s = pos[c_i]^s
    return binascii.unhexlify(m)

ciphertext = "85677bc8302bb20f3be728f99be0002ee88bc8fdc045b80e1dd22bc8fcc0034dd809e8f77023fbc83cd02ec8fbb11cc02cdbb62837677bc8f2277eeaaaabb1188bc998087bef3bcf40683cd02eef48f44aaee805b8045453a546815639e6592c173e4994e044a9084ea4000049e1e7e9873fc90ab9e1d4437fc9836aa80423cc2198882a"

available_pos_list = [1, 2, 3, 4, 5, 6, 8, 9, 10, 11, 12, 13, 14, 15]

for pos_5 in available_pos_list:
    pos = {'1': 7, '4': 0}
    pos.update({'5': pos_5})
    for pos_6 in available_pos_list:
        if pos_6 in pos.values():
            continue
        pos.update({'6': pos_6})
        pos.update({'b': pos_6^pos_5})
        pos.update({'7': pos['b']^7})
        pos.update({'e': pos['7']^pos_5})
        pos.update({'8': pos_5^7})
        for pos_2 in available_pos_list:
            if pos_2 in pos.values():
                continue
            pos.update({'2': pos_2})
            pos.update({'0': pos_2^pos['8']})
            pos.update({'3': pos_2^pos_6})
            pos.update({'f': pos_2^pos['7']})
            pos.update({'a': pos['3']^pos_5})
            pos.update({'c': pos_2^pos_5})
            for pos_d in available_pos_list:
                if pos_d in pos.values():
                    continue
                pos.update({'d': pos_d})
                pos.update({'9': pos_d^pos_6})
                reversed_pos = {value : key for (key, value) in pos.items()}
                if len(pos) == len(reversed_pos):
                    print(decrypt(pos, reversed_pos, ciphertext))
                pos.pop('9')
                pos.pop('d')
            pos.pop('c')
            pos.pop('a')
            pos.pop('f')
            pos.pop('3')
            pos.pop('0')
            pos.pop('2')
        pos.pop('8')
        pos.pop('e')
        pos.pop('7')
        pos.pop('b')
        pos.pop('6')
    pos.pop('5')
```

And we get several instances of this message: "The secret message is: Nice job! I hope you enjoyed the challenge. Here's your flag: DUCTF{d1d_y0u_Us3_gu3ss1nG_0r_l1n34r_4lg3bRA??}"

```
Flag: DUCTF{d1d_y0u_Us3_gu3ss1nG_0r_l1n34r_4lg3bRA??}
```