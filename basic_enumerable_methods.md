# Basic enumerable methods

## Using #select and #reject

```ruby
friends = ['Sharon', 'Leo', 'Leila', 'Brian', 'Arun']

friends.select { |friend| friend != 'Brian' } # => ["Sharon", "Leo", "Leila", "Arun"]
# or
friends.reject { |friend| friend == 'Brian' } # => ["Sharon", "Leo", "Leila", "Arun"]
```

## The #each method

```ruby
# Calling an each method on an array will iterate 
# through that array and will yield each element 
# to a code block, where a task can be performed: 
friends = ['Sharon', 'Leo', 'Leila', 'Brian', 'Arun']

friends.each { |friend| puts "Hello, #{friend}" }

# => Hello, Sharon
# => Hello, Leo
# => Hello, Leila
# => Hello, Brian
# => Hello, Arun

# For multiline blocks 
friends.each do |friend|
  puts "Hello #{friend}"
end

# Each also works for hashes
# By default, each iteration will yield both
# key and value individually or together (
# as an array) to the block
my_hash = { "one" => 1, "two" => 2 }

my_hash.each { |key, value| puts "#{key} is #{value}" }
# => one is 1
# => two is 2

my_hash.each { |pair| puts "the pair is #{pair}" }
# => the pair is ["one", 1]
# => the pair is ["two", 2]
```

### Warning! ⚠

- The `#each` method returns the original array or hash regardless of what
  happens inside the code block 👇

```ruby
friends = ['Sharon', 'Leo', 'Leila', 'Brian', 'Arun']

friends.each { |friend| friend.upcase }

# returns:
# => ['Sharon', 'Leo', 'Leila', 'Brian', 'Arun']
```

## The #each_with_index method

```ruby
fruits = ["apple", "banana", "strawberry", "pineapple"]

fruits.each_with_index { |fruit, index| puts fruit if index.even? }

# => apple
# => strawberry
# => ["apple", "banana", "strawberry", "pineapple"]
```

## The #map method (also #collect)

```ruby
friends = ["Sharon", "Leo", "Leila", "Brian", "Arun"]

friends.map { |friend| friend.upcase }
# => ['SHARON', 'LEO', 'LEILA', 'BRIAN', 'ARUN']

salaries = [1200, 1500, 1100, 1800]

salaries.map { |salary| salary - 700 }
# => [500, 800, 400, 1100]
```

## The #select method

```ruby
# Arrays
friends = ["Sharon", "Leo", "Leila", "Brian", "Arun"]

friends.select { |friend| friend != 'Brian' }
# => ["Sharon", "Leo", "Leila", "Arun"]

# Hashes
responses = { 'Sharon' => 'yes', 'Leo' => 'no', 'Leila' => 'no' }

responses.select { |person, response| response == 'yes' }
# => {"Sharon" => "yes"}
```

## The #reduce method

```ruby
my_numbers = [5, 6, 7, 8]

my_numbers.reduce { |sum, number| sum + number }
# => 26
```

## Bang methods

- ☝ We can see that some enumerables like `#map` and `#select` return new arrays but don't modify the arrays that they
  were called on:

```ruby
friends = ['Sharon', 'Leo', 'Leila', 'Brian', 'Arun']

friends.map { |friend| friend.upcase }
# => `['SHARON', 'LEO', 'LEILA', 'BRIAN', 'ARUN']`

friends
# => ['Sharon', 'Leo', 'Leila', 'Brian', 'Arun']
```

- But if we want to modify `friends` array instead, we could use the bang method `#map!`

```ruby
friends = ['Sharon', 'Leo', 'Leila', 'Brian', 'Arun']

friends.map! { |friend| friend.upcase }
# => `['SHARON', 'LEO', 'LEILA', 'BRIAN', 'ARUN']`

friends
# => `['SHARON', 'LEO', 'LEILA', 'BRIAN', 'ARUN']`

```