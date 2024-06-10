# Unit 2
## Question 1 i) Examine the method used for performing the multiplication of two large integers. Examine how the divide and conquer method can be used to solve the same. ii) Observe how the worst-case efficiency of quick sort is reduced using a randomized version of quick sort.

### i) Multiplication of Large Integers and Divide-and-Conquer Approach

#### Traditional Method
The traditional method of multiplying two large integers involves a straightforward algorithm that simulates the paper-and-pencil method:
1. **Align the integers**: Align the digits of the two integers.
2. **Multiply digit by digit**: Multiply each digit of the first integer by each digit of the second integer.
3. **Sum the intermediate results**: Sum up all the intermediate results with appropriate shifts (similar to carrying over in manual multiplication).

For two \( n \)-digit numbers, this approach takes \( O(n^2) \) time due to the nested loops iterating over the digits of both numbers.

#### Divide-and-Conquer Method (Karatsuba Algorithm)
The Karatsuba algorithm is a faster method to multiply two large integers using the divide-and-conquer approach:
1. **Split the numbers**: Split each number into two halves. For example, if \( x \) and \( y \) are the numbers:
   \[
   x = x_1 \cdot 10^{n/2} + x_0 \quad \text{and} \quad y = y_1 \cdot 10^{n/2} + y_0
   \]
2. **Recursively compute three products**:
   \[
   z_0 = x_0 \cdot y_0
   \]
   \[
   z_1 = (x_0 + x_1) \cdot (y_0 + y_1)
   \]
   \[
   z_2 = x_1 \cdot y_1
   \]
3. **Combine the results**:
   \[
   x \cdot y = z_2 \cdot 10^n + (z_1 - z_2 - z_0) \cdot 10^{n/2} + z_0
   \]

**Algorithm**:
```python
def karatsuba(x, y):
    # Base case for recursion
    if x < 10 or y < 10:
        return x * y
    
    # Calculate the size of the numbers
    n = max(len(str(x)), len(str(y)))
    m = n // 2
    
    # Split the digit sequences about the middle
    x1, x0 = divmod(x, 10**m)
    y1, y0 = divmod(y, 10**m)
    
    # 3 recursive calls
    z0 = karatsuba(x0, y0)
    z1 = karatsuba((x0 + x1), (y0 + y1))
    z2 = karatsuba(x1, y1)
    
    return (z2 * 10**(2*m)) + ((z1 - z2 - z0) * 10**m) + z0
```

**Time Complexity**:
- The Karatsuba algorithm reduces the multiplication problem to three multiplications of size \( n/2 \) plus some additional linear work.
- The recurrence relation is:
  \[
  T(n) = 3T(n/2) + O(n)
  \]
- Solving this recurrence using the Master Theorem gives:
  \[
  T(n) = O(n^{\log_2 3}) \approx O(n^{1.585})
  \]
- This is significantly faster than the \( O(n^2) \) time complexity of the traditional method.

### ii) Randomized Quick Sort to Reduce Worst-Case Efficiency

#### Quick Sort Overview
Quick sort is a popular sorting algorithm that uses the divide-and-conquer technique. It works by selecting a 'pivot' element from the array and partitioning the other elements into two sub-arrays, according to whether they are less than or greater than the pivot. The sub-arrays are then sorted recursively.

**Worst-Case Efficiency**:
- The worst-case time complexity of quick sort is \( O(n^2) \). This occurs when the smallest or largest element is always chosen as the pivot, leading to highly unbalanced partitions.

#### Randomized Quick Sort
Randomized quick sort improves the worst-case performance by randomly selecting the pivot element, thus reducing the likelihood of encountering the worst-case scenario.

**Algorithm**:
```python
import random

def randomized_partition(arr, low, high):
    pivot_index = random.randint(low, high)
    arr[pivot_index], arr[high] = arr[high], arr[pivot_index]
    return partition(arr, low, high)

def partition(arr, low, high):
    pivot = arr[high]
    i = low - 1
    for j in range(low, high):
        if arr[j] <= pivot:
            i += 1
            arr[i], arr[j] = arr[j], arr[i]
    arr[i + 1], arr[high] = arr[high], arr[i + 1]
    return i + 1

def randomized_quick_sort(arr, low, high):
    if low < high:
        pi = randomized_partition(arr, low, high)
        randomized_quick_sort(arr, low, pi - 1)
        randomized_quick_sort(arr, pi + 1, high)
```

**Improved Worst-Case Efficiency**:
- By randomly selecting the pivot, the probability of consistently encountering the worst-case scenario is minimized.
- The average-case time complexity of quick sort is \( O(n \log n) \).
- The worst-case time complexity remains \( O(n^2) \), but the randomization significantly reduces the chance of hitting this worst-case in practice.

**Conclusion**:
Randomized quick sort offers a significant improvement in practice over the non-randomized version by ensuring that the pivot selection process is more balanced on average, leading to more efficient sorting in the average case and a much-reduced probability of encountering the worst-case scenario.

