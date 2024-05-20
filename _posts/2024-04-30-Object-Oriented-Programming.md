---
layout: post
title: Object Oriented programming
subtitle: Practice for concept of object oriented programming
tags: [programming, class, object-oriented, inheritance, se03]
comments: true
author: Lantana Park
---

# Object oriented programming

## What is OOP(Object Oriented Programming)?

OOP, object-oriented programming, is one of the programming concepts and has four main concepts: class and instance, encapsulation, inheritance, and polymorphism.

## What is classes and objects?

**Class** is a blueprint for creating objects. It is like making a mold to bake a bread.

**Object** is an instance of a class. It is like baking bread with the mold.

JavaScript example,

```javascript
// Defining a class to set a baking mold
class Bread {
  constructor(color, ingredient) {
    this.color = color;
    this.ingredient = ingredient;
  }
}

let myBread = new Bread("brown", "Rye-wheat"); // Creating an object of the Bread class
console.log(myBread); // {color: "brown", ingredient: "Rye-wheat"}
```

## Encapsulation

Encapsulation can be called "data hiding" because I can hide certain data and limit the access the data to the subclass. This feature can be used if I want to protect data purposefully by other components.

TypeScript example,

```typescript
// Defining a class
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

let myBread = new Bread("brown", "Rye-wheat"); // Creating an object of the Bread class with this instance
console.log(myBread.bake()); // Works fine, because method is public
// "Baking brown bread with Rye-wheat."
console.log(myBread.color); // Works fine, because property is public
// "brown"
console.log(myBread.ingredient); // Error, 'ingredient' is private and only accessible within class 'Bread'
console.log(myBread.mixIngredients()); // Error, 'mixIngredients' is private and only accessible within class 'Bread'
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
    super(color, ingredient); // Calling the super class constructor and pass in the color and ingredient from the Bread class
    this.filling = filling; // Additional property specific to Sandwich
  }
  // Setting a method for describing a sandwich
  describe() {
    return `A ${this.color} sandwich made of ${this.ingredient} with ${this.filling}.`;
  }
}

// Creating an object of the Sandwich class with this instance
let mySandwich = new Sandwich("brown", "Rye-wheat", "turkey and cheese");
console.log(mySandwich.describe()); // A brown sandwich made of Rye-wheat with turkey and cheese.
```

### Multiple Inheritance

In multiple inheritance, a subclass is derived from more than one parent class. Since JavaScript does not support multiple inheritance feature, I made a python example.

```python
# Creating Bread class
class Bread:
    def __init__(self, color, ingredient):
        self.color = color # self is similar with `this` keyword in javaScript
        self.ingredient = ingredient

# Creating Spread class
class Spread:
    def __init__(self, spread_type):
        self.spread_type = spread_type

class Sandwich(Bread, Spread):  # Creating multiple inheritance class
    def __init__(self, color, ingredient, filling, spread_type):
        Bread.__init__(self, color, ingredient)  # Initializing Bread part
        Spread.__init__(self, spread_type)       # Initializing Spread part
        self.filling = filling  # Adding filling property in Sandwich class

    def describe(self):
        return f"A {self.color} sandwich made of {self.ingredient} with {self.filling} and {self.spread_type} spread." # the `f` before the string indicates that it is a formatted string literal in python.

# Creating an object of the Sandwich class
my_sandwich = Sandwich("brown", "Rye-wheat", "turkey and cheese", "mustard")
print(my_sandwich.describe())  # A brown sandwich made of Rye-wheat with turkey and cheese and mustard spread.
```

### Interface Inheritance

In interface inheritance, I can define a binding agreement for classes in the form of an interface, which specifies the properties and methods that classes must implement.

TypeScript example,

```typescript
// Defining the interface that acts as a blueprint(mold) for bread-making classes
interface Bread {
  color: string;
  ingredient: string;
  bake(): void; // Creating a method to bake a bread
}

// Implementing the interface in a specific class
class RyeBread implements Bread {
  color: string;
  ingredient: string;

  constructor(color: string, ingredient: string) {
    this.color = color;
    this.ingredient = ingredient;
  }
  // Implementing the bake method as specified in the interface
  bake() {
    console.log(`Baking a ${this.color} bread with ${this.ingredient}`);
  }
}

let myRyeBread = new RyeBread("dark brown", "Rye");
console.log(myRyeBread.bake()); // Baking a dark brown bread with Rye
```

By implementing the `Bread` interface, `RyeBread` is required to have the `color` and `ingredient` properties, as well as the bake method. And then it is necessary to provide concrete definitions for the properties and method specified in the interface.

### Prototype-based Inheritance

In prototype-based inheritance, objects can inherit properties and methods directly from other objects without the need for a class. Each object can have a prototype object, and properties and methods are shared through **this prototype chain**.

