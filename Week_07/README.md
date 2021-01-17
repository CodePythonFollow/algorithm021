# 作业

- [朋友圈](https://leetcode-cn.com/problems/friend-circles)（亚马逊、Facebook、字节跳动在半年内面试中考过）

  ```c++
  class Solution:
      def findCircleNum(self, isConnected: List[List[int]]) -> int:
          def find(index: int) -> int:
              if parent[index] != index:
                  parent[index] = find(parent[index])
              return parent[index]
          
          def union(index1: int, index2: int):
              parent[find(index1)] = find(index2)
          
          provinces = len(isConnected)
          parent = list(range(provinces))
          
          for i in range(provinces):
              for j in range(i + 1, provinces):
                  if isConnected[i][j] == 1:
                      union(i, j)
          
          circles = sum(parent[i] == i for i in range(provinces))
          return circles
  ```

- [岛屿数量](https://leetcode-cn.com/problems/number-of-islands/)（近半年内，亚马逊在面试中考查此题达到 361 次）

  ```c++
  class Solution {
  private:
      void dfs(vector<vector<char>>& grid, int r, int c) {
          int nr = grid.size();
          int nc = grid[0].size();
  
          grid[r][c] = '0';
          if (r - 1 >= 0 && grid[r-1][c] == '1') dfs(grid, r - 1, c);
          if (r + 1 < nr && grid[r+1][c] == '1') dfs(grid, r + 1, c);
          if (c - 1 >= 0 && grid[r][c-1] == '1') dfs(grid, r, c - 1);
          if (c + 1 < nc && grid[r][c+1] == '1') dfs(grid, r, c + 1);
      }
  
  public:
      int numIslands(vector<vector<char>>& grid) {
          int nr = grid.size();
          if (!nr) return 0;
          int nc = grid[0].size();
  
          int num_islands = 0;
          for (int r = 0; r < nr; ++r) {
              for (int c = 0; c < nc; ++c) {
                  if (grid[r][c] == '1') {
                      ++num_islands;
                      dfs(grid, r, c);
                  }
              }
          }
  
          return num_islands;
      }
  };
  ```

- [括号生成](https://leetcode-cn.com/problems/generate-parentheses/)（亚马逊、Facebook、字节跳动在半年内面试中考过）

  ```c++
  class Solution {
  public:
      vector<string> generateParenthesis(int n) {
          vector<string> res;
          int lc = 0, rc = 0;
          dfs(res, "", n, lc, rc);
          return res;
      }
      void dfs(vector<string>& res, string path, int n, int lc, int rc) {
          if (rc > lc || lc > n || rc > n) return;
          if (lc == rc && lc == n) {
              res.push_back(path);
              return;
          }
          dfs(res, path + '(', n, lc + 1, rc);
          dfs(res, path + ')', n, lc, rc + 1);
      }
  };
  ```

- [单词接龙](https://leetcode-cn.com/problems/word-ladder/)（亚马逊、Facebook、谷歌在半年内面试中考过）

```c++
class Solution(object):
    def ladderLength(self, beginWord, endWord, wordList):
        st=set(wordList)
        if endWord not in st:
            return 0
        m=len(beginWord)        

        queue=collections.deque()        
        queue.append((beginWord,1))

        visited=set()
        visited.add(beginWord)

        while queue:
            cur,step=queue.popleft()
            if cur==endWord:
                return step
            
            for i in range(m):                
                for j in range(26):
                    tmp=cur[:i]+chr(97+j)+cur[i+1:]
                    if tmp not in visited and tmp in st:
                        queue.append((tmp,step+1))
                        visited.add(tmp)

        return 0
```

