### 链接

- [点此跳转](https://www.acwing.com/problem/content/370/)



### 思路

利用==差分约束==的思想。

因为要求最小值，那么需要跑最长路。

第一步，使用 $tarjan$ 算法缩点，得到强连通分量的图。

第二步，在缩完点后的点建图。

第三步，根据拓扑序递推最长路。

注：

- 差分约束参考：[这篇笔记](https://zhuanlan.zhihu.com/p/104764488)



### 代码

```cpp
#include <cstdio>
#include <cstdlib>
#include <cstring>
#include <string>
#include <iostream>
#include <sstream>
#include <algorithm>
#include <cmath>
#include <vector>
#include <stack>
#include <queue>
#include <deque>
#include <bitset>
#include <set>
#include <map>
#include <unordered_set>
#include <unordered_map>
#define endl '\n'
#define PI acos(-1)
#define LL long long
#define INF 0x3f3f3f3f
#define lowbit(x) (-x&x)
#define PII pair<int, int>
#define PIL pair<int, long long>
#define mem(a, b) memset(a, b, sizeof a)
#define rev(x) reverse(x.begin(), x.end())
#define IOS ios::sync_with_stdio(false),cin.tie(0),cout.tie(0)

using namespace std;

const int N = 1e5 + 10, M = 6e5 + 10;

int n, m;
int h[N], hs[N], e[M], ne[M], w[M], idx;
int dfn[N], low[N], timestamp;
int stk[N], top;
bool in_stk[N];
int id[N], scc_cnt, cnt[N];
int dist[N];

void add(int h[], int a, int b, int c) {
	w[idx] = c, e[idx] = b, ne[idx] = h[a], h[a] = idx ++ ;
}

void tarjan(int u) {
	dfn[u] = low[u] = ++ timestamp;
	stk[ ++ top] = u, in_stk[u] = true;
	for (int i = h[u]; ~i; i = ne[i]) {
		int j = e[i];
		if (!dfn[j]) {
			tarjan(j);
			low[u] = min(low[u], low[j]);
		} else if (in_stk[j]) low[u] = min(low[u], dfn[j]);
	}
	
	if (low[u] == dfn[u]) {
		++ scc_cnt;
		int y;
		do {
			y = stk[top -- ];
			in_stk[y] = false;
			id[y] = scc_cnt;
			cnt[scc_cnt] ++ ;
		} while (y != u);
	}
}

void solve() {
	// 初始化
	mem(h, -1), mem(hs, -1);
	
	// 建图
	cin >> n >> m;
	for (int i = 0; i < m; i ++ ) {
		int t, a, b;
		cin >> t >> a >> b;
		if (t == 1) add(h, a, b, 0), add(h, b, a, 0);
		else if (t == 2) add(h, a, b, 1);
		else if (t == 3) add(h, b, a, 0);
		else if (t == 4) add(h, b, a, 1);
		else add(h, a, b, 0);
	}
	for (int i = 1; i <= n; i ++ ) add(h, 0, i, 1);
	
	// 求SCC
	tarjan(0);
	
	// 根据强连通分量再建图
	bool ok = true;
	for (int i = 0; i <= n; i ++ ) {
		for (int j = h[i]; ~j; j = ne[j]) {
			int k = e[j];
			int a = id[i], b = id[k];
			if (a == b) {
				if (w[j] > 0) {
					ok = false;
					break;
				}
			} else add(hs, a, b, w[j]);
		}
		if (!ok) break;
	}
	
	if (!ok) cout << -1 << endl;
	else {
		// 递推求最长路
		for (int i = scc_cnt; i >= 1; i -- ) {
			for (int j = hs[i]; ~j; j = ne[j]) {
				int k = e[j];
				dist[k] = max(dist[k], dist[i] + w[j]);
			}
		}
		
		LL res = 0;
		for (int i = 1; i <= scc_cnt; i ++ ) res += (LL)dist[i] * cnt[i];
		cout << res << endl;
	}
}

int main() {
	IOS;
	
	solve();
	
	return 0;
}

```

