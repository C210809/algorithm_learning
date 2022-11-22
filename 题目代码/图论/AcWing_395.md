### 链接

- [点此跳转](https://www.acwing.com/problem/content/397/)



### 思路

用 $Tarjan$ 算法将边双连通分量缩点。

缩点之后，然后再统计叶子节点的数量。

答案即为 $\frac{cnt + 1}{2}$ 。



### 代码

```cpp
// #pragma GCC optimize(3)
#include <set>
#include <map>
#include <cmath>
#include <stack>
#include <queue>
#include <deque>
#include <string>
#include <cstdio>
#include <bitset>
#include <vector>
#include <cstdlib>
#include <cstring>
#include <sstream>
#include <iostream>
#include <algorithm>
#include <unordered_set>
#include <unordered_map>
#define endl '\n'
#define fi first
#define se second
#define PI acos(-1)
// #define PI 3.1415926
#define LL long long
#define INF 0x3f3f3f3f
#define lowbit(x) (-x&x)
#define PII pair<int, int>
#define ULL unsigned long long
#define PIL pair<int, long long>
#define mem(a, b) memset(a, b, sizeof a)
#define rev(x) reverse(x.begin(), x.end())
#define IOS ios::sync_with_stdio(false),cin.tie(0),cout.tie(0)

using namespace std;

const int N = 5010, M = 20010;

int h[N], e[M], ne[M], idx;
int dfn[N], low[N], timestamp;
int stk[N], top;
int id[N], dcc_cnt;
int d[N];
bool is_bridge[M];
int n, m;

void add(int a, int b) {
	e[idx] = b, ne[idx] = h[a], h[a] = idx ++ ;
}

void tarjan(int u, int from) {
	dfn[u] = low[u] = ++ timestamp;
	stk[ ++ top] = u;
	for (int i = h[u]; ~i; i = ne[i]) {
		int j = e[i];
		if (!dfn[j]) {
			tarjan(j, i);
			low[u] = min(low[u], low[j]);
			if (low[j] > dfn[u]) is_bridge[i] = is_bridge[i ^ 1] = true;
		} else if (i != (from ^ 1)) low[u] = min(low[u], dfn[j]);
	}
	
	if (low[u] == dfn[u]) {
		++ dcc_cnt;
		int y;
		do {
			y = stk[top -- ];
			id[y] = dcc_cnt;
		} while (y != u);
	}
}

void solve() {
	mem(h, -1);
	
	cin >> n >> m;
	for (int i = 0; i < m; i ++ ) {
		int a, b;
		cin >> a >> b;
		add(a, b), add(b, a);
	}
	
	tarjan(1, -1);  // dcc缩点
	
	for (int i = 0; i < idx; i ++ ) {
		if (is_bridge[i]) d[id[e[i]]] ++ ;
	}
	
    // 统计度数为1的点，即叶子节点数目
	int cnt = 0;
	for (int i = 1; i <= dcc_cnt; i ++ ) {
		if (d[i] == 1) cnt ++ ;
	}
	
	// 结论
	cout << (cnt + 1) / 2 << endl;
}

int main() {
	IOS;
	
	solve();
	
	return 0;
}
```

