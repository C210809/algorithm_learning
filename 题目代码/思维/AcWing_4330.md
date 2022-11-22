### 链接

- [点此跳转](https://www.acwing.com/problem/content/4333/)



### 思路

暴力枚举。



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

int a[4], b[4];

bool cmp(int a[], int b[]) {
	int win = 0, lose = 0;
	for (int i = 0; i < 4; i ++ )
		for (int j = 0; j < 4; j ++ ) {
			if (a[i] > b[j]) win ++ ;
			else if (a[i] < b[j]) lose ++ ;
		}
	return win > lose;
}

bool check() {
	for (int i = 1; i <= 10; i ++ )
		for (int j = 1; j <= 10; j ++ ) 
			for (int k = 1; k <= 10; k ++ )
				for (int u = 1; u <= 10; u ++ ) {
					int c[4] = {i, j, k, u};
					if (cmp(a, b) && cmp(b, c) && cmp(c, a)) return true;
					if (cmp(b, a) && cmp(a, c) && cmp(c, b)) return true;
				}
	return false;
}

void solve() {
	int tt;
    cin >> tt;
    // tt = 1;
    while (tt -- ) {
    	for (int i = 0; i < 4; i ++ ) cin >> a[i];
		for (int i = 0; i < 4; i ++ ) cin >> b[i];
		
		if (check()) cout << "yes" << endl;
		else cout << "no" << endl;
    }

}

int main() {
	IOS;
	
	solve();
	
	return 0;
}
```

