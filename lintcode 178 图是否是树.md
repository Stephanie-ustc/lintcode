#lintcode 178 图是否是树

---
layout: post
category : lintcode
tagline: "lintcode"
tags : [lintcode]
excerpt: 。
---
{% include JB/setup %}

##题目

题目链接：http://www.lintcode.com/zh-cn/problem/graph-valid-tree/

##解题报告

主要解题思路并查集查询。
第一版 代码 是想要用DFS搜索来做，理论是也是可以的，从一个树中的任一一点出发，可以DFS到树中的任意一个点，如果n个点中存在有点被重复访问，则说明树中存在环。 同时，如果遍历完一遍后 若存在节点没有被遍历到，说明有多个独立的树 不符合条件。
但是在图的存储上采用了矩阵的形式，在内存上溢出了。改成边的形式存储即可。

第二、三版代码，使用并查集解决，感觉相对于dfs更加简单了，对所有的点进行公共祖先查询，若有存在2个祖先以上，则为错误，同样，若出现了点已经访问过了，则表示存在环路，不符合题目条件。

##Source Code / C++ 

**第三版**

```C++
	
class Solution {
public:
    /**
     * @param n an integer
     * @param edges a list of undirected edges
     * @return true if it's a valid tree, or false
     */
    
    int* ids;
    int cnt;
    int ids_size;
    
    bool validTree(int n, vector<vector<int>>& edges) {
        // Write your code here
        this->ids_size = n;
        this->cnt = n;
        this->ids = new int[n];
        //初始化
        for(int i=0; i< n; ++i) {
            this->ids[i] = i;
        }
        //并查集搜索
        for(int i =0; i< edges.size(); ++i) {
            if( !uni(edges[i][0], edges[i][1]) ) {
                return false;
            }
        }
        //删除开辟空间
        delete[] ids;
        return cnt == 1;
    }
    
    bool uni(int a, int b) {
        int src = ids[a];
        int dst = ids[b];
        
        if( src != dst ){
            for(int i =0; i < this->ids_size; ++i) {
                if(this->ids[i] == src) {
                    this->ids[i] = dst;
                }
            }
            
            cnt --;
            return true;
        } else {
            return false;
        }
    }
};


```


**第二版**

```C++

class Solution {
public:
    /**
     * @param n an integer
     * @param edges a list of undirected edges
     * @return true if it's a valid tree, or false
     */
    bool validTree(int n, vector<vector<int>>& edges) {
        // Write your code here
		UnionFind  uf(n);
		for(int i=0; i<edges.size(); ++i){
			if( !uf.Uni(edges[i][0], edges[i][1]) ) {
				return false;
			}
		}
		return uf.count() == 1;
    }
	class UnionFind {
	public:
		int* ids;
		int cnt;
		int idssize;
		UnionFind(int size){
			this->ids = new int[size];
			this->idssize = size;
			for(int i =0; i< size; ++i){
				this->ids[i] = i;
			}
			this->cnt = size;
		}
		~UnionFind(){
			delete[] this->ids;
		}
		bool Uni(int m, int n) {
			int src = find(m);
			int dst = find(n);
			if(src != dst) {
				for(int i=0; i< idssize; ++i) {
					if(ids[i] == src) {
						ids[i] = dst;
					}
				}

				cnt --;
				return true;
			} else {
			    return false;
			} 

		}

		int find(int m){
			return ids[m];
		}

		bool connect(int m, int n) {
			return find(m) == find(n);
		}

		int count() {
			return cnt;
		}

	};

};

```

**第一版**

```C++

class Solution {
public:
    /**
     * @param n an integer
     * @param edges a list of undirected edges
     * @return true if it's a valid tree, or false
     */
    bool dfs(vector< vector<int>> graph, vector<bool>& vis, int index, int father, int n){
        if(vis[index]) {
            return false;
        }
        vis[index] = true;
        for(int i=0; i<n; ++i) {
            if(graph[index][i] == 1 && i!=father){
                if( vis[i] ){
                    return false;
                }
                else {
                    if( !dfs(graph, vis, i, index, n) ) return false;
                }
                
            }
        }
        return true;
    }
     
    bool validTree(int n, vector<vector<int>>& edges) {
        // Write your code here
        if(edges.size() ==0 && n>1) return false;
        //init
        vector< vector<int> > graph;
        vector< bool > vis(n, false);
        
        for(int i=0; i< n; ++i) {
            vector<int> tmp(n,0);
            graph.push_back(tmp);
        }
        
        for(int i=0; i< edges.size(); ++i) {
            graph[ edges[i][0] ][ edges[i][1] ] =1;
            graph[ edges[i][1] ][ edges[i][0] ] =1;
        }
        bool ret =dfs(graph, vis, 0, 0, n);
        
        for(int i=0; i<n; ++i) {
            if(vis[i] == false) {
                return false;
            }
        }
        return ret;
        
    }
};

```
