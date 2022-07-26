# Blocks

A block can be declared as a single line or multiline block. Ruby convention is to use `{}` for single lines and `do..end` for the multiline ones. You can pass parameters to a block by defining them inside pipes, i.e. `|arg1,arg2|`.

```ruby
# Single line block
[1,2,3].each { |num| puts num }

[1,2,3].each do |num|
  puts num
end
```

We can also write own methods that accept blocks and even store blocks as variables

## Yield

`yield` is a keyword that can be called inside a method to relinquish execution to the accompanying block. Let’s imagine you’re writing a simple method for your library which allows users of that library to log some information to the terminal. The one key requirement you have is that users should be able to define how that information is presented. Sometimes they may just want to puts something, other times they may want to inspect something with p. If you tried to write this using only a method, it would actually be quite difficult. You’d have to account for every possible option the user of your library might want to call and then create the docs to explain it. With blocks, we can just relinquish control of the method to the block with yield and allow the user to define how they want to print it.

```ruby
def logger
  yield
end

logger { puts 'hello from the block' }
# => Hello from the logger

logger do
  p [1,2, 3]
end
```

Now the users want a method that allows tem to write whatever they want, and it gets printed twice to the terminal.

```ruby
def double_vision
  yield
  yield
end

double_vision { puts "How many fingers am I holding up?" }
# => How many fingers am I holding up?
# => How many fingers am I holding up?
```

### Passing arguments to yield

```ruby
def love_language
  yield('Ruby')
  yield('Rails')
end

love_language { |lang| puts "I love #{lang}" }
# => I love Ruby
# => I love Rails
```

We can combine the power of `yield` with the `#each` enumerable method. In the example below, we write a method that iterates through a list of transactions, and for each one yields it to a block. The caller of the method (the bank) can call it with any block they want. This way, they can define how transactions will be printed to their statement, and you can focus on delivering, bug-free banking transactions

```ruby
@transactions = [10, -15, 25, 30, -24, 70, 999]

def transaction_statement
  @transactions.each do |transaction|
    yield transaction # just yield the transaction amount
  end
end

transaction_statement do |transaction|
  p "0.2f%" % transaction # The bank that calls the method can define how it is handled.
end
#=> ["10.00", "-15.00", "25.00", "30.00", "-24.00", "-70.00", "999.00"]
```

If you want to gather the value returned from the block, you can just assign it to a variable or collect in a data structure

```ruby
@transactions = [10, -15, 25, 30, -24, 70, 999]

def transaction_statement
  formatted_transactions = []
  @transactions.each do |transaction|
    formatted_transactions << yield(transaction) # We've put () around transaction just for clarity here but they aren't required.
  end
  
  p formatted_transactions
end


transaction_statement do |transaction|
  "%0.2f" % transaction
end
#=> ["10.00", "-15.00", "25.00", "30.00", "-24.00", "-70.00", "999.00"]
```

### Block control

Oftentimes, the person who writes a method and the person who calls a method are different people. If you're writing a method that uses `yield`, how you can be sure the caller will include a block? 

```ruby
def simple_method
  yield
end

simple_method 
# => `simple_method': no block given (yield) (LocalJumpError)
```

Yep, an error. So how can you write a method that works whether or not the caller passes a block to it?

Enter `block_given?`

You can use this method as a conditional check inside your own method to see if a block was included by the caller. If so, `block_given?` returns `true`, otherwise it returns `false`. This lets you write your method so that it behaves differently depending on whether or not it receives a block.

```ruby
def maybe_block
  if block_given?
    puts "block party"
  end
  puts "executed regardless"
end

maybe_block
# => executed regardless

maybe_block {} # {} is just an empty block
# => block party
# => executed regardless
```

## Lambdas