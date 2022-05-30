---
title: 二分常见模型
date: 2018-12-10 17:57:00
tags: 
- 二分
- 算法
categories: 算法
cover: https://pic.zzzhxxx.top/img/animate/20200314104920.png
---
# 二分法常见模型
 - 二分查找（基础）
 - 二分答案（重点）
 - 代替三分(*)
 
注：*为扩展内容

# 二分答案概念
二分答案，就是二分枚举答案，由于进行二分，所以时间复杂度 O(二分次
数*单次判定时间复杂度)。

二分答案与二分查找类似，即对有着单调性的答案进行二分，确定可能的答案后，配合贪心、
DP 等其他算法检验这个答案是否合理，不断缩减范围，最终确定答案的方法。常见的检验
算法如穷举、贪心、搜索、动态规划、图论、数据结构等，可以看到，二分答案问题很好地
结合了其他算法知识，非常受命题者欢迎。
[![pic.jpg](https://i.loli.net/2018/12/08/5c0bda7887026.jpg)](https://i.loli.net/2018/12/08/5c0bda7887026.jpg)
答案的单调性大多数情况下可以转化为一个函数，其单调性证明多种多样，如下：

- 移动石头的个数越多，答案越大([NOIP2015跳石头](https://www.luogu.org/problemnew/show/P2678))
- 前 i 天的条件一定比前 i + 1 天条件更容易([NOIP2012 借教室](https://www.luogu.org/problemnew/show/P1083))
- 满足更少分配要求比满足更多的要求更容易([NOIP2010 关押罪犯](https://www.luogu.org/problemnew/show/P1525))
- 满足更大最大值比满足更小最大值的要求更容易([NOIP2015 运输计划](https://www.luogu.org/problemnew/show/P2680))
- 时间越长，越容易满足条件([NOIP2012 疫情控制](https://www.luogu.org/problemnew/show/P1084))

## 可以解决的常见问题
- 求最大的最小值([NOIP2015跳石头](https://www.luogu.org/problemnew/show/P2678))
- 求最小的最大值（[NOIP2010 关押罪犯](https://www.luogu.org/problemnew/show/P1525)）。
- 求满足条件下的最小（大）值。
- 求最靠近一个值的值。

# 代码框架

为了保证解在二分搜索的区间里，故不同的问题有着不同（但相似）的写法，可以自己画一
个区间模拟一下。

## 整数定义域上的万能二分（★推荐）
```cpp
int binary()
{
	int l =/*答案下限*/, r =/*答案上限*/, ans = 0;
	while(l <= r)
{
	int mid = (l + r) / 2;	// 防溢出, 根据数据大小调整，	mid = l+(r-l)/2
if(check(mid)) ans = mid, l = mid + 1;	// 根据具体题意，缩小范围
else r = mid - 1;
}
return ans;
}
```
## 求最小值
```cpp
int binary()
{
int l =/*答案下限*/, r =/*答案上限*/, mid;
while(l < r)
{
    mid = (l + r) / 2;
    if(check(mid)) r = mid;
    else l = mid + 1;
}
return r;
}
```

## 求最大值
```cpp
int binary()
{
int l =/*答案下限*/, r =/*答案上限*/, mid;
while(l < r)
{
    mid = (l + r + 1) /2;
    if(check(mid)) l = mid;
    else r = mid - 1;
}
return l;
}
```
## 实数定义域上的二分
```cpp
double binary()
{
 
//为了防止死循环，因为当 l+1=r 时刚好符合条件，
// (l+r)/2=l，就会无限循环。
 
double l =/*答案下限*/, r =/*答案上限*/;
while(fabs(l-r) > dlt)	// dlt=1e-6	具体精度根据题目要求决定
{
    double mid = (l + r) / 2;
    if(check(mid)) r=mid;
    else l = mid;
}
return r;// 根据具体题意，缩小范围
}
```
由于实数运算带来的精度问题，若 dlt 取太小就会导致程序死循环，因此往往指定二分次数更好。

