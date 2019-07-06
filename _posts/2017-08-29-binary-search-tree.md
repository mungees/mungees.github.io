---
layout: post
title: Binary Search Tree
description: "" 
tags: [algorithm]
categories: [TIL]
---

The following is definition of Binary Search Tree(BST) according to [Wikipedia](https://en.wikipedia.org/wiki/Binary_search_tree)

> In computer science, binary search trees (BST), sometimes called ordered or sorted binary trees, are a particular type of container: data structures that store "items" (such as numbers, names etc.) in memory. They allow fast lookup, addition and removal of items, and can be used to implement either dynamic sets of items, or lookup tables that allow finding an item by its key (e.g., finding the phone number of a person by name).

Key features of BST:
- Left sub-tree of a node has a key less than to its parent node's key
- Right sub-tree of a node has a key greater than to its parent node's key

## **Basic Operations**
- Search
- Insert
- Pre-order Traversal
- In-order Traversal
- Post-order Traversal

## **Big-O Complexity**
*Note: N is the number of nodes in the tree*

The time complexity of the BST is generally O(logN) for a balanced tree. But for unbalanced, O(N) because it is basically similar to a linear data structure. 


This website has a great table for comparing complexities. <br/>
[Big-O Algorithm Complexity Cheat Sheet](http://bigocheatsheet.com/)

## **Implementation**

```ruby
=begin
ruby version
=end
class BinarySearchTree
    class Node
        attr_reader :value, :left, :right

        def initialize(value)
            @value = value
            @left  = nil
            @right = nil
        end

        # It skips if the same value is inserted
        def insert(value)
            case value <=> @value
            when 1  # insert to right sub-tree
                @right.nil? ? @right = Node.new(value) : @right.insert(value)
            when -1 # insert to left sub-tree
                @left.nil? ? @left = Node.new(value) : @left.insert(value)
            end
        end
    end

    def initialize(value)
        @root = Node.new(value)
    end

    def print_inorder(node=@root)
        return if node.nil? # base case
    end

    def search(value, node=@root)
        return false if node.nil? # base case
        case node.value <=> value
        when 0  then true
        when -1 then search(value, node.right)
        when 1  then search(value, node.left)
        end
    end
end
```