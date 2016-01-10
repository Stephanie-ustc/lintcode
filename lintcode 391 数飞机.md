---
layout: post
category : lintcode
tagline: "lintcode"
tags : [lintcode]
excerpt: 。
---
**解题报告**

RMQ问题，可以选择使用线段树解决，但是没必要那么麻烦，所以就是简单的建立一个区间，然后求一个最大值即可。


**Source Code/ C++**

```
	/**
	 * Definition of Interval:
	 * classs Interval {
	 *     int start, end;
	 *     Interval(int start, int end) {
	 *         this->start = start;
	 *         this->end = end;
	 *     }
	 */
	class Solution {
	public:
	    /**
	     * @param intervals: An interval array
	     * @return: Count of airplanes are in the sky.
	     */
	    int countOfAirplanes(vector<Interval> &airplanes) {
	        // write your code here
	        map< int, int > num_map;
	        set< int > num_set;
	        
	        for(auto x : airplanes) {
	            num_map[x.start] ++;
	            num_map[x.end] --;
	            num_set.insert(x.start);
	            num_set.insert(x.end);
	        }
	        vector< int > num_list;
	        std::copy(num_set.begin(), num_set.end(), back_inserter(num_list));
	        int ret=0;
	        int cnt=0;
	        for ( auto x : num_list ) {
	            cnt +=num_map[x];
	            ret = max(ret, cnt);
	        }
	        return ret;
	    }
	};

```