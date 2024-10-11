# Design Patterns in JavaScript

This repository provides a concise summary of Design Patterns in JavaScript. It outlines key concepts and practical implementations of various patterns to improve code structure, maintainability, and efficiency.

# Design-Patterns

Design Patterns in JavaScript are reusable solutions to common coding problems. They help structure code for better readability and maintainability. Common patterns include Creational (e.g., Singleton), Structural (e.g., Adapter), and Behavioral (e.g., Observer). Using these patterns improves scalability and efficiency in software design.

### Design Patterns

<details>
  <summary>The Perspective of a Designer</summary>
  
- In software design, focusing on the user (another programmer) helps guide decisions. For example, a function designed to count occurrences of a substring could be written in multiple ways:

```js
function countNeedlesInHaystack(needle, haystack) {
    return haystack.split(needle).length - 1;
}
```
Design choices: Function names, parameters, and syntax all influence usability. Different patterns like object-oriented programming or function-based approaches can be used for the same problem.
```js
class Haystack {
    constructor(haystack) {
        this.haystack = haystack;
    }
    count(needle) {
        return this.haystack.split(needle).length - 1;
    }
}
```

## Characteristics of Good Design Patterns

- **Solves the problem well**: Aligns with the problem domain and makes it easier to express the solution.
- **Familiar and usable**: Other developers can quickly understand and use it.

## Hierarchical Patterns

Patterns can exist on both micro (small functions or components) and macro levels (entire system architectures). 

### For example:

- **Micro level**: Writing utility functions or modules using patterns.
- **Macro level**: Architectures like Model-View-Controller (MVC) for organizing entire applications.

## Familiarity and Maintainability

- Familiar design patterns allow for easy understanding and extension of code. A well-structured directory, like having an app/, models/, and utils/ folder, is also a pattern that enhances maintainability.

```js
// Conventional module pattern
const logger = {
    log: function (msg) {
        console.log(msg);
    }
};
```

```js
module.exports = logger;
```

## Popular JavaScript Design Patterns

- **Modular design**: Separating code into reusable modules.
```js
const myModule = (function () {
    let privateVar = "secret";
    return {
        publicMethod: function () {
            return privateVar;
        }
    };
})();
```

- **Factory pattern**: Creating objects without specifying the exact class of object that will be created.

```js
function CarFactory(type) {
    if (type === 'sedan') return new Sedan();
    if (type === 'SUV') return new SUV();
}
```
## Selecting the Right Design Pattern

- Effective design requires selecting the right pattern for the given context. Patterns should improve:

- **Reliability**: Reduces complexity, makes logic easy to follow.
- **Efficiency**: Streamlines code structure, minimizes time spent on organization.
- **Maintainability**: Adaptable to future changes or bug fixes.
- **Usability**: Easy to understand and integrate by other developers.

## Beware of Bad Patterns
- **Cargo culting**: Avoid copying patterns without understanding their purpose or context.
</details>

<details>
  <summary>Architectural Design Patterns</summary>
  
Architectural design patterns define how different parts of a codebase interact and communicate. As JavaScript frameworks like React and Angular evolve, these patterns influence the structure and flow of modern applications.

### Key Concepts
- **Architectural design patterns**: Define how modules communicate and work together in an application.
- **Modern frameworks**: React, Angular, and Vue often rely on similar architectural patterns, especially in separating data logic from rendering logic.

### The Importance of Separation
One of the most common architectural principles is the **separation of data logic and rendering logic**. This allows for more modular, maintainable code by ensuring that each part of the application has a distinct role. 

For example:
- **Data logic** deals with fetching, managing, and processing data.
- **Rendering logic** focuses on how the data is presented to the user.

This concept has its roots in the early **MVC (Model-View-Controller)** pattern, which is still widely used and forms the basis of many modern architectures.
</details>

<details>
  <summary>MVC</summary>
  
### MVC (Model-View-Controller)
**MVC** is a well-established architectural pattern that helps separate concerns in an application by splitting it into three main components:
1. **Model**: Manages the data and business logic. Any changes to the data affect the view.
2. **View**: Handles the presentation of data to the user. It interacts with the controller when user actions occur.
3. **Controller**: Acts as the intermediary between the model and the view, updating the model based on user actions and ensuring the view reflects the latest data.

</details>

