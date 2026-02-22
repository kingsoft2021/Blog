## ST表<!-- {docsify-ignore-all} -->

```cpp
for (int i = 2; i <= n; i++) {
    lg[i] = lg[i / 2] + 1;
}
for (int i = 1; i <= n; i++) {
    f[0][i] = read();
}
for (int i = 1; i <= 2 + lg[n]; i++) {
    for (int j = 1; j <= n; j++) {
        if (j + (1 << (i - 1)) <= n) {
            f[i][j] = max(f[i - 1][j], f[i - 1][j + (1 << (i - 1))]);
        }
    }
}
```