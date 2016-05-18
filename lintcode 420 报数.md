#lintcode 420 报数

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
报数指的是，按照其中的整数的顺序进行报数，然后得到下一个数。如下所示：

1, 11, 21, 1211, 111221, ...

1 读作 "one 1" -> 11.

11 读作 "two 1s" -> 21.

21 读作 "one 2, then one 1" -> 1211.

给定一个整数 n, 返回 第 n 个顺序。

 注意事项

整数的顺序将表示为一个字符串。

您在真实的面试中是否遇到过这个题？ Yes
样例
给定 n = 5, 返回 "111221".

##解题报告



##Source Code / C++ 

```C++

    //Source Code
class Solution {
public:
	/**
	* @param n the nth
	* @return the nth sequence
	*/
	string countAndSay(int n) {
		// Write your code here
		if (n <= 0) return "";
		string init = "1";
		string next = init;
		while (--n) {
			next = getNext(next);
			//cout << next << endl;
		}
		return next;
	}
	string getNext(string str) {
		if (str.size() == 0) return "";
		string ret = "";
		char ch = str[0];
		int count = 1;
		stringstream ss;		
		string tmp;
		for (int i = 1; i < str.size(); ++i) {
			if (ch == str[i]) {
				++count;
			}
			else {
				ss << count;
				ss << ch;
				ch = str[i];
				count = 1;
			}
		}
		ss << count;
		ss << ch;
		ss >> ret;
		return ret;

	}
};
```