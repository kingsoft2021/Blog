## Z函数<!-- {docsify-ignore-all} -->

```cpp
//s start at 1
int z[N];

int r = 1, p = 1;
for (int i = 2, l = 1, r = 1; i <= n; i++) {
    if (i <= r && z[i - l + 1] < r - i + 1) {
        z[i] = z[i - l + 1];
    } else {
        z[i] = max(0, r - i + 1);
        while (i + z[i] < n && s[z[i]] == s[i + z[i]]) z[i]++;
    }
    if (i + z[i] - 1 > r) l = i, r = i + z[i] - 1;
  }
```