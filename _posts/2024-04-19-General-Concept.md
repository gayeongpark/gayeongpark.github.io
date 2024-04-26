---
layout: post
title: General Concepts
subtitle: Practice for concept of types (TypeScript)
tags: [programming, typescript, general concept, types]
comments: true
author: Lantana Park
---

# Type Systems

Types in programming serve to improve both the correctness and clarity of the code.

## What is type?

- **Syntactic Role:**

Data types help the compiler or interpreter differentiate between kinds of data, allowing for the appropriate processing.

```typescript
const year: number = 2024;

console.log(year); // Outputs: 2024
```

Here, `number` is a syntactic token that signals to the compiler the nature of age.

- **Representation and Value space:**

Each type defines a range of values it can represent.

TypeScript `boolean` can hold true or false.

```typescript
let isActive: boolean = false;

if (!isCompleted) {
  isCompleted = true;
}

console.log(isCompleted); // Outputs: true
```

- **Semantic meaning:**

Types can carry specific meanings

```typescript
type Email = string;
type UserID = number;

let user1Email: Email = "user1@example.com";
let user1ID: UserID = 101;

function sendEmail(userEmail: Email) {
  console.log(`Sending email to: ${userEmail}`);
}

sendEmail(user1Email); // Clear that the function expects an Email type
```

- **Behavior:**

Data types also dictate what operations can be performed with them. For instance, arithmetic operations are typically defined for numeric types like integers and floats.

```typescript
const price: number = 29.99;
const taxRate: number = 0.07;
const productName: string = "Book";

// Calculating total cost using arithmetic operations, which are valid on numbers
let totalCost: number = price + price * taxRate;
console.log(`Total cost of the ${productName}: $${totalCost.toFixed(2)}`);

// The following line would result in a TypeScript error if uncommented
// let incorrectOperation = price + productName;  // Error: Operator '+' cannot be applied to types 'number' and 'string'.
```
