## 火车头

```cpp
#include <bits/extc++.h>
using namespace std;

namespace io {
	struct FSI {
		template <typename T>
		FSI &operator>>(T &res) {
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
			return *this;
		}
	};
	static FSI sr;
	const int MINPUT = 1000000;
#define getc() (p1 == p2 && (p2 = (p1 = buf) + inbuf->sgetn(buf, MINPUT), p1 == p2) ? EOF : *p1++)
	static char buf[MINPUT], *p1, *p2;
	struct FSII {
		template <typename T>
		FSII &operator>>(T &res) {
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
			return *this;
		}
	};
	static FSII ssr;
	struct FSO {
		template <typename T>
		FSO &operator<<(T res) {
			static std::streambuf *outbuf = cout.rdbuf();
			static char stack[21];
			static int top = 0;
			if (res < 0) {
				outbuf->sputc('-');
				res = -res;
			}
			if (!res) {
				outbuf->sputc('0');
				return *this;
			}
			while (res) {
				stack[++top] = res % 10 + '0';
				res /= 10;
			}
			while (top) {
				outbuf->sputc(stack[top]);
				--top;
			}
			return *this;
		}
	};
	static FSO sw;
	struct FSE {
		friend FSO &operator<<(FSO &out, FSE &in) {
			static std::streambuf *outbuf = cout.rdbuf();
			outbuf->sputc('\n');
			return out;
		}
	};
	static FSE sendl;
}

namespace modint {
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
}  // namespace modint

namespace matrix {
	struct matrix {
		int n, m;
		std::vector<std::vector<modint::modint>> v;
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
}  // namespace matrix

using namespace io;
using namespace modint;
using namespace matrix;

int main(int argc, char const* argv[]) {
	ios::sync_with_stdio(false);
	return 0;
}
```