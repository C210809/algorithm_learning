### 链接

- [点此跳转](https://vjudge.net/problem/CodeForces-1732A#author=Diana_Dog)



### 思路

利用到了 $gcd(a,\ a+1) =1$ ，这一个性质。

证明：

原式 $= gcd(a,a+1)$  

$=gcd(a+1,a)$

$=gcd(a,1)$

$=1$

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

const int N = 25;

int n;
int a[N];
int g;

int gcd(int a, int b) {
	return b ? gcd(b, a % b) : a;
}

void solve() {
	int tt = 1;
    cin >> tt;
    while (tt -- ) {
    	cin >> n >> g;
    	for (int i = 1; i < n; i ++ ) {
    		cin >> a[i];
    		g = gcd(g, a[i]);
    	}
    	
    	if (g == 1) cout << 0 << endl;
    	else if (gcd(g, n) == 1) cout << 1 << endl;  // 对最后一个操作
    	else if (gcd(g, n - 1) == 1) cout << 2 << endl;  // 对倒数第二个操作
        //对最后两个操作，用到上面的性质
    	else if (gcd(gcd(g, n), n - 1) == 1) cout << 3 << endl;  
    }
}

int main() {
	IOS;
	
	solve();
	
	return 0;
}
```