<details>
  <summary>A Working Example of MVC</summary>
  
#### MVC Example: Mutable Number Application

```js
// Model: Manages data and logic for incrementing/decrementing a number
class MutableNumberModel {
    constructor(value) {
        this.value = value;
    }
    increment() {
        this.value++;
        this.onChangeCallback();
    }
    decrement() {
        this.value--;
        this.onChangeCallback();
    }
    registerChangeCallback(onChangeCallback) {
        this.onChangeCallback = onChangeCallback;
    }
}

// Controller: Bridges the model and view, handling interactions
class MutableNumberController {
    constructor(model, view) {
        this.model = model;
        this.view = view;
        this.model.registerChangeCallback(() => this.view.renderUpdate());
        this.view.registerIncrementCallback(() => this.model.increment());
        this.view.registerDecrementCallback(() => this.model.decrement());
    }
}

// View: Renders the number and listens for user actions
class MutableNumberView {
    constructor(model) {
        this.model = model;
    }
    registerIncrementCallback(onIncrementCallback) {
        this.onIncrementCallback = onIncrementCallback;
    }
    registerDecrementCallback(onDecrementCallback) {
        this.onDecrementCallback = onDecrementCallback;
    }
    renderUpdate() {
        this.numberSpan.textContent = this.model.value;
    }
    renderInitial() {
        this.container = document.createElement('div');
        this.numberSpan = document.createElement('span');
        this.incrementButton = document.createElement('button');
        this.decrementButton = document.createElement('button');
        
        this.incrementButton.textContent = '+';
        this.decrementButton.textContent = '-';
        this.incrementButton.onclick = () => this.onIncrementCallback();
        this.decrementButton.onclick = () => this.onDecrementCallback();

        this.container.appendChild(this.numberSpan);
        this.container.appendChild(this.incrementButton);
        this.container.appendChild(this.decrementButton);

        this.renderUpdate();
        return this.container;
    }
}

// Initialize and connect MVC components
const model = new MutableNumberModel(5);
const view = new MutableNumberView(model);
const controller = new MutableNumberController(model, view);
document.body.appendChild(view.renderInitial());
```

- In this example, the Model holds the data and updates it, while the View renders the updated data to the user. The Controller mediates between the two, responding to user actions (like clicking a button) and triggering updates in both the model and the view**.

### Why Separation Matters

- **Separating concerns across models, views, and controllers allows for better maintainability and scalability**:
- **Model**: Focuses solely on data and business rules, without worrying about how it's displayed.
- **View**: Deals only with rendering the data, without understanding the underlying logic.
- **Controller**: Manages communication between the model and view, orchestrating the flow of information and actions.

This separation helps developers understand where to add features or fix bugs, reducing the risk of accidentally affecting other parts of the codebase.
</details>

<details>
  <summary>MVVM</summary>
  
### Overview:
- **MVVM (Model-View-ViewModel)** is a design pattern similar to MVC, focusing on a clear separation between business logic, data, and UI rendering.
- It is commonly used in front-end development due to its ability to handle constantly updated views.

### MVVM Structure:
1. **Model**:
   - Represents the data and business logic.
   - Any changes in the Model will trigger updates in the View through data binding.
   
2. **View**:
   - Describes how the data is presented (structure, layout, and appearance).
   - Interacts with the **ViewModel** via a **Data Binding** mechanism.

3. **ViewModel**:
   - Acts as the intermediary between Model and View.
   - Facilitates communication through data binding.
   - Listens for changes in the Model and updates the View accordingly.

### Key Features:
- **Data Binding**: The core mechanism that synchronizes the Model and View. Changes in the Model reflect in the View, and user interactions in the View can update the Model.
- **Constant View Updates**: MVVM is well-suited for applications where the view must frequently change based on data mutations.

### Example in JavaScript Frameworks:
- **Angular**:
  - Utilizes **ng-model** for two-way data binding.
  - Example: `<input ng-model="dataModel">` allows changes in the Model to automatically update the input field and vice versa.

### Comparison with MVC:
- **MVVM** is more suitable for front-end applications with dynamic views.
- **MVC** is often preferred on the back-end due to its simpler, render-once nature.
</details>

<details>
  <summary>MV* and the Nature of Software</summary>
  
