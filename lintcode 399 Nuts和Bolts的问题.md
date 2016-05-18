#lintcode 399 Nuts和Bolts的问题

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

给定一组 n 个不同大小的 nuts 和 n 个不同大小的 bolts。nuts 和 bolts 一一匹配。 不允许将 nut 之间互相比较，也不允许将 bolt 之间互相比较。也就是说，只许将 nut 与 bolt 进行比较， 或将 bolt 与 nut 进行比较。请比较 nut 与 bolt 的大小。

您在真实的面试中是否遇到过这个题？ Yes
样例
Nuts 用一个整数数组表示 nuts [] = {1, 5, 8, 2}. Bolts 也用一个整数数组表示 bolts[] = {3, 6, 7, 9}. 
我们将提供一个比较函数，以比较 nut 与 bolt 的大小。
将 nuts 进行升序排序，使得 nuts 与 bolts 位置对等。

##解题报告



##Source Code / C++ 

```C++

class Solution {
public:
	/**
	* @param nuts: a vector of integers
	* @param bolts: a vector of integers
	* @param compare: a instance of Comparator
	* @return: nothing
	*/
	void sortNutsAndBolts(vector<string> &nuts, vector<string> &bolts, Comparator compare) {
		// write your code here
		if (nuts.empty() || bolts.empty()) return;
		if (nuts.size() != bolts.size()) return;

		quicksort(nuts, bolts, compare, 0, nuts.size() - 1);
	}
	void quicksort(vector<string> &nuts, vector<string> &bolts, Comparator compare, int low, int high) {
		if (low < high) {
			int pivot = partition(nuts, compare, low, high, bolts[low]);
			partition(bolts, compare, low, high, nuts[pivot]);
			quicksort(nuts, bolts, compare, low, pivot - 1);
			quicksort(nuts, bolts, compare, pivot + 1, high);
		}
	}

	int partition(vector<string>& str, Comparator compare, int l, int u, string& pivot
		) {

		int m = l;
		for (int i = l + 1; i <= u; ++i) {
			if (compare.cmp(str[i], pivot) == -1 ||
				compare.cmp(pivot, str[i]) == 1) {

				++m;
				std::swap(str[m], str[i]);
			}
			else if (compare.cmp(str[i], pivot) == 0 ||
				compare.cmp(pivot, str[i]) == 0) {
				// swap nuts[l]/bolts[l] with pivot
				std::swap(str[i], str[l]);
				--i;
			}
		}
		// move pivot to proper index
		std::swap(str[m], str[l]);

		return m;
	}
	int partition1(vector<string> &nuts, Comparator compare, int low, int high, string bolt) {
		int m = low;
		for (int i = low+1; i <= high; ++i) {
			if (compare.cmp(nuts[i], bolt) == 1
				|| compare.cmp(bolt, nuts[i]) == -1) {
				m++;
				swap(nuts[m], nuts[i]);
			}
			else if( compare.cmp(nuts[i], bolt) == 0 ||
				compare.cmp(bolt, nuts[i]) == 0) {
				swap(nuts[i], nuts[low]);
				i--;
			}
		}
		swap(nuts[m], nuts[low]);
		return m;
	}
	int partition2(vector<string> &bolts, Comparator compare, int low, int high, string nut) {
		int m = low;
		for (int i = low+1; i <= high; ++i) {
			if (compare.cmp(nut, bolts[i]) == -1) {
				m++;
				swap(bolts[m], bolts[i]);
			}
			else if (compare.cmp(nut, bolts[i]) == 0) {
				swap(bolts[i], bolts[low]);
				i--;
			}
		}
		swap(bolts[m], bolts[low]);
		return m;
	}
};

    //Source Code


v2 不能用该版本的快拍 主要原因在于 == 的这个值需要确定在mid位置上，不然会影响排序.
/**
 * class Comparator {
 *     public:
 *      int cmp(string a, string b);
 * };
 * You can use compare.cmp(a, b) to compare nuts "a" and bolts "b",
 * if "a" is bigger than "b", it will return 1, else if they are equal,
 * it will return 0, else if "a" is smaller than "b", it will return -1.
 * When "a" is not a nut or "b" is not a bolt, it will return 2, which is not valid.
*/
class Solution {
public:
    /**
     * @param nuts: a vector of integers
     * @param bolts: a vector of integers
     * @param compare: a instance of Comparator
     * @return: nothing
     */
    void sortNutsAndBolts(vector<string> &nuts, vector<string> &bolts, Comparator compare) {
        // write your code here
        //partition()
        //sort(left)
        //sort(right)
        //cout << compare.cmp(nuts[1], bolts[1]);
        quicksort(nuts, bolts, compare, 0, nuts.size()-1);
        
    }
    void quicksort(vector<string> &nuts, vector<string> & bolts, Comparator compare, int left, int right) {
        if(left < right) {
            int mid = partition(nuts, bolts, compare,left, right);
            quicksort(nuts, bolts, compare, left, mid -1);
            quicksort(nuts, bolts, compare, mid+1, right);
        }
    }
    int partition(vector<string> &nuts, vector<string> &bolts, Comparator compare, int left, int right) {
		int begin = left;
		int end = right;
		string pivot = nuts[left];
		string tmp = bolts[left];
		while (left < right) {
			//cout << left << right << endl;
			while (left < right && compare.cmp(pivot, bolts[right]) <= 0) {
				right--;
			}
			bolts[left] = bolts[right];
			while (left < right && compare.cmp(pivot, bolts[left]) > 0) {
				left++;
			}
			bolts[right] = bolts[left];
		}
		bolts[left] = tmp;

		pivot = bolts[left];
		tmp = nuts[begin];
		while (begin < end) {
			while (begin < end && compare.cmp(nuts[end], pivot) > 0) {
				end--;
			}
			nuts[begin] = nuts[end];
			while (begin< end && compare.cmp(nuts[begin], pivot) <= 0 ) {
				begin++;
			}
			nuts[end] = nuts[begin];
		}
		nuts[begin] = tmp;

		return left;
	}
};
```