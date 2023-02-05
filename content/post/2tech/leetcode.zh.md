---
title: "Leetcode每日一题"
keywords: 
- leedcode
- 算法
date: 2023-01-07T09:36:47Z
lastmod: 2023-02-04T20:27:51Z
draft: false
author: ["Martin"]
categories: 
- 分类1
- 分类2
tags: 
- Leetcode
description: "总结每天学到的知识点和有价值的题型"
weight: # 输入1可以顶置文章，用来给文章展示排序，不填就默认按时间排序
slug: ""
comments: true
showToc: true # 显示目录
TocOpen: true # 自动展开目录
hidemeta: false # 是否隐藏文章的元信息，如发布日期、作者等
disableShare: true # 底部不显示分享栏
showbreadcrumbs: true #顶部显示当前路径
cover:
    image: ""
    caption: ""
    alt: ""
    relative: false
mermaid: true
---
# 将x减到0的最小操作数([1658](https://leetcode.cn/problems/minimum-operations-to-reduce-x-to-zero/))

给你一个整数数组 ```nums``` 和一个整数 ```x``` 。每一次操作时，你应当移除数组 ```nums``` 最左边或最右边的元素，然后从 ```x``` 中减去该元素的值。请注意，需要 **修改** 数组以供接下来的操作使用。

如果可以将 ```x``` **恰好** 减到 ```0``` ，返回 **最小操作数** ；否则，返回 ```-1``` 。

```
示例1
输入：nums = [1,1,4,2,3], x = 5
输出：2
解释：最佳解决方案是移除后两个元素，将 x 减到 0 。
```
## 双指针
这里引用灵神的一句话
>窗口大小不固定的叫做双指针，窗口大小固定的叫做滑动窗口。
我觉得很合理，虽然官方称自己的解法为滑动窗口，我更愿意称其为双指针。
```java
class Solution {
    public int minOperations(int[] nums, int x) {
        int n = nums.length;
        //计算出数组中所有元素总和
        int sum = Arrays.stream(nums).sum();

        if(sum<x){
            return -1;
        }

        int right = 0;
        // lsum记录前缀的和，rsum记录后缀的和
        int lsum = 0, rsum = sum;
        int ans = n+1;

        // 初始使前缀为空，left=-1；
        // 后缀为整个数组，right不断向右移并做减法。
        // 当lsum+rsum<x时，前缀指针向右移动，并做加法。
        // 最后的结果计算是根据左右指针的位置，(left+1)+(n-right)
        // left+1表示左边操作多少次，n-right表示右边操作多少次
        for(int left = -1; left<n; ++left){
            if(left!=-1){
                lsum += nums[left];
            }
            while(right<n && lsum+rsum>x){
                rsum -= nums[right];
                ++right;
            }
            if(lsum+rsum==x){
                ans = Math.min(ans, left+1+n-right);
            }

        }

        return ans > n ? -1 : ans;
    }
}
```
## 复杂度分析
- 时间复杂度：O(n)，其中 ```n``` 是数组 ```nums``` 的长度。```left``` 和 ```right``` 均最多遍历整个数组一次。

- 空间复杂度：O(1)

# 还原排列的最少操作步数([1806](https://leetcode.cn/problems/minimum-number-of-operations-to-reinitialize-a-permutation/))
这道题有意思，数学解法，实话说高中毕业后就很少接触数学了，但是好在我还看的懂答案，写在博客里记录一下吧。

给你一个偶数 ```n​​​​​​``` ，已知存在一个长度为 ```n``` 的排列 ```perm``` ，其中 ```perm[i] == i​```（下标 从 0 开始 计数）。

一步操作中，你将创建一个新数组 ```arr``` ，对于每个 ```i``` ：

- 如果 ```i % 2 == 0``` ，那么 ```arr[i] = perm[i / 2]```
- 如果 ```i % 2 == 1``` ，那么 ```arr[i] = perm[n / 2 + (i - 1) / 2]```

然后将 ```arr​​``` 赋值​​给 ```perm``` 。

要想使 ```perm``` 回到排列初始值，至少需要执行多少步操作？返回最小的 **非零** 操作步数。