### Overview:
- **MV* (MVC, MVVM, and their variations)** are foundational patterns that JavaScript developers frequently encounter.
- These patterns revolve around the fundamental aspects of software: **input**, **processing**, and **output** of data.

### Key Concepts:
- **Input**: Data enters the system (e.g., user actions).
- **Processing**: Business logic handles and mutates the data.
- **Output**: The processed data is rendered or displayed to the user.

### Commonality of MV* Patterns:
- Variations of MVC and MVVM consistently arise due to their flexibility and clear separation of concerns.
- These patterns guide developers in structuring software systems to separate **data logic** from **presentation** effectively.

### Conclusion:
- Regardless of how systems are architected, most solutions will adopt principles similar to MVC or MVVM, organizing the code to manage the flow of data, its processing, and how it is presented.

</details>

<details>
  <summary>JavaScript Modules</summary>
  
# JavaScript Modules

### Overview:
- **Modules** in JavaScript used to refer to distinct, self-contained pieces of code within a file.
- **Modern Modules** follow the ECMAScript specification, where modules are separate files that can be imported and exported.

### Key Concepts:
1. **Exporting**:
   - Default export: `export default [item]` allows import with any local name.
   - Named export: `export { item as alias }` requires specifying the exact name when importing.
   - Example:
     ```javascript
     // Exporting in DropdownComponent.js
     export default DropdownComponent;
     ```

2. **Importing**:
   - Import default: 
     ```javascript
     import MyDropdown from './DropdownComponent.js';
     ```
   - Import named: 
     ```javascript
     import { MyClass as TheClass } from './things.js';
     ```

3. **Aggregating Exports**:
   - Group multiple exports into an `index.js` file for convenience:
     ```javascript
     // components/index.js
     export { default as DropdownComponent } from './DropdownComponent.js';
     export { default as AccordianComponent } from './AccordianComponent.js';
     ```

4. **Usage**:
   - Import everything from a file:
     ```javascript
     import * from 'components/index.js';
     ```

### Notes:
- **In Browsers**: Use `<script type="module">` for module support.
- **In Node.js**: Use `.mjs` extension or `--experimental-modules` flag for ES Modules.

</details>

<details>
  <summary>Modular Design Patterns</summary>
  

### Definition
- **Modular Design Patterns** refer to structures and conventions used to create individual JavaScript modules, each serving a specific abstraction.

### Key Principles
- **Single Responsibility**: Each module (file) should export a distinct abstraction.
- **File Structure**: Organize your directory and file structure to reflect the different abstractions clearly.

### Best Practices
- **Separation of Concerns**: Avoid cramming multiple abstractions into a single file. 
- If you find yourself repeating patterns within the same file, consider splitting them into separate modules for better clarity and maintainability.

</details>

<details>
  <summary>Constructor Patterns</summary>
  
### Definition
- The **Constructor pattern** involves using a constructor function to create objects and manually assigning methods to the prototype. It mimics classical OOP behavior in JavaScript.

### Key Concepts
1. **Constructor Function**:  
   - The object is created via a function, typically in the form of a function declaration:
     ```js
     function Book(title) {
       this.title = title;
     }
     ```
   
2. **Assigning to Prototype**:  
   - Methods are added to the prototype individually:
     ```js
     Book.prototype.getNumberOfPages = function() { /* ... */ };
     ```
   - Alternatively, the entire prototype is replaced with an object literal for cleaner code:
     ```js
     Book.prototype = {
       getNumberOfPages() { /* ... */ },
       renderFrontCover() { /* ... */ },
       renderBackCover() { /* ... */ }
     };
     ```

3. **Instantiation**:  
   - The `new` keyword is used to create a new instance:
     ```js
     const myBook = new Book('JavaScript Guide');
     ```

### Best Practice
- The second approach (replacing the prototype with an object literal) is preferred for its encapsulation and conciseness.

### Important Note
- This pattern was more common before the introduction of the `class` syntax in JavaScript.
</details>

<details>
  <summary>When to Use the Constructor Pattern</summary>
  
### Applicability
The **Constructor pattern** is suitable when you want to encapsulate a concept that:
- Is expressible as a noun (e.g., `NavigationComponent`, `StorageDevice`).
- Requires construction (you want to create instances).
- May vary between instances.

If the concept doesn’t fit these criteria (like a utility module with static methods), consider using another design pattern.

