We fire up Wireshark, and search all UDP streams. We start by typing `udp.stream eq 0` in the Filter bar on top and follow the stream. Eventually on stream 6, we obtain our flag.

```
picoCTF{StaT31355_636f6e6e}
```