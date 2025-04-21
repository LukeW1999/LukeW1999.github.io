---
title: C_code_practise
published: 2025-04-18
description: ''
image: ''
tags: []
category: ''
draft: false 
lang: ''
---



<iframe width="100%" height="500px" src="https://godbolt.org/e#g:!((g:!((g:!((h:codeEditor,i:(filename:'1',fontScale:14,fontUsePx:'0',j:1,lang:c,selection:(endColumn:1,endLineNumber:1,positionColumn:1,positionLineNumber:1,selectionStartColumn:1,selectionStartLineNumber:1,startColumn:1,startLineNumber:1),source:''),l:'5',n:'0',o:'C+source+%231',t:'0')),k:50,l:'4',n:'0',o:'',s:0,t:'0'),(g:!((h:executor,i:(argsPanelShown:'1',compilationPanelShown:'0',compiler:cg132,compilerName:'',compilerOutShown:'0',execArgs:'',execStdin:'',fontScale:14,fontUsePx:'0',j:1,lang:c,libs:!(),options:'',source:1,stdinPanelShown:'1',tree:'1',wrap:'1'),l:'5',n:'0',o:'Executor+x86-64+gcc+13.2+(C,+Editor+%231)',t:'0')),k:50,l:'4',n:'0',o:'',s:0,t:'0')),l:'2',n:'0',o:'',t:'0')),version:4"></iframe>

今天是2025年4月18日，今天练习两道medium和1道hard的题目。
```
你正在维护一个项目，该项目有 n 个方法，编号从 0 到 n - 1。

给你两个整数 n 和 k，以及一个二维整数数组 invocations，其中 invocations[i] = [ai, bi] 表示方法 ai 调用了方法 bi。

已知如果方法 k 存在一个已知的 bug。那么方法 k 以及它直接或间接调用的任何方法都被视为 可疑方法 ，我们需要从项目中移除这些方法。

只有当一组方法没有被这组之外的任何方法调用时，这组方法才能被移除。

返回一个数组，包含移除所有 可疑方法 后剩下的所有方法。你可以以任意顺序返回答案。如果无法移除 所有 可疑方法，则 不 移除任何方法。
```

```c++

#include <vector>
class Solution {
public:
    vector<int> remainingMethods(int n, int k, vector<vector<int>>& invocations) {

```
关于C++的vector，学习一下它和python的list的不同，C++的vector是提前规定类型的，而python的list是动态的。而操作来说，vector有push_back(),pop_back()


得到一个n functions 需要维护 with label 0 to n-1.
input是一个n,k,一个[ai,bi]的二维数组。有点像一个linked list, 但是是二维的。
给了一个例子n=4,k=1,invocations=[[0,1],[1,2],[3,2]]
output:[0,1,2,3]
有点像esbmc,尽管需要free memory, 但是由于被后一个函数调用，所以目前不能free.

我们首先要标记哪些函数是可疑的。
```c++
class Solution {
public:
    vector<int> remainingMethods(int n, int k, vector<vector<int>>& invocations) {
        // 构建邻接表表示调用关系
        vector<vector<int>> graph(n);
        for (const auto& e : invocations) {
            graph[e[0]].push_back(e[1]);
        }
        
        // 使用DFS标记所有从k可达的节点为可疑
        vector<bool> isSuspicious(n, false);
        function<void(int)> dfs = [&](int node) {
            isSuspicious[node] = true;
            for (int next : graph[node]) {
                if (!isSuspicious[next]) {
                    dfs(next);
                }
            }
        };
        
        dfs(k);
        
        // 检查是否有非可疑方法调用可疑方法
        for (const auto& e : invocations) {
            if (!isSuspicious[e[0]] && isSuspicious[e[1]]) {
                // 如果有非可疑方法调用可疑方法，返回所有方法
                vector<int> allMethods(n);
                for (int i = 0; i < n; i++) {
                    allMethods[i] = i;
                }
                return allMethods;
            }
        }
        
        // 否则，返回所有非可疑方法
        vector<int> result;
        for (int i = 0; i < n; i++) {
            if (!isSuspicious[i]) {
                result.push_back(i);
            }
        }
        return result;
    }
};

```