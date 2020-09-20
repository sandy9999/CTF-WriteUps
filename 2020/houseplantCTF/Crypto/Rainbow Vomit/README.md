A quick google search gets us this [this](https://www.boxentriq.com/code-breaking/hexahue). The given image uses this form of encoding. But since it's annoying to decode manually, we wrote a script for which just the mapping took ages.

```
from PIL import Image

im = Image.open('o.png') 
pix = im.load()
width, height = im.size
i=2
j=2
letters = []
count=0
while i < height-4:
    j=2
    while j < width-3:
        block = []
        block.append(pix[j,i])
        block.append(pix[j+1,i])
        block.append(pix[j,i+1])
        block.append(pix[j+1,i+1])
        block.append(pix[j,i+2])
        block.append(pix[j+1,i+2])
        letters.append(block)
        j = j+2
        count=count+1
    i = i+3
# print(letters)
r = (255,0,0)
g = (0,255,0)
b = (0,0,255)
c = (0,255,255)
y = (255,255,0)
p = (255,0,255)
bl = (0,0,0)
w = (255,255,255)
gr = (128,128,128)
alphabet = [
    ["A",[ p, r, g, y, b, c]],
    ["B",[ r, p, g, y, b, c]],
    ["C",[ r, g, p, y, b, c]],
    ["D",[ r, g, y, b, p, c]],
    ["E",[ r, g, y, b, p, c]],
    ["F",[ r, g, y, b, c, p]],
    ["G",[ g, r, y, b, c, p]],
    ["H",[ g, y, r, b, c, p]],
    ["I",[ g, y, b, r, c, p]],
    ["J",[ g, y, b, c, r, p]],
    ["K",[ g, y, b, c, p, r]],
    ["L",[ y, g, b, c, p, r]],
    ["M",[ y, b, g, c, p, r]],
    ["N",[ y, b, c, g, p, r]],
    ["O",[ y, b, c, p, g, r]],
    ["P",[ b, y, c, p, r, g]],
    ["Q",[ b, y, c, p, r, g]],
    ["R",[ b, c, y, p, r, g]],
    ["S",[ b, c, p, y, r, g]],
    ["T",[ b, c, p, r, y, g]],
    ["U",[ b, c, p, r, g, y]],
    ["V",[ c, b, p, r, g, y]],
    ["W",[ c, p, b, r, g, y]],
    ["X",[ c, p, r, b, g, y]],
    ["Y",[ c, p, r, g, b, y]],
    ["Z",[ c, p, r, g, y, b]],
    [".",[ bl, w, w, bl, bl, w]],
    [",",[ w, bl, bl, w, w, bl]],
    [" ",[ w, w, w, w, w, w]],
    [" ",[ bl, bl, bl, bl, bl, bl]],
    ["0",[ bl, gr, w, bl, gr, w]],
    ["1",[ gr, bl, w, bl, gr, w]],
    ["2",[ gr, w, bl, bl, gr, w]],
    ["3",[ gr, w, bl, gr, bl, w]],
    ["4",[ gr, w, bl, gr, w, bl]],
    ["5",[ w, gr, bl, gr, w, bl]],
    ["6",[ w, bl, gr, gr, w, bl]],
    ["7",[ w, bl, gr, w, gr, bl]],
    ["8",[ w, bl, gr, w, bl, gr]],
    ["9",[ bl, w, gr, w, bl, gr]]
]
string = ""
for i in letters:
    # print (i)
    for a in alphabet:
        ans = False
        for k in range(6):
            if(i[k] == a[1][k]):
                ans = True
            else:
                ans = False
                break
        if (ans == True):
            string += a[0]
            break
print (string)
```

And this was our output.

```
THDRD IS SUCH AS THING AS A TOMCAT BUT HAVD YOU DVDR HDAR OF A TOMOG. THIS IS THD MOST IMORTANT PUDSTION OF OUR TIMD, AN UNFORTUNATDLY OND THAT MAY NDVDR BD ANSWDRD BY MODRN SCIDNCD. THD DFINITION OF TOMCAT IS A MALD CAT, YDT THD NAMD FOR A MALD OG IS MAX. WAIT NO. THD NAMD FOR A MALD OG IS JUST OG. RDGARLDSS, WHAT WOUL HADN IF WD WDRD TO COMBIND A MALD OG WITH A TOMCAT. DRHAS WD DN U WITH A OG THAT VOMITS OUT FLAGS, LIKD THIS OND RTC SHOUL,FL5G4,B3,ST1CKY,OR,N0T
```

A bit of fiddling with the flag is required for it to be accepted by the platform as the correct flag.