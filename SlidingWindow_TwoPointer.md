# Sliding Window

The Sliding Window pattern is used to perform a required operation on a specific window size of a given array or linked list, such as finding the longest subarray containing all 1s. Sliding Windows start from the 1st element and keep shifting right by one element and adjust the length of the window according to the problem that you are solving. In some cases, the window size remains constant and in other cases the sizes grows or shrinks.

Sliding Window Questions fall under the following categories:

>+ [Sliding Window of constant window size](#sliding-window-of-constant-window-size) 
>+ [Sliding Window in which window size increases depending on the constraints](#sliding-window-in-which-window-size-increases-depending-on-the-constraints)
>+ [Sliding window in which sliding window length will expand and then shrink](#sliding-window-in-which-sliding-window-length-will-expand-and-then-shrink)

## Sliding Window of constant window size

As stated, the window size will remain constant. Two pointers are maintained to store the index of the start and end of the sliding window. In each step, both pointers, lets say left and right, will be incremented by 1.

![SlidingWindow](./SlidingWindow/SlidingWindow.png)

Small code snippet of the sliding window concept:

```python
    # Create an Sliding Window of Size len(p) 
    for ch in s[:len(p)]:
        s_list[dictionary[ch]] += 1
    
    if s_list == p_list:
        result.append(0)
    
    # For each step 
    for i, ch in enumerate(s[len(p):]):
        # Remove the starting element from the window
        s_list[dictionary[s[i]]] -= 1
        # Add the new element, Window size remains constant
        s_list[dictionary[ch]] += 1
        if s_list == p_list:
            result.append(i+1)
    return result
```

Some problems on Leetcode that can be solved using this concept:

### Medium Level

1. [438. Find All Anagrams in a String](https://leetcode.com/problems/find-all-anagrams-in-a-string/)
2. [567. Permutation in String](https://leetcode.com/problems/permutation-in-string/)
3. [1052. Grumpy Bookstore Owner](https://leetcode.com/problems/grumpy-bookstore-owner/)
4. [1423. Maximum Points You Can Obtain from Cards](https://leetcode.com/problems/maximum-points-you-can-obtain-from-cards/)
5. [1456. Maximum Number of Vowels in a Substring of Given Length](https://leetcode.com/problems/maximum-number-of-vowels-in-a-substring-of-given-length/)

### Hard Level

1. [239. Sliding Window Maximum](https://leetcode.com/problems/sliding-window-maximum/)
2. [480. Sliding Window Median](https://leetcode.com/problems/sliding-window-median/)
3. [995. Minimum Number of K Consecutive Bit Flips](https://leetcode.com/problems/minimum-number-of-k-consecutive-bit-flips/)


## Sliding Window in which window size increases depending on the constraints

In this type of questions, maximum or longest subarray that satisfies the desired constraint needs to be found. 

Standard template for this type of questions:

One thing needs to be mentioned is that when asked to find maximum substring, we should update maximum after the inner while loop to guarantee that the substring is valid. On the other hand, when asked to find minimum substring, we should update minimum inside the inner while loop.

```c++
int lengthOfLongestSubstring(string s) {
        vector<int> map(128,0);
        int counter = 0, begin = 0, end = 0, d = 0; 
        while(end < s.size()){
            if(map[s[end++]]++ > 0)
                counter++; 
            while(counter > 0)
                if(map[s[begin++]]-- > 1)
                    counter--;
            d = max(d, end-begin); //while valid, update d
        }
        return d;
    }
```

Some problems on leetcode that can be solved using this concept:

### Medium Level

1. [3. Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)
2. [424. Longest Repeating Character Replacement](https://leetcode.com/problems/longest-substring-without-repeating-characters/)
3. [978. Longest Turbulent Subarray](https://leetcode.com/problems/longest-turbulent-subarray/)
4. [1004. Max Consecutive Ones III](https://leetcode.com/problems/max-consecutive-ones-iii/)
5. [1208. Get Equal Substrings Within Budget](https://leetcode.com/problems/get-equal-substrings-within-budget/)

## Sliding window in which sliding window length will expand and then shrink

This is by far the toughest concept in the sliding window, In this type the window size can either grow or shrink. As mentioned in the above code snippet, Increasing the size of the window can be done in the outer while loop and shrinking the size of the window can be in the inner while loop, depending on the constraints.

Some problems on leetcode that can be solved using this concept:

### Medium Level

1. [713. Subarray Product Less Than K](https://leetcode.com/problems/subarray-product-less-than-k/)
2. [795. Number of Subarrays with Bounded Maximum
](https://leetcode.com/problems/number-of-subarrays-with-bounded-maximum/)
3. [1438. Longest Continuous Subarray With Absolute Diff Less Than or Equal to Limit](https://leetcode.com/problems/longest-continuous-subarray-with-absolute-diff-less-than-or-equal-to-limit/)

### Hard Level
1. [76. Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/) Must solve Question ** 
