<!-- TOC -->
- [Summary-of-data-mining](#Summary-of-data-mining）
## 问题总结，一些面试题的总结，内容包括机器学习，算法与数据结构，统计学.
   -[算法与数据结构](#算法与数据结构)
	   -[1.数组，先从小到大后从大到小，找到最大值。二分查找](#数组，先从小到大后从大到小，找到最大值。二分查找)
	   -[2.概率题：1.一个随机数生成器，只能生成1-7的数字，如何用它生成1-10的数组。](#2概率题：1.一个随机数生成器，只能生成1-7的数字，如何用它生成1-10的数组。)


  -[统计](# 统计)
	   -[硬币，正面朝上概率0.7，扔一千次，出现至少一百次正的概率](#硬币，正面朝上概率0.7，扔一千次，出现至少一百次正的概率)

   [文件操作](#文件操作)
        - [1.有一个jsonline格式的文件file.txt大小约为10K](#1有一个jsonline格式的文件filetxt大小约为10k)
        - [2.补充缺失的代码](#2补充缺失的代码)
	
 ### 数组，先从小到大后从大到小，找到最大值。二分查找.
 Leetcode有求数组的峰值类似的题
 
### 2.概率题：1.一个随机数生成器，只能生成1-7的数字，如何用它生成1-10的数组。

 -一般的解法在https://blog.csdn.net/MDreamlove/article/details/48599107

### 统计
####硬币，正面朝上概率0.7，扔一千次，出现至少一百次正的概率
   考察中心极限定理

二项分布的计算有两种近似  一个是Poisson近似 一个是中心极限定理

4.t检验 单变量/多变量  正态总体以及方差齐性的条件   多个总体的均值显著差异可以用方差分析
另外，符号检验和秩和检验可以检验两总体直接中位数的差距，也是一个检验对照/试验
是否有差距的思路

### 模型
5 Kmeans   Kmeans为什么一定收敛？  涉及到EM算法Kmeans的原理就是EM框架，
EM算法收敛，所以Kmeans一定收敛


###
```Python
#头条面试
#算法题:给一组数字，这些数字里面每一个都重复出现了三次，只有一个数字x只出
#现了一个，要求在时间 O（n）空间 O（1）内解出x.
#思路：https://blog.csdn.net/baoendemao/article/details/39925679
#类似的题还有：一个数组中只有1一个元素x出现了一次，其余数组出现两次，求x
#一个数组中，只有2个互异元素x,y出现一次，其余元素出现两次，求x,y
def fill_zero(x):
    l=max([len(xx) for xx in x])
    for i in range(len(x)):
        if len(x[i])<l:
            x[i]="0"*(l-len(x[i]))+x[i]
    return x            
def get_bin(x):
    return bin(x)[2:]
def find_num(x):
    #首先把输入的数组中的每个数转化为二进制
    x_bin=list(map(get_bin,x))
    #填充0，使得所有的数组的二进制的长度一样
    x_bin_fill=fill_zero(x_bin)
    #求出二进制每个位置上的数字和，如果能被3整除，那么记为0，如果不能记为1
    a=""
    for j in range(len(x_bin_fill[0])):
        #print(j)      
        s=0
        for i in range(len(x_bin_fill)):
            s+=int(x_bin_fill[i][j])
        #print(s)
        if s%3==0:
            a+="0"
        else:
            a+="1"
    #最后把二进制转化为十进制即可，得到的就是唯一出现一次的数字
    return int(a,2)
find_num([1,2,1,2,1,2,4,4,4,6,6,6,5])
···
