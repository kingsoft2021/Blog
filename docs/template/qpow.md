## 快速幂<!-- {docsify-ignore-all} -->

```cpp
int qpow(int a, int b) {
    int res = 1;
    while (b) {
        if (b & 1) res = (res * a) % mod;
        a = (a * a) % mod;
        b >>= 1;
    }
    return res;
}
```