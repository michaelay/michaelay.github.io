---
layout: post
title: "suppress stdout and stderr when running RSpec"
date: 2014-12-15 13:45:19 -0800
comments: true
categories: ["ruby", "rspec"]
---

Sometimes code prints to stdout, stderr. Corresponding RSpec examples print the same output, which could be messy. To suppress the output: 

```ruby
    def perform_sliently
      # Store the original stderr and stdout in order to restore them later
      @original_stderr = $stderr
      @original_stdout = $stdout

      # Redirect stderr and stdout
      target_output_file = "/dev/null"
      $stderr = File.new(target_output_file, 'w')
      $stdout = File.new(target_output_file, 'w')

      yield

      $stderr = @original_stderr
      $stdout = @original_stdout
      @original_stderr = nil
      @original_stdout = nil
    end
    
    it "suppresses output" do 
    	perform_sliently do 
    		# whatever code to test 
    	end 
    end 
``` 
