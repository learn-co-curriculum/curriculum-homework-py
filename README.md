# Self Basics

## Learning Goals

- Understand the concept of self-awareness in object-oriented programming
- Understand how the `self` keyword works

## Introduction

When we create a class, each new instance of a class is considered to be an
**object**. An object is a bundle of code contains both data and behaviors.

For example, if we create a `Dog` class like this:

```rb
class Dog
  attr_accessor :name

  def initialize(name)
    @name = name
  end

  def bark
    'Woof!'
  end
end
```

We could create a new instance of `Dog` like this:

```rb
fido = Dog.new('Fido')
```

We could then access Fido's name like this:

```rb
fido.name
# => "fido"
```

...or tell Fido to bark like this:

```rb
fido.bark
# => "Woof!"
```

Fido, the individual dog that we created, has a number of methods that will
reveal its attributes, like it's name, and enact certain behaviors, like
barking.

If an object, like `fido`, is a package of data and behaviors, does an object
know about itself? In other words, does each individual object we create have
the ability to enact behaviors _on itself_?

In fact, every object is aware of itself and we can define methods in which we
tell objects to operate on themselves. Code-wise, we can use `self` keyword in
an instance method to refer to the very same object the method is being called
on.

This is where the analogy of our objects as being alive really resonates. Every
object is, quite literally, self-aware.

## Using `self`

Try this:

Run `irb` in your terminal to open an interactive REPL. Copy and paste the
following code into IRB:

```rb
class Dog
  def showing_self
    puts self
  end
end
```

Now that we have our `Dog` class ready to go, copy and paste the following
method invocations into IRB:

```rb
fido = Dog.new
fido.showing_self
```

The call to `#showing_self` should output:

```console
#<Dog:0x007faf90a88cd8>
```

How does this work? Inside the `#showing_self` method, we use the self keyword.

The `self` keyword **refers to the instance**, or object, that the
`#showing_self` **method is being called on**.

When we call `#showing_self` on `fido`, the method will output the `Dog`
instance that is `fido` to the terminal.

## Operating on `self` in an Instance Method

Let's say that Fido here is getting adopted. Fido's new owner is Sophie. Let's write an `attr_accessor` on our `Dog` for the owner attribute.

```
class Dog
  attr_accessor :name, :owner

  def initialize(name)
    @name = name
  end
end
```

Now we can set Fido's `owner` attribute equal to the string of `"Sophie"`. The name of his new owner:

```rb
fido.owner = 'Sophie'

fido.owner
# => "Sophie"
```

Great, Fido now knows the name of his owner. Let's think about the situation in which `fido` gets a new owner. This would occur at the moment in which `fido` is adopted.

To represent this with code, we could write an `#adopted` method like this:

```rb
def adopted(dog, owner_name)
  dog.owner = owner_name
end
```

Here we have a method that takes in two arguments, an instance of the `Dog` class and an owner's name. We could call our method like this:

```rb
adopted(fido, 'Sophie')

# now we can ask Fido who his owner is:

fido.owner
# => "Sophie"
```

However, the beauty of object-oriented programming is that we can encapsulate, or wrap up, attributes and behaviors into one object. Instead of writing a method that is not associated with any particular object and that takes in certain objects as arguments, we can simply teach our `Dog` instances how to get adopted.

Let's refactor our code above into an instance method on the `Dog` class.

```rb
class Dog
  attr_accessor :name, :owner

  def initialize(name)
    @name = name
  end

  def bark
    'Woof!'
  end

  def get_adopted(owner_name)
    self.owner = owner_name
  end
end
```

Here, we use the `self` keyword inside of the `#get_adopted` instance method to
refer to whichever dog this method is being called on. We set that dog's `owner`
property equal to the new owner's name by calling the `#owner=` method on `self`
inside the method body.

Think about it: if `self` **refers to the object on which the method is being
called**, and if that object is an instance of the `Dog` class, then we can call
any of our other instance methods on `self`.

Here's how we'd use the `#get_adopted` method:

```rb
fido = Dog.new('Fido')
fido.get_adopted('Sophie')
fido.owner
# => "Sophie"
```

## Resources

* [Metaprogramming in Ruby](http://yehudakatz.com/2009/11/15/metaprogramming-in-ruby-its-all-about-the-self/)
