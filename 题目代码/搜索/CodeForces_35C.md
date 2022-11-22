### 链接

- [点此跳转](https://vjudge.net/problem/CodeForces-35C)



### 思路

BFS 基础应用。



### 代码 BFS

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
#define fi first
#define se second
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

const int N = 2010;

struct Data {
	int x, y, s;
};

int n, m, k;
bool g[N][N], st[N][N];
queue<Data> q;
int dx[4] = {1, 0, -1, 0}, dy[4] = {0, 1, 0, -1};
Data maxd = {1, 1, 0};

void bfs() {
	while (q.size()) {
		auto u = q.front();
		q.pop();
		
		if (u.s > maxd.s) maxd = u;
		
		for (int i = 0; i < 4; i ++ ) {
			int x = u.x + dx[i], y = u.y + dy[i];
			if (x < 1 || x > n || y < 1 || y > m) continue;
			if (st[x][y] || g[x][y]) continue;
			st[x][y] = true, g[x][y] = true;
			q.push({x, y, u.s + 1});
		}
	}
}

void solve() {
	freopen("input.txt", "r", stdin);
  	freopen("output.txt", "w", stdout);
	cin >> n >> m >> k;
	while (k -- ) {
		int x, y;
		cin >> x >> y;
		g[x][y] = true, st[x][y] = true;
		q.push({x, y, 0});
	}
	
	bfs();
	
	cout << maxd.x << ' ' << maxd.y << endl;
}

int main() {
	IOS;
	
	solve();
	
	return 0;
}

```

