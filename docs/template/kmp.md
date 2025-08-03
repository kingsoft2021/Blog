## KMP<!-- {docsify-ignore-all} -->

```cpp
#include <bits/extc++.h>
using namespace std;

int ne[1000010];

int main() {
	ios::sync_with_stdio(false);
	string a, b;
	cin >> a >> b;
	int n = a.size();
	int m = b.size();
	int j = 0;
	for (int i = 2; i <= m; i++) {
		while (j > 0 && b[i - 1] != b[j]) {
			j = ne[j];
		}
		if (b[i - 1] == b[j]) {
			j++;
		}
		ne[i] = j;
	}
	j = 0;
	for (int i = 1; i <= n; i++) {
		while (j > 0 && a[i - 1] != b[j]) {
			j = ne[j];
		}
		if (a[i - 1] == b[j]) {
			j++;
		}
		if (j == m) {
			cout << i - m + 1 << endl;
			j = ne[j];
		}
	}
	for (int i = 1; i <= m; i++) {
		cout << ne[i] << " ";
	}
	cout << endl;
	return 0;
}
```