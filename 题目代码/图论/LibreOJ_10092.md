### 链接

-  [最大半连通子图 - LibreOJ 10092 - Virtual Judge (vjudge.net)](https://vjudge.net/problem/LibreOJ-10092) 



### 思路和代码

- 先求出原图的强连通分量。
- 然后对强连通分量再建一次图。
- 最后根据拓扑序递推，维护一条链上的节点数量和方案数。

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

const int N = 1e5 + 10, M = 2e6 + 10; 

int n, m, mod;
int h[N], hs[N], e[M], ne[M], idx;
int dfn[N], low[N], timestamp;
int stk[N], top;
bool in_stk[N];
int id[N], cnt[N], scc_cnt;
unordered_set<LL> S;
int f[N], g[N];

void add(int h[], int a, int b) {
	e[idx] = b, ne[idx] = h[a], h[a] = idx ++ ;
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
	// 第一问 求一个缩完点之后的最长链中的节点数目
	// f[i]:以i结尾的最长链的结点数目
	// g[i]:让f[i]取到最大值的方案数
	
	// 初始化
	mem(h, -1), mem(hs, -1);
	
	// 建图
	cin >> n >> m >> mod;
	for (int i = 0; i < m; i ++ ) {
		int a, b;
		cin >> a >> b;
		add(h, a, b);
	}
	
	// 求SCC
	for (int i = 1; i <= n; i ++ ) if (!dfn[i]) tarjan(i);
	
	// 根据缩完点后的图建图
	for (int i = 1; i <= n; i ++ ) {
		for (int j = h[i]; ~j; j = ne[j]) {
			int k = e[j];
			int a = id[i], b = id[k];
			LL v = (LL)a * 1000000 + b;
			if (a != b && !S.count(v)) {
				add(hs, a, b);
				S.insert(v);
			}
		}
	}
	
	// 递推
	for (int i = scc_cnt; i >= 1; i -- ) {
		if (!f[i]) {
			f[i] = cnt[i];
			g[i] = 1;
		}
		for (int j = hs[i]; ~j; j = ne[j]) {
			int k = e[j];
			if (f[k] < f[i] + cnt[k]) {
				f[k] = f[i] + cnt[k];
				g[k] = g[i];
			} else if (f[k] == f[i] + cnt[k]) g[k] = (g[k] + g[i]) % mod;
		}
	}
	
	int maxf = 0, sum;
	for (int i = 1; i <= scc_cnt; i ++ ) {
		if (f[i] > maxf) {
			maxf = f[i];
			sum = g[i];
		} else if (f[i] == maxf) {
			sum = (sum + g[i]) % mod;
		}
	}
	
	cout << maxf << endl << sum << endl;
}

int main() {
	IOS;
	
	solve();
	
	return 0;
}
```

