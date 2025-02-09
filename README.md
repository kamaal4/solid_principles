# SOLID Principles with Swift

**Single Responsibility Principle**
The Single Responsibility Principle (SRP) is the first of the SOLID principles, which are a set of guidelines for writing maintainable and scalable software[2][4]. Introduced by Robert C. Martin, the SOLID principles aim to make object-oriented designs more modular, readable, flexible, and reusable[2][4]. The SRP specifically guides developers to create code that is easier to understand, modify, and maintain[3].

The Single Responsibility Principle states that a class should have one, and only one, reason to change[2][3][6]. In practice, this means each class or module should have a single, well-defined responsibility, encapsulating one part of the software's functionality[1][3]. By adhering to this principle, developers can avoid classes that become overly complex and difficult to test[6].

Benefits of the Single Responsibility Principle:
*   **Easier Testing and Maintenance** Following SRP makes code easier to test and maintain because changes are isolated[1][3].
*   **Reduced Bugs** SRP reduces the risk of introducing bugs and makes it easier to test individual components in isolation[3].
*   **Improved Modularity** SRP encourages the separation of concerns, making the code more modular and scalable[3].
*   **Simplified Version Control** With SRP, updating a feature's logic only changes related files, reducing merge conflicts[4].

Example of SRP in Swift:

Instead of a single class handling multiple responsibilities, separate classes should handle individual tasks[5]. For example, in an e-commerce app, instead of having one class to generate and save invoices, you should have one class that generates invoices and another class that saves them[4].

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

In this example, the `User` class has one responsibility: to store and retrieve information about a user[2]. It does not handle tasks such as sending emails or validating user information[2].

Citations:
[1] https://www.bmc.com/blogs/solid-design-principles/
[2] https://dev.to/marwan8/solid-principles-in-swift-a-practical-guide-1fgk
[3] https://hackernoon.com/solid-learn-about-the-single-responsibility-principle-with-examples
[4] https://stackademic.com/blog/the-solid-principles-with-practical-examples-in-ios-swift
[5] https://www.freecodecamp.org/news/solid-principles-single-responsibility-principle-explained/
[6] https://dev.to/bionik6/solid-principles-in-swift-single-responsibility-principle-4jcd
[7] https://www.softwareyoga.com/solid-single-responsibility-principle/
[8] https://janeshswift.com/ios/swift/solid-principles-in-swift/
[9] https://www.seeleycoder.com/blog/solid-part-1-single-responsibility-principle/
[10] https://www.comviva.com/blog/solid-principles-for-ios-in-swift-enhancing-code-style-reusability/
[11] https://www.youtube.com/watch?v=UQqY3_6Epbg
[12] https://gist.github.com/mjhassan/2a61c16c68d66fd43f24306a07900bc6
[13] https://www.netguru.com/blog/solid-principles-1-single-responsibility-principle
