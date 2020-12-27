# 作业

### 简单：

- 用 add first 或 add last 这套新的 API 改写 Deque 的代码
- 分析 Queue 和 Priority Queue 的源码
- √  [删除排序数组中的重复项](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array/)（Facebook、字节跳动、微软在半年内面试中考过）
- [旋转数组](https://leetcode-cn.com/problems/rotate-array/)（微软、亚马逊、PayPal 在半年内面试中考过）
- √  [合并两个有序链表](https://leetcode-cn.com/problems/merge-two-sorted-lists/)（亚马逊、字节跳动在半年内面试常考）
- √  [合并两个有序数组](https://leetcode-cn.com/problems/merge-sorted-array/)（Facebook 在半年内面试常考）
- √  [两数之和](https://leetcode-cn.com/problems/two-sum/)（亚马逊、字节跳动、谷歌、Facebook、苹果、微软在半年内面试中高频常考）
- √  [移动零](https://leetcode-cn.com/problems/move-zeroes/)（Facebook、亚马逊、苹果在半年内面试中考过）
- √  [加一](https://leetcode-cn.com/problems/plus-one/)（谷歌、字节跳动、Facebook 在半年内面试中考过）

### 中等：

- [设计循环双端队列](https://leetcode.com/problems/design-circular-deque)（Facebook 在 1 年内面试中考过）

### 困难：

- [接雨水](https://leetcode.com/problems/trapping-rain-water/)（亚马逊、字节跳动、高盛集团、Facebook 在半年内面试常考）

## 下周预习

### 预习题目：

- [有效的字母异位词](https://leetcode-cn.com/problems/valid-anagram/description/)
- [二叉树的中序遍历](https://leetcode-cn.com/problems/binary-tree-inorder-traversal/)
- [最小的 k 个数](https://leetcode-cn.com/problems/zui-xiao-de-kge-shu-lcof/)



# 我的完成

+ 删除排序数组中的重复项

  ```c++
  class Solution {
  public:
      int removeDuplicates(vector<int>& nums) {
          // 单次遍历，用一个指针控制遍历，一个指针空值nums有效值
          // 先把第一个元素放进去，从第二个元素开始遍历，只要不相等就加入
          if (nums.size() < 2) return nums.size();
          int cur = 0;
          for (int i = 1; i < nums.size(); i++) {
              if (nums[i] != nums[cur])
                  nums[++cur] = nums[i];
          }
          return cur + 1;
      }
  };
  ```

+ 合并两个有序链表

  ```c++
  class Solution {
  public:
      ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
          ListNode* newHead = new ListNode(0);
          ListNode* tem = newHead;
          // 两个指针一起遍历得到新的链表，然后把遍历结束之后剩下的追加到新链表   
          while (l1 != nullptr && l2 != nullptr) {
              if (l1->val <= l2->val) {
                  tem->next = l1;
                  l1 = l1->next;
              } else {
                  tem->next = l2;
                  l2 = l2->next;
              }
              tem = tem->next;
          }
          if (l1 == nullptr) tem->next = l2;
          else tem->next = l1;
          return newHead->next;
      }
  };
  ```

+ 两数之和

  ```c++
  class Solution {
  public:
      vector<int> twoSum(vector<int>& nums, int target) {
          // 匹配类型记录值和索引，再遍历查找目标值与当前值得差值
          map<int, int> hashmap;
          for (int i=0; i < nums.size(); i++) {
              if (hashmap.count(target - nums[i]) > 0) {
                  return {hashmap[target - nums[i]], i};
              }
              hashmap[nums[i]] = i;
          }
          return {0, -1};
      }
  };
  ```

+ 加一

  ```c++
  class Solution {
  public:
      vector<int> plusOne(vector<int>& digits) {
          // 根据加法的原理，从右向左的加，注意全为9
          for (int i = digits.size() - 1; i >= 0; i--) {
              digits[i]++;
              if (digits[i] == 10) 
                  digits[i] = 0;
              else 
                  return digits;
          }
          digits[0] = 1;
          digits.push_back(0);
          return digits;
      }
  };
  ```

  



# 总结

+ 在写好题目后会有意识的思考时间和空间复杂度。
+ 了解数组，链表的基本操作。栈的使用在最近相关度问题。以及有关双指针，快慢指针的运用
+ 根据跳表的思想，了解升维的思想
+ 在递归法解决问题中自己还是有些不足。
+ 在本周有目的的刷题过程中，我觉得确实十分有效的在提升自己的解决问题的能力