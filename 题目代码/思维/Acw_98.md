[题目链接](https://www.acwing.com/problem/content/100/)

**考察知识点：** 坐标变换、递归、分治。

-----

核心问题：==计算出点的坐标。==

策略是递归算出子图形中的坐标，再进行平移得到当前图形中的坐标。

采用下图方式建立坐标系：原点在中心。

![](D:\资料\算法笔记\img\Acw_98.jpg)

前置知识：

$(x,y)$ 逆时针旋转 $\theta$ 角度，坐标为 $(x\cos\theta-y\sin\theta,x\sin\theta-y\cos\theta)$ 。



设 $n$ 为等级，$m$ 为在等级为 $n$ 时的编号。

$单位长度=2^{n}$ 。

$len = \frac{单位长度}{2} = 2^{n-1}$ 。

$m=4^{n}=2^{2n}$ 。

等级 $2$ 的 $0$ 号图形是由等级 $1$ 的图形顺时针旋转 $90°$ ，再进行 $y$ 轴轴对称得到。 

假设在等级 $1$ 中的坐标为 $(x,y)$ ，旋转后为 $(y,-x)$ ，再进行关于 $y$ 轴的轴对称得到 $(-y,-x)$ 。

同理可以得到如下表格：

| 原始坐标 | 图形0中坐标 | 图形1中坐标 | 图形2中坐标 | 图形3中坐标 |
| :------: | :---------: | :---------: | :---------: | :---------: |
| $(x,y)$  |  $(-y,-x)$  |   $(x,y)$   |   $(x,y)$   |   $(y,x)$   |

因为等级 $1$ 的原点和等级 $2$ 的原点不重合，所以需要将原点进行平移。

原点平移后得到最终坐标如下：

| 原始坐标 |       图形0       |      图形1      |      图形2      |      图形3      |
| :------: | :---------------: | :-------------: | :-------------: | :-------------: |
| $(x,y) $ | $(-y-len,-x+len)$ | $(x+len,y+len)$ | $(x+len,y-len)$ | $(y-len,x-len)$ |

我们的编号从 $0$ 开始，计算坐标注意减一。



**时间复杂度：** $O(n)$



#### 代码

```cpp
// #pragma GCC optimize(3)
#include <set>
#include <map>
#include <cmath>
#include <stack>
#include <queue>
#include <deque>
#include <cctype>
#include <string>
#include <cstdio>
#include <bitset>
#include <vector>
#include <cstdlib>
#include <cstring>
#include <sstream>
#include <iostream>
#include <algorithm>
// #include <unordered_set>
// #include <unordered_map>
#define endl '\n'
#define x first
#define y second
#define fi first
#define se second
#define PI acos(-1)
// #define PI 3.1415926
#define LL long long
#define INF 0x3f3f3f3f
#define lowbit(x) (-x&x)
#define ULL unsigned LL
#define PLL pair<LL, LL>
#define PIL pair<int, LL>
#define PII pair<int, int>
#define all(x) x.begin(), x.end()
#define mem(a, b) memset(a, b, sizeof a)
#define rev(x) reverse(x.begin(), x.end())
#define IOS ios::sync_with_stdio(false),cin.tie(0),cout.tie(0)

using namespace std;

LL n, a, b;

PLL calc(LL n, LL m) {
	if (n == 0) return {0, 0};
	LL len = 1ll << (n - 1), cnt = 1ll << (2 * n - 2);
	PLL pos = calc(n - 1, m % cnt);
	LL x = pos.x, y = pos.y;
	int z = m / cnt;
	if (z == 0) {
		return {-y - len, -x + len};
	} else if (z == 1) {
		return {x + len, y + len};
	} else if (z == 2) {
		return {x + len, y - len};
	} 
	return {y - len, x - len};
}

void solve() {
	int tt;
    cin >> tt;
    while (tt -- ) {
    	cin >> n >> a >> b;
    	PLL ac = calc(n, a - 1), bc = calc(n, b - 1);
    	double dx = ac.x - bc.x, dy = ac.y - bc.y;
    	
    	printf("%.0lf\n", sqrt(dx * dx + dy * dy) * 5);
    }
}

int main() {
	IOS;
	
	solve();
	
	return 0;
}
```

