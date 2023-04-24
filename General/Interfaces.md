##Interfaces in programming
###What are interfaces and why should you use them?
In object-oriented programming (OOP from now on), and interface defines a contract or a set of rules that a class must follow. An interface can specify the names, data types and signatures of the methods that a class must implement, but does not provide an implementation for those methods.

In many languages, interfaces are a built-in language feature, for example in Java or C# (it is not built-in in JavaScript). If you want to use interfaces in JavaScript you can look into TypeScript, which does have interfaces as a built-in feature.

#####Why should you use interfaces? (It might seem redundant at first)

1. Encapsulation: Interfaces help to define a clear boundary between different components of an application. They allow you to define the inputs and outputs of a component without exposing the internal implementation details.
2. Abstraction: Interfaces allow you to abstract away the implementation details of a component and focus on its external behavior. This makes it easier to reason about the behavior of a component and to change its implementation without affecting the rest of the application.
3. Code reusability: Interfaces allow you to define a contract that multiple classes can implement. This makes it easier to reuse code across different parts of an application and to build modular and exensible code.
4. Type checking: In TypeScript, interfaces can be used to define types and contracts between components. This allows the TypeScript compiler to perform static type checking at compile-time and catch errors before the code is executed.

Overall, interfaces are a powerful tool in object-oriented and type-safe programming. They can help you to write more modular, reusable, and robust code.

Example (in TypeScript):

```
interface Shape {
  area(): number;
}

class Rectangle implements Shape {
  constructor(private width: number, private height: number) {}

  area(): number {
    return this.width * this.height;
  }
}

class Circle implements Shape {
  constructor(private radius: number) {}

  area(): number {
    return Math.PI * Math.pow(this.radius, 2);
  }
}

function calculateTotalArea(shapes: Shape[]): number {
  let totalArea = 0;

  for (const shape of shapes) {
    totalArea += shape.area();
  }

  return totalArea;
}

const rectangle = new Rectangle(10, 20);
const circle = new Circle(5);

const totalArea = calculateTotalArea([rectangle, circle]);

console.log(totalArea); // Output: 314.1592653589793

```
In this example, we define an interface called '**Shape**' that specifies a single method called '**area()**' that returns a '**number**'. Then, we define two classes called '**Rectangle**' and '**Circle**' that implement the '**Shape**' interface by providing an implementation for the '**area()**' method.

*Notice how the two implementations are different from eachother.*

Finally, we define a function called '**calculateTotalArea()**' that takes an array of '**Shape**' objects and calculates the total area of all the shapes. We can then create instances of the '**Rectangle**' and '**Circle**' classes and pass them to the '**calculateTotalArea()**' function to get the total area of all the shapes.

By using the '**Shape**' interface, we can define a contract that both the '**Rectangle**' and '**Circle**' classes must follow. This allows us to write code that is more modular and reusable, as we can pass any object that implements the '**Shape**' interface to the '**calculateTotalArea()**' function. Additionally, by using the interface, the TypeScript compiler can perform static type checking and catch errors at compile-time.