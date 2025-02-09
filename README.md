## SOLID Principles

### 1. Single Responsibility Principle (SRP)

*   **Definition:** "A class should have one, and only one, reason to change."
*   **Goal:** To promote high cohesion and low coupling, leading to easier maintenance and reduced risk of bugs. Each class or module is responsible for one part of the software’s functionality.
*   **Key aspects of SRP:**
    *   Each class or module should have a single, well-defined responsibility, encapsulated within that class.
    *   A class should not have multiple responsibilities, as this can make it harder to understand and modify.
    *   Following SRP makes code easier to understand, maintain, and extend. It also reduces the risk of introducing bugs and makes it easier to test individual components in isolation.
    *   SRP encourages the separation of concerns, making the code more modular and scalable.
*   **Benefits of adhering to SRP:**
    *   **Maintainability:** SRP helps in creating code that is easier to maintain and update.
    *   **Testability:** With SRP, it is easier to test individual components in isolation.
    *   **Reduced Bugs:** SRP reduces the risk of introducing bugs when changes are made to the code.
    *   **Modularity:** SRP encourages the separation of concerns, making the code more modular and scalable.
    *   **Version Control:** SRP makes version control easier because updates to a feature only change related files.
*   **Example of violating SRP:**

    ```swift
    class Student {
        var name: String
        var email: String

        init(name: String, email: String) {
            self.name = name
            self.email = email
        }

        func registerStudent() {
            // Some logic
        }

        func calculateStudentResults() {
            // Some logic
        }

        func sendEmail() {
            // Some logic
        }
    }
    ```

    In this example, the `Student` class has three responsibilities: registering students, calculating their results, and sending emails. This violates the SRP because a class should only have one reason to change.

*   **Example of adhering to SRP:**

    ```swift
    class Student {
        var name: String
        var email: String

        init(name: String, email: String) {
            self.name = name
            self.email = email
        }
    }

    class StudentRegistrar {
      func register(student: Student) {
        // Registration logic
      }
    }

    class StudentResultCalculator {
      func calculateResults(student: Student) {
        // Calculation logic
      }
    }

    class EmailSender {
      func sendEmail(to: String, message: String) {
        // Email sending logic
      }
    }
    ```

    Here, each class has a single responsibility: `Student` represents student data, `StudentRegistrar` handles registration, `StudentResultCalculator` calculates results, and `EmailSender` sends emails.

### 2. Open/Closed Principle (OCP)

*   **Definition:** "Software entities (classes, modules, functions, etc.) should be open for extension, but closed for modification".
*   **Goal:** To allow adding new functionality without altering existing code, preventing unexpected side effects.
*   **How:** Achieved through abstraction and polymorphism (e.g., using interfaces/protocols and inheritance).
*   **Key aspects of OCP:**
    *   Allows adding new functionality without modifying existing code.
    *   Relies on abstractions to achieve extensibility.
    *   Reduces the risk of introducing bugs when adding new features.
*   **Benefits of adhering to OCP:**
    *   **Extensibility:** Makes it easy to add new features without modifying existing code.
    *   **Stability:** Reduces the risk of introducing bugs when adding new features.
    *   **Maintainability:** Code is easier to maintain because existing functionality is not affected by new changes.

*   **Example of adhering to OCP:**

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
*   **Example of Violating OCP:**

    ```swift
    class AreaCalculator {
        func calculateArea(shape: Any) -> Double {
            if let rectangle = shape as? Rectangle {
                return rectangle.width * rectangle.height
            } else if let circle = shape as? Circle {
                return .pi * circle.radius * circle.radius
            }
            return 0.0
        }
    }
    ```

    This violates OCP. To add a new shape, you'd have to modify the `calculateArea` function directly, adding more `if/else` statements.

### 3. Liskov Substitution Principle (LSP)

*   **Definition:** "Objects of a superclass should be able to be replaced with objects of its subclasses without affecting the correctness of the program."
*   **Goal:** Ensure inheritance is used correctly, maintaining the integrity of the program when subclasses are used in place of their superclasses.
*   **How:** Subclasses must adhere to the contract of their superclasses, maintaining pre- and post-conditions.
*   **Key aspects of LSP:**
    *   Subtypes must be substitutable for their base types without altering the desirable properties of the program.
    *   Guarantees that derived classes can be used interchangeably with their base classes.
    *   Promotes proper inheritance hierarchies and reduces unexpected behavior.
*   **Benefits of adhering to LSP:**
    *   **Maintainability:** Code is easier to maintain because subclasses can be used in place of their superclasses without causing errors.
    *   **Reusability:** Subclasses can be reused in different parts of the system without breaking existing functionality.
    *   **Reliability:** The system is more reliable because subclasses adhere to the contract of their superclasses.
