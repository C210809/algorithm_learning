### 链接

- [点此跳转](https://www.acwing.com/problem/content/4332/)



### 思路



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

bool st[5][5];
char g[5][5], ag[5][5];
int green, yellow;
map<char, int> mp;

void solve() {
	for (int i = 1; i <= 3; i ++ ) cin >> g[i] + 1;
	for (int i = 1; i <= 3; i ++ ) cin >> ag[i] + 1;
	
	for (int i = 1; i <= 3; i ++ ) {
		for (int j = 1; j <= 3; j ++ ) {
			if (g[i][j] == ag[i][j]) {
				green ++ ;
				st[i][j] = true;
			}
		}
	}
	
	for (int i = 1; i <= 3; i ++ ) {
		for (int j = 1; j <= 3; j ++ ) {
			if (!st[i][j]) {
				mp[g[i][j]] ++ ;
			}
		}
	}
	
	for (int i = 1; i <= 3; i ++ ) {
		for (int j = 1; j <= 3; j ++ ) {
			if (!st[i][j] && mp[ag[i][j]]) {
				yellow ++ ;
				mp[ag[i][j]] -- ;
			}
		}
	}
	
	cout << green << endl << yellow << endl;
	
}

int main() {
	IOS;
	
	solve();
	
	return 0;
}
```

