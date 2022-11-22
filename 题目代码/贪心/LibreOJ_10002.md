### 链接

- [点此跳转](https://vjudge.net/problem/LibreOJ-10002#author=0)



### 思路

参考博客：[喷水装置_贪心算法](https://blog.csdn.net/zeroheitao/article/details/110428735?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522166875718516782412583268%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=166875718516782412583268&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_click~default-1-110428735-null-null.142^v65^control,201^v3^control_2,213^v2^t3_control2&utm_term=%E5%96%B7%E6%B0%B4%E8%A3%85%E7%BD%AE)

首先计算出每个洒水器与草坪上下边界的交点的横坐标 $l$ 和 $r$ 。

按照 $l$ 升序排列，$l$ 相同时按照 $r$ 降序排列。

然后按照排好序的顺序遍历，维护最大右边界。



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
#define x first
#define y second
#define fi first
#define se second
#define PI acos(-1)
// #define PI 3.1415926
#define LL long long
#define INF 0x3f3f3f3f
#define lowbit(x) (-x&x)
#define PII pair<int, int>
#define ULL unsigned long long
#define PIL pair<int, long long>
#define all(x) x.begin(), x.end()
#define mem(a, b) memset(a, b, sizeof a)
#define rev(x) reverse(x.begin(), x.end())
#define IOS ios::sync_with_stdio(false),cin.tie(0),cout.tie(0)

using namespace std;

const int N = 15010;

struct Data {
	double l, r;
}da[N];
int n;
double L, W;

bool cmp(Data a, Data b) {
	if (a.l == b.l) return a.r > b.r;
	return a.l < b.l;
}

void solve() {
	int tt;
    cin >> tt;
    while (tt -- ) {
    	mem(da, 0);
    	
    	cin >> n >> L >> W;
    	for (int i = 0; i < n; i ++ ) {
    		double x, r, t = 0;
    		cin >> x >> r;
    		if (r > W / 2) t = sqrt(pow(r, 2) - pow(W / 2, 2));
    		da[i] = {x - t, x + t};
    	}
    	
    	sort(da, da + n, cmp);
    	
    	int count = 0;
    	double start = 0, last = -1e18;
    	for (int i = 0; i < n && start < L; i ++ ) {
    		while (i < n && da[i].l <= start) {
    			last = max(last, da[i].r);
    			i ++ ;
    		}
    		count ++ ;
    		start = last;
    		if (i == n || da[i].l <= start) i -- ;
    	}
    	
    	cout << (start >= L ? count : -1) << endl;
    }
}

int main() {
	IOS;
	
	solve();
	
	return 0;
}
```

