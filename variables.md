# Variables

## Declaring a Variable
```ruby
# This is how to create a variable:
age = 18 # => 18

# Variable names are reusable, so
# you can assign a new value at any
# point. Naturally, doing so will 
# override the original value
age = 18
age      # => 18
age = 33 
age      # => 33
```

### Some operators
```ruby
# +=
age = 18
age += 4           # => 22

# -=
age = 18
age -= 2           # => 16

# *=
cash = 10
cash *= 2          # => 20

# /=
temperature = 40   
temperature /= 10  # => 4
```

### Variables are references

```ruby
desired_location = "Berlin"
johns_location = desired_location

desired_location        # => "Berlin"
johns_location          # => "Berlin"

# With !
johns_location.upcase!  #=> "BERLIN"

desired_location        #=> "BERLIN"
johns_location          #=> "BERLIN"

# Without !
johns_location.upcase  #=> "BERLIN"

desired_location        #=> "Berlin"
johns_location          #=> "BERLIN"
```