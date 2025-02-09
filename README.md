
## SOLID Principles With Swift

### 1. Single Responsibility Principle (SRP)

*   **Definition:** "A class should have one, and only one, reason to change."
*   **Goal:** To promote high cohesion and low coupling, leading to easier maintenance and reduced risk of bugs.

### 2. Open/Closed Principle (OCP)

*   **Definition:** "Software entities (classes, modules, functions, etc.) should be open for extension, but closed for modification."
*   **Goal:** To allow adding new functionality without altering existing code, preventing unexpected side effects.
*   **How:** Achieved through abstraction and polymorphism (e.g., using interfaces/protocols and inheritance).
*   **Example:**
    ```swift
    protocol Shape {
        func area() -> Double
    }

    class Rectangle: Shape {
        var width: Double
        var height: Double

        init(width: Double, height: Double) {
            self.width = width
            self.height = height
        }

        func area() -> Double {
            return width * height
        }
    }

    class Circle: Shape {
        var radius: Double

        init(radius: Double) {
            self.radius = radius
        }

        func area() -> Double {
            return .pi * radius * radius
        }
    }
    ```
    Here we can add new shapes conforming to the `Shape` protocol without modifying existing shapes.

### 3. Liskov Substitution Principle (LSP)

*   **Definition:** "Objects of a superclass should be able to be replaced with objects of its subclasses without affecting the correctness of the program."
*   **Goal:** Ensure inheritance is used correctly, maintaining the integrity of the program when subclasses are used in place of their superclasses.
*   **How:** Subclasses must adhere to the contract of their superclasses, maintaining pre- and post-conditions.
*   **Example (Violation):** Consider a `Bird` class with a `fly()` method. A `Penguin` class inheriting from `Bird` would violate LSP because penguins cannot fly. A better design would be to separate the flying behavior into a separate abstraction (e.g., a protocol) that only birds capable of flight implement.

### 4. Interface Segregation Principle (ISP)

*   **Definition:** "Clients should not be forced to depend on methods they do not use."
*   **Goal:** Prevent classes from being forced to implement interfaces they don't need, leading to cleaner and more focused interfaces.
*   **How:** Break down large interfaces into smaller, more specific ones, so that clients only need to implement the interfaces that are relevant to them.
*   **Example:**
    ```swift
    protocol Worker {
        func work()
        func eat()
    }

    class Human: Worker {
        func work() {
           // Human Work Logic
        }
        func eat() {
           // Human Eat Logic
        }
    }

    class Robot: Worker {
        func work() {
            // Robot work logic
        }
        func eat() {
           // Robot cant eat, so it should not implement this
        }
    }
    ```
    Here `Robot` class is forced to implement `eat()` method, to avoid this scenario you can create separate interfaces `Workable` and `Eatable`.

### 5. Dependency Inversion Principle (DIP)

*   **Definition:**
    *   "High-level modules should not depend on low-level modules. Both should depend on abstractions."
    *   "Abstractions should not depend on details. Details should depend on abstractions."
*   **Goal:** Decouple high-level modules from low-level modules, making the system more flexible and maintainable.
*   **How:** Introduce abstractions (e.g., interfaces/protocols) between high-level and low-level modules, and depend on these abstractions instead of concrete implementations.
*   **Example:**
    ```swift
    protocol DataProvider {
        func getData() -> String
    }

    class APIClient: DataProvider {
        func getData() -> String {
            // Fetch data from API
            return "Data from API"
        }
    }

    class DataProcessor {
        let dataProvider: DataProvider

        init(dataProvider: DataProvider) {
            self.dataProvider = dataProvider
        }

        func processData() {
            let data = dataProvider.getData()
            // Process the data
            print("Processing data: \(data)")
        }
    }

    // Usage
    let apiClient = APIClient()
    let dataProcessor = DataProcessor(dataProvider: apiClient)
    dataProcessor.processData()
    ```
    `DataProcessor` depends on the `DataProvider` abstraction, not the concrete `APIClient`. This makes it easy to switch to a different data source (e.g., a local database) without modifying `DataProcessor`.
