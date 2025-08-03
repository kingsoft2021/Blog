## 快读<!-- {docsify-ignore-all} -->

```cpp
#define getchar() (p1==p2&&(p2=(p1=buf)+fread(buf,1,393216,stdin),p1==p2)?EOF:*p1++)
static char buf[393216], *p1 = buf, *p2 = buf;
struct FSI {
	template<typename T>
	FSI& operator >> (T &res) {
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
} scan;
```