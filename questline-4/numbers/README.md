Number Algorithms
This task focuses on solving number-based programming problems using mathematical reasoning and algorithms.

1. Palindrome Number
Problem
Given an integer `x`, determine whether it reads the same forward and backward.

Approach
We reverse the digits of the number and compare the reversed number with the original number.

Algorithm
1. If `x` is negative, return `false`.
2. Store the original value of `x`.
3. Extract the last digit using `x % 10`.
4. Add the digit to the reversed number.
5. Remove the last digit using `x / 10`.
6. Repeat until `x` becomes 0.
7. Compare the original number with the reversed number.
8. If both are equal, return `true`; otherwise return `false`.

Complexity
- Time Complexity: `O(log n)`
- Space Complexity: `O(1)`

Alternative Approach
The number can also be converted into a string and compared with its reverse. I used the mathematical approach because it works directly with the digits and uses constant extra space.

--------------------------------------------------------------------------------------------------

2. Integer to Roman

Problem
Convert an integer into its Roman numeral representation.

Approach
We store Roman numeral values in descending order and repeatedly choose the largest possible value.

Algorithm
1. Store the Roman numeral values and their corresponding symbols.
2. Start from the largest value.
3. If the current value is less than or equal to `num`, subtract it from `num`.
4. Add its corresponding Roman symbol to the result.
5. Repeat while the value can still be subtracted.
6. Continue with the next smaller value.
7. Return the final Roman numeral string.

Complexity
- Time Complexity: `O(1)`
- Space Complexity: `O(1)`

Alternative Approach
The problem can also be solved using multiple `if-else` statements for different ranges of numbers. I used arrays of values and symbols because the solution is shorter, cleaner, and easier to maintain.
