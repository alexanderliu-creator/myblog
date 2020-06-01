---
title: AboutBTree
date: 2020-05-28 10:20:36
tags:
    -大一学习
---

程序设计与算法基础的课上提到了B树非常重要，我自学了一下，把笔记记录在下面了。

---

<!--more-->

这B树吧（	心里有B树，就能学好B树）
这熟悉的感觉，嗯，确实有折半查找那味儿。

按照范围一点一点往下走本呗，NULL就找不到就完了。和树的查找很类似，平衡BTree查找效率是最高的
因此，B树的操作也应该最好建立在平衡之上。

m路BTree,意味着有m个子树，m-1个关键字，刚刚好覆盖了全范围。
根结点最少有两个NULL，这是特点。

具体的B树实现时：

	>parent结点    n(关键字个数)   k1k2k3...kn(关键字的有序集合)   p0p1p2...pn(指针指向孩子结点)   

BTree的一些操作：

```关于BTree具体的定义：
#define m NUM
typedef int Boolean
typedef struct Mbtnode
	{
	struct Mbtnode *parent;
	int keynum;
	KeyType key[m+1];
	struct Mbtnode * ptr[m+1];
	}Mbtnode,*Mbtree;

```


```关于B树的查找，若找到返回结点给fp并且将位置赋值给pos;否则，将k要被插入的地址给np，位置给pos
Boolean srch_mbtree(Mbtree mbt,KeyType k,Mbtree *np,int *pos)
{
	p = mbt;fp = NULL;found = false;i  = 0;
	while(p!=NULL&&!found){
		i  = search(p,k);
		if(i>0&&p->key[i]==k) found = true;
		else{fp = p; p = p->ptr[i]};
	}
	if(found){*np = p;*pos = j;return true;}
	else{*np = fp;*pos = i; return false;}
}
```


```
int search(Mbtree mbt,KeyType key)
{
	n = mbt->keynum;
	i = 1;
	while(i<=num&&mbt->key[i]<=key) i++;
	return(i-1);
}
```