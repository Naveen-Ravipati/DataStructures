# Dynamic Programming
Dynamic Programming is mainly an optimization over plain recursion. Wherever we see a recursive solution that has repeated calls for same inputs, we can optimize it using Dynamic Programming. 

The idea is to simply store the results of subproblems, so that we do not have to re-compute them when needed later. This simple optimization reduces time complexities from exponential to polynomial. For example, if we write simple recursive solution for Fibonacci Numbers, we get exponential time complexity and if we optimize it by storing solutions of subproblems, time complexity reduces to linear.

```java
/* simple recursive program for Fibonacci numbers */
int fib(int n) 
{ 
   if ( n <= 1 ) 
      return n; 
   return fib(n-1) + fib(n-2); 
}
```
Recursion tree for execution of fib(5)
```
                         fib(5)
                     /             \
               fib(4)                fib(3)
             /      \                /     \
         fib(3)      fib(2)         fib(2)    fib(1)
        /     \        /    \       /    \
  fib(2)   fib(1)  fib(1) fib(0) fib(1) fib(0)
  /    \
fib(1) fib(0)
```

We can see that the function fib(3) is being called 2 times. If we would have stored the value of fib(3), then instead of computing it again, we could have reused the old stored value. There are following two different ways to store the values so that these values can be reused:

>1.  Memoization (Top Down) ==> using cache
>2.  Tabulation (Bottom Up) ==> using array / matrix.


#### a) Memoization (Top Down): 
The memoized program for a problem is similar to the recursive version with a small modification that it looks into a lookup table before computing solutions. We initialize a lookup array with all initial values as NIL. Whenever we need the solution to a subproblem, we first look into the lookup table. If the precomputed value is there then we return that value, otherwise, we calculate the value and put the result in the lookup table so that it can be reused later.

Following is the memoized version for nth Fibonacci Number.
```py
# Function to calculate nth Fibonacci number 
def fib(n, lookup): 
    # Base case 
    if n == 0 or n == 1 : 
        lookup[n] = n 
    # If the value is not calculated previously then calculate it 
    if lookup[n] is None: 
        lookup[n] = fib(n-1 , lookup)  + fib(n-2 , lookup)  
    # return the value corresponding to that value of n 
    return lookup[n] 
# end of function 
```
#### b) Tabulation (Bottom Up): 
The tabulated program for a given problem builds a table in bottom up fashion and returns the last entry from table. For example, for the same Fibonacci number, we first calculate fib(0) then fib(1) then fib(2) then fib(3) and so on. So literally, we are building the solutions of subproblems bottom-up.

Following is the tabulated version for nth Fibonacci Number.
```py
def fib(n): 
    # array declaration 
    dp = [0]*(n+1) 
    # base case assignment 
    dp[1] = 1
    # calculating the fibonacci and storing the values 
    for i in xrange(2 , n+1): 
        dp[i] = dp[i-1] + dp[i-2] 
    return dp[n] 
```

Gist to solving DP problem is finding the recurrence relation. sometimes it may not be obvious to get the relation then take an example try to tabulate the sub-problem solutions with your own knowledge in a matrix and try to figure out how ```dp[i][j]``` is obtained ? what are the values it is dependent upon is it ```dp[i-1][j-1] or dp[i][j-1] or dp[i-1][j]  or dp[i][j-k] etc.```(kind of mathematical induction)

