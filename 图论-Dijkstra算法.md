# 图论-Dijkstra算法

## 简介

==1.Dijkstra算法能求解一个点到另一个点的最短路径==

## 算法思想

1.Dijkstra算法是一种标号法：给赋权图的每一个点记一个数，称为顶点的标号（临时标号，称作T标号。或者固定标号，称作P标号）。

2.T标号表示从始顶点到该标号的最短路长的上界；

3.P标号则是从始顶点到该顶点的最短路长。

4.给顶点v1标P，标号$d(v_1)=0$，给顶点$v_j$(j=2,3,......,n)标T，标号$d(v_{j})=l_{1j}$

5.在所有的T标号中取最小值，譬如，$d(v_{j0})=l_{1j0}$，则把$v_{j0}$的T标号改成P标号，并重新计算具有T标号的其他各顶点的T标号：选顶点$v_j$的T标号$d(v_j)$与$d(v_{j0})+l_{j_0j}$中较小者作为$v_j$的新的T标号。

6.重复上述步骤，知道目标顶点的标号改为P

# 带权邻接矩阵

——将图转化成矩阵

example:

0  2  8  1  inf  inf  inf  inf  inf  inf  inf

2  0  6  inf  1  inf  inf  inf  inf  inf  inf

.......

==**注：注意途中的路线是双向箭头还是单向箭头**==

# matlab实现

```matlab
%dijkstra.m
function[min,path]=dijkstra(w,start,terminal)
n=size(w,1);
label(start)=0;
f(start)=start;
for i=1:n
    if i~=start
        label(i)=inf;
    end
end
s(1)=start;
u=start;
while length(s)<n
    for i=1:n
        ins=0;
        for j=1:length(s)
            if i==s(j)
                ins=1;
            end
        end
        if ins==0
            v=i;
            if label(v)>(label(u)+w(u,v))
               label(v)=(label(u)+w(u,v));
            f(v)=u;
            end
        end
    end
    v1=0;
    k=inf;
    for i=1:n
        ins=0;
        for j=1:length(s)
            if i==s(j)
                ins=1;
            end
        end
        if ins==0
            v=i;
            if k>label(v)
                k=label(v);
                v1=v;
            end
        end
    end
    s(length(s)+1)=v1;
    u=v1;
end
min=label(terminal);
path(1)=terminal;
i=1;
while path(i)~=start
    path(i+1)=f(path(i));
    i=i+1;
end
path(i)=start;
L=length(path);
path=path(L:-1:1);
```

```matlab
%tulun_dijkstr.m
weight=[0,2,8,1,Inf,Inf,Inf,Inf,Inf,Inf,Inf;
    2,0,6,Inf,1,Inf,Inf,Inf,Inf,Inf,Inf;
    8,6,0,7,5,1,2,Inf,Inf,Inf,Inf;
    1,Inf,7,0,Inf,Inf,9,Inf,Inf,Inf,Inf;
    Inf,1,5,Inf,0,3,Inf,2,9,Inf,Inf;
    Inf,Inf,1,Inf,3,0,4,Inf,6,Inf,Inf;
    Inf,Inf,2,9,Inf,4,0,Inf,3,1,Inf;
    Inf,Inf,Inf,Inf,2,Inf,Inf,0,7,Inf,9;
    Inf,Inf,Inf,Inf,9,6,3,7,0,1,2;
    Inf,Inf,Inf,Inf,Inf,Inf,1,Inf,1,0,4;
    Inf,Inf,Inf,Inf,Inf,Inf,Inf,9,2,4,0];
[dis,path]=dijkstra(weight,1,11)
```





























