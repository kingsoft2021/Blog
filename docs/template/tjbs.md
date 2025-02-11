```cpp
stack<int> s;
int low[N], dfn[N], dcnt, scnt;
vector<pair<int, int>> G[N];
vector<int> vdc[N];

void tj(int p, int fv) {
	dfn[p] = low[p] = ++dcnt;
	s.push(p);
	for (auto j : G[p]) {
		if (j.second == (fv ^ 1)) {
			continue;
		}
		int i = j.first;
		if (dfn[i] == 0) {
			tj(i, j.second);
			low[p] = min(low[p], low[i]);
		} else {
			low[p] = min(low[p], dfn[i]);
		}
	}
	if (low[p] == dfn[p]) {
		scnt++;
		vector<int> temp;
		while (true) {
			int t = s.top();
			s.pop();
			temp.push_back(t);
			if (t == p) {
				break;
			}
		}
		vdc[scnt].push_back(temp);
	}
}

```