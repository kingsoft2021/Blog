## 火车头<!-- {docsify-ignore-all} -->

```cpp
#include <bits/extc++.h>
using namespace std;

namespace mint {
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
    friend modint operator/(const modint &x, const modint &y) {
        modint a = y.val;
        int b = mod - 2;
        modint res = 1;
        while (b) {
            if (b & 1) {
                res = res * a;
            }
            a = a * a;
            b >>= 1;
        }
        return x * res;
    }
    void operator/=(const modint &a) { *this = *this / a; }
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
}  // namespace mint

namespace io {
struct FSI {
    template <typename T>
    friend FSI &operator>>(FSI &in, T &res) {
        res = 0;
        T f = 1;
        char ch = getchar();
        while (!isdigit(ch)) {
            if (ch == '-') f = -1;
            ch = getchar();
        }
        while (isdigit(ch)) {
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
    while (isblank(ch) || ch == '\n') {
        ch = getchar();
    }
    while (!isblank(ch) && ch != '\n') {
        res.push_back(ch);
        ch = getchar();
    }
    return in;
}
static FSI sr;
const int MINPUT = 1000000;
#define getc() (p1 == p2 && (p2 = (p1 = buf) + inbuf->sgetn(buf, MINPUT), p1 == p2) ? EOF : *p1++)
static char buf[MINPUT], *p1, *p2;
struct FSII {
    template <typename T>
    friend FSII &operator>>(FSII &in, T &res) {
        static std::streambuf *inbuf = cin.rdbuf();
        res = 0;
        int f = 0, flag = false;
        char ch = getc();
        while (!std::isdigit(ch)) {
            if (ch == '-') {
                f = 1;
            }
            ch = getc();
        }
        if (std::isdigit(ch)) {
            res = res * 10 + ch - '0';
            ch = getc();
            flag = true;
        }
        while (std::isdigit(ch)) {
            res = res * 10 + ch - 48;
            ch = getc();
        }
        res = f ? -res : res;
        return in;
    }
};
template <>
FSII &operator>>(FSII &in, string &res) {
    static std::streambuf *inbuf = cin.rdbuf();
    res.clear();
    char ch = getchar();
    while (isblank(ch) || ch == '\n') {
        ch = getchar();
    }
    while (!isblank(ch) && ch != '\n') {
        res.push_back(ch);
        ch = getchar();
    }
    return in;
}
static FSII ssr;
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
FSO &operator<<(FSO &in, char *res) {
    static std::streambuf *outbuf = cout.rdbuf();
    outbuf->sputn(res, strlen(res));
    return in;
}
template <>
FSO &operator<<(FSO &in, const char *res) {
    static std::streambuf *outbuf = cout.rdbuf();
    outbuf->sputn(res, strlen(res));
    return in;
}
template <>
FSO &operator<<(FSO &in, mint::modint res) {
    static std::streambuf *outbuf = cout.rdbuf();
    in << res.val;
    return in;
}
static FSO sw;
struct FSE {
    friend FSO &operator<<(FSO &out, FSE &in) {
        static std::streambuf *outbuf = cout.rdbuf();
        outbuf->sputc('\n');
        return out;
    }
};
static FSE sendl;
struct FSEE {
    friend FSO &operator<<(FSO &out, FSEE &in) {
        static std::streambuf *outbuf = cout.rdbuf();
        cout.flush();
        return out;
    }
};
static FSEE se;
}  // namespace io

namespace mtr {
struct matrix {
    int n, m;
    std::vector<std::vector<mint::modint>> v;
    matrix operator*(const matrix &other) const {
        matrix res;
        res.n = other.n;
        res.m = m;
        res.v.resize(res.n);
        for (int i = 0; i < res.n; ++i) {
            res.v[i].resize(res.m);
            for (int k = 0; k < other.m; ++k) {
                auto tmp = other.v[i][k];
                for (int j = 0; j < res.m; ++j) {
                    res.v[i][j] = (res.v[i][j] + tmp * v[k][j]);
                }
            }
        }
        return res;
    }
    friend matrix qpow(matrix a, int b) {
        matrix res;
        res.n = res.m = a.n;
        res.v.resize(res.n);
        for (int i = 0; i < res.n; i++) {
            res.v[i].resize(res.m);
            res.v[i][i] = 1;
        }
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
}  // namespace mtr

using i32 = int;
using i64 = long long;
using namespace io;
using namespace mint;
using namespace mtr;

int main(int argc, char const *argv[]) {
    ios::sync_with_stdio(false);
    return 0;
}
```

