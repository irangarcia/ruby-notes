# Methods

## Creating a method

```ruby

def my_name
  "Joe Smith"
end

puts my_name # => "Joe Smith"
```

## Naming methods

```ruby
method_name # valid
_name_of_method # valid
1 _method_name # invalid
method_27 # valid
method? _name # invalid
method_name! # valid
begin
  # invalid (Ruby reserved word)
  begin_count # valid
```

## Args and params

```ruby

def greet(name)
  "Hello, " + name
end

puts greet("Iran") # => Hello, Iran

# Default params
def greet(name = "stranger")
  "Hello, " + name
end

puts greet("Iran") # => Hello, Iran
puts greet # => Hello, stranger
```
