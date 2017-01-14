---
layout: post
title: leetcode讲解
categories: OJ
tags: 算法
comments: true
---

一直想系统的刷一套OJ（Online Judge，在线编程练习），对于锻炼自己的思维，算法能力，以及coding能力都是非常有帮助的。

说干就干吧，我选了leetcode，选这个的原因嘛：
1. 有名气啊，大家都知道leetcode
2. 答案多啊，上网一搜，不愁没有教程，可以给解不出题的娃提供及时反馈。
3. 我知道答案不缺我这一份，讲解也不缺我这一份，但我还是再添一块砖，加一片瓦吧。说不定我可以讲的更加清楚呢。
4. 好了不胡扯，其实我就是为了锻炼自己的能力而已。

>刷题我是按AC（accept）率刷的，因为我打算全部刷完啊，直接上难题容易打击到自己幼小的心灵。其实并不是每一题都值得讲解。我争取分两步走吧，
1. 第一步把每道题的讲解和代码贴出来
2. 第二步，做个总结，按照算法体系把有价值的题归纳、举一反三，得出一些有价值的思考和结论。

下面我博客中可能会用python，也可能用C++，如果想看其他语言（python、C++，目前只有这两种语言，今后学了其他语言再来刷，哈哈，感觉有点蛋疼）的代码，就到我的github上看吧。

