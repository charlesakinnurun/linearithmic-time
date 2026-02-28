<!-- # Linearithmic-Time

**Explanation of Linearithmic Time Complexity (O(n log n))**

This repository provides examples and explanations related to **linearithmic time complexity**, often written as **O(n log n)** — a time complexity that combines both linear and logarithmic growth.

---

## 📊 What Is Linearithmic Time (O(n log n))?

In algorithm analysis, **linearithmic time complexity** occurs when an algorithm’s running time increases in proportion to the product of the input size (`n`) and the logarithm of the input size (`log n`). Algorithms with this complexity are more efficient than many naive approaches (like O(n²)) but are slower than purely linear algorithms (O(n)).

This complexity often appears in **divide-and-conquer** algorithms: the input is repeatedly divided into smaller parts (giving the `log n` factor) and then processed in linear time at each level of division.



---

## 📌 Common Examples of O(n log n) Algorithms

Here are some popular algorithms with linearithmic time complexity:

- **Merge Sort:** An efficient sorting algorithm that divides an array into halves, sorts them recursively, and then merges them. 
- **Heap Sort:** A comparison-based sort using a heap data structure. 
- **Quick Sort (average case):** A divide-and-conquer sort that usually runs in O(n log n).
- **Certain geometric and data structure operations:** Some optimized algorithms for convex hulls or balanced trees also run in linearithmic time.

---

## 📁 Source Code
```python
import time
import random 
import math


"""
LINEARITHMIC TIME COMPLEXITY: O(n log n)

What is it?
Linearithmic time is a combination of Linear time O(n) and Logarithmic time O(log n).
It is commonly found in "divide and conquer" algorithms like Merge Sort, Heap Sort, 
and Quick Sort (on average).

Why does it happen?
1. Divide: The problem is split into two halves repeatedly (the 'log n' part).
2. Combine: At each level of the split, we perform a linear scan to merge or 
   process the elements (the 'n' part).
"""

def merge_sort(arr):
    """
    Classic O(n log n) implementation.
    The list is halved until it reaches single elements (log n steps).
    The elements are then merged back together using a linear comparison (n steps).
    """

    if len(arr) <= 1:
        return arr

    # ----- The "log n" part: Dividing the data
    mid = len(arr) // 2
    left_half = merge_sort(arr[:mid])
    right_half = merge_sort(arr[mid:])

    return merge(left_half,right_half)


def merge(left,right):
    """
    The 'n' part: Merging two sorted lists requires looking at 
    every element once.
    """
    result = []
    i = j = 0

    while i < len(left) and j < len(right):
        if left[i] < right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1


    # Append any remaining elements
    result.extend(left[i:])
    result.extend(right[j:])
    return result




def simulate_growth():
    """
    Displays how O(n log n) scales compared to other complexities.
    """
    print(f"{'Input Size (n)':<15} | {'Linear (n)':<15} | {'Linearithmic (n log n)':<25} | {'Quadratic (n²)':<15}")
    print("-" * 80)

    sizes = [10,100,1000,10000]

    for n in sizes:
        linear = n
        # math.log2(n) represents the number of times we can halve n
        linearithmic = n * math.log2(n)
        quadratic = n**2

        print(f"{n:<15} | {linear:<15} | {linearithmic:<25.2f} | {quadratic:<15}")




def main():
    print ("----- Linearithmic Time Complexity O(n log n) -----")

    # 1. Real World Example
    test_data = [random.randint(1,100) for _ in range (10)]
    print(f"Original Data: {test_data}")
    sorted_data = merge_sort(test_data)
    print(f"Sorted Data: {sorted_data}")

    # 2. Performance Comparison
    print("Growth Comparison Table")
    simulate_growth()

    print("\nObservation:")
    print("Notice how n log n stays much closer to Linear than Quadratic.")
    print("When n=10,000:")
    print("- n² is 100,000,000 operations.")
    print("- n log n is only ~132,877 operations.")
    print("This makes O(n log n) the gold standard for general-purpose sorting.")

if __name__ == "__main__":
    main()
```
---

## 🔍 Why It Matters

O(n log n) algorithms are considered **efficient for large inputs** and are common in important algorithmic tasks like sorting and processing large datasets. They strike a balance between scalability and complexity — faster than quadratic or worse time complexities but not as fast as linear time algorithms.


--> 



