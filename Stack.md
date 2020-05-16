# STACK

Stacks are dynamic data structures that follow the Last In First Out (LIFO) principle. The last item to be inserted into a stack is the first one to be deleted from it.

Only 2 Supported Operations :

1. Push
2. Pop

Problems in stack can be categorized into :

1. [Basic Stack Operations Problems](#basic-stack-operations-problems)
2. [Monotonous Stack Problems](#monotonous-stack)

## Basic Stack Operations Problems

The key things to focus while solving problems on stack is :

1. What should be pushed to stack
2. When should the elements of stack be popped

For Example:

[20.Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)

We push Whenever an opening brace  ```'{', '(', '['```  is encountered and pop when closing brace is encountered  ```'}', ')', ']'```

[394. Decode String](https://leetcode.com/problems/decode-string/)

In this problem, we push an element when an opening brace ```'['``` is encountered. Pop the element off the stack when a closing brace ``` ']' ``` is encountered. After popping an element off the stack, we perform an operation on the popped element and add it to the element at the top of the stack.

Small code snippet of the operations performed:

```python
        for ch in s:
            if ch.isdigit():
              num += ch
            elif ch == '[':
                stack.append(["", int(num)])
                num = ""
            elif ch == ']':
                st, k = stack.pop()
                stack[-1][0] += st*k
            else:
                stack[-1][0] += ch
```

### List of Problems that fall into this Category

#### Easy

1. [20. Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)
2. [155. Min Stack](https://leetcode.com/problems/min-stack/)

#### Medium

1. [394. Decode String](https://leetcode.com/problems/decode-string/)
2. [636. Exclusive Time of Functions](https://leetcode.com/problems/exclusive-time-of-functions/)
3. [735. Asteroid Collision](https://leetcode.com/problems/asteroid-collision/)
4. [856. Score of Parentheses](https://leetcode.com/problems/score-of-parentheses/)
5. [895. Maximum Frequency Stack](https://leetcode.com/problems/maximum-frequency-stack/)
6. [921. Minimum Add to Make Parentheses Valid](https://leetcode.com/problems/minimum-add-to-make-parentheses-valid/)
7. [946. Validate Stack Sequences](https://leetcode.com/problems/validate-stack-sequences/)
8. [1081. Smallest Subsequence of Distinct Characters](https://leetcode.com/problems/smallest-subsequence-of-distinct-characters/)
9. [1190. Reverse Substrings Between Each Pair of Parentheses](https://leetcode.com/problems/reverse-substrings-between-each-pair-of-parentheses/)
10. [1249. Minimum Remove to Make Valid Parentheses](https://leetcode.com/problems/minimum-remove-to-make-valid-parentheses/)

#### Hard

1. [224. Basic Calculator](https://leetcode.com/problems/basic-calculator/)
2. [316. Remove Duplicate Letters](https://leetcode.com/problems/remove-duplicate-letters/)
3. [726. Number of Atoms](https://leetcode.com/problems/number-of-atoms/)
4. [772. Basic Calculator III](https://leetcode.com/problems/basic-calculator-iii/)

## Monotonous Stack

If the numbers stored in the stack are either in increasing order or decreasing order then the stack is said to be monotonous stack.

### Monotonous Increasing Stack

For a monotonous increasing stack, we push elements to the stack only if stack is empty or if the top of the stack is less than the current incoming element.

When the incoming element is less than the top of the stack, then we pop out all the elements in the stack which are less than it.

Example : Array = [2,6,9,8,1]

|stack before    | Incoming number   | stack after   |
|-----------|-------|-----------|
|   []      |   2   |   [2]     |
|   [2]     |   6   |   [2,6]   |
|   [2,6]   |   9   |   [2,6,9] |
|   [2,6,9] |   8   |   [2,6,8] |
|   [2,6,8] |   1   |   [1]     |

Common problem use cases that can be solved using Monotonous Increasing Stack are:

>+ Next Smaller Element in an Array
>+ Previous Smaller Element in an Array ( if looped in reverse )

LeetCode problems for practice :

[402. Remove K Digits](https://leetcode.com/problems/remove-k-digits/)

[1063. Number of Valid Subarrays](https://leetcode.com/problems/number-of-valid-subarrays/)

### Monotonous Decreasing Stack

This is exact opposite of Monotonous increasing stack, in here we push elements to the stack only if stack is empty or if the top of the stack is greater than the current incoming element.

When the incoming element is greater than the top of the stack, then we pop out all the elements in the stack which are less than it.

Example : Array = [2,6,3,9,8,1]

|stack before    | Incoming number   | stack after   |
|-----------|-------|-----------|
|   []      |   2   |   [2]     |
|   [2]     |   6   |   [6]     |
|   [6]     |   3   |   [6,3]   |
|   [6,3]   |   9   |   [9]     |
|   [9]     |   8   |   [9,8]   |
|   [9,8]   |   1   |   [9,8,1] |

Common problem use cases that can be solved using Monotonous Increasing Stack are:

>+ Next Larger Element in an Array
>+ Previous Larger Element in an Array ( if looped in reverse )

LeetCode problems for practice :

[739. Daily Temperatures](https://leetcode.com/problems/daily-temperatures/)

[1019. Next Greater Node In Linked List](https://leetcode.com/problems/next-greater-node-in-linked-list/)

Note : Here we talked only about strictly increasing and strictly decreasing sequences. If top of the stack is equal to incoming element, depending on the problem requirement, we decide if we want to keep that element in the stack or pop it.

Observation : From monotonous stacks, we can observe that to find the larger elements we use decreasing stack and viceversa.

### Few more interesting problems on monotonous stack

[32. Longest Valid Parentheses](https://leetcode.com/problems/longest-valid-parentheses/)

[84. Largest Rectangle in Histogram](https://leetcode.com/problems/largest-rectangle-in-histogram/)

[456. 132 Pattern](https://leetcode.com/problems/132-pattern/)

[503. Next Greater Element II](https://leetcode.com/problems/next-greater-element-ii/)

[901. Online Stock Span](https://leetcode.com/problems/online-stock-span/)

[907. Sum of Subarray Minimums](https://leetcode.com/problems/sum-of-subarray-minimums/)

[Questions and Solutions in one place for quick reference](Stack_Questions_and_Solutions.md)
