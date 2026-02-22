## Manacher<!-- {docsify-ignore-all} -->

```cpp
for (int i = 1; i <= n; i++) {
    if (i > r) {
        while (i - d[i] - 1 >= 1 && i + d[i] + 1 <= n && str[i - d[i] - 1] == str[i + d[i] + 1]) {
            d[i]++;
        }
        l = i - d[i];
        r = i + d[i];
        d[i] = d[i] * 2 + 1;
    } else if (l + r - i - d[l + r - i] > l) {
        d[i] = d[l + r - i];
    } else {
        d[i] = min(r - i, d[l + r - i] / 2);
        while (i - d[i] - 1 >= 1 && i + d[i] + 1 <= n && str[i - d[i] - 1] == str[i + d[i] + 1]) {
            d[i]++;
        }
        l = i - d[i];
        r = i + d[i];
        d[i] = d[i] * 2 + 1;
    }
    ans = max(ans, d[i] / 2);
}
```