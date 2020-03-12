## leetcode

+ 1.Two Sum

    python中的hashmap用字典实现，可以用get方法获取key对应的value，用is not None判断是否在hashmap中. PS:用in/not in来判断是否在list中。list获取特定元素的索引：nums.index(item)

    带索引的迭代：
    ```
    for idx, num in enumerate(nums):
    ```      

+ 3.Longest Substring Without Repeating Characters

    滑动窗口。其实就是一个队列,比如例中的 abcabcbb，进入这个队列（窗口）为 abc 满足题目要求，当再进入 a，队列变成了 abca，这时候不满足要求。所以，滑动这个窗口！那滑到什么位置呢？右指针的位置不变，左指针滑一直到窗口内无重复的字符为止。

+ 5.Longest Palindromic Substring

    解决这类 “最优子结构” 问题，可以考虑使用 “动态规划”：

    1、定义 “状态”；

    2、找到 “状态转移方程”。

    记号说明： 下文中，使用记号 s[l, r] 表示原始字符串的一个子串，l、r 分别是区间的左右边界的索引值，使用左闭、右闭区间表示左右边界可以取到。举个例子，当 s = 'babad' 时，s[0, 1] = 'ba' ，s[2, 4] = 'bad'。

    1、定义 “状态”，这里 “状态”数组是二维数组。

    dp[l][r] 表示子串 s[l, r]（包括区间左右端点）是否构成回文串，是一个二维布尔型数组。即如果子串 s[l, r] 是回文串，那么 dp[l][r] = true。

    当子串包含 2 个以上字符的时候：如果 s[l, r] 是一个回文串，例如 “abccba”，那么这个回文串两边各往里面收缩一个字符（如果可以的话）的子串 s[l + 1, r - 1] 也一定是回文串，即：如果 dp[l][r] == true 成立，一定有 dp[l + 1][r - 1] = true 成立。

    根据这一点，我们可以知道，给出一个子串 s[l, r] ，如果 s[l] != s[r]，那么这个子串就一定不是回文串。如果 s[l] == s[r] 成立，就接着判断 s[l + 1] 与 s[r - 1]，这很像中心扩散法的逆方法。

    事实上，当 s[l] == s[r] 成立的时候，dp[l][r] 的值由 dp[l + 1][r - l] 决定，这一点也不难思考：当左右边界字符串相等的时候，整个字符串是否是回文就完全由“原字符串去掉左右边界”的子串是否回文决定。但是这里还需要再多考虑一点点：“原字符串去掉左右边界”的子串的边界情况。

    当原字符串的元素个数为 2个或3个的时候，如果左右边界相等，那原字符串一定是回文串；

    综上，如果一个字符串的左右边界相等，以下二者之一成立即可：1、去掉左右边界以后的字符串不构成区间，即“ s[l + 1, r - 1] 至少包含两个元素”的反面，即 l - r >= -2，或者 r - l <= 2；2、去掉左右边界以后的字符串是回文串，具体说，子字符串的回文性决定了原字符串的回文性。


