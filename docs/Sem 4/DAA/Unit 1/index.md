# Unit 1
## Question 1 i) Discuss concisely the concepts of Big Oh Notation, Omega Notation, and Theta Notation, which are forms of asymptotic notation used to describe the time complexity of algorithms. Provide an example illustrating each notation. ii) Employ the most suitable notation to signify the time efficiency class of the sequential search algorithm concerning its worst case, best case, and average case scenarios.

### i) Asymptotic Notations: Big O, Omega, and Theta

Asymptotic notations are mathematical tools used to describe the time complexity of algorithms. They provide a way to express the growth rate of an algorithm's running time as the input size increases. The three most common asymptotic notations are Big O, Omega (Ω), and Theta (Θ).

#### Big O Notation (O)
- **Definition**: Big O notation provides an upper bound on the running time of an algorithm. It describes the worst-case scenario, indicating the maximum time an algorithm can take relative to the input size \(n\).
- **Mathematical Representation**: \( T(n) = O(f(n)) \) if there exist constants \( c > 0 \) and \( n_0 \) such that \( T(n) \leq c \cdot f(n) \) for all \( n \geq n_0 \).
- **Example**: For an algorithm with a running time of \( T(n) = 3n^2 + 2n + 1 \), the Big O notation is \( O(n^2) \). This means the running time grows quadratically as the input size increases.

#### Omega Notation (Ω)
- **Definition**: Omega notation provides a lower bound on the running time of an algorithm. It describes the best-case scenario, indicating the minimum time an algorithm can take relative to the input size \(n\).
- **Mathematical Representation**: \( T(n) = \Omega(f(n)) \) if there exist constants \( c > 0 \) and \( n_0 \) such that \( T(n) \geq c \cdot f(n) \) for all \( n \geq n_0 \).
- **Example**: For the same algorithm with a running time of \( T(n) = 3n^2 + 2n + 1 \), the Omega notation is \( \Omega(n^2) \). This means the running time grows at least quadratically as the input size increases.

#### Theta Notation (Θ)
- **Definition**: Theta notation provides a tight bound on the running time of an algorithm. It describes both the upper and lower bounds, indicating that the algorithm's running time grows asymptotically as \( f(n) \).
- **Mathematical Representation**: \( T(n) = \Theta(f(n)) \) if there exist constants \( c_1, c_2 > 0 \) and \( n_0 \) such that \( c_1 \cdot f(n) \leq T(n) \leq c_2 \cdot f(n) \) for all \( n \geq n_0 \).
- **Example**: For the same algorithm with a running time of \( T(n) = 3n^2 + 2n + 1 \), the Theta notation is \( \Theta(n^2) \). This means the running time grows quadratically, which is a tight bound.

### ii) Time Efficiency of Sequential Search Algorithm

The sequential search algorithm, also known as linear search, checks each element of a list one by one until the target element is found or the list ends. The time complexity varies based on the scenario:

#### Worst Case
- **Scenario**: The target element is not present in the list.
- **Time Complexity**: In this case, the algorithm needs to check all \( n \) elements.
- **Notation**: \( O(n) \)
- **Explanation**: The running time grows linearly with the number of elements because each element is checked once.

#### Best Case
- **Scenario**: The target element is the first element in the list.
- **Time Complexity**: Only one comparison is needed.
- **Notation**: \( \Omega(1) \)
- **Explanation**: The running time is constant because the element is found immediately.

#### Average Case
- **Scenario**: The target element is somewhere in the list, assumed to be uniformly distributed.
- **Time Complexity**: On average, the algorithm will need to check half of the elements.
- **Notation**: \( \Theta(n) \)
- **Explanation**: The average number of comparisons is \(\frac{n}{2}\), which grows linearly with the number of elements.

---
## Question 2 Interpret the general plan for mathematical analysis of both recursive and non-recursive relations. Additionally, State an algorithm for computing the factorial of a given number and analyze its efficiency

### General Plan for Mathematical Analysis of Algorithms

The mathematical analysis of algorithms involves understanding their behavior in terms of running time and space as the input size increases. This analysis is done separately for recursive and non-recursive algorithms due to their differing structures.

#### Non-Recursive Algorithms
1. **Identify the Basic Operation**: Determine the operation that significantly contributes to the running time (e.g., comparisons in sorting).
2. **Determine the Input Size**: Identify a parameter \( n \) that characterizes the size of the input.
3. **Analyze the Worst, Average, and Best Cases**: Establish how the basic operation count changes with varying inputs.
4. **Set Up a Summation**: Formulate a summation that represents the total number of basic operations.
5. **Simplify the Summation**: Use mathematical techniques to simplify the summation to its asymptotic form.

#### Recursive Algorithms
1. **Identify the Basic Operation**: Determine the operation that significantly contributes to the running time.
2. **Determine the Input Size**: Identify a parameter \( n \) that characterizes the size of the input.
3. **Analyze the Worst, Average, and Best Cases**: Establish how the basic operation count changes with varying inputs.
4. **Set Up a Recurrence Relation**: Formulate a recurrence relation that describes the algorithm’s behavior.
5. **Solve the Recurrence Relation**: Solve the recurrence to obtain a closed form or an asymptotic estimate.

### Algorithm for Computing Factorial

#### Algorithm (Iterative Approach)
```python
def factorial_iterative(n):
    result = 1
    for i in range(2, n + 1):
        result *= i
    return result
```

#### Algorithm (Recursive Approach)
```python
def factorial_recursive(n):
    if n == 0 or n == 1:
        return 1
    else:
        return n * factorial_recursive(n - 1)
```

### Efficiency Analysis

#### Iterative Factorial
- **Basic Operation**: Multiplication
- **Input Size**: \( n \)
- **Worst, Average, Best Cases**: All cases are the same as the number of iterations is fixed and depends on \( n \).
- **Summation**: The loop runs \( n - 1 \) times, each time performing a multiplication.
- **Time Complexity**: 
  - Each multiplication takes constant time \( O(1) \).
  - Total time complexity is \( O(n) \).

#### Recursive Factorial
- **Basic Operation**: Multiplication
- **Input Size**: \( n \)
- **Worst, Average, Best Cases**: All cases are the same as the depth of recursion depends on \( n \).
- **Recurrence Relation**: 
  - \( T(n) = T(n-1) + O(1) \)
  - Base case: \( T(0) = O(1) \)
- **Solution**: 
  - Expanding the recurrence: \( T(n) = T(n-1) + O(1) = T(n-2) + O(1) + O(1) = ... = T(1) + (n-1)O(1) = O(n) \)
  - Time Complexity: \( O(n) \)

### Conclusion
Both the iterative and recursive algorithms for computing the factorial of a number have a time complexity of \( O(n) \). The iterative approach may be slightly more efficient in practice due to the overhead of recursive function calls. However, both approaches are linear in terms of time complexity.

## Question 3 IMPORTANT PROBLEM TYPES
- Sorting
- Searching
- String processing
- Graph problems
- Combinatorial problems
- Geometric problems
- Numerical problems
