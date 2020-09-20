# Ezoterik
Forensics, 1,334 points

## Description
Inventing languages is hard. Luckily, there's plenty of them, including stupid ones.

![question](./includes/ezoterik.jpg)

## Hint
You will find what you seek beyond the whitespace
## Solution
Got trolled decoding the brainfuck on the image xD   
(It said -> `Yeah, no sorry`).  
**strings** on the image revealed some interesting text. 

>2TLEdubBbS21p7u3AUWQpj1TB98gUrgHFAiFZmbeJ8qZFb9qCUc8Qp6o86eJYkrm2NLexkSDyRYd3X9sRCRKJzoZnDtrWZKcHPxjoRaFPHfmeUyoxyyWQtiqEgdJR1WU4ywAYqRq7o55XLUgmdit6svgviN8qy72wvLvT2eWjECbqHdrKa2WjiAEvgaGxVedY8SRXXcU9JbP5Ps3RY2ieejz6DrF9NBD7mri2wrsyDs9gpVgosxnYPbwjGdmsq7GwudbqtJ7SeKgaStmygyfPast5F3ZKL9KeC2LzCeenffoZ4d4Cna7TZdkUsfdK1HNmoB46fo9jK5ENQwnWdPmZBnZ4h8uDxHpQF74rs3wPcpmch6Byu31och1cyz8JxgXkacHpTrGeAN2bEhRp8kDQpmPtj9QqaAgxTbam9hoB4mvtrRmRx5GnzzZoWW5qDxwMvgKCYWiLwtLcvjDZPNdHGbvFspFeCq7kBcTeyrjYeHxuwwwM1GpdwMdxzNiFK1jYkA4DUZRohuKxeyhBFiY9HuwD6zKf9nZMThoYwTGhAJR2d3GqVqXGsivAKLs1oBzrmH9V6vaMwAjM7Hu69TLfKHtZUThoiEDftxPJdraNxoQps3mFamNbT1U3kRdpAz5s5kq6i2jLBUjBjAdV9N8jWNqx4RgiaHTW5qqb8E6JvHgQyrVkLmMdsjoLAWaWZLRw2pQpBJehRsx1LU6wmAC1nfeLbdQxPmytaMUURBDhHVqPNxwThCzZsnA9RuKrYWGsmyTxCzVUEjvUXaU4hkoV62qn7G1TnVRiADNhRfMnxm8R2ZoSPxEhVaFyHvLweq
 
Decoding the base64 gave
```elevator lolwat
  action main
    show 114
    show 116
    show 99
    show 112
    show 123
    show 78
    show 111
    show 116
    show 32
    show 113
    show 117
    show 105
    show 116
    show 101
    show 32
    show 110
    show 111
    show 114
    show 109
    show 97
    show 108
    show 32
    show 115
    show 116
    show 101
    show 103
    show 111
    show 95
    show 52
    show 120
    show 98
    show 98
    show 52
    show 53
    show 103
    show 121
    show 116
    show 106
    show 125
  end action
  action show num
    floor num
    outFloor
  end action
end elevator
```
This is **[Elevator Esoterik Language](https://esolangs.org/wiki/Elevator)**   
Converting the printed numbers from ascii gives the flag.

## Flag
>rtcp{Not quite normal stego_4xbb45gytj}
