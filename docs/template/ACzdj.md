```cpp
#include <bits/stdc++.h>
using namespace std;
string s;
int n, cnt, c[200010], k[200010], in[200010], ans;

struct trie_node {
	int son[27];
	int fail;
	int flag;
	int ans;
	void init() {
		memset(son, 0, sizeof(son));
		fail = flag = 0;
	}
} trie[200010];

queue<int> q;

void init() {
	for (int i = 0; i <= cnt; i++) {
		trie[i].init();
	}
	for (int i = 1; i <= n; i++) {
		c[i] = 0;
	}
	cnt = 1;
	ans = 0;
}

void insert(string s, int num) {
	int u = 1;
	for (int i = 0; i < s.size(); i++) {
		int v = s[i] - 'a';
		if (!trie[u].son[v]) {
			trie[u].son[v] = ++cnt;
		}
		u = trie[u].son[v];
	}
	if (!trie[u].flag) {
		trie[u].flag = num;
	}
	k[num] = trie[u].flag;
	return;
}

void getfail() {
	for (int i = 0; i < 26; i++) {
		trie[0].son[i] = 1;
	}
	q.push(1);
	trie[1].fail = 0;
	while (!q.empty()) {
		int u = q.front();
		q.pop();
		int Fail = trie[u].fail;
		for (int i = 0; i < 26; i++) {
			int v = trie[u].son[i];
			if (!v) {
				trie[u].son[i] = trie[Fail].son[i];
				continue;
			}
			trie[v].fail = trie[Fail].son[i];
			in[trie[Fail].son[i]]++;
			q.push(v);
		}
	}
}

void topu() {
	for (int i = 1; i <= cnt; i++) {
		if (!in[i]) {
			q.push(i);
		}
	}
	while (!q.empty()) {
		int fr = q.front();
		q.pop();
		c[trie[fr].flag] = trie[fr].ans;
		int u = trie[fr].fail;
		trie[u].ans += trie[fr].ans;
		if (!(--in[u])) {
			q.push(u);
		}
	}
}

void query(string s) {
	int u = 1;
	for (int i = 0; i < s.size(); i++) {
		u = trie[u].son[s[i] - 'a'];
		trie[u].ans++;
	}
}
```