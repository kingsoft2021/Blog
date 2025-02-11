```cpp
stack<int> s;
bool vis[N];
int low[N], dfn[N], dcnt, scnt;
vector<int> edc[N];
vector<pair<int, int>> G[N];
vector<int> gd;

void tj(int rt, int p, int fv) {
	dfn[p] = low[p] = ++dcnt;
	s.push(p);
	int c = 0;
	for (auto j : G[p]) {
		if (j.second == (fv ^ 1)) {
			continue;
		}
		int i = j.first;
		if (dfn[i] == 0) {
			tj(rt, i, j.second);
			if (dfn[p] <= low[i]) {
				c++;
				scnt++;
				while (true) {
					int t = s.top();
					s.pop();
					edc[scnt].push_back(t);
					if (t == i) {
						break;
					}
				}
				edc[scnt].push_back(p);
			}
			low[p] = min(low[p], low[i]);
		} else {
			low[p] = min(low[p], dfn[i]);
		}
	}
	if ((p != rt) + c >= 2) {
		gd.push_back(p);
		vis[p] = true;
	}
}
```