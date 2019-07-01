---
layout: post
title: Quick Sort
description: "" 
tags: [Algorithm]
categories: [TIL]
---

In the quick sort algorithm, ```partition``` method is the main concept.

## **Time Complexity**
*Note: N is the size of input*

Quicksort is a popular sorting algorithm with O(N * logN) best and average-case , and O(N^2) worst case performance.

## **Implementation**

```ruby
class Array
    attr_accessor :array

    def initialize(array)
        @array = array
    end

    def quick_sort(p=0, r=array.size-1)
        if p < r
            q = partition(p, r)
            quick_sort(p, q-1)
            quick_sort(q+1, r)
        end
    end

    private
        def partition(p, r)
            x = array[r]
            i = p - 1
            (p..r-1).each do |j|
                if array[j] <= x
                    i += 1
                    array[i], array[j] = array[j], array[i]
                end
            end
            array[i+1], array[r] = array[r], array[i+1]
            return i + 1
        end
end

array = Array.new([5, 1, 10, 2])
array.quick_sort
p array.array # => [1, 2, 5, 10]
```

## **Merge Sort vs Quick Sort**
- Quick sort is significantly faster in practice.
- Quick sort has very low memory requirement.
- Quick sort divides sub-problems in vary
- Merge sort divides sub-problems in half