# -# 数据结构与算法学习笔记——杨桂淼总结

​																						*——对付东来《labuladong的算法小抄》中算法思维的总结归纳*

**写在前面：**

2022.06.20漫长的暑假开始了，总要做些什么。做啥？——当然是做好本手儿（2022年高考学的词哈哈~）

付东来大哥的这本书是2022.03.26购入，那是大二下学期的开学后不久。一个学期囫囵吞枣的看了一遍，没有get到精髓部分，代码看着很明白，自己写着错误百出。于是计划利用好这个稍微漫长的暑假，认认真真学好数据结构与算法。

本总结是杨桂淼同学基于力扣平台的题目，参考付东来大哥的解题思路编写；东来大哥每道题都给出了基于Java的解题思路，但是目前阶段本人Java语言掌握一般。于是乎，借鉴东来大哥的思路，将题目全部运用python语言实现。随着本人的不断学习积累，完善后代码会全部开源到杨桂淼的GitHub仓库中，届时，欢迎各位大佬评阅斧正；欢迎各位志同道合的同志交流学习！

[杨桂淼的GitHub仓库]: https://github.com/Mungeryang

本人秉持东来大哥的理念——致力于把算法讲清楚！

参考引用文章来源：labuladong小站

计算机中数据结构的分类：

常见的数据结构可分为「线性数据结构」与「非线性数据结构」，具体为：「数组」、「链表」、「栈」、「队列」、「树」、「图」、「散列表」、「堆」。

## 双指针技巧在链表与数组中的运用

双指针分类：1.**快慢指针**	2.**左右指针**

力扣中的对应题目如下：

数组：

