---
layout: post
title: "mocking backtick in RSpec"
date: 2014-12-08 10:54:23 -0800
comments: true
categories: [ruby, rspec]
---

\`cmd\` is a method in Kernel. 
Simply mock the `Kernel` object. 

```ruby
Kernel.expects( :` ).with( 'unzip -d /tmp test.zip' )
```
