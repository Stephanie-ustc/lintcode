#lintcode 442 实现 Trie

---
layout: post
category : lintcode
tagline: "lintcode"
tags : [lintcode]
excerpt: 。
---
{% include JB/setup %}

##题目

题目链接：http://www.lintcode.com/zh-cn/problem/restore-ip-addresses/

##解题报告

字典树

##Source Code / C++ 

```C++

/**
 * Your Trie object will be instantiated and called as such:
 * Trie trie;
 * trie.insert("lintcode");
 * trie.search("lint"); will return false
 * trie.startsWith("lint"); will return true
 */
class TrieNode {
public:
    // Initialize your data structure here.
    TrieNode() {
        count =0;
        for(int i=0; i<26; ++i){
            son[i] = NULL;
        }
    }
    int count;
    TrieNode* son[26];
    
};

class Trie {
public:
    Trie() {
        root = new TrieNode();
    }

    // Inserts a word into the trie.
    void insert(string word) {
        TrieNode* index = root;
        for(int i=0; i<word.size(); ++i) {
            if(index->son[ word[i] - 'a' ] == NULL) {
                index->son[ word[i]- 'a' ] = new TrieNode();
            }
            index = index->son[ word[i]- 'a' ];
        }
        index->count++;
    }

    // Returns if the word is in the trie.
    bool search(string word) {
        TrieNode* index = root;
        for(int i =0; i< word.size(); ++i) {
            if(index->son[ word[i]- 'a'] == NULL) {
                return false;
            }
            index = index->son[ word[i]-'a' ];
        }
        if( index->count > 0) {
            return true;
        }
        else {
            return false;
        }
    }

    // Returns if there is any word in the trie
    // that starts with the given prefix.
    bool startsWith(string prefix) {
        TrieNode* index =root;
        for(int i=0; i< prefix.size(); ++i) {
            if( index->son[ prefix[i] - 'a'] == NULL) {return false; }
            index = index->son[ prefix[i]-'a'];
        }
        
        for(int i=0; i<26; ++i) {
            if( index->son[i] != NULL || index->count >0 ) {return true;}
        }
        return false;
        
    }

private:
    TrieNode* root;
};

```