---
layout: post
title: Fast Setup Tools for Ruby on Rails
description: "" 
tags: [ruby on rails]
categories: [TIL]
---

In this post, I would like to introduce some ways to set up your own preferences using .rc files. Whenever I create a project, it was really annoying to specify a database type with ```-d``` option (beacuse rails gives SQLite as a default) and etc. So I thought it would be nice if you customize the rails generator.

I did not know the types of ```.rc``` files until I have searched about it and it was interesting. You can try with the following comman:
```
$ ls ~/.*rc
```

## **.irbrc**
In ```rails console```, you can use ```awesome_print``` as a default option.
```ruby
# ~/.irbrc
require "awesome_print"
AwesomePrint.irb!
```

## **.gemrc**
You can skip rdoc and ri generation for the faster installation of gems.
```ruby
# ~/.gemrc
gem: --no-document
```

## **.railsrc**
You can skip Test Unit and add PostgreSQL as the default option.
```ruby
# ~/.railsrc
-d postgresql --skip-test-unit
```
