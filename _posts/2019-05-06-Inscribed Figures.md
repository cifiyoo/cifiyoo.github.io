---
layout: post
title: 'Inscribed Figures'
date: 2019-05-06
categories: ACM
tags: 思维 CF
---
## 题目
 
Educational Codeforces Round 64 (Rated for Div. 2)

The math faculty of Berland State University has suffered the sudden drop in the math skills of enrolling students. This year the highest grade on the entrance math test was 8. Out of 100! Thus, the decision was made to make the test easier.

Future students will be asked just a single question. They are given a sequence of integer numbers a1,a2,…,an, each number is from 1 to 3 and ai≠ai+1 for each valid i. The i-th number represents a type of the i-th figure:

circle;
isosceles triangle with the length of height equal to the length of base;
square.
The figures of the given sequence are placed somewhere on a Cartesian plane in such a way that:

(i+1)-th figure is inscribed into the i-th one;
each triangle base is parallel to OX;
the triangle is oriented in such a way that the vertex opposite to its base is at the top;
each square sides are parallel to the axes;
for each i from 2 to n figure i has the maximum possible length of side for triangle and square and maximum radius for circle.
Note that the construction is unique for some fixed position and size of just the first figure.

The task is to calculate the number of distinct points (not necessarily with integer coordinates) where figures touch. The trick is, however, that the number is sometimes infinite. But that won't make the task difficult for you, will it?

So can you pass the math test and enroll into Berland State University?

Input
The first line contains a single integer n (2≤n≤100) — the number of figures.

The second line contains n integer numbers a1,a2,…,an (1≤ai≤3, ai≠ai+1) — types of the figures.

Output
The first line should contain either the word "Infinite" if the number of distinct points where figures touch is infinite or "Finite" otherwise.

If the number is finite than print it in the second line. It's guaranteed that the number fits into 32-bit integer type.

## 思路
题目大意，三种图形，圆，等腰三角形，矩形，分别对应1,2,3。给出一个序列求出图形叠加后的交点个数。列举出三个数的全排列情况即可，需要特别注意的是，(3,1,2)这个序列，按叠加公式来看交点个数为7，但实际上坑点在于等腰三角形的高与底长相等，故有两个交点一定重合，在这种情况下一共只有 六个交点。
## 代码
```clike
#include<bits/stdc++.h>
using namespace std;
int main(int argc, char const *argv[])
{
    int n;
    int num[105];
    bool flag = true;
    scanf("%d", &n);
    for(int i = 0 ; i < n; i++)
    {
        scanf("%d", &num[i]);
        if(i == 0)continue;
        else
        {
            if((num[i - 1] == 2 && num[i] == 3) || (num[i - 1] == 3 && num[i] == 2))
                flag = false;
        }
    }
    if(!flag) printf("Infinite\n");
    else
    {
        int sum = 0;
        for(int i = 1; i < n; i++)
        {
            int x = num[i], y = num[i - 1];
            if((x == 1 && y == 2) || (x == 2 && y == 1))sum += 3;
            else if((x == 1 && y == 3) || (x == 3 && y == 1))sum += 4;
        }
        for(int i = 2; i < n; i++)
        {
            if(num[i - 2] == 3 && num[i - 1] == 1 && num[i] == 2)
                sum--;
        }
        printf("Finite\n");
        printf("%d\n", sum);
    }

    return 0;
}
```