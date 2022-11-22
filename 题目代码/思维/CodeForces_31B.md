### 链接

- [点此跳转](https://vjudge.net/problem/CodeForces-31B)



### 思路

找出每一个 @ 符号的位置判断即可。 

注：

- C++截取字符串

```cpp
string substr(int pos = 0, int n = string::npos) const;

// pos 截取字符串的起始下标，不传参默认为 0
// n 需要截取的长度，不传参默认为原串的长度
// 返回值 截取的子串
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

string s;
vector<int> v;

void solve() {
	cin >> s;
	int sl = s.size();
	for (int i = 0; i < sl; i ++ ) {
		if (s[i] == '@') v.push_back(i);
	}
	
	bool ok = true;
	if (!v.size() || v[0] == 0 || v.back() == sl - 1) ok = false;
	for (int i = 0; i < (int)v.size(); i ++ ) {
		if (!i) continue;
		if (v[i] - v[i - 1] < 3) {
			ok = false;
			break;
		}
	}
	
	if (!ok) cout << "No solution" << endl;
	else {
		string res;
		if (v.size() == 1)  {
			cout << s << endl;
			return;
		}
		for (int i = 0; i < (int)v.size(); i ++ ) {
			string t;
			if (i == (int)v.size() - 1) t = s.substr(v[i - 1] + 2);
			else if (!i) t = s.substr(0, v[i] + 2);
			else t = s.substr(v[i - 1] + 2, v[i] - v[i - 1]);
			res += t;
			if (i == (int)v.size() - 1) break;
			res += ",";
		}
		cout << res << endl;
	}
}

int main() {
	IOS;
	
	solve();
	
	return 0;
}

```

