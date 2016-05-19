#lintcode 534 打劫房屋II

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
在上次打劫完一条街道之后，窃贼又发现了一个新的可以打劫的地方，但这次所有的房子围成了一个圈，这就意味着第一间房子和最后一间房子是挨着的。每个房子都存放着特定金额的钱。你面临的唯一约束条件是：相邻的房子装着相互联系的防盗系统，且 当相邻的两个房子同一天被打劫时，该系统会自动报警。

给定一个非负整数列表，表示每个房子中存放的钱， 算一算，如果今晚去打劫，你最多可以得到多少钱 在不触动报警装置的情况下。

 注意事项

这题是House Robber的扩展，只不过是由直线变成了圈

您在真实的面试中是否遇到过这个题？ Yes
样例
给出nums = [3,6,4], 返回　6，　你不能打劫3和4所在的房间，因为它们围成一个圈，是相邻的．

##解题报告



##Source Code / C++ 

```C++

    //Source Code
class Solution {
public:
	/**
	* @param nums: An array of non-negative integers.
	* return: The maximum amount of money you can rob tonight
	*/
	int houseRobber2(vector<int>& nums) {
		// write your code here
		if (nums.size() <= 1) return nums.empty() ? 0 : nums[0];
		return max(houseRobber(nums, 0, nums.size() - 1), houseRobber(nums, 1, nums.size()));
	}

	int houseRobber(vector<int> &nums, int left, int right) {
		if ( right - left  <= 1)  return nums[left];
		vector<int> dp(right, 0);
		dp[left] = nums[left];
		dp[left + 1] = max(nums[left], nums[left + 1]);

		for (int i = left + 2; i < right; ++i) {
			dp[i] = max(dp[i - 2] + nums[i], dp[i - 1]);
		}
		return dp[right - 1];
	}
};

```