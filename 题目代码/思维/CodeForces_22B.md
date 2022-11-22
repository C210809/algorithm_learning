### 链接

- [点此跳转](https://vjudge.net/problem/CodeForces-22B#author=0)



### 知识点

暴力枚举



### 思路和代码

枚举小矩形的边长，枚举小矩形的左上角的端点。

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
#define mem(a, b) memset(a, b, sizeof a)
#define rev(x) reverse(x.begin(), x.end())
#define IOS ios::sync_with_stdio(false),cin.tie(0)

using namespace std;

const int N = 30;

int n, m;
char g[N][N];

int check(int a, int b, int x, int y) {
	if (x + a - 1 > n || y + b - 1 > m) return -1;
	
	for (int i = x; i < x + a; i ++ )
		for (int j = y; j < y + b; j ++ )
			if (g[i][j] == '1') return -1;
    
	return 2 * (a + b);
}

void solve() {
	cin >> n >> m;
	for (int i = 1; i <= n; i ++ ) 
		for (int j = 1; j <= m; j ++ )
			cin >> g[i][j];
		
	int res = -1;
	for (int a = 1; a <= n; a ++ )
		for (int b = 1; b <= m; b ++ ) {
			for (int i = 1; i <= n; i ++ )
				for (int j = 1; j <= m; j ++ )
					res = max(res, check(a, b, i, j));
		}
			
	cout << res << endl;
}

int main() {
	IOS;
	
	solve();
	
	return 0;
}
```

