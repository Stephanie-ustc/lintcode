#lintcode 477 被围绕的区域

---
layout: post
category : lintcode
tagline: "lintcode"
tags : [lintcode]
excerpt: 

---
{% include JB/setup %}

** 题目 **

题目链接：http://www.lintcode.com/zh-cn/problem/surrounded-regions/

** 解题报告 **

dfs或者bfs的题目，主要有两种思路，

第一种是先寻找图里的封闭的区间，然后将其转为X，需要多添加一个VISmap，避免出现错误的返回寻找情况，代码实现如第一版所示，实现难度比较高，逻辑相对复杂

第二种就是直接从边界开始寻找所有没有被封闭的O，不需要添加VISmap 代码逻辑简单，就是DFS搜索，然后将连通的O 转化为一个临时变量Y，最后重新扫一遍图，将O转为X ,将Y转为O 问题得到解决。

** Source Code / C++ **

第二版

```C++

class Solution {
public:
    /**
     * @param board a 2D board containing 'X' and 'O'
     * @return void
     */
    void surroundedRegions(vector<vector<char>>& board) {
        // Write your code here
        if( board.size() == 0 || board[0].size() == 0) return;
        
        int n = board.size();
        int m = board[0].size();
        
        for(int i=0; i<n; ++i){
            if(board[i][0] == 'O'){
                dfs(board, i, 0, n ,m);
            }
            if(board[i][m-1] == 'O') {
                dfs(board, i, m-1, n, m);
            }
        }
        
        for(int j=0; j<m; ++j){
            if(board[0][j] == 'O'){
                dfs(board, 0, j, n ,m);
            }
            if(board[n-1][j] == 'O') {
                dfs(board, n-1,j, n, m);
            }
        }
        
        for(int i=0; i<n; ++i) {
            for(int j=0; j<m; ++j) {
                if(board[i][j] == 'Y') {
                    board[i][j] = 'O';
                }
                else if(board[i][j] == 'O') {
                    board[i][j] = 'X';
                }
            }
        }
    }
    
    void dfs(vector< vector<char> >& board, int x, int y, int n, int m) {
        //vis[x][y] = '1';
        
        board[x][y] = 'Y';
        if(x>=0 && x+1 < n && y>=0 && y <m && board[x+1][y] == 'O') {
            dfs(board, x+1, y, n, m);
        }
        if(x-1>=0 && x < n && y>=0 && y <m && board[x-1][y] == 'O') {
            dfs(board, x-1, y, n, m);
        }
        if(x>=0 && x < n && y>=0 && y+1 <m && board[x][y+1] == 'O') {
            dfs(board, x, y+1, n, m);
        }
        if(x>=0 && x < n && y-1>=0 && y <m && board[x][y-1] == 'O') {
            dfs(board, x, y-1, n, m);
        }
    }
};

```

**第一版 ，error**

```c++

class Solution {
public:
    /**
     * @param board a 2D board containing 'X' and 'O'
     * @return void
     */
    void surroundedRegions(vector<vector<char>>& board) {
        // Write your code here
        if( board.size() == 0 || board[0].size() == 0) return;
        
        int n = board.size();
        int m = board[0].size();
        vector<vector<char>> vis = board;
        
        for(int x =0; x<n; ++x) {
            for(int y=0; y< m; ++y) {
                //if(vis[x][y] == '1')
                //    continue;
                //vis[x][y] = '1';
                if(board[x][y] == 'O'&& vis[x][y]!='1') {
                    bool flag = dfs(board, x, y, n, m, vis);
                    if(flag == false) board[x][y] = 'O';
                }
            }
        }
        
    }
    
    bool dfs(vector< vector<char> >& board, int x, int y, int n, int m, vector< vector<char> >& vis) {
        //vis[x][y] = '1';
        //是否在被x围绕
        if(x ==0 || x ==n-1 || y==0 || y ==m-1 || vis[x][y] == '1' ) {
            vis[x][y] = '1';
            return false;
        }
        
        board[x][y] = 'X';
        int flag= true;
        if(x>=0 && x+1 < n && y>=0 && y <m && board[x+1][y] == 'O') {
            flag = flag & dfs(board, x+1, y, n, m, vis);
        }
        if(x-1>=0 && x < n && y>=0 && y <m && board[x-1][y] == 'O') {
            flag = flag & dfs(board, x-1, y, n, m, vis);
        }
        if(x>=0 && x < n && y>=0 && y+1 <m && board[x][y+1] == 'O') {
            flag = flag & dfs(board, x, y+1, n, m, vis);
        }
        if(x>=0 && x < n && y-1>=0 && y <m && board[x][y-1] == 'O') {
            flag = flag & dfs(board, x, y-1, n, m, vis);
        }
        
        if(flag == false) {
            board[x][y] ='O';
            vis[x][y] = '1';
            return false;
        }
        return true;
        
    }
};

```