# Hashes

## Creating hashes
```ruby
# Keys and values are associated with a
# special operator called hash rocket
my_hash = {
  "a random word" => "ahoy",
  "iran's math test score" => 0,
  "an array" => [1, 3, 5, 7],
  "an empty hash within a hash" => {}
}

# Just like with an array, you can call
# the `Hash` class
my_hash = Hash.new
```

## Accessing values
```ruby
shoes = {
  "summer" => "sandals",
  "winter" => "boots"
}

shoes["summer"] # => "sandals" 
shoes["hiking"] # => nil

# `fetch` method
shoes.fetch("hiking")  # => KeyError: key not found: "hiking"

# Alternatively, this method can return
# a default value instead of raising an 
# error if the given key is not found.
shoes.fetch("hiking", "hiking boots") # => "hiking boots"
```

## Adding and Changing data
```ruby
shoes["fall"] = "sneakers" 
shoes # => {"summer"=>"sandals", "winter"=>"boots", "fall"=>"sneakers"}

# Also can change an existing key
shoes["summer"] = "whatever I want"
shoes # => {"summer"=>"whatever I want", "winter"=>"boots", "fall"=>"sneakers"}
```

## Removing data
```ruby
shoes.delete("summer") # => "whatever I want"
shoes                  # => {"winter"=>"boots", "fall"=>"sneakers"}
```

## Accessing keys and values
```ruby
books = { 
  "Infinite Jest" => "David Foster Wallace", 
  "Into the Wild" => "Jon Krakauer" 
}

books.keys   # => ["Infinite Jest", "Into the Wild"]
books.values # => ["David Foster Wallace", "Jon Krakauer"]
```

## Merging two hashes
```ruby
hash_one = { "a" => 1, "b" => 2 }
hash_two = { "b" => 3, "c" => 4 }

hash_one.merge(hash_two) # => { "a" => 1, "b" => 3, "c" => 4}
```

## Symbols as hash keys
```ruby
# 'Rocket' syntax 
american_cars = { 
  :chevrolet => "Corvette", 
  :ford => "Mustang", 
  :dodge => "Ram" 
}

# 'Symbols' syntax
japanese_cars = { 
  honda: "Accord", 
  toyota: "Corolla", 
  nissan: "Altima" 
}

american_cars[:ford]    #=> "Mustang"
japanese_cars[:honda]   #=> "Accord"

japanese_cars.fetch
```