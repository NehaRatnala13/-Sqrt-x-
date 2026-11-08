# LeetCode 69: Sqrt(x)

## Problem Description

Given a non-negative integer `x`, return the square root of `x` rounded down to the nearest integer. The returned integer should be non-negative as well.

You **must not use** any built-in exponent function or operator, such as `pow(x, 0.5)` or `x ** 0.5` in Python.

### Examples

**Example 1:**
```text
Input: x = 4
Output: 2
Explanation: The square root of 4 is 2, so we return 2.
```

**Example 2:**
```text
Input: x = 8
Output: 2
Explanation: The square root of 8 is 2.82842..., and since we round it down to the nearest integer, 2 is returned.
```

### Constraints
* `0 <= x <= 2^31 - 1`

---

## Python Solution

```python
class Solution:
    def mySqrt(self, x: int) -> int:
        if x < 2:
            return x
        
        left, right = 2, x // 2
        
        while left <= right:
            mid = (left + right) // 2
            num = mid * mid
            
            if num == x:
                return mid
            elif num > x:
                right = mid - 1
            else:
                left = mid + 1
                
        return right
```

---

## Algorithmic Explanation

The solution uses **Binary Search** to find the integer square root efficiently. 

1. **Base Cases:** For `x < 2`, the square root is always `x` itself (0 → 0, 1 → 1).
2. **Search Space Optimization:** For x ≥ 4, the square root of x is always less than or equal to x // 2. This allows us to set our initial search space bounds to `left = 2` and `right = x // 2`.
3. **Binary Search Loop:** 
   * Calculate the midpoint (`mid`).
   * Square the midpoint (`num = mid * mid`).
   * If `num == x`, we found the exact square root and return `mid`.
   * If `num > x`, the value is too large, so we narrow the search space to the left half (`right = mid - 1`).
   * If `num < x`, the value is too small, so we move to the right half (`left = mid + 1`).
4. **Rounding Down:** If the loop ends without finding an exact match, `right` will point to the largest integer whose square is less than `x`, which perfectly satisfies the requirement to round down.

---

## Complexity Analysis

* **Time Complexity:** **\(\mathcal{O}(\log x)\)** 
  The search space is halved in every iteration of the binary search loop, leading to a logarithmic runtime.
* **Space Complexity:** **\(\mathcal{O}(1)\)**
  The algorithm uses only a constant amount of extra space for pointers (`left`, `right`, `mid`, `num`).

---

## How to Test

You can run this solution locally by creating a main block execution:

```python
if __name__ == "__main__":
    sol = Solution()
    
    # Test cases
    test_cases = [4, 8, 0, 1, 16, 2147483647]
    
    for case in test_cases:
        print(f"Input: {case} -> Output: {sol.mySqrt(case)}")
```
