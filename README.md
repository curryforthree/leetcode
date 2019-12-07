## leetcode
+ 1.Two Sum

    python中的hashmap用字典实现，可以用get方法获取key对应的value，用is not None判断是否在hashmap中. PS:用in/not in来判断是否在list中。list获取特定元素的索引：nums.index(item)

    带索引的迭代：
    ```
    for idx, num in enumerate(nums):
    ```      

+ 3.Longest Substring Without Repeating Characters

    滑动窗口。其实就是一个队列,比如例中的 abcabcbb，进入这个队列（窗口）为 abc 满足题目要求，当再进入 a，队列变成了 abca，这时候不满足要求。所以，滑动这个窗口！那滑到什么位置呢？右指针的位置不变，左指针滑一直到窗口内无重复的字符为止。



+ 7.Reverse Integer

    最直接的想法是字符串翻转，可以利用python字符串切片直接完成翻转：
  ```
  str = str[::-1]
  ```
    但是注意完成转换后需要判断是否溢出. 32-bit signed integer range: [−2^31,  2^31 − 1].利用左移可以直接设置上限2^31 - 1 / 2^31 

    也可直接进行翻转，但是，python存储数字理论上是无限长度，每次计算好要判断是否溢出。Python的坑： 由于Python的 // 操作是向下取整，导致正负数取余 % 操作结果不一致，因此需要将原数字转为正数操作。

+ 9.Palindrome Number

    数字<0，有负号肯定不满足，正数利用字符串切片逆转下判断是否相同即可

+ 24.Swap Nodes in Pairs

    看25题升级版吧

+ 25.Reverse Nodes in k-Group
  
    本题是24题的扩展，k==2时候就成了24题。题意是k个一组翻转链表，在翻转了前k个结点后，对剩余的链表操作其实是做了同样逻辑的操作，比较清晰的思路是把相同的操作抽象出来（较复杂可以作为一个函数），然后在对最上层的一部分做操作的时候调用自身解决下一个小规模的问题，在写递归的时候注意递归出口的条件(所谓的base case)。在本题中，base case是本次调用链表中的结点个数小于k，之后的顺序是：翻转当前链表的前k个，对剩下的链表调用自身。
  
    关于递归法翻转链表，推荐一个分析，很清晰：[步步拆解：如何递归地反转链表的一部分](https://leetcode-cn.com/problems/reverse-linked-list-ii/solution/bu-bu-chai-jie-ru-he-di-gui-di-fan-zhuan-lian-biao/) 

     分析递归算法的时候，不要跳进递归（你的脑袋能压几个栈呀？），而是要根据函数定义，来弄清楚这段代码会产生什么结果。