### Decline of Usage
The Constructor pattern is less favored since the introduction of the **class syntax** in JavaScript, which aligns more closely with traditional OOP languages.

</details>

<details>
  <summary>Inheritance with the Constructor Pattern</summary>
# Inheritance with the Constructor Pattern

### Basic Structure
To implement inheritance using the Constructor pattern, set up prototypes to create a prototypal tree. For example:

```js
function Animal() {}
Animal.prototype = {
  isAnimal: true,
  grow() {}
};

function Monkey() {}
Monkey.prototype = Object.create(Animal.prototype);
Monkey.prototype.isMonkey = true;
Monkey.prototype.screech = function() {};
```
- **Instantiation**
Instances of Monkey can access their own methods and those inherited from Animal:

```js
const monkey = new Monkey();
console.log(monkey.isAnimal); // true
console.log(monkey.isMonkey); // true
console.log(typeof monkey.grow); // "function"
console.log(typeof monkey.screech); // "function"
```

-**Bulk Assignment**

Instead of adding methods individually, you can use Object.assign() for a cleaner approach:

```js
Monkey.prototype = Object.assign(Object.create(Animal.prototype), {
  isMonkey: true,
  screech() {},
  groom() {}
});
```
</details>

<details>
  <summary>The Class Pattern</summary>
  
### Overview
The **Class pattern** is a modern approach in JavaScript, replacing the older Constructor pattern. It utilizes class definition syntax, making the language more expressive while still relying on the same prototypal mechanisms.

### Basic Structure
A class is defined using the `class` keyword. Here’s an example of a simple class representing a name:

```js
class Name {
  constructor(forename, surname) {
    this.forename = forename;
    this.surname = surname;
  }
  
  sayHello() {
    return `My name is ${this.forename} ${this.surname}`;
  }
}
```
-**Equivalent Constructor Function**

The class above can be translated into a traditional constructor function as follows:

```js
function Name(forename, surname) {
  this.forename = forename;
  this.surname = surname;
}

Name.prototype.sayHello = function() {
  return `My name is ${this.forename} ${this.surname}`;
};
```

- **Key Takeaway**
While the Class pattern offers a cleaner syntax, it functions similarly to the Constructor pattern. Both methods utilize the same underlying prototype system, so understanding the prototypal mechanism is still essential.
</details>

<details>
  <summary>When to Use the Class Pattern</summary>
  
### Appropriate Scenarios
The **Class pattern** is best utilized when:

1. **The concept is expressible as a noun:** It represents a distinct entity.
2. **The concept requires construction:** It needs to be instantiated to function.
3. **The concept will vary between instances:** Each instance should have unique properties.

### Examples of Suitable Concepts
- **Database Record:** Represents a piece of data, allowing for inquiry and manipulation.
- **Todo Item Component:** Represents a todo item, enabling it to be rendered.
- **Binary Tree:** Represents a binary-tree data structure.

### Evaluation Tips
If you're unsure whether to use the Class pattern, try writing some consumer code (pseudo code) that utilizes your abstraction. If it feels logical and easy to use, then the Class pattern is likely appropriate.

</details>

<details>
  <summary>Static Methods</summary>
  
### Definition
**Static methods and properties** are defined using the `static` keyword within a class. They are associated with the class itself rather than with instances of the class.

### Example
```javascript
class Accounts {
    static allAccounts = [];
    
    static tallyAllAccounts() {
        // ...
    }
}

// Usage
Accounts.tallyAllAccounts();
Accounts.allAccounts; // => []
```
## Adding Static Methods After Definition

- Static methods can also be added after the class has been defined:

```javascript
Accounts.countAccounts = () => {
    return Accounts.allAccounts.length;
};
```
-**Purpose**
- Static methods and properties are useful when the functionality or property pertains to the class as a whole rather than to any individual instance.
</details>

<details>
  <summary>Public and Private Fields</summary>
  ## Public Fields
- Public fields (properties) can be declared directly within the class definition:
    ```javascript
    class Rectangle {
        width = 100;
        height = 100;
    }
    ```
- These fields are initialized for each instance and are mutable. They are useful for setting sensible defaults, which can be overridden in the constructor:
    ```javascript
    class Rectangle {
        width = 100;
        height = 100;

        constructor(width, height) {
            if (width && !isNaN(width)) {
                this.width = width;
            }
            if (height && !isNaN(height)) {
                this.height = height;
            }
        }
    }
    ```

