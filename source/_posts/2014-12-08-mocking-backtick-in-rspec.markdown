---
layout: post
title: "mocking backtick in RSpec"
date: 2014-12-08 10:54:23 -0800
comments: true
categories: [ruby, rspec]
---

\`cmd\` is a method in Kernel. 

However, simply mocking the `Kernel` object does not work. 
This is because `Kernel` is a module included by class `Object`, its methods are available in every Ruby object. 

Instead of doing this: 

```ruby
Kernel.expects(:`).with(
	'unzip -d /tmp test.zip'
)
```

We should be doing this: 

```ruby
instance_of_current_object.expects(:`).with(
	'unzip -d /tmp test.zip'
)
```
