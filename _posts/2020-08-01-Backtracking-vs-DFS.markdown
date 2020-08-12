---
layout:     post
title:      Backtracking vs DFS
date:       2020-08-01
summaries:  Personal understanding between recursion, backtracking and dfs 
categories: Algorithm Backtracking DFS
---

DFS is a way of iterating through an actual graph/tree structure looking for a value, whereas backtracking is iterating through a problem space looking for a solution.

Backtracking is a more general algorithm that doesn't necessarily even relate to trees.

<div class="showcase">
  <img style="width:50%" src="/images/post/difference.png" alt="">
</div>

## **Recursion**

```java
void foo() { 
    if (conditions) {  
        ///////  
        return;  
    }  
    foo();  
}  
```

## **Backtracking**

```java
void backtrack(int current_status) {  
    if (condition) {  
        record or output  
    } else {
        for(i = 0;i < n; i++) { //traverse all the nodes of solution tree 
            Generate child parameters
            if (condition) {  
                backtrack(child condition)  
            }  
            reocover global variables //(backtracking part)
        }  
    } 
}  
```

## **Depth First Search**

```java
public void dfs(int start) {
    boolean[] isVisited = new boolean[adjVertices.size()];
    dfsRecursive(start, isVisited);
}
 
private void dfsRecursive(int current, boolean[] isVisited) {
    isVisited[current] = true;
    visit(current);
    for (int dest : adjVertices.get(current)) {
        if (!isVisited[dest])
            dfsRecursive(dest, isVisited);
    }
}
```