## Private Fields
- Private fields are declared with a `#` prefix:
    ```javascript
    class Rectangle {
        #width = 100;
        #height = 100;

        constructor(width, height) {
            if (width && !isNaN(width)) {
                this.#width = width;
            }
            if (height && !isNaN(height)) {
                this.#height = height;
            }
        }
    }
    ```
- Private fields are only accessible within the class itself. Sub-classes do not have access:
    ```javascript
    class Super {
        #private = 123;
    }

    class Sub {
        getPrivate() {
            return this.#private; // SyntaxError: Undefined private field
        }
    }
    ```

## Considerations
- JavaScript traditionally did not support private fields; programmers would use underscores (e.g., `_someProperty`) as a convention to indicate private properties.
- Use private fields cautiously, as they can limit code extensibility. Consider using pseudo-private fields with underscores if you want to allow some degree of access for extending classes.
</details>

<details>
  <summary>Extending Classes</summary>
  
## Inheritance
- Inheritance is achieved using the `class ... extends` syntax:
    ```javascript
    class Animal {}
    class Tiger extends Animal {}
    ```
- This syntax ensures that:
    - Each instance of `Tiger` has a `[[Prototype]]` that points to `Tiger.prototype`.
    - `Tiger.prototype` inherits from `Animal.prototype`.

## Prototype Chain Confirmation
- You can confirm the prototype chain using:
    ```javascript
    Object.getPrototypeOf(new Tiger()) === Tiger.prototype; // true
    Object.getPrototypeOf(Tiger.prototype) === Animal.prototype; // true
    ```
- This verifies the inheritance structure:
    - `new Tiger()` instances inherit from `Tiger.prototype`.
    - `Tiger.prototype` inherits from `Animal.prototype`.
      
</details>

<details>
  <summary>Mixing-in Classes</summary>
  
## Overview
- JavaScript lacks a native mixing-in mechanism, so mixing in methods can be achieved through:
  - Augmenting the prototype after class definition.
  - Inheriting from mixins as if they were superclasses.

## Augmenting Prototype
- You can augment a class's prototype using `Object.assign`:
    ```javascript
    const fooMixin = { foo() {} };
    const bazMixin = { baz() {} };
    class MyClass {}
    Object.assign(MyClass.prototype, fooMixin, bazMixin);
    ```
- **Limitation**: This method does not allow the class to override mixin methods:
    ```javascript
    class MyClass { foo() {} }
    Object.assign(MyClass.prototype, fooMixin, bazMixin);
    new MyClass().foo === fooMixin.foo; // true (not ideal)
    ```

## Inheritance for Mixing-in
- A better approach involves using subclass factories, which return a class extending a specified superclass:
    ```javascript
    const greetingsMixin = Super => class extends Super {
        hello() { return 'hello'; }
        hi() { return 'hi'; }
        heya() { return 'heya'; }
    };
    class Human {}
    class Programmer extends greetingsMixin(Human) {}
    new Programmer().hi(); // => "hi"
    ```

## Combining Multiple Mixins
- Implement a helper function to combine multiple subclass factories:
    ```javascript
    function mixin(...mixins) {
        return mixins.reduce((base, mixin) => {
            return mixin(base);
        }, Object);
    }
    ```
- **Usage**:
    ```javascript
    const alpha = Super => class extends Super { alphaMethod() {} };
    const bravo = Super => class extends Super { braveMethod() {} };
    class MyClass extends mixin(alpha, bravo) {
        myMethod() {}
    }
    ```
- **Result**: Instances of `MyClass` will have access to:
    - `myMethod` from `MyClass`.
    - `alphaMethod` from `alpha`.
    - `braveMethod` from `bravo`.

## Conclusion
- Mixing in methods can be tricky. Consider using libraries or established patterns to manage mixins effectively.
- Two approaches discussed:
  - Using `Object.assign()` to compose methods into a single prototype.
  - Creating an inheritance tree for a mixin hierarchy.
</details>

<details>
  <summary>Accessing a Super-Class</summary>
  
## Overview
- In classes defined using method definition syntax, the `super` binding provides access to the superclass and its properties.

