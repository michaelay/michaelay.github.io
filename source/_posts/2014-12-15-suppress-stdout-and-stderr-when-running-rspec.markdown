---
layout: post
title: "suppress stdout and stderr when running RSpec"
date: 2014-12-15 13:45:19 -0800
comments: true
categories: ["ruby", "rspec"]
---

Sometimes code prints to stdout, stderr. Corresponding RSpec examples print the same output, which could be messy. To suppress the output: 

```ruby
def silence
	# Store the original stderr and stdout in order to restore them later
	@original_stderr = $stderr
	@original_stdout = $stdout

	# Redirect stderr and stdout
	$stderr = File.new("/dev/null", 'w')
	$stdout = File.new("/dev/null", 'w')

	yield

	$stderr = @original_stderr
	$stdout = @original_stdout
	@original_stderr = nil
	@original_stdout = nil
end
    
it "suppresses output" do 
	silence do 
		# whatever code to test 
	end 
end 
``` 
