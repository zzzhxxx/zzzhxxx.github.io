---
title: Kruskal算法
tags:
  - Kruskal
  - 最小生成树
  - 算法
id: '74'
categories:
  - - 算法
date: 2020-10-16 20:45:18
<<<<<<< HEAD
cover: https://pic.zzzhxxx.top/2022/05/30/3b58cf65eff3a.png
=======
>>>>>>> a597a24e1f7e6d8057e941b01dfcd91c2ba0c5b7
---

# 存图

1.  邻接矩阵
2.  邻接表

> 邻接矩阵更适用于完全图

## 邻接表

1.前向星

```
struct edge{
  int u;
  int v;
  int w;
}e[MAXN];

for(int i=0;i<n;i++)
{
  cin>>u>>v>>w;
    e[i].u=u;
    e[i].v=v;
    e[i].w=w;
}
```

2.链式前向星

F1:

```
int u,v,w;
int head[V/*V是点数*/],cnt,E;//可能无向图要x2
struct edge{
  int u,v,w,nxt;
}e[100];
void add_edge(int u,int v,int w){
    e[++cnt].v=v;
    e[cnt].w=w;
    e[cnt].nxt=head[u];
    head[u]=cnt;
}
int main(){
    cin>>E;
    for(int i=1;i<=E;i++){
        cin>>u>>v>>w;
        add_edge(u,v,w);
    }
    //使用
    for(int i=head[u];i>0;i=e[i].nxt){
        int v=e[i].v;
        //......
    }
}
```

F2:vector

```
int V;//V是点数
int w,v,u,E;
struct node{
    int v,w;
};
vector <node> a[V];
int main(){
    cin>>E;
    for(int i=1;i<=E;i++){
        cin>>u>>v>>w;
        a[u].push_back((node){v,w});
        a[v].push_back((node){u,w});//无向图
    }
    for (int i = 0; i < a[u].size(); i++)
    {
        a[u][i].v;//终点
        a[u][w].w;
    }

}
```

# 最小生成树

> 唯一最短边一定在最小生成树上

## Kruskal算法

使用前向星储存

> 使用Kruskal求最小生成树的所有边之和

```
#include <bits/stdc++.h>
using namespace std;
int fa[1000];//父亲 用于并查集
int m,n,cnt,ans;
struct edge{
  int u,v,w,nxt;
}e[100];
bool cmp(edge x,edge y){
    return x.w<y.w;
}
int find(int x){
    if(x==fa[x]) return x;
    return fa[x]=find(fa[x]);
}
void merge(int x,int y){
    fa[find(x)]=find(y);
}
int main(){
    cin>>n>>m;
    for(int i=1;i<=n;i++) fa[i]=i;
    for(int i=1;i<=m;i++) 
        cin>>e[i].u>>e[i].v>>e[i].w;
    sort(e+1,e+m+1,cmp);
    for(int i=1;i<=m;i++){
        if(find(e[i].u)!=find(e[i].v)){
            merge(e[i].u,e[i].v);
            ans+=e[i].w;
            cnt++;
        }
        if(cnt==n-1){
            break;
        }
    }
}
```

[干草危机](https://noi.top/questions/1915)