## 欧拉定理&欧拉函数
记录题目之前，要先写一下[欧拉定理](https://oi-wiki.org/math/number-theory/fermat/)和[欧拉函数](https://oi-wiki.org/math/number-theory/euler/)，方便更多人看懂这道题。

- 欧拉定理：当```a```和```m```两个数互素时，即```gcd(a, m)=1```，则```a^(ψ(m)) = 1(mod m)```
- 欧拉函数：```ψ(m)```就是欧拉函数表示的是小于等于```m```和```m```互质的数的个数

## 数学解法
对于原排列中的第i个元素，设g(i)为进行一次操作后，该元素的新下标，
- ```g(i)```为偶数，```arr[g(i)] = perm[g(i)/2]```，令x=g(i)/2，则等式转换为```arr[2x] = perm[x]```，x∈[0, (n−1)/2]
- ```g(i)```为奇数，```arr[g(i)] = perm[n/2+(g(i)-1)/2]```，令x=n/2 + (g(i)-1)/2，则等式转换为```arr[2x-n-1] = perm[x]```，x∈[n/2, n-1]

因此可以总结出
- ```0 <= i < n/2，g(i) = 2i```;
- ```n/2 <= i < n，g(i) = 2i-(n-1)```;

对于除首尾元素外的其他元素，上述表达式可转换为对```(n-1)```取模，可以转换为```g(i) = 2i(mod(n-1))```，这个方法很微妙，我这个水平肯定是想不到了。

令 ```g^k (i)``` 表示原排列 ```perm``` 中第 ```i```个元素经过 ```k``` 次变换后的下标

举例：
```g^2 (i) = g(g(i))```

所以，```g^k (i) = 2^k i(mod(n-1))```

根据上述推论，我们直接模拟即找到最小的 k 使得满足 ```2^k ≡ 1(mod(n−1))``` 即可。

代码
```java
class Solution {
    public int reinitializePermutation(int n) {
        if (n == 2) {
            return 1;
        }
        int step = 1, pow2 = 2;
        while (pow2 != 1) {
            step++;
            pow2 = pow2 * 2 % (n - 1);
        }
        return step;
    }
}
```

## 复杂度分析

欧拉定理和欧拉函数用来计算时间复杂度

由于n是偶数，则n-1一定是奇数，n-1和2互质，根据欧拉定理，```gcd(2, n-1)=1```，所以```2^(ψ(n-1)) = 1(mod (n-1))```

由此可知，```k = ψ(n-1)```，所以k一定小于n-1，因此总的时间复杂度不超过 **O(n)**。

# 破解保险箱([753](https://leetcode.cn/problems/cracking-the-safe/))
欧拉回路题目。Leetcode的每日一题真的很耗费精神，但是都很有意思，值得记录一下。

有一个需要密码才能打开的保险箱。密码是 ```n``` 位数, 密码的每一位是 ```k``` 位序列 ```0, 1, ..., k-1``` 中的一个 。

你可以随意输入密码，保险箱会自动记住最后 ```n``` 位输入，如果匹配，则能够打开保险箱。

举个例子，假设密码是 ```345```，你可以输入 ```012345``` 来打开它，只是你输入了 ```6``` 个字符。(保险箱依旧识别最后三位输入)

请返回一个能打开保险箱的最短字符串。

## 贪心构造
这道题的方法很巧妙，值得记录一下

将所有的n-1位数作为节点，每个节点都有k条边，每个节点通过一条边可以走到对应的另一个节点。



# 能构造出连续值的最大数目([1798](https://leetcode.cn/problems/maximum-number-of-consecutive-values-you-can-make/))
给一个长度为 ```n``` 的整数数组 ```coins``` ，它代表你拥有的 ```n``` 个硬币。第 ```i``` 个硬币的值为 ```coins[i]``` 。如果你从这些硬币中选出一部分硬币，它们的和为 ```x``` ，那么称，你可以 构造 出 ```x``` 。

请返回从 ```0``` 开始（包括 ```0``` ），你最多能构造出多少个连续整数。(你可能有多个相同值的硬币。)

## 总结

这道题我最初的做法是用hashmap存储coins的值，然后遍历coins中的元素，用目标值coins中的元素，然后看该元素在hashmap中是否存在，但是我忽略了可能有相同硬币这个问题。

看了答案发现这道题思路很巧，理解了半天才绕过这个弯。首先将coins数组升序排列，然后定义一个区间[l, r]，这个区间意思是有一串连续的整数，从l到r。那么现在可以设一个区间[0, x]，找到一个值y，如果y<=x+1，那么就证明[0, x+y]也是一组连续的整数。就是这里，我理解了有一会才反应过来。通俗一点讲，已知0到x这串连续整数，新来一个y，y+0一定要小于等于x+1，才可以保持连续。举个例子：现在有一串连续的整数[0, 2]，那么下一个数(即y)一定要小于等于3。因为前方序列中有0, 1, 2。0+3=3, 1+3 = 4, 2+3 = 5。
代码如下
```java
class Solution {
    public int getMaximumConsecutive(int[] coins) {
        int res = 1;
        //先将数组升序排列
        Arrays.sort(coins);
        for (int coin : coins) {
            //判断y,若>x+1, 则推出循环，说明后面也不会有值满足条件了
            //否则，将结果+1
            if (coin > res) {
                break;
            }
            res += i;
        }
        return res;
    }
}
```