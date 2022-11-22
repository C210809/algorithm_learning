### 链接

- [点此跳转](https://vjudge.net/problem/CodeForces-431C)



### 思路

$f[i][token]$ 表示从 $f[i][token]$ 出发，走到终点的所有方案数。

$dp(num,token)$ 表示当前总和为 $num$ ，状态为 $token$ 时，到达终点 $dp(n,true)$ 的方案数。

枚举每一个当前可以选哪一个数字，使用记忆化搜索。



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

const int N = 110, mod = 1e9 + 7;

int f[N][2];
int n, k, d;

int dp(int num, bool token) {
	if (num == n) return token;
	int &e = f[num][token];
	if (~e) return e;
	e = 0;
	for (int i = 1; i <= k; i ++ ) {
		if (i + num <= n) {
			if (i >= d) e = (e + dp(num + i, true)) % mod;
			else e = (e + dp(num + i, token)) % mod;
		}
	}
	return e;
}

void solve() {
	mem(f, -1);
	cin >> n >> k >> d;
	
	cout << dp(0, false) << endl;
}

int main() {
	IOS;
	
	solve();
	
	return 0;
}

```

