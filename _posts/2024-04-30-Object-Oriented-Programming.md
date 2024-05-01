---
layout: post
title: Object Oriented programming
subtitle: Practice for concept of object oriented programming
tags: [programming, class, object-oriented, inheritance]
comments: true
author: Lantana Park
---

# Object oriented programming

## What is OOP(Object Oriented Programming)?

OOP, object-oriented programming is one of the programming concepts and has three main concepts: class and instance, encapsulation, inheritance, and polymorphism.

<!-- Object-oriented concepts:

Classes and objects
Inheritance (e.g. single/multiple inheritance, interface inheritance, abstract classes, prototype-based / class-based inheritance)
Polymorphism (incl. dynamic dispatch and late binding) -->

## What is classes and objects?

**Class** is a blueprint for creating object. It is like making bread mold.

**Object** is an instance of a class. It is like making bread using the mold.

JavaScript example,

```javascript
// setting mold to make a bread
class Bread {
  constructor(color, ingredient) {
    this.color = color;
    this.ingredient = ingredient;
  }
}

let myBread = new Bread("brown", "Rye-wheat"); // Creating an object of the Car class
```

## Inheritance

Inheritance is a feature of object-oriented programming that allows for code reuse by deriving a new class from an existing one, inheriting all its attributes and methods.

### Single inheritance

In single inheritance, a subclass inherits from one parent class.

JavaScript example,

```javascript
// Defining a Bread class for making bread for sandwich
class Bread {
  constructor(color, ingredient) {
    this.color = color;
    this.ingredient = ingredient;
  }
}

// Creating Sandwich class and inheriting all the attributes from Bread class
class Sandwich extends Bread {
  constructor(color, ingredient, filling) {
    super(color, ingredient); // Call the super class constructor and pass in the color and ingredient from the Bread class
    this.filling = filling; // Additional property specific to Sandwich
  }
  // Setting a method for describing a sandwich
  describe() {
    return `A ${this.color} sandwich made of ${this.ingredient} with ${this.filling}.`;
  }
}

// Creating an object of the Sandwich class
let mySandwich = new Sandwich("brown", "Rye-wheat", "turkey and cheese");
console.log(mySandwich.describe()); // A brown sandwich made of Rye-wheat with turkey and cheese.
```

### Multiple Inheritance

In multiple inheritance, a subclass is derived from more than one parent class. Since JavaScript does not support multiple inheritance feature, I made python example.

```python
# Creating Bread class
class Bread:
    def __init__(self, color, ingredient):
        self.color = color # self is similar with this keyword in javaScript
        self.ingredient = ingredient

# Creating Spread class
class Spread:
    def __init__(self, spread_type):
        self.spread_type = spread_type

class Sandwich(Bread, Spread):  # Creating multiple inheritance
    def __init__(self, color, ingredient, filling, spread_type):
        Bread.__init__(self, color, ingredient)  # Initializing Bread part
        Spread.__init__(self, spread_type)        # Initializing Spread part
        self.filling = filling    # Adding filling property in Sandwich class

    def describe(self):
        return f"A {self.color} sandwich made of {self.ingredient} with {self.filling} and {self.spread_type} spread."

# Creating an object of the Sandwich class
my_sandwich = Sandwich("brown", "Rye-wheat", "turkey and cheese", "mustard")
print(my_sandwich.describe())  # A brown sandwich made of Rye-wheat with turkey and cheese and mustard spread.
```

### Interface Inheritance

### Prototype-based Inheritance

### Class-based Inheritance

## Encapsulation

Encapsulation can be called "data hiding" because I can hide certain data and limit the access the data to the subclass. This feature can be used if I want to protect data purposefully by other component.

TypeScript example,

```typescript
class Bread {
  // Setting public properties can be accessed from outside the class
  public color: string;

  // Setting private properties cannot be accessed from outside the class, only within this class
  private ingredient: string;

  constructor(color: string, ingredient: string) {
    this.color = color; // Public, can be accessed and modified anywhere
    this.ingredient = ingredient; // Private, modification restricted within this class
  }

  // Setting public method to bake bread, can be called from anywhere
  public bake() {
    console.log(`Baking ${this.color} bread with ${this.ingredient}.`);
  }

  // Setting private method, can only be used internally by the class
  private mixIngredients() {
    console.log(`Mixing ingredients: ${this.ingredient}`);
  }
}

let myBread = new Bread("brown", "Rye-wheat"); // Creating an object of the Bread class
myBread.bake(); // Works fine, because method is public
console.log(myBread.color); // Works fine, because property is public

myBread.ingredient; // Error, 'ingredient' is private and only accessible within class 'Bread'
myBread.mixIngredients(); // Error, 'mixIngredients' is private and only accessible within class 'Bread'
```

## polymorphism

### dynamic binding