## Calling the Super-Class Constructor
- The `super()` function calls the constructor of the superclass. If you define a constructor in a derived class, you **must** call `super()` before accessing or modifying `this`.

### Example:
```javascript
class Tiger extends Animal {
    constructor() {
        super(); // Call Animal's constructor
    }
}
```

- **Important Restrictions** 
Attempting to call super() after modifying the instance, or not calling it at all, will result in a ReferenceError:
```
javascript
class Tiger extends Animal {
    constructor() {
        this.someProperty = 123; // Error occurs here
        super();
    }
}
new Tiger();
// ! ReferenceError: You must call the super constructor in a derived class before accessing 'this' or returning from the derived constructor
```
- **Additional Information** 
T
he super binding and its peculiarities are discussed in more detail in Chapter 6, Primitives and Built-in Types (Function bindings section).

</details>

<details>
  <summary>The Prototype Pattern</summary>
  
## Overview
- The Prototype pattern uses plain objects as templates for other objects, allowing for direct extension without instantiation via `new` or `Constructor.prototype`.

## Creating a Template
- Begin by creating a template object that contains all methods and properties related to your abstraction.
  
### Example Template:
```javascript
const inputComponent = {
    name: 'Input Component',
    render() {
        return document.createElement('input');
    }
};
``` 
-**Convention**: Template objects start with a lowercase letter; constructor functions start with an uppercase letter.
## Instantiating Objects
Create specific instances using Object.create():
```
javascript
const inputA = Object.create(inputComponent);
const inputB = Object.create(inputComponent);
```

This sets the new object's internal [[Prototype]] to the template, allowing property access from the prototype.

-**Accessing Methods**:

```javascript
inputA.render(); // Calls the render method from inputComponent
Simplifying Object Creation
Introduce a method to the template for creating instances:

```javascript
inputComponent.extend = function() {
    return Object.create(this);
};
```
-**Create instances with less code**:
```javascript
const inputA = inputComponent.extend();
const inputB = inputComponent.extend();
```
-**Extending the Template**
To create new types of inputs, extend the template:
```javascript
const numericalInputComponent = Object.assign(inputComponent.extend(), {
    render() {
        const input = inputComponent.render.call(this);
        input.type = 'number';
        return input;
    }
});
```
**Note**: Use call() to reference and invoke the parent method, as super cannot be used in this context.
-**Naming Confusion**
The Prototype pattern may be better referred to as the Object Extension Pattern or No-Constructor Approach to Prototypal Inheritance, as it is less commonly used compared to classical OOP patterns.
</details>

<details>
  <summary>When to Use the Prototype Pattern</summary>
  
## When to Use
The Prototype pattern is best used when:
- You need an abstraction that **varies between instances** but **does not require construction**.
- Objects are semantically related through **inheritance** rather than instantiation.

## Key Features
- The Prototype pattern is based on extending objects using `Object.create`.
- It provides **inheritance** without requiring constructors or class-based instantiation.

## Example Scenario
Consider a sandwich object `theBLT`:
```javascript
const theBLT = {
  name: 'The BLT',
  breadType: 'Granary',
  slotA: 'Bacon',
  slotB: 'Lettuce',
  slotC: 'Tomato'
};
```
To create a variation of theBLT, like a BLT with Avocado instead of Tomato:

```javascript
const theBLA = Object.assign(Object.create(theBLT), {
  slotC: 'Avocado'
});
```
Here, theBLA inherits from theBLT, so any changes to theBLT (e.g., bread type) will reflect in theBLA:

```javascript
theBLT.breadType = 'Sourdough';
theBLA.breadType; // => 'Sourdough'
```
**Advantages**
- Simplifies inheritance for objects without needing constructors.
- Less clunky code compared to using full classes for simple objects.

**Potential Pitfalls**
- If misapplied, the Prototype pattern can add complexity rather than simplifying the code.

**Best Used For**
Objects with simple, varying data where full class-based inheritance may be overkill.


## Best Use Cases
- **Data models** where small variations exist between objects, but these objects share a significant amount of **common structure**.
- **Configuration objects** or objects with **reusable behavior** that can be shared across multiple instances.
- **Avoiding constructor overhead** when creating objects with similar properties and behaviors, but without needing complex class hierarchies.

## Summary
The Prototype pattern is useful when you need **simple inheritance** without the need for constructors or classes. It works well in scenarios where objects share common traits but may differ slightly. With the Prototype pattern, you can easily create object extensions 
and variations while maintaining inheritance relationships that automatically reflect changes in parent objects. However, care must be taken to avoid over-complicating the design when simpler solutions may suffice.

</details>

<details>
  <summary>The Revealing Module Pattern</summary>
  
  
### Main Concept
The **Revealing Module pattern** is used to **encapsulate private logic** and expose a **public API**. It typically involves an **Immediately Invoked Function Expression (IIFE)** that returns an object containing **public methods and properties**.

### Structure
1. **Private Variables/Functions**: Encapsulated logic within the IIFE.
2. **Public API**: Exposes only specific methods or properties for external use.

```javascript
const myModule = (() => {
  const privateFoo = 1;  // Private variable
  const privateBaz = 2;  // Private variable
  return {
    publicFoo() {},       // Public method
    publicBaz() {}        // Public method
  };
})();
```
## Features
- **Encapsulation**: Only the returned object exposes public methods, keeping other logic private.
- **Closure**: Public methods form a closure around the private variables, allowing access to the private scope.

**Example**: Notification Component
- A simple DOM component using the Revealing Module pattern to display a notification message.

```javascript
const notification = (() => {
  const d = document;
  const container = d.body.appendChild(d.createElement('div'));
  const message = container.appendChild(d.createElement('p'));
  const dismissBtn = container.appendChild(d.createElement('button'));
  
  container.className = 'notification';
  dismissBtn.textContent = 'Dismiss!';
  
  dismissBtn.onclick = () => {
    container.style.display = 'none';
  };
  
  return {
    display(msg) {
      message.textContent = msg;
      container.style.display = 'block';
    }
  };
})();

