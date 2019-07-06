---
layout: post
title: Insertion Sort
description: "" 
tags: [algorithm]
categories: [TIL]
---

**Insertion Sort** is a simple sorting algorithm. If a large list is given, more advanced sorting algorithms such as quicksort, heapsort, or merge sort are recommended. Therefore, it is used when the list is small and of course it has some advantages.

> - Simple
> - Efficient for small data sets, much like other quadratic sorting algorithms
> - More efficient in practice than most other simple quadratic algorithms such as selection or bubble sort
> - Stable: it does not change the relative order of elements with equal keys
> - In-place: it only requires a constant amount O(1) of additional memory space

## **Implementation**

```ruby
# iterative version
def insertion_sort(array)
    # we can say that one element is already sorted
    # therefore start with index 1
    (j=1..array.size-1).each do |j|
        key = array[j] # temp value
        
        # insert array[j] into sorted sequence of array[0..j-1]
        # i>= 0 ensures that when i becomes -1 then stop the loop and
        # insert the temp key value 
        i = j-1
        while (i >= 0 && array[i] > key)
            array[i+1] = array[i]
            i -= 1
        end
        array[i+1] = key
    end

    return array
end

array = [5, 1, 10, 2]
p insertion_sort(array, array.size) # => [1, 2, 5, 10]
```

## **Complexity**

#### **Time Complexity**
The worst case happens when a given list is reverse sorted then it takes O(n<sup>2</sup>) time and the best case happens when a list is already sorted and takes Ω(n).

#### **Space Complexity**
It is an in-place algorithm so it takes a constant time which is O(1). As you can see above, only three extra variables are used which are key, i, and j.

#### **Reduce complexity**
The time complexity of insertion sort depends on two steps. One is the number of comparisons and the other is the number of movements. If so, can we decrease time complexity by applying a binary search or a linked list? The answer is "NO".

Assume that we have an array A, then we know A[0..j-1] is sorted. So we can find the correct position of A[j] by applying binary search then it searching time is reduced to O(log n). However, inserting at a correct position takes O(n) because if we insert at an index 0 then all elements from 1 have to be re-placed. Therefore, every search and placement are going to take O(n) time and it has to be done by nearly n-1 time so O(n<sup>2</sup>).

If we don't want any movement, a double linked list should be considered. In this case, we can insert an element at correct position directly without affecting position of elements. So it takes O(1) for the movement. However, to find a correct position takes O(n) because it is a linear search. Therefore, it has to be done by nearly n-1 time and takes O(n<sup>2</sup>).

 | Comparison | Movement
:---: | :---: | :---: 
Binary search| O(log n) | O(n)
Double linked list | O(n) | O(1)

