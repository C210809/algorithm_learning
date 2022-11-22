### 链接

- [点此跳转](https://vjudge.net/problem/LibreOJ-10224)
- [推荐博客](https://www.acwing.com/solution/content/46059/)



### 知识点

- 矩阵快速幂

### 思路和代码

设 $f[i][j]$ 为长度是 $i$ ，不包含不吉利串，最大后缀与不吉利串匹配的长度是 $j$ 的所有字符串集合中，所有字符串的==数量==。

转移方程：

$f[i+1][k] = \sum_{j=0}^{m-1}f[i][j]\times A[j][k]$

用 $F(i)$ 表示 $[f[i][0],...,f[i][m-1]]$ 这个向量，$A[\ ][\ ]$ 表示系数矩阵。

如何求 $A[\ ][\ ]$ 呢？

如果 $f[i][j]$ 可以转移到 $f[i+1][k]$ ，那么让 $A[j][k]++$ ，即让 $f[i+1][k]+=f[i][j]$ 。

最后结果为：$\sum_{i=1}^{m-1} f[n][i]$

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
#define mem(a, b) memset(a, b, sizeof a)
#define rev(x) reverse(x.begin(), x.end())
#define IOS ios::sync_with_stdio(false),cin.tie(0)

using namespace std;

const int N = 50;

int n, m, mod;
int ne[N];
string s, t;
int a[N][N];

void get_ne() {
	for (int i = 2, j = 0; i <= m; i ++ ) {
		while (j && s[i] != s[j + 1]) j = ne[j];
		if (s[i] == s[j + 1]) j ++ ;
		ne[i] = j;
	}
}

void mul(int c[][N], int a[][N], int b[][N]) {
	static int t[N][N];
	memset(t, 0, sizeof t);
	
	for (int i = 0; i < m; i ++ )
		for (int j = 0; j < m; j ++ )
			for (int k = 0; k < m; k ++ )
				t[i][j] = (t[i][j] + a[i][k] * b[k][j]) % mod;
				
	memcpy(c, t, sizeof t);
}

int qmi(int k) {
	int f[N][N] = {1};
	while (k) {
		if (k & 1) mul(f, f, a);
		mul(a, a, a);
		k >>= 1;
	}
	
	int res = 0;
	for (int i = 0; i < m; i ++ ) res = (res + f[0][i]) % mod;
	return res;
}

void solve() {
	string t;
	cin >> n >> m >> mod >> t;
	s = " " + t;  // 下标从 1 开始
	
	// kmp
	get_ne();
	
	// 求A[][]
	for (int j = 0; j < m; j ++ )
		for (int c = '0'; c <= '9'; c ++ ) {
			int k = j;
			while (k && s[k + 1] != c) k = ne[k];
			if (s[k + 1] == c) k ++ ;
			if (k < m) a[j][k] ++ ;
		}
	
	// 快速幂
	cout << qmi(n) << endl;
}

int main() {
	IOS;
	
	solve();
	
	return 0;
}
```

