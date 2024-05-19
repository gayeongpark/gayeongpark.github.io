---
layout: post
title: General types programming
subtitle: Practice for types and type systems
tags: [programming, typescript, general concept, types, se03]
comments: true
author: Lantana Park
---

# What is types in programming?

Types in programming serve **to improve both the correctness and clarity of programming constructs**, such as variables, expressions, functions or modules.

## The role of Types

- **Syntactic Role:**

Types help the compiler or interpreter **differentiate between kinds of data**, allowing for the appropriate processing and catching errors early during the development.

TypeScript example,

```typescript
const year: number = 2030;

console.log(year); // 2030
```

`number` tells the complier that `year` is a numeric value, helping with operations and error checking.

- **Representation and Value space:**

Types defines a range of values it can represent.

TypeScript example,

```typescript
let isActive: boolean = false;

if (!isActive) {
  isActive = true;
}

console.log(isActive); //true
```

`boolean` restricts `isActive` variable to only `true` or `false`, ensuring consistent usage.

- **Semantic meaning:**

Types show how types can provide specific, meaningful information about the data being used.

TypeScript example,

```typescript
type email = string; // Email is an alias for string
type userID = number; // userId is an alias for number

let user1Email: email = "user1@example.com";
let user1ID: userID = 101;

function sendEmail(userEmail: email) {
  console.log(`Sending email to: ${userEmail}`);
}

sendEmail(user1Email); // "Sending email to: user1@example.com"
sendEmail(user1ID); // Error: Argument of type 'UserID' is not assignable to parameter of type 'Email'.
```

Alias like `email` and `userId`improves code readability and ensures type safety by preventing incorrect usage.

- **Behavior:**

Types can dictate what operations can be performed with them. For instance, arithmetic operations are typically defined for numeric types like integers and floats.

TypeScript example,

```typescript
const price: number = 29.99;
const taxRate: number = 0.07;
const productName: string = "Book";

// Calculating total cost using arithmetic operations, which are valid on numbers
let totalCost: number = price + price * taxRate;
console.log(`Total cost of the ${productName}: $${totalCost.toFixed(2)}`);
// "Total cost of the Book: $32.09"
```

`number` types allows arithmetic operations.

In summary,

Proper use of types leads to more robust, maintainable, and less error-prone code. Types not only help with catching errors early during development but also make the code more understandable and easier to maintain.

## Primitive types and reference types

In programming, data types can generally be classified into two categories: **primitive types** and **reference types**.

### Primitive types

Primitive types are the most **basic forms of data**. In TypeScript, these include types like `number`, `string`, `boolean`, `null`, `undefined`, `symbol`, and `bigint`. These types store their data directly in the location the variable accesses.

```typescript
let year: number = 2030; // Here, `year` is a variable of primitive type `number`
let isActive: boolean = true; // `isActive` is a primitive type `boolean`

console.log(year); // 2030
console.log(isActive); // true
```

### Reference types

Reference types **store references to their data rather than the data itself**. This means the variable actually **stores a pointer to the location in memory** where the data is stored. Common reference types in TypeScript include `object`, `array`, and `function`.

Since It allows alter the original data by storing references, it saves memory.

```typescript
let user: { name: string; age: number } = { name: "Jane Doe", age: 28 };
// The variable `user` is an object type.
console.log(user); // { name: "Jane Doe", age: 28 }

let numbers: number[] = [1, 2, 3];
// The variable `numbers` is an array type.
numbers.push(4);
console.log(numbers); // [1, 2, 3, 4]
// This is mutability by altering the original data.
```

## Type systems

A type system is a set of rule to manage and manipulate data types more effectively.

### Dynamic vs Static typing

#### Static typing

Static typing involves **type checking during compilation**, before program execution. Once a variable is assigned a data type, **it remains unchanged throughout the programs execution**.

Static typing reduces the chances of runtime errors(this error happens after compilation) and detects errors at an early stage.

On the other side, it will be hard to have small type revisions and these small type changes can draw bigger architectural changes.

TypeScript example,

```typescript
function staticTyping(value: number): number {
  return value * 2;
}

console.log(staticTyping(5)); // 10
```

The function type is `number` and its argument type is `number`. These types should not be changed throughout this function execution.

#### Dynamic typing

Once a specific function is called, types of the function are checked **during the runtime** , after compilation. **Dynamic typing allows for type changes within a variable, even during function execution**, so it is more flexible and **requires solid unit test** to reduce possible errors.

Python example,

```python
def dynamic_typing(value):
    print(type(value))  # type of 'value' is 'int' because value will be recognized as 10
    value = "Now I'm a string" # reassigned value
    print(type(value))  # new type of 'value' is `str` based on the reassigned value

dynamic_typing(10)
```

