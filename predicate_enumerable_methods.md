# Predicate enumerable methods

## The #include? method

```ruby
numbers = [5, 6, 7, 8]

numbers.include?(8) # => true
numbers.include?(1) # => false

friends = ['Sharon', 'Leo', 'Leila', 'Brian']

invited_list = friends.select { |friend| friend != 'Brian' }
invited_list.include?('Brian') # => false
```

## The #any? method

```ruby
numbers = [21, 42, 303, 499, 520, 801]

numbers.any? { |number| number > 500 } # => true

numbers.any? { |number| number < 10 } # => false
```

## The #none? method

```ruby
fruits ['apple', 'banana', 'strawberry', 'pineapple']

fruits.none? { |fruit| fruit.length > 10 } # => true

fruits.none? { |fruit| fruit.length > 6 } # => false


```