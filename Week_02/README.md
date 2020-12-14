## 本周作业

### 简单：

- [有效的字母异位词](https://leetcode-cn.com/problems/valid-anagram/description/)（亚马逊、Facebook、谷歌在半年内面试中考过）

  ```c++
  class Solution {
  public:
      bool isAnagram(string s, string t) {
          if (s.length() != t.length()) {
              return false;
          }
          sort(s.begin(), s.end());
          sort(t.begin(), t.end());
          return s == t;
      }
  };
  ```

  

- √  [两数之和](https://leetcode-cn.com/problems/two-sum/description/)（近半年内，亚马逊考查此题达到 216 次、字节跳动 147 次、谷歌 104 次，Facebook、苹果、微软、腾讯也在近半年内面试常考）

  ```c++
  class Solution {
  public:
      vector<int> twoSum(vector<int>& nums, int target) {
          map<int, int>hashmap;
          for (int i = 0; i < nums.size(); i++) {
              if (hashmap.count(nums[i]) != 0)
                  return {hashmap[nums[i]], i};
              hashmap[target - nums[i]] = i;
          }
          return {-1, 1};
      }
  };
  ```

  

- [N 叉树的前序遍历](https://leetcode-cn.com/problems/n-ary-tree-preorder-traversal/description/)（亚马逊在半年内面试中考过）

  ```c++
  // 迭代法之后待研究
  class Solution {
  public:
      vector<int> res;
      vector<int> preorder(Node* root) {
          if(!root)   return res;
          res.push_back(root -> val);
          for(auto i : root -> children){
              preorder(i);
          }
          return res;
      }
  };
  ```

  

- HeapSort ：自学 https://www.geeksforgeeks.org/heap-sort/

# 总结

+ 集合哈希理论已经看了好几遍，之前有关的题目也都重新刷了
+ 用递归法实现树已经十分了解，已用代码测试，也看了老师发的可视化网站。
+ 迭代法不是太熟，还是要多多熟练。
+ 堆和二叉堆，图理论熟悉，但是相关题目尚未尝试