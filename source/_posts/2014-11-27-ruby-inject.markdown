---
layout: post
title:  "Ruby enumerator inject"
date:   2014-11-27 22:54:56
categories: ruby
---
Loop over enumerator with a seed, takes output from last round as input. 

eg. 

array to hash

{% highlight ruby %}
array = [ 1, 2, 3 ] 
hash = array.inject({}) do |memo, n| 
  memo["key " + n] = "value " + n
end
# hash: { "key 1" => "value 1", "key 2" => "value 2", "key 3" => "value 3" } 
{% endhighlight %}