+ 6.ZigZag Conversion

    题目要求得到z字型字符串，但只需要按行打印即可，可以从按行打印入手，每一行作为一个字符串拼接即可。设numRows行字符串分别为$S_1$...$S_n$,显然，按顺序遍历字符串时，每个字符的行索引从小到大，再从大到小。如此模拟便可。

    PS：python列表生成式:[廖雪峰](https://www.liaoxuefeng.com/wiki/1016959663602400/1017317609699776)

+ 7.Reverse Integer

    最直接的想法是字符串翻转，可以利用python字符串切片直接完成翻转：
    ```
    str = str[::-1]
    ```
    但是注意完成转换后需要判断是否溢出. 32-bit signed integer range: [−2^31,  2^31 − 1].利用左移可以直接设置上限2^31 - 1 / 2^31 

    也可直接进行翻转，但是，python存储数字理论上是无限长度，每次计算好要判断是否溢出。Python的坑： 由于Python的 // 操作是向下取整，导致正负数取余 % 操作结果不一致，因此需要将原数字转为正数操作。

+ 8.String to Integer (atoi)

    string去空格，strip(),去左空格lstrip()

    python一行解法 正则表达式 还是强啊...

    ```
    class Solution:
    def myAtoi(self, s: str) -> int:
        return max(min(int(*re.findall('^[\+\-]?\d+', s.lstrip())), 2**31 - 1), -2**31)

    ```  

    ```
    ^：匹配字符串开头
    [\+\-]：代表一个+字符或-字符
    ?：前面一个字符可有可无
    \d：一个数字
    +：前面一个字符的一个或多个
    \D：一个非数字字符
    *：前面一个字符的0个或多个
    ```


    ```
    max(min(数字, 1<<31 - 1), -1<<31) #用来防止结果越界
    ```

+ 9.Palindrome Number

    数字<0，有负号肯定不满足，正数利用字符串切片逆转下判断是否相同即可


+ 13.Roman to Integer

    建立map后，逆着读取字符串，若本位比上位小，就减去该位，否则加上该位。

+ 14.Longest Common Prefix

    模拟即可，python可用zip来提升速度

    ```
    zip(*strs)对strs解包后进行zip
    ```


+ 15.3Sum

    暴力搜索o(N^3)会超时，排序后，利用元素大小作为限制以及双指针的思想减小解空间来优化效率。

    注意要避免重复组合的保存，如果python写判断list是否在res中，一样也会超时。注意下面两种情况的优化。

    （1）当 nums[k] > 0 时直接break跳出：因为 nums[j] >= nums[i] >= nums[k] > 0，即 33 个数字都大于 00 ，在此固定指针 k 之后不可能再找到结果了。
    
    （2）当 k > 0且nums[k] == nums[k - 1]时即跳过此元素nums[k]：因为已经将 nums[k - 1] 的所有组合加入到结果中，本次双指针搜索只会得到重复组合。

    当判断存在一组解后，在两边的指针保证不相交的情况下，两个指针都要移到与前一个位置不同的地方，否则还是已存在的解。

+ 16.3Sum Closest

    15题的拓展版。采用双指针对撞的思路。在对撞过程中，可以加入常规的剪枝操作（最外层重复元素直接跳过），来加快速度。

+ 17.Letter Combinations of a Phone Number

    回溯法，循环+递归。理解的关键在于，循环的嵌套层数，就是输入的字符串长度。输入的字符串长度是1，循环只有1层。输入的字符串长度是3，循环就是3层。如果输入的字符串长度是10，那么循环就是10层。可是输入的字符串长度是不固定的，对应的循环的嵌套层数也是不固定的，那这种情况怎么解决呢？这时候递归就派上用场了。递归调用的时候，就像一颗树一样。

    写好递归边界后，考虑最外层的逻辑，写好后debug一下一般问题不大了。

    tips:ord(c) - 48 是获取c的ASCII码然后-48,48是0的ASCII

+ 20.Valid Parentheses

    典型的栈的题目，python实现stack用list即可，可以append和pop

    用一个hashmap存储右括号对应的左括号可以提高速度。


+ 24.Swap Nodes in Pairs

    为了速度可以不用递归，采用迭代的方法，为了保持第一个部分和后面的一致性，先添加一个空头，再进行交换。

    比较经典的题目

+ 25.Reverse Nodes in k-Group
  
    本题是24题的扩展，k==2时候就成了24题。题意是k个一组翻转链表，在翻转了前k个结点后，对剩余的链表操作其实是做了同样逻辑的操作，比较清晰的思路是把相同的操作抽象出来（较复杂可以作为一个函数），然后在对最上层的一部分做操作的时候调用自身解决下一个小规模的问题，在写递归的时候注意递归出口的条件(所谓的base case)。在本题中，base case是本次调用链表中的结点个数小于k，之后的顺序是：翻转当前链表的前k个，对剩下的链表调用自身。
  
    关于递归法翻转链表，推荐一个分析，很清晰：[步步拆解：如何递归地反转链表的一部分](https://leetcode-cn.com/problems/reverse-linked-list-ii/solution/bu-bu-chai-jie-ru-he-di-gui-di-fan-zhuan-lian-biao/) 

    分析递归算法的时候，不要跳进递归（你的脑袋能压几个栈呀？），而是要根据函数定义，来弄清楚这段代码会产生什么结果。

    设计递归算法时，首先要先明确该函数的作用，然后再确定何时结束与何时调用该函数。


+ 35.Search Insert Position

    参照69题题解里面的链接，当num[mid] < target 的时候一定不可能满足条件.

+ 36.Valid Sudoku

    判断 数独是否有效，判断三个条件可以放在一个循环里完成。

    主要是每一个小正方形的表示，可以将9个小正方形编号，每一个格子(x,y)对应到正方形的序号是：(x // 3) * 3 + y //3。用九个hashmap记录是否有存在即可。

+ 37.Sudoku Solver

    回溯+剪枝，本题主要优化的地方在于：先找到哪些地方需要填数字 和 每行只能填哪些数字，这些都用set数据结构来存储会有客观的速度提升。

+ 50.Pow(x, n)

    直接暴力会超时，可以采用快速幂。

    法一：递归，每次分一半去计算，往下一层的结果应该是次数减一半，同样的底数就要是平方，即$x^n=(x*x)^{n/2}$。要注意的是指数小于0 要返回倒数。

    法二：迭代，以 x 的 10 次方举例。10 的 2 进制是 1010，然后用 2 进制转 10 进制的方法把它展成 2 的幂次的和。$x^{10}=x^{(1010)_2}=x^{1*2^3+0*2^2+1*2^1+0*2^2}=x^{1*8+0*4+1*2+0*1}$,这样可以利用位运算来实现，一直右移&1判断是是否是1,指数始终是本身的平方增长。
​	
+ 51.N-Queens

    n皇后问题，这就是 “全排列”问题 + “剪枝” 。 “剪枝” 的依据就是题目中描述的 “N 皇后” 问题的规则。
    搜索的深度设定为x(行)，另外设置三个set()去分别记录y列数，x+y（撇），x-y（捺）。
    只要这三个set里面没有就进行下次层递归，否则跳过，递归好一层后退出即可。

+ 52.N-Queens II

    只要求返回不同结果的数量，不要求保存结果。

    这里就涉及了搜索时，如何保存最优方案的问题，有两种主要的方法。
    
    一个是设定一个全局的temp与res,temp用来记录当前的搜索路径，当试图进入某一分支时要将当前的结点选择添加进temp，而当分支结束要将其弹出。当temp是一个正确答案时，保存进res。

    另一个是把路径(如list，数组，vecto等)当做函数参数，可以不用每次压入弹出。

+ 69.Sqrt(x)

    法一：二分查找

    在讨论区看到一个大佬总结了一个二分的模板，很强，传送门：[二分模板讲解](https://leetcode-cn.com/problems/search-insert-position/solution/te-bie-hao-yong-de-er-fen-cha-fa-fa-mo-ban-python-/)
    
    总结一下几点：
    
    1.循环条件写left < right, 这样就不用担心返回结果是l还是r了。

    2.写if-else判断，去思考nums[mid]满足什么性质的时候，mid 不是解。进而接着判断 mid 的左边有没有可能是解，mid 的右边有没有可能是解。此时 mid 作为待查找数组就分为两个区间，一个部分可能存在目标元素，一个部分一定不存在目标元素，mid 作为这两个区间的分界点。

    3.当赋值为left = mid时，需要调整为取右中位数。

    搜索范围可以通过一些数学关系去缩小，但是注意一般设置大一点点，避免边界查不到

    法二：牛顿法

    思想是以直代曲，求方程的根

+ 70.Climbing Stairs

    动态规划，设爬到第n个台阶的走法总数为f(n), f(n) = f(n - 1) + f(n - 2)

    其实是斐波那契，可以用斐波那契求第n个的公式直接得出

    $F_n=1/\sqrt 5*[(\frac{1+\sqrt 5}{2})^n-(\frac{1-\sqrt 5}{2})^n]$


+ 72.Edit Distance

    典型的动态规划解决字符串问题，解决两个字符串的动态规划问题，一般都是用两个指针 i,j 分别指向两个字符串的最后，然后一步步往前走，缩小问题的规模。
    
    dp[i][j] 代表 word1 到 i 位置转换成 word2 到 j 位置需要最少步数.

    在草稿纸上画出二维数组，这样可以更加直观的来初始化，初始化第0行和第0列。

    当 word1[i] == word2[j]，dp[i][j] = dp[i-1][j-1]；

    当 word1[i] != word2[j]，dp[i][j] = min(dp[i-1][j-1], dp[i-1][j], dp[i][j-1]) + 1

    其中，dp[i-1][j-1] 表示替换操作，dp[i-1][j] 表示删除操作，dp[i][j-1] 表示插入操作。这里，具体表示什么可以举个例子然后用自然语言描述出来，如下：

    以 word1 为 "horse"，word2 为 "ros"，且 dp[5][3] 为例，即要将 word1的前 5 个字符转换为 word2的前 3 个字符，也就是将 horse 转换为 ros，因此有：

    (1) dp[i-1][j-1]，即先将 word1 的前 4 个字符 hors 转换为 word2 的前 2 个字符 ro，然后将第五个字符 word1[4]（因为下标基数以 0 开始） 由 e 替换为 s（即替换为 word2 的第三个字符，word2[2]）

    (2) dp[i][j-1]，即先将 word1 的前 5 个字符 horse 转换为 word2 的前 2 个字符 ro，然后在末尾补充一个 s，即插入操作

    (3) dp[i-1][j]，即先将 word1 的前 4 个字符 hors 转换为 word2 的前 3 个字符 ros，然后删除 word1 的第 5 个字符

    这是两个个比较好的题解：[1.编辑距离面试题详解](https://leetcode-cn.com/problems/edit-distance/solution/bian-ji-ju-chi-mian-shi-ti-xiang-jie-by-labuladong/)

    [2.自底向上 和自顶向下](https://leetcode-cn.com/problems/edit-distance/solution/zi-di-xiang-shang-he-zi-ding-xiang-xia-by-powcai-3/)

+ 79.Word Search

    先记录个问题，python中变量前面加self.和不加的区别。self就表示实例对象，变量加了self.就是成员变量(属性)，可以由类的实例调用，如果不加就代表是方法的局部变量.

    用dfs搜索结果，注意条件判断进行剪枝，避免不必要的搜索。记录是否visit的情况，可以开另一个数组来记录，也可以在访问的位置上设成没有的字符，如'!','#'

    四连通在python中可以用list来记录。

+ 98.Validate Binary Search Tree

    二叉搜索树中序遍历是递增的,所以我们可以中序遍历判断前一数是否小于后一个数.

    法一：把中序结果保存在list中，判断排序后的list和原本的list是否一样。另外！第一遍不通过原因是没有加上：判断无重复元素，可以利用len(set(res)) == len(res) 实现

    法二：在进行中序时，利用前置指针来判断值的大小顺序是否满足条件！不能想当然的判断当前根的值和左子树右子树的值，要用一个前置指针保存前一个结点。整体中序的框架不变，在处理根时，把pre更新为当前结点即可

    法三：利用最大最小值

    写一个helper函数参数加上树中的最大和最小值参数。
    Python中可以用如下方式表示正负无穷：float("inf"), float("-inf")

+ 102.Binary Tree Level Order Traversal

    在二维数组中保存二叉树的层序遍历结果。
    
    法一：在用BFS注意用一个变量表示当前层次，队列不空时循环，每次将一层的结点加入结果。

    tips:python中队列可以想入队列结点和层数的结构体，可以元祖入队：queue.append((depth,node))

    法二：递归，其实就是DFS。

+ 104.Maximum Depth of Binary Tree

    法一：递归

    法二：BFS，最后一个遍历到的结点的层数就是最大层数
    
+ 111.Minimum Depth of Binary Tree

    法一： BFS第一次碰到叶子结点，其层数就是最小值

    法二： 递归

+ 120.Triangle

    法一：dfs，速度较慢

    法二：dp，dp的思考方式要和递归相反，从底向上思考，容易去定义状态和状态转移方程。

+ 121.Best Time to Buy and Sell Stock

+ 122.Best Time to Buy and Sell Stock II   

+ 123.Best Time to Buy and Sell Stock III

    以上三题均参照188

+ 141.Linked List Cycle

    链表判环

    方法一：将链表每个结点的地址存在set中，遍历判断是否在set中出现，若出现则有环

    方法二：快慢指针，设置一个快指针每次前进两步，一个慢指针每次前进一步，一直循环，若相遇则有环，可以想象成在操场（环状）两个跑步速度不一样的人总会相遇

    方法三：置空，每次遍历都把经过的结点val值置空

+ 152.Maximum Product Subarray

    动态规划，因为有负数的存在，需要保存当前位置的最大乘积，和最小乘积，因为负数可以将最大乘积变最小，将最小变最大。

    可以扩展维数来存储状态，也可以直接用单个变量来记录，或者开一个2*2的循环数组来进行计算。


+ 169.Majority Element

    法一：众数是出现次数超过一半的数，所以排序后中间的数就是众数.

    法二：hashmap记录次数，若次数>n//2返回。

    法三：摩尔投票法，核心思想是抵消

+ 188.Best Time to Buy and Sell Stock IV

    当k足够大时，会内存超限，其实稍微想一下就可以明白：

    当k >= len(prices) // 2时就可以将问题退化为无限次交易，采用贪心法解决。

    在动态规划时，假如因为状态不够，而导致无法递推，就可以增加状态数组的维数。

    本题用MP[i][k][j] 来作为状态，第一个是天数，第二个是交易次数，第三个是当前的持有状态。可以用自然语言描述出每一个状态的含义。

    比如说 MP[3][2][1] 的含义就是：今天是第三天，我现在手上持有着股票，至今进行了 2 次交易。

    本题还有一个坑，即交易次数的定义，是买入股票就算一次交易？还是卖出后才算一次交易？其实都是可以的，不同的定义方式会导致dp方程的不同，以及初始化的不同。

    一般递推时可以把0空出，当做状态转移的开始。

    本题如果假定买入就算一次交易，初始状态:
    
    MP[0][t][0] 0天t次交易，手上不持有：可能的 0

    MP[0][t][1] 0天t次交易，手上持有：不可能，设为-inf，0天没有股票，不会持有

    MP[i][0][0] i天0次交易，手上不持有：0

    MP[i][0][1] i天0次交易，手上持有：不可能，只要持有就会有交易次数。


+ 191.Number of 1 Bits

    x & (x - 1)表示消掉 x的最后一位1！！！！！！！一直消直到为0 记录次数。

+ 208.Implement Trie (Prefix Tree)

    py可以用dict来实现字典树。

    Python中collections.defaultdict()可以更加方便的去实现dict。

    举个例子，在初始化一个dict的时候，普通dict假如不存在键，想插入值，就会报错。

    defaultdict()的参数可以是list, set, int, 甚至是自己创建的类以实现不同功能。默认在缺失键的情况下初始化什么样的值。

+ 212.Word Search II

    用字典树来优化时间复杂度。

    把所有待查询的words保存进字典树中，根据当前字典树dict映射的字符，来判断是否进下一层递归。

+ 225.Implement Stack using Queues

    用队列实现栈，用标准库queue中的Queue实现，get(),put()方法是常用的。

+ 239.Sliding Window Maximum

    法一：大顶堆

    法二：双端队列维护，始终保证双端队列最左边是滑窗中最大的。

    python实现deque 可以用list,左侧pop，用pop(0),右侧用pop()。也可以用collections库里面的deque,用popleft(),和pop()


+ 230.Kth Smallest Element in a BST

    利用python生成器，在中序递归的时候利用生成器存储中序结果。

    ```
    yield from some_generator
    ```
    相当于

    ```
    for x in some_generator: 
        yield x
    ```

+ 231.Power of Two

    满足1.x只有一位1，2.x>0。

    x & (x - 1)表示消掉 x的最后一位1！！！！！！！！！！



+ 232.Implement Queue using Stacks

    用栈实现队列，用两个栈即可，在__init__中初始化两个栈

+ 300.Longest Increasing Subsequence

    定义状态为：选定当前元素的最大递增子序列

    有时候状态不好定义，要加上选定当前位置

+ 332.Coin Change

    可以等同为爬楼梯问题。

+ 338.Counting Bits

    x & (x - 1)表示消掉 x的最后一位1!

    递推关系: dp[i] = dp [i & (i - 1)] + 1

+ 347.Top K Frequent Elements

    获得前k个高频的元素，然后利用优先队列（堆）来实现排序即可。

    在Python中可以使用 heapq库中的nlargest方法，一行解决。

    在Python中：collections 库中的Counter方法，用来 构建我们所需要的元素对应频次的哈希表。



+ 703.Kth Largest Element in a Stream


    堆（heap），它是一种优先队列。优先队列让你能够以任意顺序添加对象，并随时（可能是在两次添加对象之间）找出（并删除）最小的元素。相比于列表方法min，这样做的效率要高得多。
    
    实际上，Python没有独立的堆类型，而只有一个包含一些堆操作函数的模块。这个模块名为heapq（其中的q表示队列），它包含6个函数，其中前4个与堆操作直接相关。必须使用列表来表示堆对象本身。

    
    | heapq常用方法 |  | 
    | ------ | ------ |
    | 函数 | 描述 | 
    | heappush(heap, x)    | 将x压入堆中 | 
    | heappop(heap)        | 从堆中弹出最小的元素 | 
    | heapify(heap)        | 让列表具备堆特征 | 
    | heapreplace(heap, x) | 弹出最小的元素，并将x压入堆中 | 
    | nlargest(n, iter)    | 返回iter中n个最大的元素 | 
    | nsmallest(n, iter)   | 返回iter中n个最小的元素 | 

+ 714.Best Time to Buy and Sell Stock with Transaction Fee

    参考188题题解，两个维度的状态就可以了，dp方程加上手续费就OK了

+ 739.Daily Temperatures

    利用单调栈（Monotone Stack），每个数字只进栈并处理一次，而解决问题的核心就在处理这块，当前数字如果破坏了单调性，就会触发处理栈顶元素的操作，而触发数字有时候是解决问题的一部分。

+ 994.

    采用BFS
    以下是BFS的写法
    ```
    depth = 0 # 记录遍历到第几层
    while queue 非空:
        depth++
        n = queue 中的元素个数
        循环 n 次:
            node = queue.pop()
            for node 的所有相邻结点 m:
                if m 未访问过:
                    queue.push(m)
    ```      

+ 1071.Greatest Common Divisor of Strings

    如果它们有公因子 abc，那么 str1 就是 mm 个 abc 的重复，str2 是 nn 个 abc 的重复，连起来就是 m+nm+n 个 abc，好像 m+nm+n 个 abc 跟 n+mn+m 个 abc 是一样的。

    所以如果 str1 + str2 === str2 + str1 就意味着有解。

    我们也很容易想到 str1 + str2 !== str2 + str1 也是无解的充要条件。

    当确定有解的情况下，最优解是长度为 gcd(str1.length, str2.length) 的字符串。



+ 1103.Distribute Candies to People

    法一：模拟，用i%kids来表示当前到哪个小孩，记剩下的糖果，给的糖果始终是min（剩下的糖果，当前次数 + 1）

    法二：数学推导，用 等差数列来推导，详细见：[详细解释数学方法怎么做，高中知识就能看懂哦](https://leetcode-cn.com/problems/distribute-candies-to-people/solution/xiang-xi-jie-shi-shu-xue-fang-fa-zen-yao-zuo-gao-z/)
    写的很好
    