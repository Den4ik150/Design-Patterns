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
Копировать код
Accounts.countAccounts = () => {
    return Accounts.allAccounts.length;
};
```
-**Purpose**
- Static methods and properties are useful when the functionality or property pertains to the class as a whole rather than to any individual instance.
</details>

<details>
  <summary>Public and Private Fields</summary>
  
  - Summary to be added...
</details>

<details>
  <summary>Extending Classes</summary>
  
  - Summary to be added...
</details>

<details>
  <summary>Mixing-in Classes</summary>
  
  - Summary to be added...
</details>

<details>
  <summary>Accessing a Super-Class</summary>
  
  - Summary to be added...
</details>

<details>
  <summary>The Prototype Pattern</summary>
  
  - Summary to be added...
</details>

<details>
  <summary>When to Use the Prototype Pattern</summary>
  
  - Summary to be added...
</details>

<details>
  <summary>The Revealing Module Pattern</summary>
  
  - Summary to be added...
</details>

<details>
  <summary>The Conventional Module Pattern</summary>
  
  - Summary to be added...
</details>

<details>
  <summary>When to Use the Conventional Module Pattern</summary>
  
  - Summary to be added...
</details>

<details>
  <summary>The Singleton Class Pattern</summary>
  
  - Summary to be added...
</details>

<details>
  <summary>When to Use the Singleton Class Pattern</summary>
  
  - Summary to be added...
</details>

<details>
  <summary>Planning and Harmony</summary>
  
  - Summary to be added...
</details>

<details>
  <summary>Summary</summary>
  
  - Summary to be added...
</details>
