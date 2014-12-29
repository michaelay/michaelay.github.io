---
layout: post
title: "Java object creation" 
date: 2014-12-22 10:09:21 -0800
comments: true
categories: java
---

*Work in progress* 

Notes from reading "Effective Java" 

### Static factory method 
* advantages
	* with names 
	* not required to create new object when invoked
	* can return object of any subtype of its return type
* disadvantages 
	* classes without public or protected constructors cannot be subclassed 

```java
public class Foo { 
	private Foo() {} 
	public static Foo getInstance() {
		//...
	}
	public static Foo valueOf(bool value) {
		//... 
	}  
} 
```
### Builder 
Used when there are many constructor parameters 

```java
public class Foo {
	private final int required1; 
	private final int required2;
	private final int optional1; 
	private final int optional2;
	
	public static class Builder {
		// required 
		private final int required1; 
		private final int required2;
		// optional 
		private final int optional1; 
		private final int optional2;
		
		public Builder(int required1, int required2) { 
			this.required1 = required1; 
			this.required2 = required2; 
		}
		
		public Builder required1(int val) { 
			required1 = val; 
			return this; 
		}
		public Builder required2(int val) { 
			required2 = val; 
			return this; 
		}
		public Builder optional1(int val) { 
			optiona1 = val; 
			return this; 
		}    
		public Builder optional2(int val) { 
			optiona2 = val; 
			return this; 
		}    
		
		public Foo build() { 
			return new Foo(this); 
		} 
	} 
	
	private Foo(Builder builder) { 
		required1 = builder.required1 
		required2 = builder.required2 
		optional1 = builder.optional1
		optional2 = builder.optional2 
	} 
}

// usage example 
Foo fooInstance = new Foo.Builder(10, 10).optional1(100).optional2(200).build(); 

// build should throw IllegalStateException if parameters violate rules 

// method that uses Builder 
// assume Builder is defined as: 
 
public interface Builder<T> { 
	public T build(); 
} 

Tree nodeMethod(Builder<? extends Node> nodeBuilder) {
	//...
} 
```
advantages: 

* no long, unnamed list of parameters 
* can fill up optional values 
* 
disadvantages: 

* speed
