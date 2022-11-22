### 链接

- [点此跳转](https://www.acwing.com/problem/content/description/4266/)



### 代码1 动态规划

$f[i][j][k][st]$ 表示当前在 $(i,j)$ 位置上，且转向次数为 $k$ 次，且上一步是左边的点（$st=0$）或上边的点（$st=1$）的所有方案的集合，存方案数量。

```c++
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

const int N = 60;

int n, K;
char g[N][N];
int dp[N][N][5][2];

void solve() {
	int tt;
	cin >> tt;
	while (tt -- ) {
		mem(dp, 0);
		cin >> n >> K;
		for (int i = 1; i <= n; i ++ ) cin >> g[i] + 1;
		
		dp[1][1][0][0] = dp[1][1][0][1] = 1;
		for (int i = 1; i <= n; i ++ ) {
			for (int j = 1; j <= n; j ++ ) {
				if (i == 1 && j == 1) continue;
				if (g[i][j] == 'H') continue;
				for (int k = 0; k <= K; k ++ ) {
					if ((i == 1 ||  j == 1) && k > 0) continue;
					dp[i][j][k][0] = dp[i - 1][j][k][0];
					dp[i][j][k][1] = dp[i][j - 1][k][1];
					if (k > 0) {
						dp[i][j][k][0] += dp[i - 1][j][k - 1][1];
						dp[i][j][k][1] += dp[i][j - 1][k - 1][0];
					}
				}
			}
		}
		
		int ans = 0;
		for (int k = 0; k <= K; k ++ ) {
			ans += dp[n][n][k][0] + dp[n][n][k][1];
		}
		
		cout << ans << endl;
	}
}

int main() {
	IOS;
	
	solve();
	
	return 0;
}
```



### 代码2 DFS(O3优化)

```cpp
#pragma GCC optimize(3)
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

const int N = 100;

int n, k, ans;
char g[N][N];
int dx[2] = {0, 1}, dy[2] = {1, 0};

/* x,y--当前坐标 last--上一次的方向 sum--转向次数 */
void dfs(int x, int y, int last, int sum) {
	if (sum > k) return;
	if (x == n && y == n) {
		ans ++ ;
		return;
	}
	
	for (int i = 0; i < 2; i ++ ) {
		int xx = x + dx[i], yy = y + dy[i];
		if (xx > n || yy > n) continue;
		if (g[xx][yy] == 'H') continue;
		dfs(xx, yy, i, sum + (last == -1 ? 0 : (last != i)));
	}
}

void solve() {
	int tt;
    cin >> tt;
    // tt = 1;
    while (tt -- ) {
    	mem(g, 0);
    	ans = 0;
    	cin >> n >> k;
    	for (int i = 1; i <= n; i ++ ) cin >> g[i] + 1;
    	
    	dfs(1, 1, -1, 0);
    	
    	cout << ans << endl;
    }
}

int main() {
	IOS;
	
	solve();
	
	return 0;
}

```

