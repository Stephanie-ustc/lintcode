#lintcode 

---
layout: post
category : lintcode
tagline: "lintcode"
tags : [lintcode]
excerpt: 

---
{% include JB/setup %}

##题目

题目：

在一个排序矩阵中找从小到大的第 k 个整数。

排序矩阵的定义为：每一行递增，每一列也递增。

您在真实的面试中是否遇到过这个题？ Yes
样例
给出 k = 4 和一个排序矩阵：

[
  [1 ,5 ,7],
  [3 ,7 ,8],
  [4 ,8 ,9],
]
返回 5。

挑战 
使用O(k log n)的方法，n为矩阵的宽度和高度中的最大值。

##解题报告



##Source Code / C++ 

```C++

    //Source Code

class Solution {
public:
	/**
	* @param matrix: a matrix of integers
	* @param k: an integer
	* @return: the kth smallest number in the matrix
	*/
	int kthSmallest(vector<vector<int> > &matrix, int k) {
		// write your code here
		int n = matrix.size();
		int m = matrix.front().size();
		// type pair<int, pair<int, int>>  : value, index_x ,index_y;

		priority_queue< pair<int, pair<int, int> >, vector< pair<int, pair<int, int> > >, greater<pair<int, pair<int, int> > > > q;
		map<pair<int, int>, bool> visited;
		q.push(make_pair(matrix[0][0], make_pair(0, 0)));
		visited[make_pair(0, 0)] = true;

		while (k--) {
			pair<int, pair<int, int>> cur = q.top();
			if (k == 0) {
				return cur.first;
			}

			q.pop();
			if (cur.second.first + 1 < n && visited[make_pair(cur.second.first + 1, cur.second.second)] == false) {
				q.push(make_pair(matrix[cur.second.first + 1][cur.second.second], make_pair(cur.second.first + 1, cur.second.second)));
				visited[make_pair(cur.second.first + 1, cur.second.second)] = true;
			}
			if (cur.second.second + 1 < m && visited[make_pair(cur.second.first, cur.second.second + 1)] == false) {
				q.push(make_pair(matrix[cur.second.first][cur.second.second + 1], make_pair(cur.second.first, cur.second.second + 1)));
				visited[make_pair(cur.second.first, cur.second.second + 1)] = true;
			}
		}
	}
};
```