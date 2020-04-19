Appears to be straightforward RSA. We can obtain p and q easily from n using Fermat factorization.

```
def fermat_factor(n):
    assert n % 2 != 0

    a = gmpy2.isqrt(n)
    b2 = gmpy2.square(a) - n

    while not gmpy2.is_square(b2):
        a += 1
        b2 = gmpy2.square(a) - n

    p = a + gmpy2.isqrt(b2)
    q = a - gmpy2.isqrt(b2)
    return int(p), int(q)
```

In case you used the inverse function of Crypto.Util.number to find the inverse of e mod phi, well, bad luck! Turns out the inverse function is inaccurately implemented, and the inverse actually doesn't exist. If you noticed that gcd(e,phi) = 2, you'd figure this out sooner.

So what do we do?

We have c congruent to m^e mod n.

We can find (e/2)^-1 only however.

So how about we write c^((e/2)^-1) congruent to m^(2*(e/2)*((e/2)^-1)).

A number multipled by its modular multiplicative inverse mod phi is congruent to 1 mod phi!

So we get c congruent to m^2 mod n

Obtain the 4 modulo quadratic roots. I used this [tool](https://www.alpertron.com.ar/QUADMOD.HTM). One of them has the flag.


