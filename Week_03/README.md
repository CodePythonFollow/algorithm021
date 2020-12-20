# 作业

+ [二叉树的最近公共祖先](https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-tree/)

  ```c++
  class Solution {
  public:
      TreeNode* ans;
      bool dfs(TreeNode* root, TreeNode* p, TreeNode* q) {
          if (root == nullptr) return false;
          bool lson = dfs(root->left, p, q);
          bool rson = dfs(root->right, p, q);
          if ((lson && rson) || ((root->val == p->val || root->val == q->val) && (lson || rson))) {
              ans = root;
          } 
          return lson || rson || (root->val == p->val || root->val == q->val);
      }
      TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
          dfs(root, p, q);
          return ans;
      }
  };
  ```

+ [组合](https://leetcode-cn.com/problems/combinations/)

  ```c++
  class Solution:
      def combine(self, n: int, k: int) -> List[List[int]]:
          if n < k or n < 1:
              return []
          if k == 0:
              return [[]]
          if n == k:
              return [[i for i in range(1, n+1)]]
          ans1 = self.combine(n-1, k-1)
          ans2 = self.combine(n-1, k)
          print(n, k, ans1, ans2)
          if ans1:
              for i in ans1:
                  i.append(n)
          return ans1+ans2
  
  ```

# 总结

+ 本结知识确实比较薄弱，还需要多刷题，多理解。
+ 记住模板之后再刷题效果确实会好很多。