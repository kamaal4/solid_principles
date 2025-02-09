The Single Responsibility Principle (SRP) is the first of the SOLID principles of object-oriented design[7][5]. Robert C. Martin introduced the SOLID principles, which aim to make software designs more modular, maintainable, and flexible[4][2]. The SRP specifically guides developers to create code that is easier to understand, modify, and maintain[3].

The Single Responsibility Principle states: "A class should have one, and only one, reason to change"[1][2][3].

**Key aspects of SRP:**
*   Each class or module should have a single, well-defined responsibility, encapsulated within that class[3].
*   A class should not have multiple responsibilities, as this can make it harder to understand and modify[3].
*   Following SRP makes code easier to understand, maintain, and extend[3]. It also reduces the risk of introducing bugs and makes it easier to test individual components in isolation[3].
*   SRP encourages the separation of concerns, making the code more modular and scalable[3].

**Benefits of adhering to SRP:**
*   **Maintainability** SRP helps in creating code that is easier to maintain and update[3][5].
*   **Testability** With SRP, it is easier to test individual components in isolation[3].
*   **Reduced Bugs** SRP reduces the risk of introducing bugs when changes are made to the code[3].
*   **Modularity** SRP encourages the separation of concerns, making the code more modular and scalable[3].
*   **Version Control** SRP makes version control easier because updates to a feature only change related files[4].

**Example of violating SRP:**

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

In this example, the `Student` class has three responsibilities: registering students, calculating their results, and sending emails[5]. This violates the SRP because a class should only have one reason to change[5].

**Example of applying SRP:**

```swift
class User {
    var name: String
    var email: String

    init(name: String, email: String) {
        self.name = name
        self.email = email
    }
}
```

In this example, the `User` class has only one responsibility: to store and retrieve information about a user[2]. It has no other responsibilities, such as sending an email or validating the user’s information[2]. This makes it easy to understand and maintain[2].

Citations:
[1] https://www.bmc.com/blogs/solid-design-principles/
[2] https://dev.to/marwan8/solid-principles-in-swift-a-practical-guide-1fgk
[3] https://hackernoon.com/solid-learn-about-the-single-responsibility-principle-with-examples
[4] https://stackademic.com/blog/the-solid-principles-with-practical-examples-in-ios-swift
[5] https://www.freecodecamp.org/news/solid-principles-single-responsibility-principle-explained/
[6] https://dev.to/bionik6/solid-principles-in-swift-single-responsibility-principle-4jcd
[7] https://www.softwareyoga.com/solid-single-responsibility-principle/
[8] https://gist.github.com/mjhassan/2a61c16c68d66fd43f24306a07900bc6
[9] https://www.seeleycoder.com/blog/solid-part-1-single-responsibility-principle/
[10] https://www.comviva.com/blog/solid-principles-for-ios-in-swift-enhancing-code-style-reusability/
[11] https://www.youtube.com/watch?v=UQqY3_6Epbg
[12] https://pyartez.github.io/architecture/solid-principles-in-swift-single-responsibility-principle.html
[13] https://www.netguru.com/blog/solid-principles-1-single-responsibility-principle
