---
layout: post
title: Ruby Enumerable Methods
description: "" 
tags: [ruby on rails]
categories: [TIL]
---

Recently, I have realized that there are many powerful enumerable methods in Ruby so I would like to introduce them in this post. I will keep adding contents as I learn more methods. 

## **inject vs each_with_object**

Building a new hash and mapping, you should consider using ```inject``` and ```each_with_object``` methods.

Let's say we would like to return a hash of its correct length with given an array. So for example:
```ruby
hash = ['ben', 'chris', 'mark']
puts get_string_lengths(hash)
# expected {"ben"=>3, "chris"=>5, "mark"=>4}
``` 

All versions below give the same result.
```ruby
# solution 1
def get_string_lengths_v1(strings)
    strings.inject({}) do |hash, string|
        hash[string] = string.length
        hash
    end
end

# solution 2
def get_string_lengths_v2(strings)
    strings.inject({}) do |hash, string|
        hash.merge(string => string.length)
    end
end

# solution 3
def get_string_lengths_v3(strings)
    strings.each_with_object({}) do |string, hash|
        hash[string] = string.length
    end
end

puts get_string_lengths_v1(%w(ben chris mark))
puts get_string_lengths_v2(%w(ben chris mark))
puts get_string_lengths_v3(%w(ben chris mark))
```

For the first solution, ```inject``` requires memoized value for subsequent block calls, so I returned the hash object in the block. I felt it is less convenient so I tried using ```merge``` method in the second solution because it returns a hash. Lastly, I used ```each_with_object``` method and I felt more convenient.

You cannot use immutable objects for ```each_with_object``` method. 
```ruby
(1..5).each_with_object(0) do |item, sum|
  sum += item
end
# => 0 since numbers are immutable
```
In this case, ```inject``` method is used for immutable objects which return a new value.
```ruby
(1..5).inject(:+)
```

