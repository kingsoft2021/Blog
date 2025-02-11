```cpp
int pe[N], low[N], dfn[N], dcnt, scnt, siz[N], id[N];
vector<int> G[N];
stack<int> s;
bool vis[N];

void tj(int p) {
	dfn[p] = low[p] = ++dcnt;
	s.push(p);
	vis[p] = true;
	for (int i : G[p]) {
		if (dfn[i] == 0) {
			tj(i);
			low[p] = min(low[p], low[i]);
		} else if (vis[i]) {
			low[p] = min(low[p], dfn[i]);
		}
	}
	if (low[p] == dfn[p]) {
		scnt++;
		while(true) {
			int t = s.top();
			s.pop();
			vis[t] = false;
			siz[scnt] += pe[t];
			id[t] = scnt;
			if (t == p) {
				break;
			}
		}
	}
}
```