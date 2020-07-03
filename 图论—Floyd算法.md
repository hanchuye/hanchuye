# 图论—Floyd算法

## 简介

Floyd算法是一个经典的动态规划算法，目标是寻找从点i到点j的最短路径。

## 算法思想

从任意节点i到任意节点j的最短路径不外乎2钟可能，1是直接从i到j，2是从i经过若干个点节点k到j。所以，我们假设Dis（i，j）为节点u到节点v的最短路径，对于每一个节点k，我们检查Dis(i,k)+Dis(k,j)<Dis(i,j)是否成立，如果成立，证明从i到k再到j的路径比直接从i到j的路径短，我们便设置Dis(i,j)=Dis(k,j)+Dis(k.j)，这样一来，当我们遍历完所有节点k，Dis(i,j)中记录的便是i到j的最短路径的距离。

## 

```matlab
%floyd.m
a=[0,50,inf,40,25,10;
    50,0,15,20,inf,25;
    inf,15,0,10,20,inf;
    40,20,10,0,10,25;
    25,inf,20,10,0,55;
    10,25,inf,25,55,0];
[D,path]=floyd(a)
```

```matlab 
%tulun_floyd.m
function[D,path,mim1,path1]=floyd(a,start,terminal)
D=a;
n=size(D,1);
path=zeros(n,n);
for i=1:n
    for j=1:n
        if D(i,j)~=inf
            path(i,j)=j;
        end
    end
end
for k=i:n
    for i=1:n
        for j=1:n
            if D(i,k)+D(k,j)<D(i,j)
                D(i,j)=D(i,k)+D(k,j);
                path(i,j)=path(i,k);
            end
        end
    end
end
if nargin==3
    min1=D(start,terminal);
    m(1)=start;
    i=1;
    path1=[ ];
    while path(m(i),terminal)~=terminal
        k=i+1;
        m(k)=path(m(i),terminal);
        i=i+1;
    end
    m(i+1)=terminal;
    path1=m;
end
```

```
%输出解释
>> tulun_floyd

D =

     0    35   Inf    35    25    10
    35     0    15    20    80    25
   Inf    15     0    10    20   Inf
    35    20    10     0    10    25
    25    80    20    10     0    55
    10    25   Inf    25    55     0


path =

     1     6     0     6     5     6
     6     2     3     4     6     6
     0     2     3     4     5     0
     6     2     3     4     5     6
     1     6     3     4     5     6
     1     2     0     4     5     6
    
path是路径输出矩阵
例如从2到5的最短走法为，path(2,5)=4;path(4,5)=5;path(5,5)=5;
所以最短路径为2->4->5;

D是最短距离矩阵：
例如从2到5的距离为，D(2,5)=30，D(4,5)=10;
所以最短路长为30+10=40;
```

