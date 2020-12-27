# 本周作业

- [柠檬水找零](https://leetcode-cn.com/problems/lemonade-change/description/)（亚马逊在半年内面试中考过）

  ```c++
  class Solution {
  public:
      bool lemonadeChange(vector<int>& bills) {
          // 贪心
          map<int, int> have;
          for (int i = 0; i < bills.size(); i++) {
              // 模拟 加 贪心
              if (bills[i] == 5) {
                  if (have.count(5) == 1) have[5] += 1;
                  else have[5] = 1;
              } else if (bills[i] == 10) {
                  // 先判断是否有钱找
                  if (have.count(5) == 1 && have[5] > 0) have[5] -= 1;
                  else return false;
                  // 拿10元
                  if (have.count(10) == 1) have[10] += 1;
                  else have[10] = 1;
              // 给20的可以贪心，因为希望保留5元 有10元就给10元
              } else {
                  // 有10元
                  if (have.count(10) == 1 && have[10] > 0) {
                      have[10] -= 1;
                      // 有5元找5元， 没有五元直接错误
                      if (have.count(5) == 1 && have[5] > 0) have[5] -= 1;
                      else return false;
                  // 没有10元
                  } else {
                      if (have.count(5) == 1 && have[5] >= 3) have[5] -= 3;
                      else return false;
                  }
              }  
          }
          return true;
      }
  };
  ```

- [买卖股票的最佳时机 II ](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-ii/description/)（亚马逊、字节跳动、微软在半年内面试中考过）

  ```c++
  class Solution {
  public:
      int maxProfit(vector<int>& prices) {
          // 双指针
          int left = 0, right, ans = 0;
          while (left < prices.size()) {
              // 确定最小的做指针
              while (left + 1 < prices.size() && prices[left + 1] < prices[left]) left++;
              right = left + 1;
              // 确定最大的右指针
              while (right + 1 < prices.size() && prices[right + 1] > prices[right]) right++;
              if (right < prices.size()) ans += prices[right] -prices[left];
              // 下一次从 right + 1 开始
              left = right + 1;
          }
          return ans;
      }
  };
  ```

- [分发饼干](https://leetcode-cn.com/problems/assign-cookies/description/)（亚马逊在半年内面试中考过）

  ```c++
  class Solution:
      def findContentChildren(self, g: List[int], s: List[int]) -> int:
          s.sort()
          g.sort()
          len_s = len(s)
          len_g = len(g)
          # 贪心
          i = j = result = 0
          while i < len_g and j < len_s:
              if s[j] >= g[i]:
                  result += 1
                  i += 1
              j += 1
          return result
  ```

- [岛屿数量](https://leetcode-cn.com/problems/number-of-islands/)（近半年内，亚马逊在面试中考查此题达到 350 次）

  - BFS

  ```c++
  class Solution {
  public:
      int numIslands(vector<vector<char>>& grid) {
          int count = 0;
          for (int row = 0; row < grid.size(); row++) {
              for (int col = 0; col < grid[0].size(); col++) {
                  if (grid[row][col] == '1') {
                      bfs(row, col, grid);
                      count++;
                  }
              }
          }
          return count;
      }
      void bfs(int row, int col, vector<vector<char>>& grid) {
          queue<pair<int, int>> que;
          que.push({row, col});
          // 下面一行是先访问再入队列的写法。
          grid[row][col] = '0';
          int maxrow = grid.size();
          int maxcol = grid[0].size();
          // 队列保证一层数据在一起   如果每次遍历一层再访问，那么每一层的每一个元素会多很多重复操作（周围），每次入队列的时候就visited会减少时间复杂度
          while (!que.empty()) {
              // 访问当前值
              pair<int, int> cur = que.front();
              que.pop();
              int i = cur.first;
              int j = cur.second;
              // grid[i][j] = '0';
              // 下一层入队列 左右上下
              if (0 <= i - 1 && grid[i - 1][j] == '1') {
                  que.push({i - 1, j});
                  grid[i - 1][j] = '0';
              } 
              if (i + 1 < maxrow && grid[i + 1][j] == '1') {
                  que.push({i + 1, j});
                  grid[i + 1][j] = '0';
              } 
              if (0 <= j - 1 && grid[i][j - 1] == '1'){
                  que.push({i, j - 1});
                  grid[i][j - 1] = '0';
              } 
              if (j + 1 < maxcol && grid[i][j + 1] == '1') {
                  que.push({i, j + 1});
                  grid[i][j + 1] = '0';
              } 
          }
      }
  };
  ```

  + DFS

    ```c++
    class Solution:
        def numIslands(self, grid: List[List[str]]) -> int:
            result = 0
            for row in range(len(grid)):
                for col in range(len(grid[0])):
                    if grid[row][col] == '1':
                        self.dfs(row, col, grid)
                        result += 1
            return result
    
        
        def dfs(self, row, col, grid):
            # terminal 
            if row < 0 or col < 0 or row >= len(grid) or col >= len(grid[0]) or grid[row][col] != '1':
                return 
            # visited
            grid[row][col] = '0'
    
            # next
            self.dfs(row - 1, col, grid)
            self.dfs(row + 1, col, grid)
            self.dfs(row, col - 1, grid)
            self.dfs(row, col + 1, grid) 
    
    ```

    

# 本周总结

+ 本周是之前一直比较害怕，目前学习自己感觉还是很满意的。
+ 对于分治、回溯感觉还是比较模糊
+ 深度优先于广度优先在做岛屿数量时有了更清晰的理解。
+ 二分查找，小细节很多，思想一直会，但是还是得多敲代码。