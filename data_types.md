# Basic data types

## Strings

### Concatenation

```ruby
# Plus operator
"Welcome " + "to " + "Iran!" # => "Welcome to Iran!"

# Shovel operator
"Welcome " << "to " << "Iran!" # => "Welcome to Iran!" 

# Concat method
"Welcome ".concat("to ").concat("Iran!") # => "Welcome to Iran!"
```

### Substrings

```ruby
"hello"[0] # => "h"

"hello"[0..1] # => "he"

"hello"[0, 4] # => "hell"

"hello"[-1] # => "o"
```

### Escape characters

```ruby
"\\" # => Need a backslash in your string?
"\b" # => Backspace
"\r" # => Carriage return, for those of you that love typewriters
"\n" # => Newline. You'll likely use this one the most.
"\s" # => Space
"\t" # => Tab
```

### Interpolation

```ruby 
name = "Iran"

# Must be double quote
"Hello, #{name}" # => "Hello, Iran"

# Does not work
'Hello, #{name}' # => "Hello, #{name}"
```

### Converting other objects to string

```ruby 
5.to_s       # => "5"

nil.to_s     # => ""

:symbol.to_s # => "symbol"
```

### Methods

```ruby 
# .capitalize 
"hello".capitalize      # => "Hello"

# .include?
"hello".include?("lo")  # => true 
"hello".include?("z")   # => false 

# .upcase
"hello".upcase          # => "HELLO"

# .downcase
"HELLO".downcase        # => "hello" 

# .empty?
"hello".empty?          # => false 
"".empty?               # => true

# .length
"hello".length          # => 5

# .reverse
"hello".reverse         # => "olleh"

# .split
"hello world".split     # => ["hello", "world"]
"hello".split("")       # => ["h", "e", "l", "l", "o"]

# .strip 
"hello, world  ".strip  # => "hello, world"

# others
"he77o".sub("7", "l")   # => "hel7o"

"h3y".gsub("3", "e")    # => "hey"

"hey".insert(-1, "man") # => "heyman"

"hello".delete("l")     # => "heo"

"!".prepend("hello")    # => "hello!"
```

---

## Numbers

### Operations

```ruby
# Addition
1 + 1 # => 2

# Subtraction 
2 - 1 # => 1

# Multiplication 
2 * 2 # => 4

# Division
10 / 5 # => 2

# Exponent
2 ** 2 # => 4
3 ** 4 # => 81

## Modulus (remainder of division)
8 % 2 # => 0 (8  / 2 = 4; no remainder)
10 % 4 # => 2 (10 / 4 = 2; with a remainder of 2) 
```

### Integers and Floats

```ruby
17 / 5 # => 3, not 3.4
17 / 5.0 # => 3.4
```

- #### Converting number types

```ruby
# Convert an integer to a float
13.to_f # => 13.0

# Convert a float to an integer
13.0.to_i # => 13
13.9.to_i # => 13
```

### Methods

```ruby
# .even?
6.even? # => true
7.even? # => false

# .odd?
6.odd? # => false
7.odd? # => true
```

--- 

## Symbols

- Strings can be changed, so every time a string is used, Ruby has to
  store it in memory even if an existing string with the same value already
  exists. Symbols, on the other hand, are stored in memory only once,
  making them faster in certain situations. One common application where
  symbols are preferred over strings are the keys in hashes.

### Creating a symbol

```ruby
# Simply put a colon at the beginning of any text
:my_symbol
:"surprisingly, this is also a symbol"
```

### Symbols vs Strings

```ruby
"string" == "string" # => true 

"string".object_id == "string".object_id # => false

:symbol.object_id == :symbol.object_id # => true
```

---

## Booleans

- `true`
- `false`
- `nil`