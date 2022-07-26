# Inheritance

Inheritance is the ability of one class to be a child of another class, and therefore **inherit** all its characteristics, including methods and variables.

In ruby a class inherits from another class using the `<` notation. Unlike some other languages, a class can only have ONE parent.

```ruby
class Viking < Person
```

Now `Viking` has access to all `Person`'s methods. Viking now **extends** Person

We can also overwrite existing methods.

```ruby
class Array
    def each
        puts "HAHA no each here!"
    end
end

> [1,2,3].each {|item| puts item }
HAHA no each here!
=> nil
```

If `Viking` extends `Person`, we similarly have the option to overwrite any of `Person`'s methods. Maybe viking `#heal` twice as fasat as normal people. We could write:

```ruby
class Person
    MAX_HEALTH = 120
    ...
    def heal 
        self.health += unless self.health + 1 > MAX_HEALTH
    end
end

class Viking < Person
    ...
    def heal
        self.health = [self.health + 2, MAX_HEALTH].min
    end
end
```

We will often use that in the `#initialize` method when we want to use the parent's `#initialize` but just add a tweak or two of your own

```ruby
class Viking < Person
    def initialize(name, health, age, strength, weapon)
        super(name, health, age, strength)
        @weapon = weapon
    end
end
```

## Scope

Is the formal term that represents when we can access a variable or method and when we can't. It's nothing explicit in the code (we're never calling a method named `scope` or anything like that); it's just a concept. If our variable is "in scope" then it's available for use, otherwise it's "out of scope". 

Think of scope like a container of one-way glass around certain chunks of code. Inside that container, your variable or method can see (or use) anything in the world outside the container but the outside world can't see in.

**A new scope** is created when you first define a variable. That variable is then accessible by anything "downstream" of it in the code, until the current scope is exited (by leaving a method or loop, for instance)

```ruby
def launch_longships(longships)
    # here we cant' yet use `longship`, `longships_count` or `longship_name`
    launched_ships = 0
    # now `launched_ships` in scope so we can use it
    longships.each do |longship|
        # now `longship` is in scope, so we can it
        longship_name = "#{longship.owner.name}'s Reaver"
        # now `longship_name` is in scope so we can use it
        longship.launch
        launched_ships += 1
        puts "#{longship_name} successfully launched!"
    end
    # now we've exited the loop, so `longship` and `longship_name` 
    # are no longer in scope so we cannot use them.
end
```

A good rule of thump for scope is that you create a new scope any time you should indent your cande and any time within that indent a new variable is defined.


**Method scope** is similar but has some important differences because it deals much more explicitly with the notion of **privacy**. You still can't call a method until the Ruby interpreter has had the chance to define it. By default, instance methods can be calle by any instance of a class (e.g `oleg.sleep`) and class methods can be calle directly on the class itself (e.g `Viking.new`)

BUt what if we've got a really sensitive method like `#die` that we don't want anyone else to be able to call directly? it should **ONLY** be available to other methods from withing that **PARTICULAR** instance of a Viking. So we don't wanto to be able to say `> oleg.die` from the CLI, but we do want to be able to kill off oleg if he loses all his healt, so we create a chunk of code marked as **`private`**

```ruby
class Viking
    ...
    def take_damage(damage)
        @health -= damage
        die if @healt <= 0
    end
    private
        def die
            puts "#{self.name} has been killed"
            self.dead = true
        end
end
```

```console
$ oleg = Viking.create_warrior("Oleg")
$ oleg.die
NoMethodError: private method `die' called for #<Viking:0x007ffd4c041e50>

$ oleg.take_damage(200)
Oleg has been killed
=> true
```

If you create methods that should only be accessible by other methods within your class, make them `private`. This is the default setting for instance variables unless you expose using the afore-mentioned `attr_accessor`

If we create an #attack method for one instance to #attack another, then we can have that method deal with the damage stuff on its own so the user is none-the-wiser. But we can't make our #take_damage method private because otherwise we could only call it on the specific viking who is DOING the attacking. We want to call it on the RECIPIENT of the attack (remember, private methods can only be called from within the same instance).

Since we don't want `#take_damage` to be visible to anyone on the CLI but we do want it tobe visible to the methods inside other instances of `VIking`, we call `protected`. `protected` provides most of the privacy of `private` but lets the methods inside other instances of the same class or it descedents also access it

```ruby
class Viking < Person
    ... 
    def attack(recipient)
        if recipient.dead
            puts "#{recipient.name} is already dead"
            return false
        end

        damage = (rand * 10 + 10).round(0)
        recipient.take_damage(damage)  # `take_damage` called on `recipient`!
    end
    protected 
        def take_damage(damage)
            self.health -= damage
             puts "Ouch! #{self.name} took #{damage} damage and has #{self.health} health left"
            die if @health <= 0  
            # `die` called from within the same object as take_damage was (the `recipient` as well!)
        end
    private 
        def die
            puts "#{self.name} has bene killed"
            self.dead = true
        end
end
```