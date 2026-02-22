## SAM<!-- {docsify-ignore-all} -->

```cpp
struct node {
    int nx[26];
    int len, fa;
} sam[2000010];

int tcnt, rt;

void add(char c) {
    int p = rt;
    sam[rt = ++tcnt].len = sam[p].len + 1;
    while (p && !sam[p].nx[c - 'a']) {
        sam[p].nx[c - 'a'] = rt;
        p = sam[p].fa;
    }
    if (!p)
        sam[rt].fa = 1;
    else {
        if (sam[sam[p].nx[c - 'a']].len == sam[p].len + 1)
            sam[rt].fa = sam[p].nx[c - 'a'];
        else {
            sam[++tcnt] = sam[sam[p].nx[c - 'a']];
            sam[tcnt].len = sam[p].len + 1;
            sam[sam[p].nx[c - 'a']].fa = sam[rt].fa = tcnt;
            int tmp = sam[p].nx[c - 'a'];
            while (p && sam[p].nx[c - 'a'] == tmp) {
                sam[p].nx[c - 'a'] = tcnt;
                p = sam[p].fa;
            }
        }
    }
}
```