*   **Example (Violation):** Consider a `Bird` class with a `fly()` method. A `Penguin` class inheriting from `Bird` would violate LSP because penguins cannot fly.
    ```swift
    class Bird {
        func fly() {
            print("Flying!")
        }
    }

    class Penguin: Bird {
        override func fly() {
            fatalError("Penguins can't fly!")
        }
    }

    func makeBirdFly(bird: Bird) {
        bird.fly()
    }

    let bird = Bird()
    let penguin = Penguin()

    makeBirdFly(bird: bird) // Output: Flying!
    makeBirdFly(bird: penguin) // Fatal error! This breaks the program
    ```
*   **Example of Adhering to LSP:**
    ```swift
    protocol Animal {
        func makeSound()
    }

    protocol Flyable {
        func fly()
    }

    class Bird: Animal, Flyable {
        func makeSound() {
            print("Chirp!")
        }

        func fly() {
            print("Flying!")
        }
    }

    class Penguin: Animal {
        func makeSound() {
            print("Squawk!")
        }
    }

    func animalSound(animal: Animal) {
        animal.makeSound()
    }

    let bird = Bird()
    let penguin = Penguin()

    animalSound(animal: bird) // Output: Chirp!
    animalSound(animal: penguin) // Output: Squawk!

    // Flyable check example:
    if let flyableBird = bird as? Flyable {
        flyableBird.fly() // Output: Flying!
    }
    ```
    Here,  `Penguin` only inherits the `Animal` protocol. This design respects LSP because we can now use `Animal` objects without assuming they can all `fly()`.

### 4. Interface Segregation Principle (ISP)

*   **Definition:** "Clients should not be forced to depend on methods they do not use."
*   **Goal:** Prevent classes from being forced to implement interfaces they don't need, leading to cleaner and more focused interfaces.
*   **How:** Break down large interfaces into smaller, more specific ones, so that clients only need to implement the interfaces that are relevant to them.
*   **Key aspects of ISP:**
    *   No client should be forced to depend on methods it does not use.
    *   Fewer, more specific interfaces are better than one general-purpose interface.
    *   Promotes loose coupling and increases code flexibility.
*   **Benefits of adhering to ISP:**
    *   **Flexibility:** Code is more flexible because clients only depend on the methods they need.
    *   **Maintainability:** Code is easier to maintain because interfaces are smaller and more focused.
    *   **Reusability:** Interfaces can be reused in different parts of the system without forcing clients to implement unnecessary methods.

*   **Example of Violating ISP:**

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

    Here `Robot` class is forced to implement `eat()` method, even though a robot doesn't eat.

*   **Example of Adhering to ISP:**

    ```swift
    protocol Workable {
        func work()
    }

    protocol Eatable {
        func eat()
    }

    class Human: Workable, Eatable {
        func work() {
            // Human Work Logic
        }

        func eat() {
            // Human Eat Logic
        }
    }

    class Robot: Workable {
        func work() {
            // Robot Work Logic
        }
    }
    ```

    Now, `Human` implements both `Workable` and `Eatable`, while `Robot` only implements `Workable`, adhering to ISP.

### 5. Dependency Inversion Principle (DIP)

*   **Definition:**
    *   "High-level modules should not depend on low-level modules. Both should depend on abstractions."
    *   "Abstractions should not depend on details. Details should depend on abstractions."
*   **Goal:** Decouple high-level modules from low-level modules, making the system more flexible and maintainable.
*   **How:** Introduce abstractions (e.g., interfaces/protocols) between high-level and low-level modules, and depend on these abstractions instead of concrete implementations.
*   **Key aspects of DIP:**
    *   High-level modules should not depend on low-level modules; both should depend on abstractions.
    *   Abstractions should not depend on details; details should depend on abstractions.
    *   Inversion of control is achieved through dependency injection or other mechanisms.
*   **Benefits of adhering to DIP:**
    *   **Flexibility:** Code is more flexible because high-level modules are not tied to specific implementations of low-level modules.
    *   **Testability:** Code is easier to test because dependencies can be easily mocked or stubbed.
    *   **Reusability:** Modules can be reused in different parts of the system without requiring changes to their dependencies.

*   **Example of Adhering to DIP:**

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

*   **Example of Violating DIP:**

    ```swift
    class APIClient {
        func fetchData() -> String {
            return "Data from API"
        }
    }

    class DataProcessor {
        let apiClient = APIClient() // High-level module directly depends on low-level module

        func processData() {
            let data = apiClient.fetchData()
            print("Processing data: \(data)")
        }
    }
    ```

    Here, `DataProcessor` directly depends on the `APIClient` class, making it difficult to switch to a different data source or test the `DataProcessor` in isolation. Changes to `APIClient` could break `DataProcessor`.

### Example which follows all the principles

