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
};
```