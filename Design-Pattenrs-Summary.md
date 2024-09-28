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
  
  - Summary to be added...
</details>

<details>
  <summary>MVC</summary>
  
  - Summary to be added...
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
