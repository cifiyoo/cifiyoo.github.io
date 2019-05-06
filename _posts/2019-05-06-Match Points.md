---
layout: post
title: 'Math Points'
date: 2019-05-06
categories: ACM
tags: 思维 CF
---
## 题目

Educational Codeforces Round 64 (Rated for Div. 2)

You are given a set of points x1, x2, ..., xn on the number line.

Two points i and j can be matched with each other if the following conditions hold:

neither i nor j is matched with any other point;
|xi−xj|≥z.
What is the maximum number of pairs of points you can match with each other?

Input
The first line contains two integers n and z (2≤n≤2⋅105, 1≤z≤109) — the number of points and the constraint on the distance between matched points, respectively.

The second line contains n integers x1, x2, ..., xn (1≤xi≤109).

Output
Print one integer — the maximum number of pairs of points you can match with each other.
## 思路
题目大意，有n个数，每个数只能使用一次，两个数配对要求是两数之差不小于z.求最多有多少对。排序，然后通过尺取法求解。
## 代码
```clike
#include<bits/stdc++.h>
using namespace std;
int main(int argc, char const *argv[])
{
    int n, z;
    int num[200010], vis[200010];
    scanf("%d %d", &n, &z);
    for(int i = 0; i < n; i++)
        scanf("%d", &num[i]);
    sort(num, num + n);
    int ban = n / 2;
    int ans = 0;
    for(int i = 0 ; i < n / 2; i++)
    {
        for(; ban < n; ban++)
        {
            if(num[ban] - num[i] >= z)
            {
                ban++;
                ans++;
                break;
            }
        }
    }
    printf("%d\n", ans );
    return 0;
}
```