## modint<!-- {docsify-ignore-all} -->

```cpp
struct modint {
    int val;
    modint() {}
    modint(int _v) {
        val = _v;
    }
    friend modint operator + (const modint& a, const modint& b) {
        modint res;
        res.val = a.val + b.val;
        res.val = res.val >= mod ? res.val - mod : res.val;
        return res;
    }
    friend modint operator * (const modint& a, const modint& b) {
        modint res;
        res.val = 1ll * a.val* b.val % mod;
        return res;
    }
    void operator += (const modint& a) {
        val += a.val;
        val = val >= mod ? val - mod : val;
    }
    void operator *= (const modint& a) {
        val = 1ll * val* a.val % mod;
    }
    friend modint operator - (const modint& a, const modint& b) {
        modint res;
        res.val = a.val - b.val;
        res.val = res.val < 0 ? res.val + mod : res.val;
        return res;
    }
    void operator -= (const modint& a) {
        val -= a.val;
        val = val < 0 ? val + mod : val;
    }
    modint inv() {
        int a = val, b = mod - 2, res = 1;
        while (b) {
            if (b & 1) {
                res = 1ll * res * a % mod;
            }
            a = 1ll * a * a % mod;
            b >>= 1;
        }
        return modint(res);
    }
};
```