## Question 2 Analysis of Quicksort, Randomized Version of Quick sort

### Analysis of Quick Sort and Randomized Quick Sort

#### Quick Sort

**Concept**: Quick Sort is an efficient, in-place, divide-and-conquer sorting algorithm. It works by selecting a 'pivot' element from the array and partitioning the other elements into two sub-arrays, according to whether they are less than or greater than the pivot. The sub-arrays are then sorted recursively.

**Algorithm**:
```python
def quick_sort(arr, low, high):
    if low < high:
        pi = partition(arr, low, high)
        quick_sort(arr, low, pi - 1)
        quick_sort(arr, pi + 1, high)

def partition(arr, low, high):
    pivot = arr[high]
    i = low - 1
    for j in range(low, high):
        if arr[j] <= pivot:
            i += 1
            arr[i], arr[j] = arr[j], arr[i]
    arr[i + 1], arr[high] = arr[high], arr[i + 1]
    return i + 1
```

**Time Complexity**:
- **Best Case**: \( O(n \log n) \)
  - Occurs when the pivot divides the array into two nearly equal halves consistently.
- **Average Case**: \( O(n \log n) \)
  - On average, quick sort performs well due to balanced partitions.
- **Worst Case**: \( O(n^2) \)
  - Occurs when the smallest or largest element is consistently chosen as the pivot, resulting in highly unbalanced partitions (e.g., an already sorted array).

**Space Complexity**:
- **In-place**: Quick sort is an in-place sorting algorithm, meaning it requires a small, constant amount of extra space for the stack frames in the recursion.
- **Auxiliary Space**: \( O(\log n) \) for the best and average cases due to recursion stack depth; \( O(n) \) for the worst case.

**Limitations**:
- Highly sensitive to pivot selection. Poor pivot choices can degrade performance significantly.
- Performance can be poor for already sorted arrays if not implemented with safeguards like randomized pivot selection.

#### Randomized Quick Sort

**Concept**: Randomized Quick Sort improves the worst-case performance by randomly selecting the pivot element, thus reducing the likelihood of encountering the worst-case scenario where the pivot is consistently the smallest or largest element.

**Algorithm**:
```python
import random

def randomized_quick_sort(arr, low, high):
    if low < high:
        pi = randomized_partition(arr, low, high)
        randomized_quick_sort(arr, low, pi - 1)
        randomized_quick_sort(arr, pi + 1, high)

def randomized_partition(arr, low, high):
    pivot_index = random.randint(low, high)
    arr[pivot_index], arr[high] = arr[high], arr[pivot_index]
    return partition(arr, low, high)

def partition(arr, low, high):
    pivot = arr[high]
    i = low - 1
    for j in range(low, high):
        if arr[j] <= pivot:
            i += 1
            arr[i], arr[j] = arr[j], arr[i]
    arr[i + 1], arr[high] = arr[high], arr[i + 1]
    return i + 1
```

**Time Complexity**:
- **Best Case**: \( O(n \log n) \)
  - Like the regular quick sort, occurs when partitions are balanced.
- **Average Case**: \( O(n \log n) \)
  - Due to the random pivot selection, the likelihood of balanced partitions increases, leading to good average-case performance.
- **Worst Case**: \( O(n^2) \)
  - The worst-case remains \( O(n^2) \), but the probability of hitting this case is significantly reduced due to the randomization.

**Space Complexity**:
- **In-place**: Like the regular quick sort, it uses \( O(\log n) \) auxiliary space on average for the recursion stack.
- **Auxiliary Space**: Reduced risk of deep recursion, thus maintaining \( O(\log n) \) space complexity on average.

**Advantages**:
- **Reduced Worst-Case Probability**: By randomizing the pivot selection, the chance of consistently picking poor pivots (leading to unbalanced partitions) is minimized.
- **Robust Performance**: The randomized quick sort performs well on average and reduces the risk of degraded performance on already sorted or nearly sorted arrays.

**Disadvantages**:
- **Random Number Generator Overhead**: There is a slight overhead due to the use of a random number generator.
- **Still Susceptible to Worst Case**: Though the probability is low, the worst-case time complexity remains \( O(n^2) \).

### Conclusion

**Quick Sort**:
- Excellent average-case performance with \( O(n \log n) \) time complexity.
- In-place sorting, making it memory efficient.
- Susceptible to \( O(n^2) \) worst-case performance without precautions.

**Randomized Quick Sort**:
- Maintains the average-case \( O(n \log n) \) time complexity.
- Significantly reduces the likelihood of \( O(n^2) \) worst-case scenarios.
- Adds a slight overhead due to random pivot selection but provides more robust performance across various input cases.

Randomized quick sort is often preferred in practice due to its improved performance stability and reduced risk of hitting the worst-case time complexity.