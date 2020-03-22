# Maximal Rectangle
## https://leetcode.com/problems/maximal-rectangle

Given a 2D binary matrix filled with 0's and 1's, find the largest rectangle containing only 1's and return its area.
```
Example:

Input:
[
  ["1","0","1","0","0"],
  ["1","0","1","1","1"],
  ["1","1","1","1","1"],
  ["1","0","0","1","0"]
]
Output: 6
```

# Implementation :

```java
class Solution {
    public int largestRectangleArea(int[] heights) {
        Stack<Integer> stack = new Stack<>();
        int maxArea = 0;
        int index = 0;
        while (index < heights.length) {
            if (stack.empty() || heights[index] >= heights[stack.peek()]) {
                stack.push(index++);
            } else {
                int top = stack.pop();
                int width = stack.empty() ? index : index - stack.peek() - 1;
                maxArea = Math.max(maxArea, heights[top] * width);
            }
        }
        while (!stack.empty()) {
            int top = stack.pop();
            int width = stack.empty() ? index : index - stack.peek() - 1;
            maxArea = Math.max(maxArea, heights[top] * width);
        }

       return maxArea;
    }

    public int maximalRectangle(char[][] matrix) {
        if (matrix.length == 0) return 0;
        int maxarea = 0;
        int[] dp = new int[matrix[0].length];

        for(int i = 0; i < matrix.length; i++) {
            for(int j = 0; j < matrix[0].length; j++) {

                // update the state of this row's histogram using the last row's histogram
                // by keeping track of the number of consecutive ones

                dp[j] = matrix[i][j] == '1' ? dp[j] + 1 : 0;
            }
            // update maxarea with the maximum area from this row's histogram
            maxarea = Math.max(maxarea, largestRectangleArea(dp));
        } 
        return maxarea;
    }
}
```

