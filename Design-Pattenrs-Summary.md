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

- **In this example, the Model holds the data and updates it, while the View renders the updated data to the user. The Controller mediates between the two, responding to user actions (like clicking a button) and triggering updates in both the model and the view**.

### Why Separation Matters

- **Separating concerns across models, views, and controllers allows for better maintainability and scalability**:
- **Model**: Focuses solely on data and business rules, without worrying about how it's displayed.
- **View**: Deals only with rendering the data, without understanding the underlying logic.
- **Controller**: Manages communication between the model and view, orchestrating the flow of information and actions.

This separation helps developers understand where to add features or fix bugs, reducing the risk of accidentally affecting other parts of the codebase.
</details>

<details>
  <summary>A Working Example of MVC</summary>
  
  - Summary to be added...
</details>

<details>
  <summary>MVVM</summary>
  
  - Summary to be added...
</details>

<details>
  <summary>MV* and the Nature of Software</summary>
  
  - Summary to be added...
</details>

<details>
  <summary>JavaScript Modules</summary>
  
  - Summary to be added...
</details>

<details>
  <summary>Modular Design Patterns</summary>
  
  - Summary to be added...
</details>

<details>
  <summary>Constructor Patterns</summary>
  
  - Summary to be added...
</details>

<details>
  <summary>When to Use the Constructor Pattern</summary>
  
  - Summary to be added...
</details>

<details>
  <summary>Inheritance with the Constructor Pattern</summary>
  
  - Summary to be added...
</details>

<details>
  <summary>The Class Pattern</summary>
  
  - Summary to be added...
</details>

<details>
  <summary>When to Use the Class Pattern</summary>
  
  - Summary to be added...
</details>

<details>
  <summary>Static Methods</summary>
  
  - Summary to be added...
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
