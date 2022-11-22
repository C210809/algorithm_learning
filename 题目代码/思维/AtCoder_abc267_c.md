### 链接

- [点此跳转](https://vjudge.net/problem/AtCoder-abc267_c)



### 思路

预处理前缀和，处理一下偏移量。



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

const int N = 2e5 + 10;

int n, m;
LL a[N], sum1[N], sum2[N];

void solve() {
	cin >> n >> m;
	LL ans = -1e18;
	for (int i = 1; i <= n; i ++ ) {
		cin >> a[i];
		sum2[i] = sum2[i - 1] + a[i];
		sum1[i] = sum1[i - 1] + i * a[i];
		if (i > m) {
			ans = max(ans, 
			sum1[i] - sum1[i - m - 1] - (sum2[i] - sum2[i - m - 1]) * (i - m)); 
		} else if (i == m) ans = max(ans, sum1[m]);
	}
	cout << ans << endl;
}

int main() {
	IOS;
	
	solve();
	
	return 0;
}
```

