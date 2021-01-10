

# 作业

- [最小路径和](https://leetcode-cn.com/problems/minimum-path-sum/)（亚马逊、高盛集团、谷歌在半年内面试中考过）

  ```c++
  class Solution {
  public:
      int minPathSum(vector<vector<int>>& grid) {
          int m = grid.size(), n = grid[0].size();
          for (int i = 0; i < m; i++) {
              for (int j = 0; j < n; j++) {
                  // 边界只有一种走法  
                  if (i == 0) {
                      if (j > 0) grid[i][j] += grid[i][j - 1];
                  } 
                  else if (j == 0) {
                      if (i > 0) grid[i][j] += grid[i - 1][j];
                  }
                  // 内部取最小值走
                  else {
                      grid[i][j] += min(grid[i - 1][j], grid[i][j - 1]);
                  }
              }
          }
          return grid[m - 1][n - 1];
      }
  };
  ```

- [最小覆盖子串](https://leetcode-cn.com/problems/minimum-window-substring/)（Facebook 在半年内面试中常考）

  ```c++
  class Solution {
  public:
      string minWindow(string s, string t) {
          vector<int> worker(128, 0);
          for (char &c : t) ++worker[c];
          int l = 0, r = 0, n = t.size(), len = INT_MAX, start = 0;
          while (r < s.size()) {
              // 非t类字母永远 >= 0
              if (worker[s[r++]]-- > 0) --n; 
              while (!n) {
                  if (r - l < len) len = r - (start = l);
                  // t类字母永远 <= 0
                  if (++worker[s[l++]] > 0) ++n;
              }
          }
          return len == INT_MAX ? "" : s.substr(start, len);
      }
  };
  
  ```

# 总结

+ 本周一直在刷课上的题目，作业写的少了点。。。
+ 理解上确实比较复杂，所以刷题，思考到最后写出来，以及看优秀题解都花了很久。
+ 视频基本上看了3遍左右。不过确实找到感觉了，后面我会慢慢把这些题目刷完。
+ 爬楼梯，兑换硬币以及最小路径问题，理解的比较深入，也尝试过多种解法。觉得状态和本身的值老是会混淆。现在再看就有种豁然开朗的感觉。