# Enumerators

[Enumerators](http://ruby-doc.org/core-2.1.3/Enumerable.html) allows for iterative actions on data structures, specifically in Ruby arrays and hashes.

Enumerator methods can be called on hashes and arrays and take blocks as their argument, where the block is yielded to for every item in the array or hash. In other words, when we call:

```ruby
array = [1, 2, 3, 4]
array.each do |num|
  num * 2
end
```

You can imagine it as: 
```array.each(some code that gets executed on each member of the array)```

The **block** is the code between the `do`, `end` syntax. You can also define a block with curly braces, `{}`. We'll be learning more about blocks in a later lesson. 

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

