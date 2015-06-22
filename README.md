# Enumerators

## Objectives

1. Become familiar with some enumerators
2. Get comfortable reading the official Ruby documentation on enumerators
3. Understand the difference between `.each` and `.collect`

## Introduction

[Enumerators](http://ruby-doc.org/core-2.1.3/Enumerable.html) allows for iterative actions on data structures, specifically in Ruby arrays and hashes.

Enumerator methods allow us to iterate over every member of a collection and *do something to each* member of that collection. 

### Why do we need Enumerators?

Let's revisit our earlier example of Professor Snape's list of Hogwarts students. Professor Snape is having a bad day and he'd like to vent some of that frustration by turning each of his students into a frog. He therefore needs to preform a certain action on each student. 

Let's take a look at our student array: 

`students = ["Harry Potter", "Ron Weasley", "Hermione Granger", "Draco Malfroy"]`

Snape has written a method (okay, spell), that he needs to call on each student: `turn_into_frog`. 

```ruby
def turn_into_frog(person)
  puts "Poof! #{person} is a frog."
end
```

Without enumerators, he'd have to do something like this: 

```ruby
turn_into_frog(students[0]) 
turn_into_frog(students[1])
turn_into_frog(students[2])
...
```

This approach has a number of serious drawbacks: 

* We are repeating ourselves on every line. 
* We need to know exactly how many students are in the array in order to operate on each one––and this could change!
* What if we have a long list of students? Maybe Snape had a *really* bad day and he wants to turn everyone in Hogwarts into a frog? It would take forever. 

Let's take a look at the same task using an enumerator:

```ruby
students.each do |student|
  turn_into_frog(student)
end
```

This would successfully output: 

```ruby
"Poof! Harry Potter is a frog."
"Poof! Ron Weasley is a frog."
"Poof! Hermione Granger is a frog."
...
```

We went from many lines of code requiring us to grab each student one at a time, to just a few lines of code using our `.each` enumerator. Much better. 

There are many enumerators available to you in Ruby, below are just a few. Read more about them in the official Ruby documenation. 


## `.each`

`.each` is a common enumerator method. The defining characteristic of it is that its return value is the original data structure it was called on. Whatever is happening within the block will be evaluated as well.

Here's how `.each` works:

```ruby
cool_nums = [1, 2, 3]

def change_nums(nums)
  nums.each do |x|
    puts x + 1
  end
end

change_nums(cool_nums)
2
3
4
#=> [1, 2, 3]
```

You can see that we are moving over every element in the array and executing the code in the `do`, `end` block for each element. That is exactly how enumerators work––we call them on a collection (i.e. `array.each`), pass that method call a block (i.e. code in between the `do` and the `end`), and that code runs for every element in the collection. 

## `.collect`/`.map`

`.collect` and `.map` are identical in functionality, and are similar to to `.each` with one distinct difference: when you call `.collect` or `.map` on an array or hash a new array or hash object is returned, **not** the original one.

Let's take a look:

```ruby
cool_nums = [1, 2, 3]

def change_nums(nums)
  nums.collect do |x| 
    x + 1
  end
end

change_nums(cool_nums)
#=> [2, 3, 4]
```

However, the original array does not change:

```ruby 
cool_nums
#=> [1, 2, 3]
```

## `.each` vs. `.collect`

While the two are similar, there are times when it makes sense to use one over the other. If you need the return value of your method to be a collection that's been modified by what's happening within the block, then `.collect` is for you. Of course, it's quite possible to work with `.each` to accomplish that. One way is to make a new "placeholder" (array or hash) in memory and scope of the method, and then return that new placeholder as the last line of the method:

```ruby
cool_nums = [1, 2, 3]

def change_nums(nums)
  new_count = []
  nums.each do |x|
    x += 1
    new_count << x
  end
  new_count
end

change_nums(cool_nums)
#=> [2, 3, 4]
```

But doesn't this code smell a little bit? It's a lot of lines to accomplish something that `.collect` does itself.

## `.select`

`.select` returns all items in a collection (as a new collection object, like `.collect`) for which the block is true:

```ruby
cool_nums = [1, 2, 3]

def even_nums(nums)
  nums.select do |x|
    x.even?
  end
end

even_nums(cool_nums)
#=> [2]
```

Take a look at the [Enumerable Module](http://ruby-doc.org/core-2.1.3/Enumerable.html) and read about the different methods available.

## `.find`

`.find` is very similar to `.select`, but instead of collecting and returning all of the items for which a condition is true, it returns the *first* item for which it is true.

```ruby
[1, 3, 5, 7].find do |num|
  num.odd?
end
  => 1
```

## `.delete_if`

`.delete_if`, on the other hand, will delete from the collection any items that return true for a certain condition:

```ruby
[1, 2, 4, 7].delete_if do |num|
  num.odd?
end

  => [2, 4]
``` 
## `include?`

You can use the `include?` method to determine if a collection contains a certain item. 

```ruby
[1, 2, 3].include?(1)
  => true
```

## Helpful Tools

As you move forward through this unit, you'll be required to use the above enumerable methods to complete labs and get rspec tests passing. Rely on the Ruby docs on Enumerators, linked to below, to help you. You can also use resources like Stack Overflow and good old fashioned googling to gain deeper understandings of how these methods work. Learning when and what to google is a valuable skill in programming, don't be afraid to use it. 

Let's use an example. Say you are completing a lab that asks you to build a method that takes in an array as an argument and return the *first* item in the array that meets a certain condition. "Oh no!" you might think (having forgotten to refer back to this excellent Readme). But don't worry––a google query along the lines of "ruby method to return first item of collection that meets condition" is very likey to point you in the right direction. 

## Resources 

[Enumerators](http://ruby-doc.org/core-2.1.3/Enumerable.html)
