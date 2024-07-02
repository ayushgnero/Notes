# The Role of Algorithms in Computing

What are algorithms? Why is the study of algorithms worthwhile? What is the role of algorithms relative to other technologies used in computing?

## Algorithm

An algorithm is a sequence of computational steps that transform the input to an output or it is a step-by-step procedure for solving a problem.

## Time Complexity

Time Complexity measures the amount of time an algorithm takes to run as a function of the input size.

### Big O Notation

The Big O Notation is used to describe the worst-case scenario for an algorithm's running time.

### How to Calculate Time Complexity

1. **Identify the Basic Operation:** Identify the fundamental operation that dominates the execution time of the algorithm. This could be:
   - Assignments
   - Comparisons
   - Arithmetic Operations
   - Loop Iterations
   - Function Calls

2. **Analyze Loop Structures:** 

    - **Single Loops:** For a loop that runs `n` times, the time complexity is `O(n)`.

    ```python
    for i in range(n):
        # Constant time operation
    ```

    - **Nested Loops:** For nested loops, multiply the time complexity of each loop.

    ```python
    for i in range(n):
        for j in range(n):
            # Constant time operation
    # Time complexity is O(n*n) = O(n^2)
    ```

    - **Consecutive Statements:** Add the time complexities of consecutive statements. However, in Big O notation, we drop the lower-order terms.

    ```python
    for i in range(n):      # O(n)
        # Constant time operation
    for j in range(m):      # O(m)
        # Constant time operation
    # Overall time complexity is O(n) + O(m) = O(n + m)
    ```
    If `n` and `m` are of the same order, we simplify to `O(n)`.

    - **Analyze Conditional Statements:** For conditional statements, take the time complexity of the branch with the highest complexity.

    ```python
    if condition:
        # O(n)
    else:
        # O(1)
    # Time Complexity is O(n)
    ```

3. **Recursive Algorithms:** For recursive algorithms, use the recurrence relation to express the time complexity.

    **Example:** Binary Search

    ```python
    def binary_search(arr, target):
        if len(arr) == 0:
            return False
        mid = len(arr) // 2
        if arr[mid] == target:
            return True
        elif arr[mid] < target:
            return binary_search(arr[mid + 1:], target)
        else:
            return binary_search(arr[:mid], target)
    ```
    Binary Search splits the array into two halves each time. The recurrence relation is:
    $$
    T(n) = T(n/2) + O(1)
    $$
    Solving this recurrence gives:
    $$
    T(n) = O(\log n)
    $$

    **Example:** Merge Sort

    ```python
    def merge_sort(arr):
        if len(arr) <= 1:
            return arr
        mid = len(arr) // 2
        left = merge_sort(arr[:mid])
        right = merge_sort(arr[mid:])
        return merge(left, right)
    ```
    Merge sort divides the array into two halves and then merges them. The recurrence relation is:
    $$
    T(n) = 2T(n/2) + O(n)
    $$
    Solving this recurrence gives:
    $$
    T(n) = O(n \log n)
    $$

4. **Use the Master Theorem for Recurrence Relations:** The Master Theorem provides a shortcut for solving recurrences of the form:
    $$
    T(n) = aT(n/b) + f(n)
    $$
    Where:
    - $a$ is the number of subproblems in the recursion.
    - $n/b$ is the size of each subproblem.
    - $f(n)$ is the cost outside the recursive calls.

    Three cases for the Master Theorem:
    1. If $f(n) = O(n^c)$ and $c < \log_{b}a$, then $T(n) = O(n^{\log_{b}a})$.
    2. If $f(n) = O(n^{\log_{b}a})$, then $T(n) = O(n^{\log_{b}a} \log n)$.
    3. If $f(n) = O(n^c)$ and $c > \log_{b}a$, then $T(n) = O(f(n))$.
