Greedy Algorithms
Introduction
A greedy algorithm makes the best possible choice at each step,
with the goal of finding the best overall solution.

1. Lemonade Change
2. Assign Cookies

1. Lemonade Change
Problem
Observation
Each lemonade costs $5. Customers pay using $5, $10, or $20 bills.
For each customer, we must give the correct change.

The goal is to determine whether we can serve every customer
in the given order.

Approach
I keep track of how many $5 and $10 bills I have.
- If the customer gives $5, we keep the bill.
- If the customer gives $10, we need to give one $5 as change.
- If the customer gives $20, we need $15 as change.

For a $20 bill, I first try to give one $10 and one $5.
If that is not possible, we try to give three $5 bills.

Greedy Choice
For a $20 bill, we prefer:
$10 + $5

instead of:
$5 + $5 + $5

This is because $5 bills are more useful for giving change
to future customers who pay with $10.

Why It Works
At every step, we make the choice that preserves the most
useful bills for future customers. Therefore, if we cannot
give change at some point, it is impossible to serve all
customers.

Complexity
Time Complexity: O(n)
Space Complexity: O(1)

----------------------------------------------

2. Assign Cookies

Problem
Observation
Each child has a greed factor, which represents the minimum
cookie size needed to make that child happy.
Each cookie has a size. A cookie can be given to only one child.

The goal is to maximize the number of happy children.

Approach
First, we sort both the greed factors and cookie sizes.
Then we start with the least greedy child and the smallest cookie.
If the cookie is large enough to satisfy the child, we give it
to that child and move to the next child.
If the cookie is too small, we skip it and try the next larger
cookie.

Greedy Choice
we always give the smallest cookie that can satisfy the current
child.
This prevents larger cookies from being wasted on children
who could be satisfied with smaller cookies.

Why It Works
By satisfying the least greedy child with the smallest possible
cookie, larger cookies remain available for children with higher
greed factors.

This allows us to maximize the number of satisfied children.

Complexity
Time Complexity: O(n log n + m log m)
Space Complexity: O(1) extra space apart from sorting.

----------------------------------------

Conclusion
Both problems demonstrate the greedy strategy of making a
locally optimal choice at each step.

In Lemonade Change, we preserve useful $5 bills.

In Assign Cookies, we use the smallest sufficient cookie.

These local choices help us obtain the globally optimal solution.
