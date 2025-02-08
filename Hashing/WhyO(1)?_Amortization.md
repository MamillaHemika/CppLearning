**Concept of Amortization**

Amortization in computer science is a technique used to analyze the average time complexity of an algorithm over a sequence of operations rather than a single operation. This approach is particularly useful when an algorithm may occasionally perform expensive operations, but these operations happen infrequently relative to cheaper operations.

**Intuition Behind Amortization**

When we say that a certain operation has an average time complexity of ( O(1) ) (constant time), we mean that while there might be specific scenarios that take ( O(n) ) time, these scenarios are rare. The average time taken per operation over a long series of operations will still be constant.

**Example: Dynamic Array**

Let’s illustrate the concept of amortization using a dynamic array, such as std::vector in C++.

**Scenario with Dynamic Arrays**

1. **Insertion Scenario**: When you insert an element into a dynamic array:
    - If the array has enough capacity (more space than current size), the insertion takes ( O(1) ) time.
    - If the array has reached its capacity, it needs to be resized:
        - A new array is created, typically double the size of the previous one.
        - All the existing elements need to be copied into the new array, which takes ( O(n) ) time.

**Cost Analysis without Amortization**

- Assume you perform ( n ) insertions.
- If every insertion were ( O(1) ) except for the resizing operations, it would make the total time complexity:
  - ( O(n) ) for insertions where no resizing occurs.
  - Plus ( O(n) ) for copying in all the resizing operations.

This naive consideration might suggest that the insertion operation has an average complexity of ( O(n) ), which is misleading.

**Amortized Analysis**

- Let's analyze this with the idea of amortization:
  - For the first insertion, time = ( O(1) )
  - For the second insertion, time = ( O(1) )
  - For the third insertion, time = ( O(1) )
  - ...
  - As soon as you need to resize the array (say, after inserting the capacity-fill threshold), you perform one costly operation that takes ( O(n) ).

However, the key insight is that when you double the size of your array, you are not just doing it for one insertion; you are preparing for many future insertions.

Here’s a clearer breakdown:

- Assume your initial capacity is 1.
- Let’s say you insert 8 elements:
  - Insertion 1, no resizing needed ( \\rightarrow O(1) )
  - Insertion 2, resizing needed: ( O(1 + 1) )
  - Insertion 3, resizing needed: ( O(1 + 2) )
  - Insertion 4, resizing needed: ( O(1 + 4) )
  - ...

Over every series of insertions, every time a resizing operation occurs, it serves a broader range of subsequent operations. In fact, if you count up the costs of all these resizing operations over a total of insertions, you can observe:

1. Each element can be inserted in ( O(1) ) operations until resizing is necessary.
2. The total cost of resizing is distributed among all insertions, leading to an average:  
    \[  
    \\text{Amortized Time for Each Insertion} = \\frac{\\text{Total Insertions}}{\\text{Number of Operations}} \\longrightarrow O(1)  
    \]

**Result**

Thus, on average:

- Each insertion operation is ( O(1) ), even accounting for the rare ( O(n) ) time taken for resizing, because the cost of resizing is spread over many insertions. In summary, although there are some insertions that take longer (in case of resizing), the average time taken per operation across all insertions is constant.

**Conclusion**

Amortized analysis effectively captures the cost of infrequent, expensive operations by distributing their cost over numerous cheap operations. It provides a realistic assessment of an algorithm's performance in practical scenarios, making sure you recognize that while worst-case performance might imply higher costs, the average cost remains manageable through amortization.

Let’s clarify what it means to "spread the cost over many insertions" with a more detailed example that highlights how amortized analysis works, focusing on why we can say that insertions in a dynamic array have an average time complexity of ( O(1) ) even when resizing costs ( O(n) ) occasionally.

**Concept of Cost Spreading**

When we say that the cost of resizing is "spread over many insertions," we mean that while resizing operations (costing ( O(n) ) time) do occur, they are infrequent relative to the number of normal insertions (which take ( O(1) ) time). Thus, the "cost" of those infrequent costly operations can be averaged out over many cheap operations.

**Example Walkthrough**

Let’s say we start with a dynamic array that doubles its capacity whenever it runs out of space. Here’s the breakdown of the costs in a step-by-step format:

1. **Initial Setup**:
    - Let’s say the dynamic array starts with a capacity of 1.
    - When we insert the first element, it goes smoothly since there’s space.

**Insertions with Costs**

| **Insert #** | **Action** | **Cost** | **Cumulative Cost** |
| --- | --- | --- | --- |
| 1   | Add element 1 | ( O(1) ) | ( O(1) ) |
| 2   | Need to resize (capacity 1 to 2) + Add 2 | ( O(1) + O(1) ) = ( O(2) ) | ( O(3) ) |
| 3   | Add element 3 | ( O(1) ) | ( O(4) ) |
| 4   | Need to resize (capacity 2 to 4) + Add 4 | ( O(1) + O(2) ) = ( O(3) ) | ( O(7) ) |
| 5   | Add element 5 | ( O(1) ) | ( O(8) ) |
| 6   | Add element 6 | ( O(1) ) | ( O(9) ) |
| 7   | Add element 7 | ( O(1) ) | ( O(10) ) |
| 8   | Add element 8 | ( O(1) ) | ( O(11) ) |
| 9   | Need to resize (capacity 4 to 8) + Add 9 | ( O(1) + O(4) ) = ( O(5) ) | ( O(16) ) |
| 10  | Add element 10 | ( O(1) ) | ( O(17) ) |

**Total Cost of Insertions**

Now let’s summarize the total costs:

- Total cost of all insertions: ( O(1) + O(2) + O(1) + O(3) + O(1) + O(1) + O(1) + O(1) + O(5) + O(1) = O(17) )
- Number of insertions = 10

**Average (Amortized) Time per Insertion**

To find the **amortized time** per insertion:

\[  
\\text{Amortized Time for Each Insertion} = \\frac{\\text{Total Cost}}{\\text{Number of Insertions}} = \\frac{O(17)}{10} = O(1.7)  
\]

In big-O notation, we drop the constant factors, so we can simplify this result to ( O(1) ).

**Key Insight**

While operations 2, 4, and 9 involve resizing and are more computationally expensive, they happen infrequently compared to the total number of insertions. As the number of insertions grows, the impact of these costlier operations becomes smaller when averaged over the numerous cheap operations.

**Conclusion**

- When we say the cost is "spread over many insertions," we mean that the high cost of occasional resizing is effectively borne by many low-cost insertions. Thus, even though a few operations take longer, the average across all operations still leads to a time complexity of ( O(1) ).

In terms of practical understanding:

- If you insert many elements into a dynamic array, most of the time, you’re simply doing a cheap insertion. The rare, costly resizing operations are outweighed when calculating the average time for all insertions, meaning that for every individual insertion you perform, you can consider it to be efficient at ( O(1) ).
