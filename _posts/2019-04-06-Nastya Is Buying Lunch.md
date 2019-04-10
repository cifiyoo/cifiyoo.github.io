---
layout: post
title: 'Nasya Is Buying Lunch'
date: 2019-04-10
categories: ACM
tags: 思维 CF
---
## 题目
Codeforces Round #546(div2)

At the big break Nastya came to the school dining room. There are n pupils in the school, numbered from 1 to n. Unfortunately, Nastya came pretty late, so that all pupils had already stood in the queue, i.e. Nastya took the last place in the queue. Of course, it's a little bit sad for Nastya, but she is not going to despond because some pupils in the queue can agree to change places with some other pupils.

Formally, there are some pairs u, v such that if the pupil with number u stands directly in front of the pupil with number v, Nastya can ask them and they will change places.

Nastya asks you to find the maximal number of places in queue she can move forward.

Input
The first line contains two integers n and m (1≤n≤3⋅105, 0≤m≤5⋅105) — the number of pupils in the queue and number of pairs of pupils such that the first one agrees to change places with the second one if the first is directly in front of the second.

The second line contains n integers p1, p2, ..., pn — the initial arrangement of pupils in the queue, from the queue start to its end (1≤pi≤n, p is a permutation of integers from 1 to n). In other words, pi is the number of the pupil who stands on the i-th position in the queue.

The i-th of the following m lines contains two integers ui, vi (1≤ui,vi≤n,ui≠vi), denoting that the pupil with number ui agrees to change places with the pupil with number vi if ui is directly in front of vi. It is guaranteed that if i≠j, than vi≠vj or ui≠uj. Note that it is possible that in some pairs both pupils agree to change places with each other.

Nastya is the last person in the queue, i.e. the pupil with number pn.

Output
Print a single integer — the number of places in queue she can move forward.
## 思路
队列中有N个人，有K种允许的交换顺序，请问最后一个人最多可以向前进多少位。只允许相邻的交换。记录下在每一位后面可以到达这一位的位置的个数，如果等于他后面的位置的个数，那么最后一位数一定能到达这一位。
## 代码
```clike
#include<bits/stdc++.h>
using namespace std;
const int maxn = 3e5 + 5;
vector<int>v[maxn];
int num[maxn], a[maxn];
int main()
{
    int n, m, ans = 0;
    scanf("%d%d", &n, &m);
    for(int i = 1; i <= n; i++)
        scanf("%d", &a[i]);
    while(m--)
    {
        int uu, vv;
        scanf("%d%d", &uu, &vv);
        v[vv].push_back(uu);
    }
    for(int i = 0; i < v[a[n]].size(); i++)
        num[v[a[n]][i]]++;
    for(int i = n - 1; i >= 1; i--)
    {
        if(num[a[i]] == n - i - ans)ans++;
        else
        {
            for(int j = 0; j < v[a[i]].size(); j++)
                num[v[a[i]][j]]++;
        }
    }
    printf("%d\n", ans);
}
```