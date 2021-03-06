# GoAlgorithm

# 前言

Golang是谷歌推出的一门静态开发语言， 此仓库尝试Go实现各种数据结构和算法.见算法[可视化](https://www.cs.usfca.edu/~galles/visualization/Algorithms.html)

算法示例：

```
--sort
----quicksort 快速排序

--heaplike
----heaps 最小堆
----leftist 左偏树
```

## 排序

### 快速排序

```
1. 定义
快速排序由C. A. R. Hoare在1962年提出。快速排序是对冒泡排序的一种改进，采用了一种分治的策略。

2. 基本思想
通过一趟排序将要排序的数据分割成独立的两部分，其中一部分的所有数据都比另外一部分的所有数据都要小，然后再按此方法对这两部分数据分别进行快速排序，整个排序过程可以递归进行，以此达到整个数据变成有序序列。

3. 步骤
a. 先从数列中取出一个数作为基准数。
b. 分区过程，将比这个数大的数全放到它的右边，小于或等于它的数全放到它的左边。
c. 再对左右区间重复第二步，直到各区间只有一个数。
```

### 堆排序

使用优先队列-最小/最大堆可实现。

## 优先队列

优先队列是一种能完成以下任务的队列：插入一个数值，取出最小的数值（获取数值，并且删除）。优先队列可以用二叉树来实现，我们称这种为二叉堆。

### 最小堆

最小堆是二叉堆的一种，是一颗完全二叉树（一种平衡树）， 其特点是父节点的键值总是小于或者等于子节点。

```
实现细节(两个操作)：

push：向堆中插入数据时，首先在堆的末尾插入数据，然后不断向上提升，直到没有大小颠倒时。
pop：从堆中删除最小值时首先把最后一个值复制到根节点上，并且删除最后一个数值。然后不断向下交换， 直到没有大小颠倒为止。在向下交换过程中，如果有两个子儿子都小于自己，就选择较小的

插入时间复杂度O(logN)，删除时间复杂度O(logN)，两个二叉堆合并时间复杂性O(NlogN).
```

最大堆同理。可用此结构实现堆排序算法。

## 左偏树

最小堆/最大堆如果两个堆进行合并，时间复杂度较高，左偏树是可合并的二叉堆，首先满足所有的堆的性质，其外，各种操作时间复杂度都是O(logN)。

```
左偏树的树节点需要保存的信息有：

1.左右子树节点编号
2.此节点到有空子结点的最短距离len(空子节点的节点，就是子节点数不足2个的节点)
3.自身权值


左偏就是每个节点的左子节点的len不小于右子节点的len（但并不代表左子节点数一定不小于右子节点数），那么可知左偏树中一个节点的距离就是右儿子距离+1（或没有右儿子），且左右子树都是左偏树。

合并树A和树B的操作方法如下： 

1.如果A或B有一个是空树，返回另一个。 
2.如果A的优先级比B低，交换A,B。(确保左堆根节点小于右堆根节点) 
3.递归处理，将B和A的右子树合并。(B,Right(A)递归处理) 
4.如果合并过后A的右儿子距离大于A的左儿子，交换A的左右儿子。(确保左儿子距离大于右儿子) 
5.更新A的距离。
```

左偏树合并操作合并的是两棵左偏树，对于堆的插入，就是合并一棵树和一个节点，对于堆的删除，就是合并根的两棵子树。