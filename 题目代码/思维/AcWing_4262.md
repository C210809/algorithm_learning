### 链接

- [点此跳转](https://www.acwing.com/problem/content/4265/)



### 思路

差分 + 贪心。

先将两个序列做差，对作完差的序列取差分序列 $s$ 。

我们需要求将 $s$ 转化为全零差分序列的最小操作次数 $t$ 。

证明：

- 将相应的操作取逆操作就能由全零的差分序列得到 $s$ ，由 $s$ 得到差序列，在加回去得原序列。

因为只能区间加减 $1$ ，结论是为 `t = max(pos, neg)` 。

证明：

- 设差分序列中正数的和为 $pos$ ，负数的和为 $neg$ 。
- 不妨设 $pos > neg$ 。
- 首先可以进行 $neg$ 次操作，将所有负数归零。
- 然后再进行 $pos - neg$ 次操作，将所有正数归零，减 $1$ 对第 $n - 1$ 个数操作(不影响差序列)。
- 所以当 $pos > neg$ 时，$t = pos$ 。
- 同理，当 $neg > pos$ 时，$t = neg$ 。
- 综上所述，$t=max(pos,neg)$ 。



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

const int N = 1e5 + 10;

int a[N];
int n;

void solve() {
	cin >> n;
	for (int i = 1; i <= n; i ++ ) cin >> a[i];
	for (int i = 1; i <= n; i ++ ) {
		int b;
		cin >> b;
		a[i] -= b;
	}
	
	for (int i = n; i; i -- ) a[i] -= a[i - 1];
	
	int pos = 0, neg = 0;
	for (int i = 1; i <= n; i ++ ) {
		if (a[i] > 0) pos += a[i];
		else neg -= a[i];
	}
	
	cout << max(pos, neg) << endl;
}

int main() {
	IOS;
	
	solve();
	
	return 0;
}

```

