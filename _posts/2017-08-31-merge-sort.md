---
layout: post
title: Merge Sort
description: "" 
tags: [algorithm]
categories: [TIL]
---

**Merge Sort** is a divide and conquer algorithm. It divides an input array in half recursively. 

## **Time Complexity**
Merging n elements take O(N) time so total time complexity takes in time O(N * logN) where N is the size of input.

## **Implementation**

```ruby
def merge_sort(array)
    # base case
    if array.size <= 1
        return array
    end

    # find a mid
    mid = array.size / 2
    
    left  = merge_sort(array[0..mid-1])
    right = merge_sort(array[mid..array.size-1])

    # merging left and right arrays
    return merge(left, right)
end

def merge(left, right)
    array_sorted = []
    
    # compare first elements of each left and right array
    # smaller gets pushed to array_sorted and removed from the array
    while left.any? && right.any?
        if left.first >= right.first
        array_sorted << right.shift
        else
        array_sorted << left.shift
        end
    end

    # add left elements to array_sorted
    return array_sorted + left + right
end

array = [5, 1, 10, 2]
p merge_sort(array) # => [1, 2, 5, 10]
```