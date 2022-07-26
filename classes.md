# Classes 

We've been over storing data in hashes, but what happens when we want to treat that data like a real object and make it move? Or if you want to handle 10.000 different instances of it? When you just store your's `Viking`'s `name`, `age`, `health`, and `strength`, it just kinds of sit here. What about when you want to make an army of `Viking` who can do stuff like `#eat`, `#travel`, `#sleep`. 

```ruby
class Viking
    # put your methods and variables here
end
```

Everything in Ruby is an object, whether strings, hashes, arrays or numbers, and these objects are instances of some type of classes.

```console
$ > 1.class
=> Integer
$ > [].class
=> Array
```

Just like being a part of `Array` gives `[1,2,3]` the `#each` method, you can create your own classes that have access to shared methods as well.

To be able to create a `Viking`, we need to create new ones. Each time we do that, it's called **Instatiating** a new Viking. You use a special `::new` method to do that. You've done it many times for the Array class already:

```console
$ > my_array = Array.new
=> []
```

`::new` is a **Class Method**, which means that you call it on the class.

It's also why we designate it with the two colons `::` when talking about it here. When you call that method, it creates a new instance of that class and then runs a special method in the class called `#initialize`

```ruby
class Viking
    def initialize(name, age, health, strength)
        # set up the viking however you want
    end
end
```

Classes share their methods, but what about variables? You don't all your vikings to have the same strength, so we use **instance variables** to take care of that. You designate an instnace variable using **`@variable_name`** notation, and we'll be able to use it the same way for every instance of Viking but it will have an unique value for each. These instance variables are part of setting up your object's state. When your instance is destroyed, you lose access to its instance variables as well. You'd usually set them up in your `#initialize` method:

```ruby
class Viking
    def initialize(name, age, health, strength)
        @name     = name
        @age      = age
        @health   = health
        @strength = strength
    end
end
``` 

```console
$ oleg = Viking.new("Oleg", 19, 100, 8)
=> #<Viking:007ffc0597bae0>
```

Note that the class name is always capitalized and, for multiple words uses **CamelCase**. 

---

## Instance Methods

```ruby
class Viking
    def initialize(name, age, health, strength)
        # codecodecode
    end

    def attack(enemy)
        # code to fight
    end
end
```

Now, if we had two vikings, `oleg` and `lars`, I could say `lars.atack(oleg)` and would run that method. So now we want to know the oleg health

```console
$ > oleg.health
=> NoMethodError: undefined method 'health' for #<Viking:0x007ffc0597bae0>
```

We can't acccess them from outside so we have to create a method specifically to get that variable, called a **getter** method, and just name it the same thing as the variable we want:

```ruby
class Viking
    ...
    def health
        @health
    end
    ...
end
```

```console
$ > oleg.health
=> 87
```

And if we want to set that variable by ourselves? 
Then we need to create **setter** method, which is similar syntas to the gether but with an equals sign and taking an arg:

```ruby
class Viking
    ...
    def health=(new_health)
        @health = new_health
    end
    ...
end
```

### Helper method with getters and setters

There is a helper method called `attr_accessor`, which will create those getters and setters for you. Just pass it the symbols for whatever variables you want to make accessible and POOF! those methods will now exist for you to use:

```ruby
class Viking
    attr_accessor :name, :age, :health, :strength
end
```

We shouldn't make anything readable and certainly writeable without a good reason, but Ruby gives us the similar `attr_reader` and `attr_writer` methods.

Because of our getters and setters, there are two different ways to access an instance variable from inside the class, either calling it normally using `@age` or calling the method on the instance using `self`. Before, we said it represented whatever object called a particular method. Since the original method (below it's `#take_damage`) is being called on an instance of the class, that instance becomes self. An example is clearer:

```ruby
class Viking
    ...
    def take_damage(damage)
        self.health -= damage
            # OR we could have said @health -= damage
        self.shout("🤮")
    end

    def shout(str)
        puts(str)
    end 
    ...
end
```

## Class variables and Class methods

Class variables are denoted with two `@@`, are owned by the class itself so there is only one of them overall instead of one per instance.

```ruby
class Viking
    @@starting_health
    def initialize(name, age, strength)
        @health = @@starting_health
        ...
    end
end
```

About class methods: you can define just by preceding its name with self (e.g. `def selc.class_method`), or identically, just the name of the class (e.g `def Viking.class_method`). There's a less common method that puts the line `class << self` ahead of your method definitions

### Factory method

- Is designed to save us from having to keep passing a bunch of params manually to your `#initialize` method

```ruby
class Viking
    def initialize(name, health, age, strength)
        # ... set variables
    end

    def self.create_warrior(name)
        ange = rand * 20 + 15
        health = [age * 5, 120].min
        strength = [age / 2, 10].min    

        Viking.new(name, health, age, strength)
    end
end
```

```console
$ sten = Viking.create_warrior("Sten")
=> #<Viking:0x007ffc05a79848 @age=21.388120526202737, @name="Sten", @health=106.94060263101369, @strength=10>
```

---

## Quick basics

- Classes are useful to use when you want to give methods to your data or have multiple instances of your data
- Class methods have acces to other class methods and class variables but don't have access to instance methods or instance variables
- Instance methods can call other instance methods, instance variables, class methods, or class variables.