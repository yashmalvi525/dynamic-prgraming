# **Understanding Dynamic Programming (DP) ~YASH MALVI**

## **What is Dynamic Programming?**
Dynamic Programming (DP) is a **programming technique**, not a data structure. It is used to **optimize recursive solutions** by storing and reusing previously computed results to avoid redundant calculations.

## **When to Apply DP?**
A problem can be solved using DP if it satisfies the following properties:

### **1. Overlapping Subproblems**
- The problem can be broken down into smaller subproblems, which are solved multiple times.

### **2. Optimal Substructure**
- The optimal solution of the main problem can be built using the optimal solutions of its subproblems.

### **Example: Fibonacci Series**
Fibonacci numbers follow the recurrence relation:

\[ F(n) = F(n-1) + F(n-2) \]
\[ F(0) = 0, \quad F(1) = 1 \]

Without DP, using recursion alone, this leads to redundant calculations. DP ensures that each problem is solved **only once** and reused whenever needed.

### **Visual Representation: Recursive Tree for Fibonacci (Without DP)**

```
               F(5)
             /     \
        F(4)       F(3)
       /    \      /    \
   F(3)    F(2)  F(2)  F(1)
  /   \     /  \   /  \
F(2)  F(1) F(1) F(0) F(1) F(0)
```

- Here, `F(3)` and `F(2)` are calculated multiple times.
- This redundant computation can be **avoided using DP**.

## **Types of DP Approaches**

### **1. Top-Down Approach (Recursion + Memoization)**
#### **Steps:**
1. Identify the type of DP problem and create a **DP array**.
2. Whenever solving a subproblem, **store** the result in the DP array.
3. If the answer already exists in the DP array, **use it directly** instead of recomputing.

#### **Code (Top-Down Approach)**
```cpp
class Solution {
public:
    int solveUsingMem(int n, vector<int>& dp) {
        if (n == 0) return 0;
        if (n == 1) return 1;

        // If the result is already computed, return it
        if (dp[n] != -1) {
            return dp[n];
        }

        // Compute and store the result in DP array
        dp[n] = solveUsingMem(n-1, dp) + solveUsingMem(n-2, dp);
        return dp[n];
    }

    int fib(int n) {
        vector<int> dp(n+1, -1); // Step 1: Create DP array
        return solveUsingMem(n, dp);
    }
};
```

### **2. Bottom-Up Approach (Tabulation)**
#### **Steps:**
1. **Create a DP array**.
2. **Analyze the base case** and initialize the DP array accordingly.
3. **Reverse the recursive approach** and solve iteratively.

#### **Visual Representation: Bottom-Up Computation**

```
F(0) = 0
F(1) = 1
F(2) = F(1) + F(0) = 1 + 0 = 1
F(3) = F(2) + F(1) = 1 + 1 = 2
F(4) = F(3) + F(2) = 2 + 1 = 3
F(5) = F(4) + F(3) = 3 + 2 = 5
```

#### **Code (Bottom-Up Approach)**
```cpp
class Solution {
public:
    int usingTabulation(int n) {
        if (n == 0) return 0;

        // Step 1: Create DP array
        vector<int> dp(n+1, -1);
        dp[0] = 0;
        dp[1] = 1;

        // Step 2: Fill the DP array iteratively
        for (int i = 2; i <= n; i++) {
            dp[i] = dp[i-1] + dp[i-2];
        }

        return dp[n];
    }
};
```

### **3. Space Optimization**
#### **Steps:**
1. Observe the **pattern** in the bottom-up approach.
2. Use **dry run** to check if you really need the full DP array.
3. If only a few previous values are required, **remove the DP array** and use variables instead.

#### **Code (Space Optimization Approach)**
```cpp
class Solution {
public:
    int spaceOptimised(int n) {
        if (n == 0) return 0;
        if (n == 1) return 1;

        int prev = 0, curr = 1, ans;
        for (int i = 2; i <= n; i++) {
            ans = prev + curr;
            prev = curr;
            curr = ans;
        }
        return curr;
    }
};
```

## **Final Thoughts**
### **Key Takeaways:**
- **Top-Down (Memoization)**: Uses recursion + DP array to store results.
- **Bottom-Up (Tabulation)**: Uses iteration and eliminates recursion.
- **Space Optimization**: Removes the DP array by recognizing patterns in previous values.

By following these approaches, you can efficiently solve **many DP problems** while improving time and space complexity! 🚀

