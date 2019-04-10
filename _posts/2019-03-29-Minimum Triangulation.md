---
layout: post
title: 'Minimum Triangulation'
date: 2019-03-29
categories: ACM
tags: 数论 CF
---
## 题目
You are given a regular polygon with n vertices labeled from 1 to n in counter-clockwise order. The triangulation of a given polygon is a set of triangles such that each vertex of each triangle is a vertex of the initial polygon, there is no pair of triangles such that their intersection has non-zero area, and the total area of all triangles is equal to the area of the given polygon. The weight of a triangulation is the sum of weigths of triangles it consists of, where the weight of a triagle is denoted as the product of labels of its vertices.

Calculate the minimum weight among all triangulations of the polygon.

Input
The first line contains single integer n (3≤n≤500) — the number of vertices in the regular polygon.

Output
Print one integer — the minimum weight among all triangulations of the given polygon.
## 思路
直接计算$∑ i×(i+1)$即可,具体数论知识后面补坑。
## 代码
```clike
#include<bits/stdc++.h>
using namespace std;
int main(int argc, char const *argv[])
{
    int n, index = 2;
    long long sum = 0;
    cin >> n;
  	for (int i = 1; i <= n-2 ; ++i)
  	{
  		sum += index * (index+1);
  		index++;
  	}
  	cout << sum << endl;
    return 0;
}
```