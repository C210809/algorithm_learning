### 链接

- [点此跳转](https://vjudge.net/problem/CodeForces-24B)



### 知识点

- 自定义规则排序



### 思路和代码

根据描述定义排序规则。

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
#define IOS ios::sync_with_stdio(false),cin.tie(0)

using namespace std;

const int N = 1010, P = 21;

int idx, n, m;
unordered_map<string, int> H;
int sum[N], rk[N][60], a[N];
int sco[10] = {25, 18, 15, 12, 10, 8, 6, 4, 2, 1};
string h[N], s;

int get(string s) {
	if (!H[s]) {
		H[s] = ++ idx;
		return idx;
	}
	return H[s];
}

bool cmp1(int a, int b) {
	if (sum[a] != sum[b]) return sum[a] > sum[b];
	for (int i = 0; i < 50; i ++ ) 
		if (rk[a][i] != rk[b][i])
			return rk[a][i] > rk[b][i];
	return true;
}

bool cmp2(int a, int b) {
	for (int i = 0; i < 50; i ++ ) {
		if (rk[a][i] != rk[b][i]) return rk[a][i] > rk[b][i];
		else if (!i && sum[a] != sum[b]) return sum[a] > sum[b];
	}
	return true;
}

void solve() {
	for (int i = 0; i < N; i ++ ) a[i] = i;
	
	cin >> n;
	for (int i = 0; i < n; i ++ ) {
		cin >> m;
		for (int j = 0, e; j < m; j ++ ) {
			cin >> s;
			e = get(s), h[e] = s;
			sum[e] += (j < 10 ? sco[j] : 0);
			rk[e][j] ++ ;
		}
	}
	
	sort(a + 1, a + idx + 1, cmp1);
	cout << h[a[1]] << endl;
	
	sort(a + 1, a + idx + 1, cmp2);
	cout << h[a[1]] << endl;
}

int main() {
	IOS;
	
	solve();
	
	return 0;
}
```

