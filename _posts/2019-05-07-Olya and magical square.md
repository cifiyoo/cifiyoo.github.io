---
layout: post
title: 'Olya and magical square'
date: 2019-05-06
categories: ACM
tags: 思维 数学 CF
---
## 题目

Codeforces Round #524 (Div. 2)

Recently, Olya received a magical square with the size of 2n×2n.

It seems to her sister that one square is boring. Therefore, she asked Olya to perform exactly k splitting operations.

A Splitting operation is an operation during which Olya takes a square with side a and cuts it into 4 equal squares with side a2. If the side of the square is equal to 1, then it is impossible to apply a splitting operation to it (see examples for better understanding).

Olya is happy to fulfill her sister's request, but she also wants the condition of Olya's happiness to be satisfied after all operations.

The condition of Olya's happiness will be satisfied if the following statement is fulfilled:

Let the length of the side of the lower left square be equal to a, then the length of the side of the right upper square should also be equal to a. There should also be a path between them that consists only of squares with the side of length a. All consecutive squares on a path should have a common side.

Obviously, as long as we have one square, these conditions are met. So Olya is ready to fulfill her sister's request only under the condition that she is satisfied too. Tell her: is it possible to perform exactly k splitting operations in a certain order so that the condition of Olya's happiness is satisfied? If it is possible, tell also the size of the side of squares of which the path from the lower left square to the upper right one will consist.

Input
The first line contains one integer t (1≤t≤103) — the number of tests.

Each of the following t lines contains two integers ni and ki (1≤ni≤109,1≤ki≤1018) — the description of the i-th test, which means that initially Olya's square has size of 2ni×2ni and Olya's sister asks her to do exactly ki splitting operations.

Output
Print t lines, where in the i-th line you should output "YES" if it is possible to perform ki splitting operations in the i-th test in such a way that the condition of Olya's happiness is satisfied or print "NO" otherwise. If you printed "YES", then also print the log2 of the length of the side of the squares through space, along which you can build a path from the lower left square to the upper right one.

You can output each letter in any case (lower or upper).

If there are multiple answers, print any.
## 思路
题目大意，有一个2^n大小的正方形，每一次做十字切割，一共有K次切割机会，要求切割后从左下角到右上角的步数等于切割后路径上方形大小的边长，要使用完k次切割且最小分隔到边长1.
好难一题，重点分割路径，并且分析数据范围可知n>32时已超过k的数据范围。
## 代码
```clike
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
ll n, k, op[100];
int main()
{
    for(int i = 1; i <= 31; i++)
        //内侧，右下角格切法数量
    op[i] = op[i - 1] * 4LL + 1LL;//1 5 21 85
    int t;
    scanf("%d", &t);
    while(t--)
    {
        scanf("%I64d %I64d", &n, &k);
        if(n > 31)
        {
            printf("YES %I64d\n", n - 1);
            continue;
        }
        ll tot = 0, now = 1, j = 0, re = 0;
        while(now + tot <= k && j < n)
        {
            tot += now;//边缘圈格切割次数
            now = now * 2 + 1; // now更新为下轮操作需要操作的边缘圈的格数
            j++; // 对边缘圈的小格各操作一次 那么每格的边长又小了一半 即由2^(n-j)变为2^(n-(j+1))
            re += op[n - j] * (now - 2);//每次边缘格更新后，非边缘格的可切割数量增加
        }
        if(k > tot + re) printf("NO\n"); // 全部切到1*1小格的操作次数tot+re 仍然不够k次
        else printf("YES %I64d\n", n - j); // n-j 即缩小到最后的 log2(边长)
    }
    return 0;
}
```