|                           LeetCode                           |                             力扣                             | 难度 |
| :----------------------------------------------------------: | :----------------------------------------------------------: | :--: |
| [5. Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/) | [5. 最长回文子串](https://leetcode.cn/problems/longest-palindromic-substring/) |  🟠   |
| [26. Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/) | [26. 删除有序数组中的重复项](https://leetcode.cn/problems/remove-duplicates-from-sorted-array/) |  🟢   |
| [27. Remove Element](https://leetcode.com/problems/remove-element/) | [27. 移除元素](https://leetcode.cn/problems/remove-element/) |  🟢   |
| [83. Remove Duplicates from Sorted List](https://leetcode.com/problems/remove-duplicates-from-sorted-list/) | [83. 删除排序链表中的重复元素](https://leetcode.cn/problems/remove-duplicates-from-sorted-list/) |  🟢   |
| [167. Two Sum II - Input Array Is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/) | [167. 两数之和 II - 输入有序数组](https://leetcode.cn/problems/two-sum-ii-input-array-is-sorted/) |  🟢   |
| [283. Move Zeroes](https://leetcode.com/problems/move-zeroes/) |   [283. 移动零](https://leetcode.cn/problems/move-zeroes/)   |  🟢   |
| [344. Reverse String](https://leetcode.com/problems/reverse-string/) | [344. 反转字符串](https://leetcode.cn/problems/reverse-string/) |  🟢   |

链表：

|                           LeetCode                           |                             力扣                             | 难度 |
| :----------------------------------------------------------: | :----------------------------------------------------------: | :--: |
| [19. Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/) | [19. 删除链表的倒数第 N 个结点](https://leetcode.cn/problems/remove-nth-node-from-end-of-list/) |  🟠   |
| [21. Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/) | [21. 合并两个有序链表](https://leetcode.cn/problems/merge-two-sorted-lists/) |  🟢   |
| [23. Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/) | [23. 合并K个升序链表](https://leetcode.cn/problems/merge-k-sorted-lists/) |  🔴   |
| [86. Partition List](https://leetcode.com/problems/partition-list/) | [86. 分隔链表](https://leetcode.cn/problems/partition-list/) |  🟠   |
| [141. Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/) | [141. 环形链表](https://leetcode.cn/problems/linked-list-cycle/) |  🟢   |
| [142. Linked List Cycle II](https://leetcode.com/problems/linked-list-cycle-ii/) | [142. 环形链表 II](https://leetcode.cn/problems/linked-list-cycle-ii/) |  🟠   |
| [160. Intersection of Two Linked Lists](https://leetcode.com/problems/intersection-of-two-linked-lists/) | [160. 相交链表](https://leetcode.cn/problems/intersection-of-two-linked-lists/) |  🟢   |
| [876. Middle of the Linked List](https://leetcode.com/problems/middle-of-the-linked-list/) | [876. 链表的中间结点](https://leetcode.cn/problems/middle-of-the-linked-list/) |  🟢   |

在处理数组和链表相关问题时，双指针技巧是经常用到的，双指针技巧主要分为两类：**左右指针**和**快慢指针**。

所谓左右指针，就是两个指针相向而行或者**相背而行**；而所谓快慢指针，就是两个指针**同向而行**，一快一慢。

对于单链表来说，大部分技巧都属于快慢指针。

在数组中并没有真正意义上的指针，但我们可以把**索引**当做数组中的指针，这样也可以在数组中施展双指针技巧，**本文先讲数组相关的双指针算法**，**再讲链表有关的双指针算法。**

### Array~快慢指针技巧

**数组问题中比较常见的快慢指针技巧，是让你原地修改数组**。

简单解释一下什么是原地修改：

如果不是原地修改的话，我们直接 new 一个 `int[]` 数组，把去重之后的元素放进这个新数组中，然后返回这个新数组即可。

但是现在题目让你原地删除，不允许 new 新数组，只能在原数组上操作，然后返回一个长度，这样就可以通过返回的长度和原始数组得到我们去重后的元素有哪些了。

由于数组已经排序，所以重复的元素一定连在一起，找出它们并不难。但如果毎找到一个重复元素就立即原地删除它，由于数组中删除元素涉及数据搬移，整个时间复杂度是会达到 `O(N^2)`。

高效解决这道题就要用到快慢指针技巧：

我们让慢指针 `slow` 走在后面，快指针 `fast` 走在前面**探路**，找到一个不重复的元素就赋值给 `slow` 并让 `slow` 前进一步。

这样，就保证了 `nums[0..slow]` 都是无重复的元素，当 `fast` 指针遍历完整个数组 `nums` 后，`nums[0..slow]` 就是整个数组去重之后的结果。
//Java实现
int removeDuplicates(int[] nums){
    if (nums.length == 0)
    {
        return 0;
    }
    int slow = 0,fast = 0;
    while (fast < nums.length)
    {
        if (nums[fast] != nums[slow])
        {
            slow++;
            nums[slow] = nums[fast];
                
        }
        fast++; 
    }
    return slow + 1;
}
#python实现
class Solution(object):
    def removeDuplicates(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if(len(nums) == 0):
            return 0
        #can't assign to literal的错误来源是slow=0，fast=0写在了一行中
        #要么用逗号隔开，用么分成两行写
        slow=0
        fast=0
        while(fast < len(nums)):
            if(nums[fast] != nums[slow]):
                slow += 1
                nums[slow] = nums[fast]
            fast += 1

        return slow + 1
        
 类似的，例如力扣中的**移动零**题目：

给定一个数组 `nums`，编写一个函数将所有 `0` 移动到数组的末尾，同时保持非零元素的相对顺序。

本质就是数组去重后将尾巴部分元素改为0
class Solution(object):
    def moveZeroes(self, nums):
        """
        :type nums: List[int]
        :rtype: None Do not return anything, modify nums in-place instead.
        """
        #老套路，设置快慢指针
        slow=0
        fast=0
        #核心代码区，区分不同目标值的设置
        while(fast <len(nums)):
            if(nums[fast] != 0):
                nums[slow] = nums[fast]
                slow += 1
            fast += 1
        #与前面题唯一的不同点，是将数组去重后尾部元素修改为0，此处我用的for循环，有其他新方法欢迎大佬们修改提出意见
        for i in range(slow,len(nums)):
            nums[i] = 0
           
**去重的核心代码块**：
while(fast <len(nums)):
            if(nums[fast] != 0):
                nums[slow] = nums[fast]
                slow += 1
            fast += 1

