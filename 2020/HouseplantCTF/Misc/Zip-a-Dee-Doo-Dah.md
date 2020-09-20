# Zip-a-Dee-Doo-Dah
Misc, 129 points

## Description
I zipped the file a bit too many times it seems... and I may have added passwords to some of the zip files... eh, they should be pretty common passwords right?  
[1819.gz](./includes/1819.gz)

## Hints
-> A script will help you with this, please don't try do this manually...  
-> All passwords should be in the SecLists/Passwords/xato-net-10-million-passwords-100.txt file, which you can get here : https://github.com/danielmiessler/SecLists/blob/master/Passwords/xato-net-10-million-passwords-100.txt
or alternatively, use "git clone https://github.com/danielmiessler/SecLists"

## Solution
Wrote a python script to recursively unzip
```
import subprocess
import os
from zipfile import ZipFile
counter = 1819
while counter >= 0:
    dir_list  = os.listdir()
    result = [i for i in dir_list if i.startswith(str(counter)+'.')]
    ext = result[0].split(".")[1]
    if ext != 'zip':
        subprocess.check_output(["7z","e",result[0]])
    else:
        f = open('hash','w')
        f.truncate()
        subprocess.call(["zip2john",result[0]],stdout=f)
        subprocess.call(["john","--wordlist=~/ctfs/tools/xato-net-10-million-passwords-100.txt","hash"])
        show = subprocess.check_output(["john","--show","hash"]).decode("ascii")
        password = show.split(":")[1].split(":")[0]
    
        with ZipFile(result[0]) as zf:
            zf.extractall(pwd=password.encode('ascii'))
    counter = counter - 1
```
Finally, we get flag.txt

## Flag
>rtcp{z1pPeD_4_c0uPl3_t00_M4Ny_t1m3s_a1b8c687}
