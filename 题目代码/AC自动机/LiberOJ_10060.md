### 链接

- [点此跳转](https://vjudge.net/problem/LibreOJ-10060)



### 知识点

- $AC$ 自动机
- $BFS$ 基础



### 思路和代码

先考虑如何求出一个单词 $S_i$ 在所有单词中的出现次数。

很暴力地想到，可以遍历所有单词的所有前缀，有哪些前缀的后缀等于 $S_i$ 。

但这样，时间复杂度为 $O(N \sum|S_i|)$ ，大概率会超时。

那么需要优化。

根据 $AC$ 自动机的 $ne$ 指针的定义，将当前单词的最大后缀出现次数加到 $ne$ 指针所指的单词上。

这样就可以从最长的单词，一直递推到一个字母。

只需要保证我们是按照拓扑序来递推，可以保证线性的时间复杂度。

具体做法：

- 先将所有的单词插入到字典树中，插入的同时将每个前缀的个数加一。

- 使用创建 $AC$ 自动机时的顺序，来递推每个单词出现的次数。

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

const int N = 1e6 + 10;

int n;
int tr[N][26], ne[N], cnt[N], idx;
int id[N], q[N];
char str[N];

void insert(int x) {
	int p = 0;
	for (int i = 0; str[i]; i ++ ) {
		int j = str[i] - 'a';
		if (!tr[p][j]) tr[p][j] = ++ idx;
		p = tr[p][j];
		cnt[p] ++ ;
	}
	id[x] = p;
}

void build() {
	int hh = 0, tt = -1;
	for (int i = 0; i < 26; i ++ )
		if (tr[0][i]) q[ ++ tt] = tr[0][i];
		
	while (hh <= tt) {
		int u = q[hh ++ ];
		for (int i = 0; i < 26; i ++ ) {
			int &v = tr[u][i];
			if (!v) v = tr[ne[u]][i];
			else {
				ne[v] = tr[ne[u]][i];
				q[ ++ tt ] = v;
			}
		}
	}
}

void solve() {
	cin >> n;
	for (int i = 0; i < n; i ++ ) {
		cin >> str;
		insert(i);
	}
	
	build();
	
	for (int i = idx - 1; i >= 0; i -- ) cnt[ne[q[i]]] += cnt[q[i]];
	
	for (int i = 0; i < n; i ++ ) cout << cnt[id[i]] << endl;
}

int main() {
	IOS;
	
	solve();
	
	return 0;
}
```

