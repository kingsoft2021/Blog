## 火车头<!-- {docsify-ignore-all} -->

```cpp
#include <bits/extc++.h>
using namespace std;

template <typename T>
using lim = numeric_limits<T>;
template <typename T>
using prq = priority_queue<T>;
template <typename T>
using urq = priority_queue<T, vector<T>, greater<T>>;
#define For(i, a, b) for (int i = (a); i <= (b); i++)
#define Rof(i, a, b) for (int i = (a); i >= (b); i--)
#define Fo(i, a) for (auto i : a)
#define pb push_back
#define ob pop_back
#define fi first
#define se second
#define ins insert
#define ers erase
#define m0(p) memset(p, 0, sizeof(p))
#define mmx(p) memset(p, 0x3f, sizeof(p))
#define mmn(p) memset(p, 0xcf, sizeof(p))
#define smid ((l + r) >> 1)
#define lson(p) p << 1
#define rson(p) (p << 1) | 1
#define ls(p) (p << 1), l, smid
#define rs(p) (p << 1) | 1, smid + 1, r
using i64 = long long;
#define sr cin
#define sw cout
#define endl '\n'

int main(int argc, char const* argv[]) {
    ios::sync_with_stdio(false), cin.tie(0), cout.tie(0);
    return 0;
}
```

```cpp
#include <bits/extc++.h>
using namespace std;

namespace hd {
const int mod = 998244353;
struct modint {
    unsigned int val;
    modint() { val = 0; }
    modint(unsigned int _v) { val = _v; }
    friend modint operator+(const modint &a, const modint &b) {
        return modint(a.val + b.val >= mod ? a.val + b.val - mod : a.val + b.val);
    }
    friend modint operator*(const modint &a, const modint &b) { return modint(1ll * a.val * b.val % mod); }
    void operator+=(const modint &a) { *this = *this + a; }
    void operator*=(const modint &a) { *this = *this * a; }
    friend modint operator-(const modint &a, const modint &b) {
        return modint(a.val + mod - b.val >= mod ? a.val - b.val : a.val + mod - b.val);
    }
    void operator-=(const modint &a) { *this = *this - a; }
    friend modint pow(modint a, int b) {
        modint res = 1;
        while (b) {
            if (b & 1) res = res * a;
            a = a * a, b >>= 1;
        }
        return res;
    }
    modint inv() { return pow(*this, mod - 2); }
};
template <typename T>
using lim = numeric_limits<T>;
template <typename T>
using prq = priority_queue<T>;
template <typename T>
using urq = priority_queue<T, vector<T>, greater<T>>;
#define For(i, a, b) for (int i = (a); i <= (b); i++)
#define Rof(i, a, b) for (int i = (a); i >= (b); i--)
#define Fo(i, a) for (auto i : a)
#define pb push_back
#define ob pop_back
#define fi first
#define se second
#define ins insert
#define ers erase
#define m0(p) memset(p, 0, sizeof(p))
#define mmx(p) memset(p, 0x3f, sizeof(p))
#define mmn(p) memset(p, 0xcf, sizeof(p))
#define smid ((l + r) >> 1)
#define lson(p) p << 1
#define rson(p) (p << 1) | 1
#define ls(p) (p << 1), l, smid
#define rs(p) (p << 1) | 1, smid + 1, r
struct BFSI {
    virtual char gc() { return 0; }
    template <typename T>
    friend BFSI &operator>>(BFSI &in, T &res) {
        res = 0;
        T f = 1;
        char ch = in.gc();
        while (!isdigit(ch) && ch != EOF) {
            if (ch == '-') f = -1;
            ch = in.gc();
        }
        if (ch == EOF) return res = 0, in;
        while (isdigit(ch) && ch != EOF) res = (res * 10) + (ch - 48), ch = in.gc();
        return res *= f, in;
    }
};
template <>
BFSI &operator>>(BFSI &in, string &res) {
    res.clear();
    char ch = in.gc();
    while ((isblank(ch) || ch == '\n') && ch != EOF) ch = in.gc();
    if (ch == EOF) return res = "", in;
    while (!isblank(ch) && ch != '\n' && ch != EOF) res.push_back(ch), ch = in.gc();
    return in;
}
struct BFSO {
    virtual void flush() {}
    virtual streambuf *getbuf() { return 0; };
    template <typename T>
    friend BFSO &operator<<(BFSO &out, T res) {
        static auto buf = out.getbuf();
        static char stack[110];
        static int top = 0;
        if (res < 0) buf->sputc('-'), res = -res;
        if (!res) return out.getbuf()->sputc('0'), out;
        while (res) stack[++top] = res % 10 + '0', res /= 10;
        while (top) buf->sputc(stack[top]), --top;
        return out;
    }
};
template <>
BFSO &operator<<(BFSO &out, string res) {
    return out.getbuf()->sputn(res.c_str(), res.size()), out;
}
template <>
BFSO &operator<<(BFSO &out, const char *res) {
    return out.getbuf()->sputn(res, strlen(res)), out;
}
template <>
BFSO &operator<<(BFSO &out, modint res) {
    return out << res.val, out;
}
static bool flag = false;
void inter(bool f = true) { flag = f; }
BFSO &endl(BFSO &out) {
    out.getbuf()->sputc('\n');
    if (flag) out.flush();
    return out;
}
BFSO &operator<<(BFSO &out, BFSO &(*f)(BFSO &)) { return f(out); }
struct FSI : BFSI {
    char gc() { return cin.get(); }
};
static FSI sr;
struct FISI : BFSI {
    ifstream fin;
    FISI(string filename) { fin.open(filename); }
    char gc() { return fin.get(); }
};
struct FSO : BFSO {
    void flush() { cout.flush(); }
    streambuf *getbuf() { return cout.rdbuf(); }
};
static FSO sw;
struct FISO : BFSO {
    ofstream fout;
    FISO(string filename) { fout.open(filename); }
    void flush() { fout.flush(); }
    streambuf *getbuf() { return fout.rdbuf(); }
};
}  // namespace hd

using i64 = long long;
using namespace hd;

int main(int argc, char const *argv[]) {
    ios::sync_with_stdio(false), cin.tie(0), cout.tie(0);
    return 0;
}
```