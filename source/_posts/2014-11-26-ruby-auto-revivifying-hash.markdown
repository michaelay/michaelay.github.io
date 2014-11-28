---
layout: post
title:  "Ruby auto revivifying hash" 
date:   2014-11-26 16:34:56
categories: ruby
---
Hash auto revivification allows you to create content on the fly when accessing undefined hash element. 
Comes in handy when you need to build a nested hash

{% highlight ruby %}
hash = Hash.new{ |h,k| h[k] = Hash.new(&h.default_proc) }
hash['a']['b'] = 1
hash['a']['c'] = 1
hash['b']['c'] = 1
puts hash.inspect
# "{"a"=>{"b"=>1, "c"=>1}, "b"=>{"c"=>1}}"
{% endhighlight %}
