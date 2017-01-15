---
layout: post
title: leetcode讲解之开篇--刷题技巧
categories: leetcode
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

### 94. Binary Tree Inorder Traversal

Given a binary tree, return the inorder traversal of its nodes' values.

For example:
Given binary tree [1,null,2,3],
   1
    \
     2
    /
   3
return [1,3,2].

Note: Recursive solution is trivial, could you do it iteratively?

[题目地址](https://leetcode.com/problems/binary-tree-inorder-traversal/)

嗯，经典的题目，中序遍历二叉树。题目说递归做起来太简单，请用迭代。我觉得还是先用递归做一下吧，也许我递归都不会呢？谁知道呢，是吧。然后发现，嗯，果然很简单，我好像已经不是从前那个菜逼了。

代码如下：

```
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
private:
        vector<int> vec;
public:
    vector<int> inorderTraversal(TreeNode* root) {//中序遍历
        if(root){
            inorderTraversal(root->left);
            vec.push_back(root->val);
            inorderTraversal(root->right);
        }
        return vec;
    }
    vector<int> preorderTraversal(TreeNode* root){//先序遍历
      if(root){
        vec.push_back(root->val);
        preorderTraversal(root->left);
        preorderTraversal(root->right);
      }
      return vec;
    }
    vector<int> postorderTraversal(TreeNode* root){//后序遍历
      if(root){
        postorderTraversal(root->left);
        postorderTraversal(root->right);
        vec.push_back(root->val);
      }
      return vec;
    }
};
```

是不是简单的不要不要的，**递归就是这么美**。

好了，现在想想怎么用迭代中序遍历呢。别想了，用栈吧，不用栈你做给我看试试。

>层次遍历树相当于图的广度优先遍历(BFS,breadth first search)，先序、中序、后序遍历二叉树都相当于图的深度优先遍历(DFS,depth first search)。要用迭代可以啊，广度优先请用队列，深度优先请用栈。

借助栈深度优先遍历时，首先我们压栈第一个结点（入口结点），然后又pop栈顶结点，我们把pop出来的结点的所有子节点都压进栈中，然后又是pop栈顶，继续进行如上操作。也许你发现了一个问题：没有说哪个孩子先压进栈，哪个后压栈，但有一点很明显，先压栈的会靠后访问，后压栈的会先被访问。

上代码：

```
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
private:
    vector<int> vec;
    stack<TreeNode*> s;
    stack<TreeNode*> s1;
public:
    vector<int> inorderTraversal(TreeNode* root) {//中序遍历
        TreeNode* current=root;
        while(!s.empty() || current!=NULL){
            while(current){//如果结点存在，则入栈，然后判断左孩子
                s.push(current);//越靠近root的越先压栈哦
                current = current->left;
            }
            //往左走到了尽头，然后就是pop栈顶了
            current = s.top();
            s.pop();
            vec.push_back(current->val);
            //接着是判断右孩子
            current = current->right;
        }
        return vec;
    }
    vector<int> preorderTraversal(TreeNode* root){//先序遍历
      TreeNode* current=root;
      while(!s.empty() || current!=NULL){
        while(current){
          vec.push_back(current->val);//遇到一个就先访问一个呗
          s.push(current->right);//右孩子压栈，越靠近root的越先压栈哦
          current = current->left;
        }
        current=s.top();
        s.pop();
      }
      return vec;
    }
    //后序遍历，后序遍历就有点复杂了，需要两个栈，蛋疼。。。，
    //什么你问我为啥多了一个栈，因为根节点要存起来啊，它非得要最后访问，就把它一脚踢进栈里。
    vector<int> postorderTraversal(TreeNode* root){
      TreeNode* current=root;
      s.push(current);
      while(!s.empty()){
          current = s.top();
          s.pop();
          s1.push(current);//s1就是用来放后序遍历中的根结点的，root被压到最底下了，哈哈。s1放的是逆序打印顺序哦
          if(current->left)
            s.push(current->left);//左孩子先压栈，先压栈的后访问呐，左孩子不是应该先访问吗，拜托，后面要压入s1，顺序又反了。。
          if(current->right)
            s.push(current->right);//右孩子后压栈
      }
      while(!s1.empty()){//全部释放出来
        vec.push_back(s1.top()->val);
        s1.pop();
      }
      return vec;
    }
};
```

嗯，总的来说用迭代遍历确实烧脑，没什么性能上的特殊需求还是用递归写法吧，对程序员友好哦。

### 217. Contains Duplicate

Given an array of integers, find if the array contains any duplicates. Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct.

so easy的一道题。我直接上代码吧：

```
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        unordered_map<int, int> hash;
        for(auto i:nums){
            hash[i]++;
        }
        for(auto i:hash){
            if(i.second>=2)
                return true;
        }
        return false;
    }
};
```
