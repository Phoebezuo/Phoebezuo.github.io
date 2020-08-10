---
layout:     post
title:      Courses Schedule in Java
date:       2020-08-10
summary:    Summaries a few questions in Leetcode about Course Schedule
categories: Algorithm Leetcode
---

## [Course Schedule](https://leetcode.com/problems/course-schedule/)

There are a total of numCourses courses you have to take, labeled from 0 to numCourses. Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: [0,1]. Given the total number of courses and a list of prerequisite pairs, **is it possible** for you to finish all courses?

🖥 [Video Explanation](https://www.youtube.com/watch?v=IfmEjwyNrBU)

```
Input: numCourses = 2, prerequisites = [[1,0],[0,1]]
Output: false
Explanation: There are a total of 2 courses to take. To take course 1 you should have finished course 0, and to take course 0 you should also have finished course 1. So it is impossible.
```

``` java
class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        List<List<Integer>> adjacency = new ArrayList<List<Integer>>();
        for (int i = 0; i < numCourses; i++) {
            adjacency.add(new ArrayList<Integer>());
        }
        
        // get the indegree and adjacency of every course
        int[] indegrees = new int[numCourses];
        for (int[] cp : prerequisites) {
            // to take course cp[0], you have to first take course cp[1]
            indegrees[cp[0]]++; // it need one more step from cp[1] to get to cp[0]
            adjacency.get(cp[1]).add(cp[0]); // adjaceny of cp[1] is cp[0]
        }
        
        // get all the courses with the indegree of 0
        Queue<Integer> queue = new LinkedList<Integer>();
        for (int i = 0; i < numCourses; i++) {
            if (indegrees[i] == 0) { queue.add(i); }
        }

        while (!queue.isEmpty()) {
            // has already take this course 
            int pre = queue.poll();
            numCourses--;
            
            // iterate to next course
            for (int cur : adjacency.get(pre)) {
                indegrees[cur]--;
                
                // get all the courses with the indegree of 0.
                if (indegrees[cur] == 0) { queue.add(cur); }
            }
        }
        
        return numCourses == 0;
    }
}
```

## [Course Schedule II](https://leetcode.com/problems/course-schedule-ii/)

There are a total of numCourses courses you have to take, labeled from 0 to numCourses. Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: [0,1]. Given the total number of courses and a list of prerequisite pairs, return one of **correct orders**.

🖥 [Video Explanation](https://www.youtube.com/watch?v=79jkJGlvuGU)

```
Input: 4, [[1,0],[2,0],[3,1],[3,2]]
Output: [0,1,2,3] or [0,2,1,3]
Explanation: There are a total of 4 courses to take. To take course 3 you should have finished both courses 1 and 2. Both courses 1 and 2 should be taken after you finished course 0. So one correct course order is [0,1,2,3]. Another correct ordering is [0,2,1,3] .
```

``` java
class Solution {
    public int[] findOrder(int numCourses, int[][] prerequisites) {
        List<List<Integer>> adjacency = new ArrayList<List<Integer>>();
        for (int i = 0; i < numCourses; i++) {
            adjacency.add(new ArrayList<Integer>());
        }
        
        // get the indegree and adjacency of every course
        int[] indegrees = new int[numCourses];
        for (int[] cp : prerequisites) {
            // to take course cp[0], you have to first take course cp[1]
            indegrees[cp[0]]++; // it need one more step from cp[1] to get to cp[0]
            adjacency.get(cp[1]).add(cp[0]); // adjaceny of cp[1] is cp[0]
        }
        
        // get all the courses with the indegree of 0
        Queue<Integer> queue = new LinkedList<Integer>();
        for (int i = 0; i < numCourses; i++) {
            if (indegrees[i] == 0) { queue.add(i); }
        }
        
        List<Integer> ans = new ArrayList<Integer>();
        while (!queue.isEmpty()) {
            // has already take this course 
            int pre = queue.poll();
            ans.add(pre);
            numCourses--;
            
            // iterate to next course
            for (int cur : adjacency.get(pre)) {
                indegrees[cur]--;
                
                // get all the courses with the indegree of 0.
                if (indegrees[cur] == 0) { queue.add(cur); }
            }
        }
        
        if (numCourses == 0) {
            return ans.stream().mapToInt(i->i).toArray();
        } else {
            return new int[0];
        }
    }
}
```

## [Course Schedule III](https://leetcode.com/problems/course-schedule-iii/)

Each courses represented by pairs (t,d), has duration t and closed on d. A course should be taken continuously for t days and must be finished before or on the d day. Find the **maxima**l number of courses that can be taken. 

🖥 [Video Explanation]()

```
Input: [[100, 200], [200, 1300], [1000, 1250], [2000, 3200]]
Output: 3
Explanation: 
There're totally 4 courses, but you can take 3 courses at most:
- First, take the 1st course, it costs 100 days so you will finish it on the 100th day, and ready to take the next course on the 101st day.
- Second, take the 3rd course, it costs 1000 days so you will finish it on the 1100th day, and ready to take the next course on the 1101st day. 
- Third, take the 2nd course, it costs 200 days so you will finish it on the 1300th day. 
The 4th course cannot be taken now, since you will finish it on the 3300th day, which exceeds the closed date.
```

``` java
public class Solution {
    public int scheduleCourse(int[][] courses) {
        // sorted based on end day
        Arrays.sort(courses, (a, b) -> a[1] - b[1]);
        
        // courses[x][0] -> duration of course
        // courses[x][1] -> end day of course 
        
        int time = 0;
        int count = 0;
        for (int i = 0; i < courses.length; i++) {
            if (time + courses[i][0] <= courses[i][1]) {
                time += courses[i][0];
                count++;
            } else { // cannot take this course due to exceed the ending day 
                
                // find the maximum duration time before current course 
                int max_dur = i;
                for (int j = 0; j < i; j++) {
                    if (courses[j][0] > courses[max_dur][0]) { max_dur = j; }
                }
                
                // when the current does not have maximum duration time 
                if (courses[max_dur][0] != courses[i][0]) {
                    // a saving can be achived, which can help to fit in more courses 
                    time += courses[i][0] - courses[max_dur][0];
                }
                
                // indicate this course has not been taken and will not be taken in the future 
                courses[max_dur][0] = -1;
            }
        }
        return count;
    }
}
```

## [Course Schedule IV](https://leetcode.com/problems/course-schedule-iv/)

There are total of n courses you have to take, some courses may have direct prerequisite, e.g. to take course 0 you have first to take course 1, whcih is expressed as a pair: [1, 0]. You should answer for each `queries[i]` whether the course `queries[i][0]` is a prerequisite of the course `queries[i][1]` or not.

🖥 [Video Explanation](https://www.youtube.com/watch?v=mjgqp9laZnk)

``` 
Input: n = 5, prerequisites = [[0,1],[1,2],[2,3],[3,4]], queries = [[0,4],[4,0],[1,3],[3,0]]
Output: [true,false,true,false]
```

``` java
class Solution {
      public List<Boolean> checkIfPrerequisite(int n, int[][] prerequisites, int[][] queries) {
        //      key      higher level 
        HashMap<Integer, HashSet<Integer>> map = new HashMap<Integer, HashSet<Integer>>();
        for (int[] val : prerequisites) {
            HashSet<Integer> set; // higher level course for val[0]
            if (map.containsKey(val[0])) {
                set = map.get(val[0]);
            } else {
                set = new HashSet<Integer>();
            }
            set.add(val[1]);
            map.put(val[0], set);
        }

        // loop through all the possible path 
        HashSet<String> path = new HashSet<String>();
        for (int i = 0; i < n; i++) {
            bfs(map, i, n, path);
        }

        // check qeries with possible path 
        List<Boolean> ans = new ArrayList<Boolean>();
        for (int[] val : queries) {
            ans.add(path.contains(val[0] + "_" + val[1]));
        }
        return ans;
    }

    private void bfs(HashMap<Integer, HashSet<Integer>> map, int i, int n, HashSet<String> path) {
        if (!map.containsKey(i)) { return; }
        
        LinkedList<Integer> queue = new LinkedList<Integer>();
        boolean[] visited = new boolean[n]; // initialized to be false 
 
        queue.add(i);
        visited[i] = true;
        
        while (!queue.isEmpty()) {
            HashSet<Integer> higher_level = map.get(queue.poll());
            if (higher_level != null) {
                
                // loop through all the course of higher level 
                for (Integer d : higher_level) {
                    
                    // if have not learn this course 
                    if (!visited[d]) {
                        // i -> lower level, d -> higher level 
                        path.add(i + "_" + d);
                        queue.add(d);
                        visited[d] = true;
                    }
                }
            }
        }
    }
}
```

