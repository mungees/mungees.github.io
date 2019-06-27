---
layout: post
title: Introduction to heaps
description: "" 
tags: [Algorithm]
categories: [TIL]
---

You should choose a data structure depending on what operations you want. In this post, I would like to introduce a heap data structure. For operations such as insert, find or delete min, heap is the first option that you should consider. The following table shows that how efficient the heap is compare to other data structures.

|                      | insert        | search   | find min | delete min|
|----------------      |:-------------:|:--------:|:--------:|:---------:|
| unsorted array       | O(1)          | O(n)     | O(n)     | O(n)      |
| sorted array         | O(n)          | O(logn)  | O(1)     | O(1)      |
| unsorted linked list | O(1)          | O(n)     | O(n)     | O(n)      |
| min heap             | O(logn)       | O(n)     | O(1)     | O(logn)   |

Heap is an almost complete binary tree which means that if all leaves present in one level then they should be filled from left to right. So the previous level should be completely filled first before going to the next level.

*Side Note:*  
Given n elements, if the list is already sorted either a max or min heap, you should not sort it to make a heap.
The reason is that it takes O(n * logn). If your purpose is just to construct a heap, there is a algorithm which takes only O(n).

### **Height & Nodes**
In a complete binary tree, the relation between the height and the number of nodes is following:

| H    | 1    | 2    | 3     | 4     |
|:----:|:----:|:----:|:-----:|:-----:|
| Max  | 3    | 7    | 15    | 31    |

*Note that **H** represents the height of a tree and **Max** represents the number of maximum nodes relative to the height of the tree.*

Therefore, Max = (2^(h+1) - 1) and H = floor(log n).

### **Implementation**
The index of leaves starts from floor(n/2) + 1 to n and you can say that every leaf is a heap.

```ruby
def max_heapify(array, i)
  l = (2*i)
  r = (2*i)+1

  # we should subtract since given array includes 'nil' at position 0
  heap_size = array.size - 1

  # l <= heap_size condition ensures that the left child exists
  if l <= heap_size && array[l] > array[i]
    largest = l
  else
    largest = i
  end

  # r <= heap_size condition ensures that the right child exists
  if r <= heap_size && array[r] > array[largest]
    largest = r
  end

  # if root is the largest then no need to exchange
  if largest != i
    array[i], array[largest] = array[largest], array[i]
    max_heapify(array, largest)
  end
end
```

The time and space complexity is both O(log N).

```ruby
def build_max_heap(array)
  # array.size / 2 => last index of non-leaf
  # leaf starts at the index of floor(array.size / 2) + 1
  (array.size/2..1).each do |i|
    max_heapify(array, i)
  end
end
```

The time complexity is O(n) and the space complexity is O(log n).

```ruby
array = [nil, 5, 10, 1, 20, 3, 11, 100]
p build_max_heap(array) # => [nil, 100, 20, 11, 10, 3, 5, 1]
```

```ruby
def extract_max(array)
  # base case
  if array.size <= 1
    return
  end

  # last element becomes the root then
  # max heapify with array which the last element is already removed
  max = array[1]
  A[1] = array[-1]
  max_heapify(array[0..array.size-1], 1) # => takes O(log n)

  return max
end
```

In ```extract_max``` function, it takes constant time until ```max_heapify``` is called. We have already seen that ```max_heapify``` takes the O(h) which is the height of the tree and therefore O(log n). The space complexity is also O(log n).

```ruby
def increase_key(array, i, key)
  if key < array[i]
    return
  end
  
  array[i] = key

  # i > 1 condition ensures not to go beyond the root
  # if the parent is less than the child then exchange
  while i > 1 && array[i/2] < array[i]
    array[i], array[i/2] = array[i/2], array[i]
    i = i/2
  end
end
```

The main operation occurs in while loop. The worst case happens when it starts from the deepest leaf and to the root. Then, it takes O(log n). The space complexity requires O(1) since it does not have a recursion.

## **Conclusion**
Heap is optimized for the operations below:

|          | Find max | Delete max | Insert key | Increase key | Decrease key |
|:----:    |:----:    |:----:      |:-----:     |:-----:       |:----:        |
| Max Heap | O(1)     | O(log n)   | O(log n)   | O(log n)     | O(log n)     |

We should consider a better data structures if these operations are required below:

|          | Find min | Search | Delete |
|:-----:   |:----:    |:----:  |:----:  |
| Max Heap | O(n)     | O(n)   | O(n)   |

## References
- [Introduction to heaps](https://www.youtube.com/watch?v=40iljMQmqmY&list=PLEbnTDJUr_IeHYw_sfBOJ6gk5pie0yP-0&index=11)
- [Max heapify algorithm and complete binary tree](https://www.youtube.com/watch?v=2fA1FdxNqiE&index=12&list=PLEbnTDJUr_IeHYw_sfBOJ6gk5pie0yP-0)
- [Build max heap algorithm and analysis](https://www.youtube.com/watch?v=HI97KDV23Ig&index=13&list=PLEbnTDJUr_IeHYw_sfBOJ6gk5pie0yP-0)
- [Extract max, increase key and insert key into heap](https://www.youtube.com/watch?v=j5ij59EjPh0&t=2s)