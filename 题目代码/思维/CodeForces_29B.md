### 链接

- [点此跳转](https://vjudge.net/problem/CodeForces-29B)



### 思路

设从起点走到红绿灯用时 $t= \frac{d}{v}$ ，

令 $k=\frac{t}{g+r},\ tr=t \% (g+r)$ ，

如果 $tr < g$ ，那么从起点走到红绿灯总用时为 $t_1=k\times (g+r)+tr$ ，

如果 $tr \ge g$ ，那么从起点走到红绿灯总用时为$t_1=k\times (g+r) +(g+r)$ ，

再加上剩下的时间，$t_2=\frac{l-d}{v}$ ，

综上所述，总用时即为 $T=t_1+t_2$ 。

注：

- 关于浮点数取模问题。

```c
double fmod(double x, double y);  // 返回值为 x % y
```



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

void solve() {
	double l, d, v, g, r, t, tt;
	cin >> l >> d >> v >> g >> r;
	
	t = d / v;
	tt = floor(t / (g + r));
	t = fmod(t, g + r);
	if (t >= g) t = g + r;
	
	printf("%.6lf\n", tt * (g + r) + t + (l - d) / v);
}

int main() {
	IOS;
	
	solve();
	
	return 0;
}
```

