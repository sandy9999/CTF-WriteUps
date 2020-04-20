Recursive extract of tar files. I wrote the following bash script

```
#!/bin/sh

for ((i=1000;i>0;i-=1))
do
tar -xvf $i.tar
done
```

And on opening the resulting png file, I obtain the flag.
```
picoCTF{l0t5_0f_TAR5}
```