贴出项目地址：[leetcode讲解](https://github.com/liuqinh2s/leetcode)

### 343. Integer Break

[题目地址](https://leetcode.com/problems/integer-break/)

好吧我还是把题目贴出来，反正不长：

Given a positive integer n, break it into the sum of at least two positive integers and maximize the product of those integers. Return the maximum product you can get.

For example, given n = 2, return 1 (2 = 1 + 1); given n = 10, return 36 (10 = 3 + 3 + 4).

Note: You may assume that n is not less than 2 and not larger than 58.

又是一个要 **靠罗列来发现规律** 的例子：

规模n|最大值
----|----
2   | `1*1`
3   | `2*1`
4   | `2*2`
5   | `3*2`
6   | `3*3`
7   | `3*2*2`
8   | `3*3*2`
9   | `3*3*3`
10  | `3*3*2*2`
11  | `3*3*3*2`
12  | `3*3*3*3`

>好，我们定义一个最大值数组`dp[n]`(dynamic programming)，`dp[5]`即规模为5时候的最大值。

从上面的表中，你发现了什么规律？

1. 尽可能避免拆成1
2. 规模为4的时候，恰好`dp[4]=4`，之后`dp[5]`就开始>5了，而之前的`dp[2]、dp[3]`都是小于自身规模（n=2,n=3）的。
3. 如果我们把2到6看成基本集合，那么后面从7开始是可以归因到2到6的，首先归因到6肯定不对，我们不欢迎1的拆分除非迫不得已（2和3只能那样拆才能拆成2个数的乘积啊），比如7可以写成`2*dp[5]=2*3*2`，也可以写成`3*dp[4]=3*2*2`，但是没必要写成`4*dp[3]`了，因为`dp[3]`已经小于3了，也就是说，我们每次归因都到`dp[4]`打止。但这还是不对，我们看9，9可以归因为`2*dp[7],3*dp[6]，4*dp[5],5*dp[4]`（这可不行啊，5已经小于`dp[5]`了，所以完全不能用，之后的什么6啊，7啊更加不能用，所以其实也是到4打止了，不再往前搜），所以实际上我们最多往前归因4位。其实这还是不对，聪明的你应该已经发现，往前归因4位，其实跟归因2位两次是一样的。所以我们只需从`2*dp[n-2],3*dp[n-3]`中选出大者就行。
4. 我们得到动态规划公式（**动态规划就是归因（多元因）啊，而递归则是单一因**）：`dp[n]=max(2*dp[n-2],3*dp[n-3])`，且n>=7（因为我们不越过`dp[4]`啊）。

代码如下：

```
class Solution(object):
    def integerBreak(self, n):
        """
        :type n: int
        :rtype: int
        """
        dp = [0]*(n+7)
        dp[2]=1
        dp[3]=2
        dp[4]=4
        dp[5]=6
        dp[6]=9
        if(n>=7):
            for x in range(7, n + 1):
                dp[x] = max(3 * dp[x - 3], 2 * dp[x - 2])
        return dp[n]
```

我自己感到这代码有着深深的蛋疼（手动赋了一大堆值），因为我看到别人是这样写的：

```
class Solution(object):
    def integerBreak(self, n):
        """
        :type n: int
        :rtype: int
        """
        if n<4:
            return n-1
        dp = [0]*(n+1)
        dp[2], dp[3] = 2, 3
        for x in range(4, n + 1):
            dp[x] = max(3 * dp[x - 3], 2 * dp[x - 2])
        return dp[n]
```

好吧，他的代码其实也差不多。

下面真正吊炸天的来了。

聪明的你肯定已经发现，这完全就是个2跟3的游戏，是的，事实就是如此。

- n%3==0时，就全部用3
- n%3==2时，勉为其难用个2吧
- n%3==1时，就再勉为其难用两个2吧

当n%3==3，哈哈别傻了，

当然你还得看到，最开始的2个里面是有1的，可不要忘了。

所以，得到牛逼的专门解题代码：

```
class Solution(object):
    def integerBreak(self, n):
        """
        :type n: int
        :rtype: int
        """
        if n < 4:
            return n - 1
        if n % 3 == 0:
            return 3 ** (n / 3)
        if n % 3 == 1:
            return 3 ** ((n - 3) / 3) * 4
        if n % 3 == 2:
            return 3 ** ((n - 2) / 3) * 2
```

这种题也就娱乐娱乐，程序员还是要以工程代码为主业啊。

### 169. Majority Element

Given an array of size n, find the majority element. The majority element is the element that appears more than ⌊ n/2 ⌋ times.

You may assume that the array is non-empty and the majority element always exist in the array.

[题目地址](https://leetcode.com/problems/majority-element/)

唉，看到这题就想起了，当年，青葱岁月，菜鸡的我做阿里的笔试题，对的，就是这题。当时题目改成了小明收红包，找出现次数超过一般的那个红包，要求线性时间复杂度，也就是说不能用排序（排序算法最优情况是：O(nlogn)）。

出现次数超过一半的那个数，我们怎么在O(n)时间复杂度内把它揪出来，我教你：大浪淘沙法，是金子总会发光法，我要打十个法（意思就是，这一个数就能干翻全场剩下的所有数，是不是？因为它超过一半啊）。我们来想象一下：我们遍历这个数组的时候，定义一个count用来计数，这个超过一半的数，它遇到自己就给count加1，遇到不是自己的数，就给count减1，最后会怎样呢，count肯定大于0呐，因为这个数的个数超过一半。好，进一步的，我们先随便找个数当这个老大（个数超过一半），如果它的个数不超过一半，就会在相消中时count为0，那么就把它换掉，最后剩下的那个就是，个数超过一半的那个数了。

代码如下：

```
class Solution(object):
    def majorityElement(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        count = 1
        n = nums[0]
        for x in range(1, len(nums)):
            if count == 0:
                n = nums[x]
                count += 1
            else:
                if nums[x] == n:
                    count += 1
                else:
                    count -= 1
        return n
```

超过一半呐，多么重的一条信息，稍微想想就知道，用相消法都能消出那个数，跟那个用异或消出只出现一次的数（其它的数都是成对的，就是都恰好有两个）是不是异曲同工呐，嗯还是扯得有点远。

另外这个题在leetcode上的难度是easy哦，好伤心啊，当初的我连这题都没想出解法，真是够年轻啊。

### 409. Longest Palindrome

Given a string which consists of lowercase or uppercase letters, find the length of the longest palindromes that can be built with those letters.

This is case sensitive, for example "Aa" is not considered a palindrome here.

Note:
Assume the length of given string will not exceed 1,010.

Example:

Input:
"abccccdd"

Output:
7

Explanation:
One longest palindrome that can be built is "dccaccd", whose length is 7.

[题目地址](https://leetcode.com/problems/longest-palindrome/)

这题有点小儿科了，很简单，你看有多少个对子（打过牌吗，就是看有多少对子），然后看有没有一个单（注意：只需要一个单，放中间就行了）。

```
class Solution {
public:
    int longestPalindrome(string s) {
        unordered_map<char, int> hash;
        int count=0;
        int flag=0;//看有没有单
        for(auto i:s){
            hash[i]++;
        }
        for(auto i:hash){
            if(i.second%2 != 0)
                flag=1;
            count += (i.second/2)*2;//把对子全都加上
        }
        return count+flag;
    }
};
```

### 392. Is Subsequence

Given a string s and a string t, check if s is subsequence of t.

You may assume that there is only lower case English letters in both s and t. t is potentially a very long (length ~= 500,000) string, and s is a short string (<=100).

A subsequence of a string is a new string which is formed from the original string by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters. (ie, "ace" is a subsequence of "abcde" while "aec" is not).

Example 1:
s = "abc", t = "ahbgdc"

Return true.

Example 2:
s = "axc", t = "ahbgdc"

Return false.

Follow up:
If there are lots of incoming S, say S1, S2, ... , Sk where k >= 1B, and you want to check one by one to see if T has its subsequence. In this scenario, how would you change your code?

[题目地址](https://leetcode.com/problems/is-subsequence/)

这题我觉得很简单啊，不知道为何评级是medium。

就是遍历两个字符串就行了。直接上代码，看不懂可以在评论里面写上，我会针对性讲解。

```
class Solution {
public:
    bool isSubsequence(string s, string t) {
        int i=0,j=0;
        while(i<s.size() && j<t.size()){
            if(s[i]==t[j]){
                i++;
                j++;
            }else{
                j++;
            }
        }
        if(i!=s.size())
            return false;
        return true;
    }
};
```
