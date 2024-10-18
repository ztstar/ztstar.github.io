---
title: Solution NAQ2024.D
description: 2024 ICPC North America Qualifier (NAQ) D. Colorful Trees
slug: 2024-NAQ-D
date: 2024-10-18 00:00:00+0000
image: cover.jpg
categories:
    - ICPC Solution
tags:
    - ICPC
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
math: true
---

this is just a test blog

https://open.kattis.com/problems/colorfultrees

> Statement: On a tree of $n$ $(n\leq10^5)$ nodes, each node has a color $c_i$ $(c_i\leq n)$. For each edge on the tree, print the number of paths that passes it and has same color on its two ends. 

Solution: For each node $x$, create a map that counts the appearances for each color in its subtree. We use the small to large strategy to merge maps. Time complexity: $\mathcal O(n\log^2n)$.

```c++
#include<bits/stdc++.h>

using namespace std;

int const N = 1e5+5;

int n;
int c[N],s[N];
vector<pair<int,int> > E[N];

long long ans[N],val[N];
map<int,int> mp[N];

void dfs(int x,int up_id)
{
    mp[x][c[x]] = 1;
    val[x] = s[c[x]]-1;
    for(auto i:E[x])
    {
        int y=i.first, id=i.second;
        if(id==up_id) continue;
        dfs(y,id);
        if(mp[x].size()<mp[y].size()) swap(mp[x],mp[y]),swap(val[x],val[y]);
        val[x] += val[y];
        for(map<int,int>::iterator it = mp[y].begin();it != mp[y].end();++it)
        {
            int col = it->first;
            val[x] -= 1ll*(s[col]-mp[x][col])*mp[x][col] + 1ll*(s[col]-mp[y][col])*mp[y][col];
            mp[x][col] += mp[y][col];
            val[x] += 1ll*(s[col]-mp[x][col])*mp[x][col];
        }
        mp[y].clear();
    }
    ans[up_id] = val[x];
}

int main()
{
    // freopen("data.in","r",stdin);
    scanf("%d",&n);
    for(int i=1;i<=n;++i)
    {
        scanf("%d",&c[i]);
        ++s[c[i]];
    }
    for(int i=1;i<n;++i)
    {
        int x,y;
        scanf("%d%d",&x,&y);
        E[x].push_back({y,i});
        E[y].push_back({x,i});
    }
    dfs(1,0);
    for(int i=1;i<n;++i) printf("%lld\n",ans[i]);
    return 0;
}
/*
g++ D2.cpp -o D2 && D2

*/
```

