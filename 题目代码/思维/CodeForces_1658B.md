### 链接

- [点此跳转](https://vjudge.net/problem/CodeForces-1658B)



### 思路

$gcd(1\times p_1,2\times p_2,...,n\times p_n)$ 最大值为 $2$ 。

证明参考：[CF官网证明](https://codeforces.com/blog/entry/101302)

当 $n$ 为偶数的时。

构造方法为：奇数与偶数匹配，偶数与奇数匹配，答案数量为 $(\frac{n}{2}!)^2$ 。

当 $n$ 为奇数时，答案为 $0$ 。



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

const int N = 1e3 + 10, mod = 998244353;

int n;
int ans[N];

int fac(int x) {
	int res = 1;
	for (int i = 1; i <= x; i ++ ) res = (LL)res * i % mod;
	return res;
}

void init() {
	for (int i = 1; i <= 1000; i ++ ) {
		if (i & 1) ans[i] = 0;
		else ans[i] = (LL)fac(i / 2) % mod * fac(i / 2) % mod;
	}
}

void solve() {
	init();
	
	int tt = 1;
    cin >> tt;
    while (tt -- ) {
    	cin >> n;
    	cout << ans[n] << endl;
    }
}

int main() {
	IOS;
	
	solve();
	
	return 0;
}
```

