---
title: P5661 公交换乘 题解
date: 2020-04-28 08:32:46
tags: 
    - Luogu
    - OI
    - CSP-J
    - 随笔
---
你谷不能写题解啊.
# 那这就很厉害了
[R33168573 记录详情](https://www.luogu.com.cn/record/33168573)
## 思路
维护一个100005大小的栈`S`,结构`transfer{p,t,used}`
- 输入`n`
- 循环如下
    - 输入`type,price,time`
    - 如果是地铁
        - `ans+=price;`
        - `Push(S,{price,time});`
    - 如果是公交
        - 指针`tick=NULL`;
        - 从`max(0,S.top-45)`循环到`S.top`
            - 如果`OK(S[i])`
                - `tick=&S[i];`
                - `S[i].used=true`
                - `break;`
        - 如果`tick==NULL`
            - `ans+=price;`
- 输出`ans;`
> talk is cheap and show me the code.
## Code
```c++
#include <bits/stdc++.h>
using namespace std;
struct transfer {
  long long p, t;
  bool used;
};
transfer S[100005] = {0};//栈,只压不弹
long long top = 0;
const transfer null = {-1, -1, 0};//这样比较方便判定
void Push(transfer S[], transfer t) {
  S[top] = t;
  top++;
}
//条件判断
bool OK(const long long &n, const long long &p, const long long &t) {
  if (S[n].used || S[n].p < p || t - S[n].t > 45) {
    return false;
  }
  return true;
}
//只能单独写一个了
long long select() {
  if (top - 45 < 0) {
    return 0;
  } else {
    return top - 45;
  }
}
int main() {
  long n;
  long long ans = 0;
  cin >> n;
  for (long i = 0; i < n; i++) {
    long long type, p, t;
    cin >> type >> p >> t;
    if (type == 1) {
      const transfer *trans = &null;
      for (long long j = select(); j < top; j++) {
        if (OK(j, p, t)) {
          trans = &S[j];
          S[j].used = true;
          break;
        }
      }
      if (trans == &null) {//如果未找到符合条件的票
        ans += p;
      }
    } else {
      transfer tmp = {p, t, false};//这里可以删掉
      Push(S, tmp);                //然后这里Push(S,(transfer){p,t,false});
      ans += p;
    }
  }
  cout << ans;
  return 0;
}
```
### 后记

关于这个算法的复杂度,我想说:$O(45n)$.

说多了都是泪啊.

具体可以看[这个](https://www.luogu.com.cn/discuss/show/212582)和[这个](https://www.luogu.com.cn/discuss/show/213648)

> 总是在抱0之后
> 才会想起
> ~~这道题真简单~~