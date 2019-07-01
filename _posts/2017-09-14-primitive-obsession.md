---
layout: post
title: Primitive Obsession
description: "" 
tags: [ruby on rails]
categories: [TIL]
---

Instead of making a class, defining a primitive field is much simpler. However, if you keep adding fields more and more, eventually, it becomes huge. One way to solve this problem is to replace data value with object.

```ruby
# dollars/cents

[5, 30]
# OR
{
  dollars: 5.
  cents: 30
}
```

```ruby
# Dave with age 30

['Dave', 30]
# OR
{
  name: 'Dave'.
  age: 30
}
```

#### **Replace with an object**
```ruby
class Money
  attr_reader :dollars, :cents

  def from_cents(cents)
    new(cents/100, cents%100)
  end

  def initialize(dollars, cents)
    @dollars, @cents = dollars, cents
  end
end

p Money.new.from_cents(530) #<Money:... @dollars=5, @cents=30>
```
