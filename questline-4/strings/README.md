String Algorithms
This task focuses on solving string-based programming challenges using efficient string processing techniques.

1. Valid Palindrome

Problem
Determine whether a string is a palindrome after ignoring non-alphanumeric characters and differences in uppercase and lowercase.

Approach
We use the two-pointer approach. One pointer starts from the beginning and another from the end. Non-alphanumeric characters are skipped, and the remaining characters are compared after converting them to lowercase.

Algorithm
1. Initialize two pointers at the beginning and end of the string.
2. Skip non-alphanumeric characters from both sides.
3. Convert both characters to lowercase and compare them.
4. If they are different, return false.
5. Move the pointers toward the center.
6. If no mismatch is found, return true.

Edge Cases
- Empty string
- Single character
- String containing only spaces or punctuation
- Uppercase and lowercase characters
- Strings containing numbers

Complexity
- Time Complexity: O(n)
- Space Complexity: O(1)

-----------------------------------------------------------------------------------------------------------------

2. Zigzag Conversion

Problem
Convert a string into a zigzag pattern across a given number of rows and then read the characters row by row.

Approach
I simulated the zigzag movement using a separate string for each row. The direction changes whenever the top or bottom row is reached.

Algorithm
1. Create a string for each row.
2. Start from the first row.
3. Add each character to the current row.
4. Move downward until the bottom row is reached.
5. Change direction and move upward.
6. Continue until all characters are placed.
7. Combine all rows to obtain the final result.

Edge Cases
- Number of rows is 1
- Number of rows is greater than or equal to the string length
- Very short strings
- Direction changes at the first and last rows

Complexity
- Time Complexity: O(n)
- Space Complexity: O(n)