<!-- # 📘 Linearithmic Time – README -->

<h1 align="center">Linearithmic Time</h2>

## Overview

**Linearithmic Time** refers to an algorithm whose runtime grows proportional to n × log n.

It combines aspects of linear time (O(n))** and **logarithmic time (O(log n)), and is often seen in divide-and-conquer algorithms.

In algorithm analysis, it is represented as:

```
O(n log n)
```

Linearithmic time is efficient and widely used for sorting and other scalable operations.

<a href="/src/main.py">Check out for source code</a>

---

## ⚙️ What Linearithmic Time Means

An algorithm runs in linearithmic time when it:

* Processes every element (linear part)
* Repeatedly divides the problem (logarithmic part)

This commonly occurs in sorting and merging operations:

* Merge Sort
* Heap Sort
* Quick Sort (average case)
* Certain divide-and-conquer algorithms

For n elements, the runtime is roughly proportional to n × log₂(n).

---

## 🧠 Python Examples

### Example 1 — Merge Sort

```python id="lnlog_merge1"
def merge_sort(arr):
    if len(arr) <= 1:
        return arr

    mid = len(arr) // 2
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])

    return merge(left, right)

def merge(left, right):
    result = []
    i = j = 0
    while i < len(left) and j < len(right):
        if left[i] < right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1
    result.extend(left[i:])
    result.extend(right[j:])
    return result

numbers = [38, 27, 43, 3, 9, 82, 10]
print(merge_sort(numbers))  # Output: [3, 9, 10, 27, 38, 43, 82]
```

Merge Sort divides the array and merges → **O(n log n)**.

---

### Example 2 — Heap Sort

```python id="lnlog_heap2"
def heapify(arr, n, i):
    largest = i
    left = 2*i + 1
    right = 2*i + 2

    if left < n and arr[left] > arr[largest]:
        largest = left
    if right < n and arr[right] > arr[largest]:
        largest = right

    if largest != i:
        arr[i], arr[largest] = arr[largest], arr[i]
        heapify(arr, n, largest)

def heap_sort(arr):
    n = len(arr)
    for i in range(n//2 - 1, -1, -1):
        heapify(arr, n, i)
    for i in range(n-1, 0, -1):
        arr[i], arr[0] = arr[0], arr[i]
        heapify(arr, i, 0)
    return arr

numbers = [4, 10, 3, 5, 1]
print(heap_sort(numbers))  # Output: [1, 3, 4, 5, 10]
```

Heap construction and extraction → **O(n log n)**.

---

### Example 3 — Quick Sort (Average Case)

```python id="lnlog_quick3"
def quick_sort(arr):
    if len(arr) <= 1:
        return arr
    pivot = arr[len(arr)//2]
    left = [x for x in arr if x < pivot]
    middle = [x for x in arr if x == pivot]
    right = [x for x in arr if x > pivot]
    return quick_sort(left) + middle + quick_sort(right)

numbers = [3, 6, 8, 10, 1, 2, 1]
print(quick_sort(numbers))  # Output: [1, 1, 2, 3, 6, 8, 10]
```

Divide-and-conquer approach → **O(n log n)** average case.

---

## ⏱️ Time Complexity Comparison

| Complexity     | Meaning           |
| -------------- | ----------------- |
| O(1)           | Constant time     |
| O(log n)       | Logarithmic time  |
| O(n)           | Linear time       |
| **O(n log n)** | Linearithmic time |
| O(n²)          | Quadratic time    |

Linearithmic time scales efficiently for large datasets.

---

## 👍 Advantages

* Efficient for sorting and divide-and-conquer algorithms
* Scales well for large datasets
* Predictable runtime
* Often the best practical choice for comparison-based sorting

## 👎 Disadvantages

* More complex than linear or quadratic algorithms
* Not suitable for extremely small datasets (simpler sorts may be faster)
* Recursive calls can add overhead

---

## 📌 When Linearithmic Time Occurs

Linearithmic time operations appear when:

* Sorting using Merge Sort, Heap Sort, or Quick Sort
* Divide-and-conquer algorithms that process all elements at each level
* Efficient aggregation or merging of datasets

---

## 🏁 Summary

Linearithmic time complexity **O(n log n)** is common in efficient sorting and divide-and-conquer algorithms.
It balances the growth of input size with repeated problem division, making it highly scalable and practical for large datasets.
