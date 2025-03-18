```cpp
struct node {
    int ls, rs, val;
} tree[N << 5];

int cnt, root[N], nums[N];

void build(int &p, int l, int r) {
    p = ++cnt;
    if (l == r) {
        tree[p].val = nums[l];
        return;
    }
    int mid = (l + r) >> 1;
    build(tree[p].ls, l, mid);
    build(tree[p].rs, mid + 1, r);
}

int clone(int a) {
    tree[++cnt] = tree[a];
    return cnt;
}

int update(int p, int l, int r, int pos, int val) {
    p = clone(p);
    if (l == r && l == pos) {
        tree[p].val = val;
        return p;
    }
    int mid = (l + r) >> 1;
    if (pos <= mid) {
        tree[p].ls = update(tree[p].ls, l, mid, pos, val);
    } else {
        tree[p].rs = update(tree[p].rs, mid + 1, r, pos, val);
    }
    return p;
}

int query(int p, int l, int r, int pos) {
    if (l == r) {
        return tree[p].val;
    }
    int mid = (l + r) >> 1;
    if (pos <= mid) {
        return query(tree[p].ls, l, mid, pos);
    } else {
        return query(tree[p].rs, mid + 1, r, pos);
    }
}
```