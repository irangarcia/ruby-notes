# Nested collections

## Nested arrays

### Accessing elements

```ruby
teacher_mailboxes = [
  ["Adams", "Baker", "Clark", "Davis"],
  ["Jones", "Lewis", "Lopez", "Moore"],
  ["Perez", "Scott", "Smith", "Young"]
]

# array[x][y] where `x` is the index 
# of the nested element and `y` is
# the index inside of the nested element.
teacher_mailboxes[0][0] # => Adams
teacher_mailboxes[1][0] # => Jones
teacher_mailboxes[2][0] # => Perez

# Acessing an index of a nonexistent nested element
teacher_mailboxes[5][0] # => NoMethodError
teacher_mailboxes.dig(5, 0) # => nil
teacher_mailboxes.dig(0, 5) # => nil
```

## Nested hashes

### Accessing data

```ruby
vehicles = {
  alice: { year: 2019, make: "Toyota", model: "Corolla" },
  blake: { year: 2020, make: "Volkswagen", model: "Beetle" },
  caleb: { year: 2015, make: "Fiat", model: "Palio" }
}

# hash[:x][:y] where `:x` is the key 
# of the hash and `:y` is the key of
# the nested hash
vehicles[:alice][:year] # => 2019 
vehicles[:blake][:make] # => Volkswagen
vehicles[:caleb][:model] # => Palio

# Acessing an index of a nonexistent key
vehicles[:zoe][:year] # => NoMethodError
vehicles.dig(:zoe, :year) # => nil
vehicles.dig(:alice, :color) # => nil
```

