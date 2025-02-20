```cpp
struct matrix {
    int n, m;
    std::vector<std::vector<int>> v;
    matrix operator*(const matrix &other) const {
        matrix res;
        res.n = other.n;
        res.m = m;
        res.v.resize(res.n);
        for (int i = 0; i < res.n; ++i) {
            res.v[i].resize(res.m);
            for (int k = 0; k < other.m; ++k) {
                int tmp = other.v[i][k];
                for (int j = 0; j < res.m; ++j) {
                    res.v[i][j] = (res.v[i][j] + 1ll * tmp * v[k][j]) % mod;
                }
            }
        }
        return res;
    }
};
```