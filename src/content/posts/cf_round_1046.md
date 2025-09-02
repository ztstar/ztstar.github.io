---
title: CF Round 1046 (div1)
published: 2025-09-01
description: ''
image: ''
tags: []
category: 'ICPC'
draft: false 
lang: 'en'
---

[Problem A](https://codeforces.com/problemset/problem/2135/A)

This is an easy 1D DP problem. ~ Leetcode Difficulty. 

[Problem B](https://codeforces.com/problemset/problem/2135/B)

An interactive problem. 

No idea for it when I first see it. 

[Problem C](https://codeforces.com/problemset/problem/2135/B)

Keyword: Graph, xor, path, counting. 

You need to discover the property of the graph to satisfy the condition. After that, it's almost template for finding Edge Biconnectted Component (边双连通分量). When I first made guesses about the property, there is a situation I overlooked. Analyzing the giving example inputs and outputs will help with it. 

Some knowledge that are similar to each other: Strongly Connected Component (SCC, 强连通分量), Edge Biconnected Component(边双连通分量), Vertex Biconnected Component(点双连通分量). In this problem we don't need to use Tarjan. We can use a difference array. Here is an OI wiki link about BCC: [link](https://oi-wiki.org/graph/bcc/).

The official solution uses Tarjan, and it looks simpler.

My code: 
```c++
#include<bits/stdc++.h>

using namespace std;

int const N = 2e5+5;
long long const mod = 998244353;

int n,m,V;

int a[N];

vector<int> E[N];

int fa[N], dep[N];

vector<pair<int,int> > cr; // all the cross edges on dfs tree (and they must connect a node and its ancestor)

void dfs(int x) {
    dep[x] = dep[fa[x]] + 1;
    for(auto y:E[x]) {
        if (y==fa[x]) continue;
        if(fa[y] || y==1) {
            cr.push_back(make_pair(x,y));
            continue;
        }
        fa[y] = x;
        dfs(y);
    }
}

int r[N];
bool odd[N]; // whether this BCC has an odd loop

int get_root(int x) {
    return x==r[x] ? x : r[x] = get_root(r[x]);
}

void merge(int x,int y) {
    x = get_root(x), y = get_root(y);
    if(x==y) return;
    r[x] = y;
    odd[y] |= odd[x];
}

vector<int> bcc[N];

void solve() {
    cr.clear();
    scanf("%d%d%d",&n,&m,&V);
    for(int i=1;i<=n;++i) {
        scanf("%d",&a[i]);
        E[i].clear();
        bcc[i].clear();
        fa[i] = 0;
        r[i] = i;
        odd[i] = false;
    }
    for(int i=1;i<=m;++i) {
        int x,y;
        scanf("%d%d", &x, &y);
        E[x].push_back(y);
        E[y].push_back(x);
    }
    // get the dfs tree
    dfs(1);
    // merge together BCC
    for(auto i:cr) {
        int x = i.first, y = i.second;
        if(dep[x]<dep[y]) swap(x,y); // make sure that y is x's ancestor
        if((dep[x]&1)==(dep[y]&1)) {
            odd[get_root(x)] = true;
        }
        while(get_root(x)!=get_root(y)) {
            merge(x, fa[get_root(x)]);
        }
    }
    for(int i=1;i<=n;++i) {
        bcc[get_root(i)].push_back(i);
    }
    long long ans = 1;
    bool contradiction = false;
    for(int i=1;i<=n;++i) {
        if(!bcc[i].size()) continue;
        int val = -1;
        int cnt = 0;
        for(auto x:bcc[i]) {
            if(a[x]!=-1) {
                if(val==-1) val=a[x];
                else if(a[x]!=val) contradiction = true;
            } else {
                ++ cnt;
            }
        }
        if(odd[i]) {
            if(val==0 || val==-1) {
                ans = ans; // if has odd loop, then all the -1 node can only be 0
            } else {
                contradiction = true;
            }
        } else {
            if(cnt&&val==-1) ans = ans*V%mod;
        }
    }
    if(contradiction) printf("0\n");
    else printf("%lld\n", ans);
}

int main() {
    // freopen("data.in", "r", stdin);
    int T;
    scanf("%d", &T);
    while(T--) solve();
    return 0;
}
```

[Problem D2](https://codeforces.com/problemset/problem/2135/D2)

another interacitve problem. 

[Problem E2](https://codeforces.com/problemset/problem/2135/E2)

not sure if I'm going to do this for my current training?