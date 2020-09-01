---
title: DFS
date: 2020-06-08 10:00:34
tags:
    -大一学习
---
周一无课的早上整理一下树和图中运用到的DFS算法和思想
---

<!--more-->

# 树中的DFS算法的应用：

## 主要体现在树的先根遍历上。

## 树的先根遍历非递归算法代码:
```
void pre_order(BiTree root){
    if(root!=NULL){
        Visit(root->data);
        pre_order(root->left);
        pre_order(root->right);
    }
}
# 先根遍历是明显的深度优先算法，不断地往下走去遍历。
```

## 二叉树的先根遍历递归算法代码:
```
void Preorder(BiTree root)
{
    InitStack(&s);
    BiTree p = root;
    while (p != NULL || !IsEmpty(&S))
    {
        if (p != NULL)
        {
            printf("%2d", p->data);
            Push(&s, p);
            p = p->LChild;
        }
        else
        {
            Pop(&s,&p);
            p = p->RChild;
        }
    }
}
# 本质十分易见的，通过栈的方式去实现先根遍历的思想。
读取一个结点的值，然后把它的儿子都push到栈里面，
每次pop一个出来重复上述操作，其实本质十分清楚。
运用了栈的特性。
```

## 将二叉树的先根遍历拓展到树的先根遍历：
```
void RootFirst(CSTree root){
    if(root!=NULL){
        Visit(root->data);
        p = root->FirstChild;
        while(p!=NULL){
            RootFirst(p);
            p = p->Nextsibling;
        }
    }
}
# 本质上就是栈的性质的运用而已
```

## 将树的先根遍历拓展到图的DFS算法思路
```
void TraverseGraph(Graph G){
    for(vi=0;vi<g.venxum;vi++) visited[vi]=False;
    for(vi=0;vi<g.vexnum;vi++){
        if(!visited[vi]) DepthFirstSearch(g,vi);
    }
}
# 图的遍历

void DepthFirstSearch(Graph G,int v0){
    visit(v0);visited[v0] = True;

    w = FirstAdjVertex(g,v0);
    while(w!=-1){
        if(!visited[w]) DepthFirstSearch(g,w);
        
        w = NextAdjVertex(g,v0,w);
    }
}
```

## 将树的先根遍历拓展到图的邻接矩阵的DFS
```
void DepthFirstSearch(AdjMatrix g,int v0){
    visit(v0); visited[v0] = True;
    for(vj=0;vj<g,vexnum;vj++){
        if(!visited[vj]&&arcs[v0][vj].adj==1){
            DepthFirstSearch(g,vj);
        }
    }
}
```

## 将树的先根遍历拓展到图的邻接表的DFS
```
void DepthFirstSearch(AdjList g, int v0){
    visit(v0); visited[v0] = True;
    p = g.vertex[v0].firstarc;
    while(p!=NULL){
        if(!visited[p->adjvex]) DepthFirstSearch(g,p->adjvex);
        p = p->nextarc;
    }
}
```

# summary:
## DFS使用的是栈的结构去实现的，秉承着一直向下走走到底的感觉
## 相比之下BFS则使用的是队列去实现以达到广度优先搜索的目的
## 下周有时间把广度优先搜索做了吧，树的那一章有一个层次遍历，图的那一张还有图的BFS