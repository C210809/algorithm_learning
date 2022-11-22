### 链接

- [点此跳转](https://vjudge.net/problem/LibreOJ-10091#author=0)



### 思路和代码

先求出原图中的所有强连通分量， 以下简称分量。

再统计每个分量的出度。

如果出度为 $0$ 的点的数目等于 $1$ ，答案为该分量中点的数量。

如果出度为 $0$ 的点的数目大于 $1$ 或等于 $0$ ，那么说明答案为 $0$ ，因为没有任何一个点可以被其余点达到。

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
#define IOS ios::sync_with_stdio(false),cin.tie(0)

using namespace std;

const int N = 10010, M = 50010;

int h[N], e[M], ne[M], idx, times;
int id[N], scc_cnt, cnt[N];
int dfn[N], low[N];
int stk[N], top;
bool in_stk[N];
int dout[N];
int n, m;
int zeros, sum;

void add(int a, int b) {
	e[idx] = b, ne[idx] = h[a], h[a] = idx ++ ;
}

void tarjan(int u) {
	dfn[u] = low[u] = ++ times;
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
	mem(h, -1);
	cin >> n >> m;
	for (int i = 0; i < m; i ++ ) {
		int a, b;
		cin >> a >> b;
		add(a, b);
	}
	for (int i = 1; i <= n; i ++ ) if (!dfn[i]) tarjan(i);  //求所有强连通分量
	for (int i = 1; i <= n; i ++ ) {  //统计每个强连通分量的出度
		for (int j = h[i]; ~j; j = ne[j]) {
			int k = e[j];
			int a = id[i], b = id[k];
			if (a != b) dout[a] ++ ;
		}
	}
	for (int i = 1; i <= scc_cnt; i ++ ) { // 遍历所有强连通分量
		if (!dout[i]) {
			zeros ++ ;
			sum += cnt[i];
			if (zeros > 1) {
				sum = 0;
				break;
			}
		}
	}
	cout << sum << endl;
}

int main() {
	IOS;
	
	solve();
	
	return 0;
}
```