The type of this argument value is determined at runtime (after compilation) and can change as the program executes.

#### Type conversion (type casting)

Type conversion is the process of converting the type of a variable from one to another by assigning new data type to the new variable.

- Implicit conversion: This happens when the programming language **automatically converts** a type to another **to perform some operation**.

- Explicit conversion: This requires the programmer to **write code specifying the conversion**.

Python example,

```python
x = 10         # Integer type
y = 3.14       # Float type
z = x + y      # Implicit conversion: x is converted to float
print(z)       # 13.14

a = "123"
b = int(a)     # Explicit conversion: string to integer
print(b + 10)  # 133
```

Type casting can be used in static typing, when I want to convert between different types.

#### dynamic typing vs type conversion

while dynamic typing allows for changing the type of a variable during program execution without the need for explicit type conversions, type conversion involves explicitly creating a new variable or expression to hold the converted value while leaving the original variable unchanged.

#### Type inference (static type system)

The compiler or interpreter analyzes the code and **infers the data types of variables based on their usage and the context in which they are declared**.

Haskell example,

```haskell
-- Define a function that adds two numbers
add :: Num a => a -> a -> a
add x y = x + y

-- Call the function without explicitly specifying types
result = add 5 10

-- Haskell infers the types of 'result', 'x', and 'y'
-- 'result' will have the same type as the arguments (in this case, 'Int' because literals are inferred as 'Int')
-- 'x' and 'y' will also be inferred as 'Int' based on the usage
main = print result
-- 15
```

The types of `result`, `x`, and `y` were deduced based on their usage.

### Structural typing (dynamic type system)

Structural typing determines an object's type by **its structure** rather than its explicit type declaration. **The compiler checks that the types have the same structure** without requiring them to be declared as the same. Since **type checking occurs at the compile time**, errors can be caught early in the development process.

TypeScript example,

```typescript
// Define structures for objects with 'playSound' method
type AudioPlayer = {
  playSound: (file: string) => void;
};

// A class for a music player that matches the AudioPlayer structure
class MusicPlayer {
  playSound(file: string) {
    console.log(`Playing music from file: ${file}`);
  }
}

// A class for a podcast player that also matches the AudioPlayer structure
class PodcastPlayer {
  playSound(file: string) {
    console.log(`Streaming podcast from file: ${file}`);
  }
}

// A function that accepts any object that matches the AudioPlayer structure
function startPlaying(player: AudioPlayer, file: string) {
  player.playSound(file);
}

// Create instances of both players
const myMusicPlayer = new MusicPlayer();
const myPodcastPlayer = new PodcastPlayer();

// Both players can be passed to 'startPlaying' function
// As `MusicPlayer` and `PodcastPlayer` classes match with `AudioPlayer` structure
startPlaying(myMusicPlayer, "favorite_song.mp3"); // Playing music from file: favorite_song.mp3
startPlaying(myPodcastPlayer, "interesting_podcast.mp3"); // Streaming podcast from file: interesting_podcast.mp3
```

### Duck typing (dynamic typing system)

Duck typing is a dynamic typing concept that **determines an object's type by what methods and properties it has**, not what it is named to be. **The type check happens at runtime**.

Python example,

```python
class Bird:
    def fly(self):
        print("Flies into the sky!")

class Airplane:
    def fly(self):
        print("Takes off the runway!")

def make_it_fly(thing):
    thing.fly()

make_it_fly(Bird())        # Flies into the sky!
make_it_fly(Airplane())    # Takes off the runway!
```

Here, both `Bird` and `Airplane` can be passed to `make_it_fly` function because they both have a `fly` method. The system doesn’t care what type `thing` is, as long as it meets the necessary functional criteria.

### Nominal typing (static typing system)

Nominal typing, also known as name-based typing, means that **a type is considered different from another type if they have different names**, regardless of whether they have the same structure or not. **Type compatibility is checked at compile-time on explicit declaration**.

TypeScript example,

```typescript
class Vehicle {
  drive() {
    console.log("Driving on the road");
  }
}

class Car extends Vehicle {
  drive() {
    console.log("Car driving");
  }
}

let myCar: Vehicle = new Car(); // Works because Car is a subclass of Vehicle

class Motorcycle {
  drive() {
    console.log("Motorcycle driving");
  }
}

let myBike: Vehicle = new Motorcycle(); // Errors because Motorcycle isn't a Vehicle
```

`Car` can be assigned to a variable of type `Vehicle` because `Car` extends `Vehicle`. However, `Motorcycle`, despite having a similar structure, cannot be treated as a `Vehicle` without explicit inheritance, showing nominal typing’s emphasis on explicit declarations and heritage.