notification.display('Hello user! Something happened!');
```

- **Best Use Cases**
- When you need to separate private and public logic.
- When there is specific initialization logic that doesn’t fit well with object-oriented patterns like Class or Constructor patterns.

- **Considerations**
- With the introduction of class definitions and private fields (#private) in JavaScript, the Revealing Module pattern has fallen out of favor.
- It can still be used due to aesthetic preferences but is less common in modern JavaScript practices.

- **Summary**
The Revealing Module pattern is useful for creating privacy and encapsulation in JavaScript, especially before modern class features. While its usage has declined, it still offers a simple, clear mechanism for separating private logic from the public API.
</details>

<details>
  <summary>The Conventional Module Pattern</summary>
  
### Main Concept
The **Conventional Module pattern** uses **plain object literals** to create a collection of methods. This approach is **simple** and **flexible** as it leverages JavaScript’s ability to treat functions as **first-class citizens**.

### Structure
- A plain object literal containing methods.
- Optionally includes methods for **initialization** (`initialize`, `init`, `setup`) or **configuration** (`setConfig`).

```javascript
const timeDiffUtility = {
  setConfig(config) {
    this.config = config;
  },
  minutesBetween(dateA, dateB) {},
  hoursBetween(dateA, dateB) {},
  daysBetween(dateA, dateB) {}
};
```

## Features
-**Plain Object**: The module is a plain object, making it easy to manage and extend.
-**Flexibility**: Methods can be composed from external functions and inserted into the module directly.

```javascript
const log = () => console.log(this);
const library = {
  books: [],
  addBook() {},
  log // Added external log method
};
```
## Advantages
-**Easy Composition**: You can simply add or reference functions from outside the module, avoiding complex inheritance or mixins.
-**Simple Design**: Ideal for utility modules that don't require instantiation or object-oriented structures.

## Best Use Cases
- When you need a straightforward collection of methods.
- Utility modules that require static methods without needing object creation.

## Summary
- The Conventional Module pattern is a flexible and lightweight approach to organizing related methods in JavaScript. It’s ideal for simple utility modules and leverages JavaScript’s functional composition to add methods dynamically.
</details>

<details>
  <summary>When to Use the Conventional Module Pattern</summary>
  
 ### Key Use Case
The **Conventional Module pattern** is most effective when you want to **group related methods** or properties under a common name. It’s typically used for utility collections or simple abstractions.

### Examples
- **Logging utilities**:
  ```javascript
  const logger = {
    log(message) { /* ... */ },
    warn(message) { /* ... */ },
    error(message) { /* ... */ }
  };
  ```
## Features
- **Grouping of related methods**: Easily encapsulates common functionality under one object.
- **No need for construction**: This pattern is just a plain object, so no need for instance creation or complex abstractions.

## Best Scenarios
- When you need a collection of utility methods that work together, like logging, date formatting, etc.
- For modules that don’t require instantiation or inheritance.

## Summary
The Conventional Module pattern is a simple and effective way to group related methods into a common object. It’s ideal for utility modules and doesn't require the complexity of class-based patterns or object creation.

</details>

<details>
  <summary>The Singleton Class Pattern</summary>
  

### Key Use Case
The **Singleton Class pattern** allows you to **create utility objects** or **singleton instances** using a class definition, encapsulating initialization logic in the constructor.

### Features
- **Encapsulation**: Initialization logic can be defined in the constructor, providing a structured setup for private variables and public methods.
- **Immediate Instantiation**: The class is instantiated immediately, creating a singleton-like instance with private and public methods.
- **Similar to Revealing Module Pattern**: Like an IIFE, it encapsulates logic but leverages the class constructor for setup and private variables.

### Example
```javascript
const utils = new class {
  constructor() {
    this.#privateThing = 123;
    // Other initialization logic here...
  }
  utilityA() {}
  utilityB() {}
  utilityC() {}
};
utils.utilityA();
```

## Best Scenarios
- When you need a singleton utility object with both private and public methods.
- To encapsulate initialization logic and ensure it runs only once upon instantiation.

## Summary
The Singleton Class pattern offers an easy way to define utility objects with encapsulation and initialization logic. It's a flexible approach for creating singletons without requiring traditional instantiation or inheritance patterns.

</details>

<details>
  <summary>When to Use the Singleton Class Pattern</summary>
  
### Key Use Case
The **Singleton Class pattern** is used when **only one instance** of a class is required throughout the application.

### Common Use Cases
- **Utilities**: Centralized tools or helper methods.
- **Logging**: A single instance to manage application-wide logging.
- **Caching**: A unified caching mechanism.
- **Global Event Buses**: Handling global events through one instance.

### Features
- **Single Instance**: Ensures that only one instance of the class exists.
- **Encapsulation**: Allows for private variables and initialization logic in the constructor.
- **Flexible Initialization**: Like the Conventional or Revealing Module patterns, but with class-based structure.

### Summary
Use the **Singleton Class pattern** when you need a **single, globally accessible instance** of a class, often for purposes like utilities, logging, or global event management.
</details>

<details>
  <summary>Planning and Harmony</summary>
  
 ### Key Considerations
When deciding on architectural and modular design patterns, it’s essential to recognize that projects evolve, and initial decisions may need adaptation. Keep in mind these principles to maintain **harmony** and **consistency** in your codebase.

### Key Principles

1. **Expect Change and Adaptation**  
   - Every project will undergo change. Instead of trying to create the "One True Solution" from the start, focus on iterating and refining your design. Be flexible and open to revising initial judgments.

2. **Consult with Other Programmers**  
   - Collaborate with teammates and other stakeholders who will interact with your code. Their insights can provide valuable feedback, ensuring that your design choices are well-informed.

3. **Avoid Cargo Culting and Ego**  
   - Be cautious of blindly adopting patterns or methodologies simply because they are familiar. Avoid allowing your ego to influence design decisions, which might lead to poor choices based on personal preferences rather than suitability.

4. **Bias Toward Harmony and Consistency**  
   - Strive for harmony in your architecture. While customization is possible, too many inconsistencies can make maintenance difficult and decrease the overall quality and reliability of the codebase.

### Summary
When designing a system, prioritize flexibility, collaboration, and consistency to achieve long-term maintainability and productivity.
</details>

<details>
  <summary>Summary</summary>
  
 In this chapter, we delved into the **purpose** and **application** of design patterns in JavaScript. We discussed:

- The foundational concepts of **design patterns**.
- Various **modular** and **architectural patterns** commonly used in JavaScript.
- Different ways to declare abstractions using JavaScript’s **native mechanisms** like **classes** and **prototypes**.
- Other mechanisms like the **Revealing Module pattern**.

This comprehensive coverage equips us with a wide range of options to craft effective abstractions.
</details>