```swift
// MARK: - Single Responsibility Principle (SRP)

// Each class/protocol has one specific responsibility.

// Protocol for sending notifications
protocol NotificationSender {
    func send(message: String, recipient: String)
}

// Protocol for formatting messages
protocol MessageFormatter {
    func format(message: String) -> String
}

// MARK: - Open/Closed Principle (OCP) & Liskov Substitution Principle (LSP)

// Base class for different notification channels (open for extension, closed for modification).
class BaseNotificationChannel: NotificationSender {
    let formatter: MessageFormatter

    init(formatter: MessageFormatter) {
        self.formatter = formatter
    }

    func send(message: String, recipient: String) {
        let formattedMessage = formatter.format(message: message)
        sendMessage(formattedMessage: formattedMessage, recipient: recipient)
    }

    //Abstract method
    func sendMessage(formattedMessage: String, recipient: String) {
        fatalError("Abstract method must be implemented in sublcass")
    }
}

// Subclasses for specific notification channels
class EmailChannel: BaseNotificationChannel {
    override func sendMessage(formattedMessage: String, recipient: String) {
        print("Sending email to \(recipient) with message: \(formattedMessage)")
        // Email sending logic here
    }
}

class SMSChannel: BaseNotificationChannel {
    override func sendMessage(formattedMessage: String, recipient: String) {
        print("Sending SMS to \(recipient) with message: \(formattedMessage)")
        // SMS sending logic here
    }
}

// MARK: - Interface Segregation Principle (ISP)

// Different formatters for various types of notifications
class BasicFormatter: MessageFormatter {
    func format(message: String) -> String {
        return message
    }
}

class UrgentFormatter: MessageFormatter {
    func format(message: String) -> String {
        return "URGENT: \(message.uppercased())"
    }
}

// MARK: - Dependency Inversion Principle (DIP)

// High-level module: Notification Service
class NotificationService {
    private let sender: NotificationSender

    init(sender: NotificationSender) {
        self.sender = sender
    }

    func sendNotification(message: String, recipient: String) {
        sender.send(message: message, recipient: recipient)
    }
}

// MARK: - Usage

// Configure dependencies
let basicFormatter = BasicFormatter()
let urgentFormatter = UrgentFormatter()
let emailChannel = EmailChannel(formatter: basicFormatter)
let smsChannel = SMSChannel(formatter: urgentFormatter)

// Inject dependencies
let notificationServiceViaEmail = NotificationService(sender: emailChannel)
let notificationServiceViaSMS = NotificationService(sender: smsChannel)

// Send notifications
notificationServiceViaEmail.sendNotification(message: "Hello, world!", recipient: "user@example.com")
notificationServiceViaSMS.sendNotification(message: "Alert!", recipient: "+15551234567")
```

**Explanation of how the principles are applied:**

*   **SRP:**
    *   `NotificationSender`: Only responsible for sending notifications.
    *   `MessageFormatter`: Only responsible for formatting messages.
    *   `NotificationService`: Only responsible for orchestrating the sending of notifications using a `NotificationSender`.
    *   `EmailChannel` and `SMSChannel`: Only responsible for sending message with Email and SMS
*   **OCP:**  You can add new notification channels (e.g., push notifications) or message formatters without modifying the existing `NotificationService`, `EmailChannel` or `SMSChannel`.  The `BaseNotificationChannel` class allows you to extend it using inheritance.
*   **LSP:** `EmailChannel` and `SMSChannel` can be used interchangeably with `BaseNotificationChannel` without breaking the application's behavior.  They fulfill the contract defined by the base class.
*   **ISP:**  Instead of having one large `NotificationChannel` interface with methods that some channels might not implement, we have separate `NotificationSender` and `MessageFormatter` protocols. Channels only need to conform to the protocols relevant to them.
*   **DIP:**  The `NotificationService` depends on abstractions (`NotificationSender`), not concrete implementations (`EmailChannel`, `SMSChannel`). This makes it easy to switch between different notification channels without modifying the `NotificationService`. The formatters are injected and used rather than created inside these classes.

**Important Considerations:**

*   **Over-Engineering:** SOLID principles should be applied judiciously.  Don't blindly apply them everywhere, as it can lead to over-engineering. Consider the complexity and potential for change in your application.
*   **Real-World Complexity:**  This is a simplified example.  Real-world notification systems often involve more complex logic, error handling, and third-party integrations.
*   **Testing:**  This design makes it easier to test the different components in isolation. You can mock the `NotificationSender` and `MessageFormatter` to test the `NotificationService`, and vice versa.
*   **Flexibility:** The design is highly flexible and adaptable to future requirements.

This example provides a foundation for understanding how the SOLID principles can be applied together in a Swift project. Remember to always consider the specific needs of your application and the trade-offs involved when applying these principles.
