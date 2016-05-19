#lintcode 392 打劫房屋

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
假设你是一个专业的窃贼，准备沿着一条街打劫房屋。每个房子都存放着特定金额的钱。你面临的唯一约束条件是：相邻的房子装着相互联系的防盗系统，且 当相邻的两个房子同一天被打劫时，该系统会自动报警。

给定一个非负整数列表，表示每个房子中存放的钱， 算一算，如果今晚去打劫，你最多可以得到多少钱 在不触动报警装置的情况下。

您在真实的面试中是否遇到过这个题？ Yes
样例
给定 [3, 8, 4], 返回 8.

##解题报告



##Source Code / C++ 

```C++

    //Source Code
class Solution {
public:
	/**
	* @param A: An array of non-negative integers.
	* return: The maximum amount of money you can rob tonight
	*/
	long long houseRobber(vector<int> A) {
		// write your code here
		int n = A.size();
		if (n == 0) return 0;
		long long ret = A[0];
		vector<long long> dp(3, 0);
		for (int i = 0; i < n; ++i) {
			long long int temp = 0;
			for (int j = 0; j < 2; ++j) {
				temp = max(temp, dp[j] + A[i]);
			}
			ret = max(ret, temp);
			dp.push_back(temp);
			dp.erase(dp.begin());
		}
		return ret;
	}
};
```