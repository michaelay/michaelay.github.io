---
layout: post
title: "user-defined metadata in rspec"
date: 2014-12-05 13:47:09 -0800
comments: true
categories: [ruby, rspec]
---

Rspec `describe`, `context` and `it` supports metadata in the form of a hash. Syntax as follow: 
```ruby
RSpec.describe "some description", :foo => 1, :bar do 

	context "when some condition", :value => true do 
	
		it "does something", :hihi, :day => 10 do |example| 
			expect(exapmle.metadata[:foo]).to eq(1) 
			expect(example.metadata[:value]).to be true
			expect(example.metadata[:hihi]).to be true 
			expect(example.metadata[:day]).to eq(10) 
		end 
	
	end 
	
end
```
There are 2 ways that I use metadata in RSpec. 
### To include shared_examples / shared_context 
RSpec includes shared_context and shared_examples with same metadata
```ruby 
RSpec.shared_context "shared stuff", :a => :b do 
	def shared_method 
		pp "hello" 
	end 
end 
```
```ruby
Rspec.describe "use shared stuff", :a => :b do 
end 
```
is equivalent to 
```ruby
Rspec.describe "use shared stuff" do 
	include_context "shared_stuff" 
end 
```
### Use metadata as variables 
```ruby 
RSpec.describe "use metadata as var", :num_elements => 7 do 

	let(:elements) do |example|
		(1..example.metadata[:num_elements]).map { |n| "element#{n}" }
	end 
	
	it "prints elements" do 
		pp elements 
	end 

end 
```
