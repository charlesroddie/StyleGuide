# F# Style Guide (writen for MathSpire)
(in progress)

## Objectives
* Easy to understand 
* Easy to modify and extend
* Correct function
* (Good performance)

## Methods and Rules

### Simplicity
* Come up with multiple aproaches and **choose the simplest** one.
* Don't look for higher performance at the cost of more complex code.
* If additional minor features require greater complexity they should be abandoned.

### Clear definitions
* **Code should be readable** in order and understandable by an intellgent programmer.
* **Each definition should reflect a concept** and its meaning and purpose should be clear / simply explained in comments.
* Functions should have **simple type signatures** which are natural and informative about the function's purpose.
* **Appropriate naming**
* Concise **XML documentation and comments**, explaining what is not immediately obvious. Only after making as much as possible immediately obvious through naming, type signatures, and location.

### Code structure
* Place code in the **natural or expected locations**. (close to where they are used, with similar definitions)
* **Encapsulation through objects.** When data and methods are more complex than their purpose or the thing they are modelling, define a class, expose the purpose through members, and hide the implementation.
* **Scoping.** Where possible move a definition into into a narrower context where it is only visible by code that needs to see it.
    This reduces the noise of irrelevant definitions in the broader context and increases intelligibility of the moved definitions.
```fsharp
//Bad
let glass = …
let w = window(glass)
let bricks = …
let myHouse = house(w,b)

//Good
let myHouse =
    let w =
        let glass = …
        window(glass)
    let bricks = …
    house(w,b)
```
* Do not stop work when code works. Stop work when code works and is beautiful.
## F# Gives
* A linear structure, so to understand a definition you need to understand only previous definitions.
* A requirement to think before coding, especially about the structure of data.
* Static typing, where code that type-checks usualy works.
* The ability to express concepts faithfully using functional and discriminated union types.
* Less complexity via default immutability.
* Concision
* Performance esp. with AOT compilation
* Good interoperability with .Net Libraries

## F# Style
* Indent by four spaces and usually keep indentation levels as a multiple of 4.
* Tupled functions are preferred unless partial application will be used, when curried functions must be used.
* Classes are preferred over records unless structural equality is needed, when records are convenient.
* Locally-confined mutability is fine and sometimes gives better performance and readability compared with pure functional approaches.
* Left to right flow to help type inference.
* To improve AOT compatibility, increase explicitness and improve performance, minimize use of reflection outside of debug code.
* Avoid single-case DUs.
* Follow the [F# Style Guide](https://docs.microsoft.com/en-us/dotnet/fsharp/style-guide/).

## UI
* **Views/ViewModels**
  * Move as much logic as possible from Views (which a UI framework dependency) to ViewModels (which don't)
  * This usually results in a cleaner structure, and minimizes the work to target another UI framework.
* To handle mutable state use a **reactive** approach (Gjallarhorn)

## Code Smells
* Classes that **expose implementation details**
* Types whose intention or structure **cannot be understood without reading ahead**. E.g. types that don't seem natural for their purpose and whose explanation requires an explanation of how they are going to be used.
* **Downcasting**
* Usage of **strings as identifiers**, or anything else that **circumvents the type system**. (MVVM bindings are ruled out by this.)
