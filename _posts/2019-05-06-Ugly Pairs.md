---
layout: post
title: 'Ugly Pairs'
date: 2019-05-06
categories: ACM
tags: 思维 CF
---
## 题目
Educational Codeforces Round 64 (Rated for Div. 2)

You are given a string, consisting of lowercase Latin letters.

A pair of neighbouring letters in a string is considered ugly if these letters are also neighbouring in a alphabet. For example, string "abaca" contains ugly pairs at positions (1,2) — "ab" and (2,3) — "ba". Letters 'a' and 'z' aren't considered neighbouring in a alphabet.

Can you rearrange the letters of a given string so that there are no ugly pairs? You can choose any order of the letters of the given string but you can't add any new letters or remove the existing ones. You can also leave the order the same.

If there are multiple answers, print any of them.

You also have to answer T separate queries.

Input
The first line contains a single integer T (1≤T≤100) — the number of queries.

Each of the next T lines contains string s (1≤|s|≤100) — the string for the next query. It is guaranteed that it contains only lowercase Latin letters.

Note that in hacks you have to set T=1.

Output
Print T lines. The i-th line should contain the answer to the i-th query.

If the answer for the i-th query exists, then print such a rearrangment of letters of the given string that it contains no ugly pairs. You can choose any order of the letters of the given string but you can't add any new letters or remove the existing ones. You can also leave the order the same.

If there are multiple answers, print any of them.

Otherwise print "No answer" for that query.
## 思路
题目大意，有一个小写字母的字符串要求改变字符的顺序使字符串相邻字符之间的差不为1.排序，将其分为两个部分（奇偶分），连续相同字符看做是同奇偶。最后判断两字符串的头尾差是否为1，输出即可，若两字符串的头尾都相差1，则无解。
## 代码
```clike
#include<bits/stdc++.h>
using namespace std;
int main(int argc, char const *argv[])
{
    int n;
    char s[105];
    scanf("%d", &n);
    while(n--)
    {
        int j1 = 0, j2 = 0;
        bool flag = true;
        char x[105], y[105];
        scanf("%s", s);
        int len = strlen(s);
        sort(s, s + len);
        int number = 0;
        for(int i = 0; i < len; i++)
        {
            if(number % 2 == 0)
            {
                if(s[i] == s[i - 1] && i >= 1)y[j2++] = s[i];
                else x[j1++] = s[i], number = (number + 1) % 2;
            }
            else
            {
                if(s[i] == s[i - 1] && i >= 1)x[j1++] = s[i];
                else y[j2++] = s[i], number = (number + 1) % 2;
            }
        }

        if(abs(y[0] - x[j1 - 1]) != 1)// printf("No answer\n");
        {
            for(int i = 0; i < j1; i++)
                printf("%c", x[i]);
            //printf("\n");
            for(int i = 0 ; i < j2; i++)
                printf("%c", y[i]);
            printf("\n");
        }
        else if(abs(x[0] - y[j2 - 1]) != 1)
        {
            for(int i = 0; i < j2; i++)
                printf("%c", y[i]);
            //printf("\n");
            for(int i = 0 ; i < j1; i++)
                printf("%c", x[i]);
            printf("\n");
        }
        else printf("No answer\n");
    }

    return 0;
}
```
