#405 和为零的子矩阵

---
layout: post
category : lintcode
tagline: "lintcode"
tags : [lintcode]
excerpt: 

---
{% include JB/setup %}

##题目

题目链接：http://www.lintcode.com/zh-cn/problem/submatrix-sum/
给定一个整数矩阵，请找出一个子矩阵，使得其数字之和等于0.输出答案时，请返回左上数字和右下数字的坐标。

您在真实的面试中是否遇到过这个题？ Yes
样例
给定矩阵

[
  [1 ,5 ,7],
  [3 ,7 ,-8],
  [4 ,-8 ,9],
]
返回 [(1,1), (2,2)]

挑战 
O(n3) 时间复杂度。

##解题报告



##Source Code / C++ 

```C++

class Solution {
public:
	/**
	* @param matrix an integer matrix
	* @return the coordinate of the left-up and right-down number
	*/
	vector<vector<int>> submatrixSum(vector<vector<int>>& matrix) {
		// Write your code here
		vector< vector<int> > ret(2, vector<int>(2, 0));
		if (matrix.empty()) return ret;
		int sum = 0;
		int lx, ly, rx, ry;
		for (lx = 0; lx< matrix.size(); ++lx) {
			for (ly = 0; ly < matrix.front().size(); ++ly) {
				int sum = matrix[lx][ly];
				ret[0][0] = lx;
				ret[0][1] = ly;

				for ( rx = lx + 1; rx < matrix.size(); ++rx) {
					for (ry = ly + 1; ry < matrix.front().size(); ++ry) {
						sum += matrix[rx][ry];
						if (sum == 0) {
							ret[1][0] = rx;
							ret[1][1] = ry;
							break;
						}

					}
				}
			}
		}
		return ret;

	}
};

```