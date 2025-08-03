## 快读<!-- {docsify-ignore-all} -->

```cpp
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