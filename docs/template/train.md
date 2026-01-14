## 火车头<!-- {docsify-ignore-all} -->

```cpp
#include <bits/extc++.h>
using namespace std;

namespace hd {
const int mod = 998244353;
struct modint {
    int val;
    modint() { val = 0; }
    modint(int _v) { val = _v; }
    friend modint operator+(const modint &a, const modint &b) {
        modint res;
        res.val = a.val + b.val;
        res.val = res.val >= mod ? res.val - mod : res.val;
        return res;
    }
    friend modint operator*(const modint &a, const modint &b) {
        modint res;
        res.val = 1ll * a.val * b.val % mod;
        return res;
    }
    void operator+=(const modint &a) {
        val += a.val;
        val = val >= mod ? val - mod : val;
    }
    void operator*=(const modint &a) { val = 1ll * val * a.val % mod; }
    friend modint operator-(const modint &a, const modint &b) {
        modint res;
        res.val = a.val - b.val;
        res.val = res.val < 0 ? res.val + mod : res.val;
        return res;
    }
    void operator-=(const modint &a) {
        val -= a.val;
        val = val < 0 ? val + mod : val;
    }
    modint inv() {
        modint a = val;
        int b = mod - 2;
        modint res = 1;
        while (b) {
            if (b & 1) {
                res = res * a;
            }
            a = a * a;
            b >>= 1;
        }
        return res;
    }
    friend modint pow(modint a, int b) {
        modint res = 1;
        while (b) {
            if (b & 1) {
                res = res * a;
            }
            a = a * a;
            b >>= 1;
        }
        return res;
    }
};
struct FSI {
    template <typename T>
    friend FSI &operator>>(FSI &in, T &res) {
        res = 0;
        T f = 1;
        char ch = getchar();
        while (!isdigit(ch) && ch != EOF) {
            if (ch == '-') f = -1;
            ch = getchar();
        }
        if (ch == EOF) {
            res = 0;
            return in;
        }
        while (isdigit(ch) && ch != EOF) {
            res = (res * 10) + (ch - 48);
            ch = getchar();
        }
        res *= f;
        return in;
    }
};
template <>
FSI &operator>>(FSI &in, string &res) {
    res.clear();
    char ch = getchar();
    while ((isblank(ch) || ch == '\n') && ch != EOF) {
        ch = getchar();
    }
    if (ch == EOF) {
        res = "";
        return in;
    }
    while (!isblank(ch) && ch != '\n' && ch != EOF) {
        res.push_back(ch);
        ch = getchar();
    }
    return in;
}
static FSI sr;
struct FSO {
    template <typename T>
    friend FSO &operator<<(FSO &out, T res) {
        static std::streambuf *outbuf = cout.rdbuf();
        static char stack[110];
        static int top = 0;
        if (res < 0) {
            outbuf->sputc('-');
            res = -res;
        }
        if (!res) {
            outbuf->sputc('0');
            return out;
        }
        while (res) {
            stack[++top] = res % 10 + '0';
            res /= 10;
        }
        while (top) {
            outbuf->sputc(stack[top]);
            --top;
        }
        return out;
    }
};
template <>
FSO &operator<<(FSO &in, string res) {
    static std::streambuf *outbuf = cout.rdbuf();
    outbuf->sputn(res.c_str(), res.size());
    return in;
}
template <>
FSO &operator<<(FSO &in, const char *res) {
    static std::streambuf *outbuf = cout.rdbuf();
    outbuf->sputn(res, strlen(res));
    return in;
}
template <>
FSO &operator<<(FSO &in, modint res) {
    static std::streambuf *outbuf = cout.rdbuf();
    in << res.val;
    return in;
}
static FSO sw;
static bool flag = false;
void inter(bool f = true) { flag = f; }
struct FSE {
    friend FSO &operator<<(FSO &out, FSE &in) {
        static std::streambuf *outbuf = cout.rdbuf();
        outbuf->sputc('\n');
        if (flag) {
            cout.flush();
        }
        return out;
    }
};
static FSE sendl;
FSO &endl(FSO &in) {
    in << sendl;
    return in;
}
FSO &operator<<(FSO &in, FSO &(*f)(FSO &)) { return f(in); }
}  // namespace hd

using i64 = long long;
using namespace hd;

int main(int argc, char const *argv[]) {
    ios::sync_with_stdio(false);
    return 0;
}
```
