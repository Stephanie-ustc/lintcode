#lintcode 186 最多有多少个点在一条直线上

---
layout: post
category : lintcode
tagline: "lintcode"
tags : [lintcode]
excerpt: 

---
{% include JB/setup %}

##题目

题目链接：http://www.lintcode.com/zh-cn/problem/max-points-on-a-line/

##解题报告

一个点加一个斜率，就可以唯一的确定一条直线。所以我们对每个点，都计算一下该点和其他点连线的斜率，这样对于这个点来说，相同斜率的直线有多少条，就意味着有多少个点在同一条直线上，因为这些直线是相同的。另外，如果计算过点A和点B的直线，当算到点B时，就不用再和A连线了，因为AB这条直线上的点数已经都计算过了。这里，我们用哈希表，以斜率为key，记录有多少重复直线。

##Source Code / C++
 
```C++

/**
 * Definition for a point.
 * struct Point {
 *     int x;
 *     int y;
 *     Point() : x(0), y(0) {}
 *     Point(int a, int b) : x(a), y(b) {}
 * };
 */
class Solution {
public:
    /**
     * @param points an array of point
     * @return an integer
     */
    int maxPoints(vector<Point>& points) {
        // Write your code here
        if( points.size() <=1 ) return points.size();
        map<double, int> slope_map;
        int ret = 1;
        for(int i =0; i< points.size(); ++i) {
            //过当前点的直线组成哈希表，斜率为key
            slope_map.clear();
            int same_point_num =0, res = 1; 
            for( int j =i+1; j<points.size(); ++j) {
                double slope = numeric_limits<double>::infinity();
                
                if(points[i].x != points[j].x) {
                    slope = 1.0 * (points[i].y - points[j].y) / (points[i].x - points[j].x);
                } else if (points[i].y == points[j].y){
                    ++same_point_num;
                    continue;
                }
                
                int slope_num = 0;
                if( slope_map.find(slope) != slope_map.end()) {
                    slope_num = ++ slope_map[slope];
                } else {
                    slope_map.insert( map<double, int>::value_type(slope, 2));
                    slope_num = 2;
                }
                res = max(slope_num, res);
            }
            
            ret = max(ret, res + same_point_num);
        }
        return ret;
    }
};
```