## 火车尾 <!-- {docsify-ignore-all} -->

```cpp
#include <bits/stdc++.h>
using namespace std;
struct FSI{
#define ttt template<typename T>
#define lld long double
#define ll long long
#define eps 1e-9
#define endl '\n'
#define cin scio
#define cout scio
private:
    static constexpr int BUF_SIZE=1<<20; // 1MB 缓冲区
    char in_buf[BUF_SIZE],out_buf[BUF_SIZE];
    char *in_ptr=in_buf,*in_end=in_buf,*out_ptr=out_buf;
    int mod_num=0,double_num_digit=8,a[40];
    void load_input(){size_t bytes=fread(in_buf,1,BUF_SIZE,stdin);in_ptr=in_buf,in_end=in_buf+bytes;}
    char next_char(){if(in_ptr==in_end) load_input();return (in_ptr==in_end)?EOF:*in_ptr++;}
    void flush_output(){fwrite(out_buf,1,out_ptr-out_buf,stdout);out_ptr=out_buf;}
    void write_char(char ch){if(out_ptr==out_buf+BUF_SIZE) flush_output();*out_ptr++=ch;}
    ttt void write(T res){
        if(!res) return write_char('0');int cnt=0;
        while(res) a[++cnt]=res%10,res/=10;
        while(cnt) write_char(a[cnt--]^48);
    }
public:
    ll qpow(ll x,ll k,ll p=0){
        ll res=1;if(p)x%=p;
        while(k){if(k&1){res=res*x;if(p)res%=p;}x=x*x;if(p) x%=p;k>>=1;}
        return res;
    }
    FSI(){static FSI* instance=this;atexit([]{instance->flush_output();});} // 程序结束时自动刷新缓冲区
    void mod_on_off(int num){mod_num=num;}// 输入的取模开关
    void double_digit(int num){double_num_digit=num;}// 浮点数输出的精度重定义
    FSI& operator>>(char &ch){while(isblank(ch=next_char())||ch=='\n')ch=ch;return *this;}
    FSI& operator>>(string &s){
        char ch;s="";
        while(isblank(ch=next_char())||ch=='\n')ch=ch;s+=ch;
        while(!isblank(ch=next_char())&&ch!='\n'&&ch!=EOF) s+=ch;
        return *this;
    }
    FSI& operator>>(lld &res){
        res=0;ll s=0,f=1,t=0,cnt=0;char ch;
        while(!isdigit(ch=next_char()))if(ch=='-')f=-1;
        while(isdigit(ch)) s=(s<<1)+(s<<3)+(ch^48),ch=next_char();
        if(ch=='.'){while(isdigit(ch=next_char())) t=(t<<1)+(t<<3)+(ch^48),cnt++;res+=(lld)(t)/qpow(10,cnt);}
        res=s+(lld)(t)/qpow(10,cnt);
        res*=f;return *this;
    }
    ttt FSI& operator>>(T &res){
        res=0;T f=1;char ch;
        while(!isdigit(ch=next_char()))if(ch=='-')f=-1;
        while(isdigit(ch)){res=(res<<1)+(res<<3)+(ch^48),ch=next_char();if(mod_num) res%=mod_num;}
        if(mod_num) res%=mod_num;res*=f;
        return *this;
    }
    void flush(){flush_output();}// 刷新缓冲区
    FSI& operator<<(const char ch){write_char(ch);return *this;}
    FSI& operator<<(const string s){int l=s.size();for(int i=0;i<l;i++) write_char(s[i]);return *this;}
    FSI& operator<<(const char* s){int l=strlen(s);for(int i=0;i<l;i++) write_char(s[i]);return *this;}
    FSI& operator<<(lld res){
        res+=eps,write((ll)res),res-=floor(res);
        if(res>eps && double_num_digit){
            write_char('.');int cnt=0;
            while(res!=0&&cnt<double_num_digit) res*=10,write_char((ll)(res)^48),res-=floor(res),cnt++;
        }return *this;
    }
    FSI& operator<<(bool res){write_char(res^48);return *this;}
    ttt FSI& operator<<(T res){
        if(res<0) write_char('-'),res=-res;
        write(res);return *this;
    }
}scio;
signed main(){
    
    return 0;
}
```