JavaScript example,

```javascript
// Defining the constructor function designed to create objects and define initial properties
function Bread(color, ingredient) {
  this.color = color;
  this.ingredient = ingredient;
}

// Adding the back method to the Bread prototype
Bread.prototype.bake = function () {
  console.log(`Baking ${this.color} bread with ${this.ingredient}.`);
};

// Creating an instance of Bread to use the property from a gene
let ryeBread = new Bread("brown", "Rye-wheat");
console.log(ryeBread.bake()); // Baking brown bread with Rye-wheat.

// Creating a new bread object based on the ryeBread prototype
let multiGrainBread = Object.create(ryeBread);
multiGrainBread.ingredient = "Multigrain";
console.log(multiGrainBread.bake()); // Baking brown bread with Multigrain.
```

`multiGrainBread` inherits properties and methods from `ryeBread` due to `Object.create(ryeBread)`. This creates a prototype chain: `multiGrainBread` -> `ryeBread` -> `Bread.prototype`.

### Class-based Inheritance

In class-based inheritance, I can define a class and then extend the class by creating subclasses.

TypeScript example,

```typescript
// Defining a Bread class
class Bread {
  color: string;
  ingredient: string;

  constructor(color: string, ingredient: string) {
    this.color = color;
    this.ingredient = ingredient;
  }

  bake(): void {
    console.log(`Baking ${this.color} bread with ${this.ingredient}.`);
  }
}
// Extending the Bread class by using extends keyword and creating a SourdoughBread subclass
class SourdoughBread extends Bread {
  constructor(ingredient: string) {
    super("cream", ingredient); // super is to use the properties from the parent class
  }
}

let mySourdough = new SourdoughBread("sourdough starter");
console.log(mySourdough.bake()); // Baking cream bread with sourdough starter.
```

## Polymorphism

`Poly` means MANY and `morphism` means FORM. So it means MANY FORM, indicating that a single interface can be used to represent different underlying forms (data types).

**Compile-Time Polymorphism (Static Binding)**: This is achieved through method overloading. The method to be invoked is determined **at compile time**.

**Run-Time Polymorphism (Dynamic Binding/Late Binding)**: This is achieved through method overriding. The method to be invoked is determined **at runtime**, which involves dynamic dispatch and late binding.

Late binding in TypeScript example,

```typescript
// Defining the base Bread class
class Bread {
  color: string;
  ingredient: string;

  constructor(color: string, ingredient: string) {
    this.color = color;
    this.ingredient = ingredient;
  }

  bake(): string {
    return `Baking bread: ${this.color} bread with ${this.ingredient}.`;
  }
}

// Extending the Bread class to create specific bread types
class RyeBread extends Bread {
  constructor() {
    super("dark brown", "rye and wheat");
  }
  // Overriding the method from Bread class to provide specific baking instructions for each type of bread (Dynamic dispatch)
  bake(): string {
    return `Baking ${this.color} rye bread using traditional methods with ${this.ingredient}.`;
  }
}

// Extending the Bread class to create specific bread types
class SourdoughBread extends Bread {
  constructor() {
    super("light creamy", "sourdough starter");
  }
  // Overriding the method from Bread class to provide specific baking instructions for each type of bread (Dynamic dispatch)
  bake(): string {
    return `Baking ${this.color} sourdough bread with a slow fermentation using ${this.ingredient}.`;
  }
}

// Using the function with different bread types
let myRyeBread = new RyeBread();
let mySourdough = new SourdoughBread();

console.log(myRyeBread.bake()); // Dynamic binding: Baking dark brown rye bread using traditional methods with rye and wheat.
console.log(mySourdough.bake()); // Dynamic binding: Baking light creamy sourdough bread with a slow fermentation using sourdough starter.
```

Static binding in TypeScript example,

```typescript
// Defining the base Bread class
class Bread {
  color: string;
  ingredient: string;

  constructor(color: string, ingredient: string) {
    this.color = color;
    this.ingredient = ingredient;
  }

  // This method will be statically bound
  description(): string {
    return `This is a ${this.color} bread with ${this.ingredient}.`;
  }
}

// Extending the Bread class to create specific bread types
class RyeBread extends Bread {
  constructor() {
    super("dark brown", "rye and wheat");
  }
}

// Extending the Bread class to create specific bread types
class SourdoughBread extends Bread {
  constructor() {
    super("light creamy", "sourdough starter");
  }
}

// Using the function with different bread types
let myRyeBread: Bread = new RyeBread();
let mySourdough: Bread = new SourdoughBread();

console.log(myRyeBread.description()); // Static binding: This is a dark brown bread with rye and wheat.
console.log(mySourdough.description()); // Static binding: This is a light creamy bread with sourdough starter.
```