## Patterns :
[1. Minimum (Maximum) Path to Reach a Target](#minimum-(maximum)-path-to-reach-a-target)

[2. Distinct Ways](#distinct-ways)

[3. Merging Intervals](#merging-intervals)

[4. DP on Strings](#dp-on-strings)

[5. Decision Making](#decision-making)

### Minimum (Maximum) Path to Reach a Target
statement :
>Given a target find minimum (maximum) cost / path / sum to reach the target.

Approach :
>Choose minimum (maximum) path among all possible paths before the current state, then add value for the current state.

```py
routes[i] = min(routes[i-1], routes[i-2], ... , routes[i-k]) + cost[i]
```
Generate optimal solutions for all values in the target and return the value for the target.
```java
for (int i = 1; i <= target; ++i) {
   for (int j = 0; j < ways.size(); ++j) {
       if (ways[j] <= i) {
           dp[i] = min(dp[i], dp[i - ways[j]] + cost / path / sum) ;
       }
   }
}
return dp[target]
```

#### Similar Problems:
#### Easy
[746. Min Cost Climbing Stairs Easy](https://leetcode.com/problems/min-cost-climbing-stairs/)
#### Medium
[64. Minimum Path Sum](https://leetcode.com/problems/minimum-path-sum/)

[322. Coin Change](https://leetcode.com/problems/coin-change/)

[931. Minimum Falling Path Sum](https://leetcode.com/problems/minimum-falling-path-sum/)

[983. Minimum Cost For Tickets](https://leetcode.com/problems/minimum-cost-for-tickets/)

[650. 2 Keys Keyboard](https://leetcode.com/problems/2-keys-keyboard/)

[279. Perfect Squares](https://leetcode.com/problems/perfect-squares/)

[1049. Last Stone Weight II](https://leetcode.com/problems/last-stone-weight-ii/)

[120. Triangle](https://leetcode.com/problems/triangle/)

[474. Ones and Zeroes](https://leetcode.com/problems/ones-and-zeroes/)

[221. Maximal Square](https://leetcode.com/problems/maximal-square/)

#### Hard
[1240. Tiling a Rectangle with the Fewest Squares](https://leetcode.com/problems/tiling-a-rectangle-with-the-fewest-squares/)

[174. Dungeon Game](https://leetcode.com/problems/dungeon-game/)

[871. Minimum Number of Refueling Stops](https://leetcode.com/problems/minimum-number-of-refueling-stops/)

### Distinct Ways
statement :
>Given a target find a number of distinct ways to reach the target.

Approach :
>Sum all possible ways to reach the current state.

```py
routes[i] = routes[i-1] + routes[i-2], ... , + routes[i-k]
```
Generate sum for all values in the target and return the value for the target.
```java
for (int i = 1; i <= target; ++i) {
   for (int j = 0; j < ways.size(); ++j) {
       if (ways[j] <= i) {
           dp[i] += dp[i - ways[j]];
       }
   }
}
return dp[target]
```
Note

>Some questions point out the number of repetitions, in that case, add one more loop to simulate every repetition.

#### Similar Problems:
#### Easy
[70. Climbing Stairs](https://leetcode.com/problems/climbing-stairs/)
#### Medium
[62. Unique Paths](https://leetcode.com/problems/unique-paths/)

[1155. Number of Dice Rolls With Target Sum](https://leetcode.com/problems/number-of-dice-rolls-with-target-sum/)

[688. Knight Probability in Chessboard](https://leetcode.com/problems/knight-probability-in-chessboard/)

[494. Target Sum](https://leetcode.com/problems/target-sum/)

[377. Combination Sum IV](https://leetcode.com/problems/combination-sum-iv/)

[935. Knight Dialer](https://leetcode.com/problems/knight-dialer/)

[1223. Dice Roll Simulation](https://leetcode.com/problems/dice-roll-simulation/)

[416. Partition Equal Subset Sum](https://leetcode.com/problems/partition-equal-subset-sum/)

[808. Soup Servings](https://leetcode.com/problems/soup-servings/)

[790. Domino and Tromino Tiling](https://leetcode.com/problems/domino-and-tromino-tiling/)

[801. Minimum Swaps To Make Sequences Increasing](https://leetcode.com/problems/minimum-swaps-to-make-sequences-increasing/)

[673. Number of Longest Increasing Subsequence](https://leetcode.com/problems/number-of-longest-increasing-subsequence/)

[63. Unique Paths II](https://leetcode.com/problems/unique-paths-ii/)

[576. Out of Boundary Paths](https://leetcode.com/problems/out-of-boundary-paths/)

#### Hard
[1269. Number of Ways to Stay in the Same Place After Some Steps](https://leetcode.com/problems/number-of-ways-to-stay-in-the-same-place-after-some-steps/)

[1220. Count Vowels Permutation](https://leetcode.com/problems/count-vowels-permutation/)

### Merging Intervals
statement :
>Given a set of numbers find an optimal solution for a problem considering the current number and the best you can get from the left and right sides.

Approach :
>Find all optimal solutions for every interval and return the best possible answer.

```java
// from i to j
dp[i][j] = dp[i][k] + result[k] + dp[k+1][j]
```

Get the best from the left and right sides and add a solution for the current position.

```java
for(int l = 1; l<n; l++) {
   for(int i = 0; i<n-l; i++) {
       int j = i+l;
       for(int k = i; k<j; k++) {
           dp[i][j] = max(dp[i][j], dp[i][k] + result[k] + dp[k+1][j]);
       }
   }
}
return dp[0][n-1]
```

#### Similar Problems:
#### Medium
[1130. Minimum Cost Tree From Leaf Values](https://leetcode.com/problems/minimum-cost-tree-from-leaf-values/)

[96. Unique Binary Search Trees](https://leetcode.com/problems/unique-binary-search-trees/)

[1039. Minimum Score Triangulation of Polygon](https://leetcode.com/problems/minimum-score-triangulation-of-polygon/)

[546. Remove Boxes](https://leetcode.com/problems/remove-boxes/)

[1000. Minimum Cost to Merge Stones](https://leetcode.com/problems/minimum-cost-to-merge-stones/)

[375. Guess Number Higher or Lower II](https://leetcode.com/problems/guess-number-higher-or-lower-ii/)

#### Hard
[312. Burst Balloons](https://leetcode.com/problems/burst-balloons/)

### DP on Strings
General problem statement for this pattern can vary but most of the time you are given two strings where lengths of those strings are not big

statement :
>Given two strings s1 and s2, return some result.

Approach :
>Most of the problems on this pattern requires a solution that can be accepted in O(n^2) complexity.

```java
// from i to j
dp[i][j] = dp[i][k] + result[k] + dp[k+1][j]
```

Get the best from the left and right sides and add a solution for the current position.

```java
// i - indexing string s1
// j - indexing string s2
for (int i = 1; i <= n; ++i) {
   for (int j = 1; j <= m; ++j) {
       if (s1[i-1] == s2[j-1]) {
           dp[i][j] = /*code*/;
       } else {
           dp[i][j] = /*code*/;
       }
   }
}
```
If you are given one string s the approach may little vary

```java
for (int l = 1; l < n; ++l) {
   for (int i = 0; i < n-l; ++i) {
       int j = i + l;
       if (s[i] == s[j]) {
           dp[i][j] = /*code*/;
       } else {
           dp[i][j] = /*code*/;
       }
   }
}
```

#### Similar Problems:
#### Medium

[1143. Longest Common Subsequence](https://leetcode.com/problems/longest-common-subsequence/)

[647. Palindromic Substrings](https://leetcode.com/problems/palindromic-substrings/)

[516. Longest Palindromic Subsequence](https://leetcode.com/problems/longest-palindromic-subsequence/)

[1092. Shortest Common Supersequence](https://leetcode.com/problems/shortest-common-supersequence/)

[712. Minimum ASCII Delete Sum for Two Strings](https://leetcode.com/problems/minimum-ascii-delete-sum-for-two-strings/)

[5. Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/)

#### Hard

[72. Edit Distance](https://leetcode.com/problems/edit-distance/)

[115. Distinct Subsequences](https://leetcode.com/problems/distinct-subsequences/)

### Decision Making
The general problem statement for this pattern is forgiven situation decide whether to use or not to use the current state. So, the problem requires you to make a decision at a current state.

statement :
>Given a set of values find an answer with an option to choose or ignore the current value.

Approach :
>If you decide to choose the current value use the previous result where the value was ignored; vice-versa, if you decide to ignore the current value use previous result where value was used.

```java
// i - indexing a set of values
// j - options to ignore j values
for (int i = 1; i < n; ++i) {
   for (int j = 1; j <= k; ++j) {
       dp[i][j] = max({dp[i][j], dp[i-1][j] + arr[i], dp[i-1][j-1]});
       dp[i][j-1] = max({dp[i][j-1], dp[i-1][j-1] + arr[i], arr[i]});
   }
}
```
#### Similar Problems:
#### Easy
[198. House Robber](https://leetcode.com/problems/house-robber/)

[121. Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)

#### Medium
[714. Best Time to Buy and Sell Stock with Transaction Fee](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/)

[309. Best Time to Buy and Sell Stock with Cooldown](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/)

#### Hard
[123. Best Time to Buy and Sell Stock III](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/)

[188. Best Time to Buy and Sell Stock IV](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv/)
