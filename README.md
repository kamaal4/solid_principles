## SOLID Principles

Here are the SOLID principles with examples in Swift:

### 1. **Single Responsibility Principle (SRP)**

**Meaning**: A class should have only one reason to change.

**Example in Swift**:

Instead of having a `UserManager` class that handles both user authentication and data storage, split it into `UserAuthenticator` and `UserDataStore`.

```swift
// Before SRP
class UserManager {
    func authenticate(username: String, password: String) -> Bool {
        // Authentication logic
        return true
    }
    
    func saveUserData(_ data: [String: String]) {
        // Data storage logic
    }
}

// After SRP
class UserAuthenticator {
    func authenticate(username: String, password: String) -> Bool {
        // Authentication logic
        return true
    }
}

class UserDataStore {
    func saveUserData(_ data: [String: String]) {
        // Data storage logic
    }
}

// Usage
let authenticator = UserAuthenticator()
let dataStore = UserDataStore()

if authenticator.authenticate(username: "user", password: "pass") {
    dataStore.saveUserData(["name": "John Doe"])
}
```

### 2. **Open-Closed Principle (OCP)**

**Meaning**: Software entities should be open for extension but closed for modification.

**Example in Swift**:

Suppose you have a `PaymentGateway` class that supports only credit card payments. To add PayPal support without modifying the existing class, create an abstract `PaymentMethod` class and concrete subclasses like `CreditCardPayment` and `PayPalPayment`.

```swift
// Before OCP
class PaymentGateway {
    func processPayment(amount: Double) {
        // Credit card payment logic
    }
}

// After OCP
protocol PaymentMethod {
    func processPayment(amount: Double)
}

class CreditCardPayment: PaymentMethod {
    func processPayment(amount: Double) {
        // Credit card payment logic
    }
}

class PayPalPayment: PaymentMethod {
    func processPayment(amount: Double) {
        // PayPal payment logic
    }
}

class PaymentGateway {
    func processPayment(amount: Double, using paymentMethod: PaymentMethod) {
        paymentMethod.processPayment(amount: amount)
    }
}

// Usage
let gateway = PaymentGateway()
let creditCard = CreditCardPayment()
let paypal = PayPalPayment()

gateway.processPayment(amount: 100, using: creditCard)
gateway.processPayment(amount: 100, using: paypal)
```

### 3. **Liskov Substitution Principle (LSP)**

**Meaning**: Derived classes should be substitutable for their base classes.

**Example in Swift**:

If you have a `Vehicle` class with subclasses `Car` and `Truck`, any method that uses `Vehicle` should work with `Car` or `Truck` without knowing the difference.

```swift
// Before LSP
class Vehicle {
    func drive() {
        print("Driving")
    }
}

class Car: Vehicle {
    override func drive() {
        print("Driving a car")
    }
}

class Truck: Vehicle {
    override func drive() {
        print("Driving a truck")
    }
}

// After LSP (No change needed as Swift supports polymorphism)
// Usage
func driveVehicle(_ vehicle: Vehicle) {
    vehicle.drive()
}

let car = Car()
let truck = Truck()

driveVehicle(car) // Output: Driving a car
driveVehicle(truck) // Output: Driving a truck
```

### 4. **Interface Segregation Principle (ISP)**

**Meaning**: Clients should not be forced to depend on interfaces they do not use.

**Example in Swift**:

Instead of having a large `NetworkService` interface with methods for both HTTP and WebSocket communication, split it into separate interfaces like `HTTPService` and `WebSocketService`.

```swift
// Before ISP
protocol NetworkService {
    func sendHTTPRequest(_ url: String)
    func establishWebSocketConnection(_ url: String)
}

class NetworkManager: NetworkService {
    func sendHTTPRequest(_ url: String) {
        // HTTP logic
    }
    
    func establishWebSocketConnection(_ url: String) {
        // WebSocket logic (not needed for HTTP-only clients)
    }
}

// After ISP
protocol HTTPService {
    func sendHTTPRequest(_ url: String)
}

protocol WebSocketService {
    func establishWebSocketConnection(_ url: String)
}

class HTTPNetworkManager: HTTPService {
    func sendHTTPRequest(_ url: String) {
        // HTTP logic
    }
}

class WebSocketNetworkManager: WebSocketService {
    func establishWebSocketConnection(_ url: String) {
        // WebSocket logic
    }
}

// Usage
let httpManager = HTTPNetworkManager()
httpManager.sendHTTPRequest("https://example.com")
```

### 5. **Dependency Inversion Principle (DIP)**

**Meaning**: High-level modules should not depend on low-level modules. Both should depend on abstractions.

**Example in Swift**:

Suppose you have a `WeatherForecast` class that depends on a specific `WeatherAPI` class. Instead, define an abstract `WeatherDataSource` interface that both `WeatherAPI` and other data sources (like a mock data source for testing) can implement.

```swift
// Before DIP
class WeatherAPI {
    func fetchForecast() -> String {
        // Fetch forecast from API
        return "Sunny"
    }
}

class WeatherForecast {
    let api = WeatherAPI()
    
    func getForecast() -> String {
        return api.fetchForecast()
    }
}

// After DIP
protocol WeatherDataSource {
    func fetchForecast() -> String
}

class WeatherAPI: WeatherDataSource {
    func fetchForecast() -> String {
        // Fetch forecast from API
        return "Sunny"
    }
}

class MockWeatherDataSource: WeatherDataSource {
    func fetchForecast() -> String {
        // Mock forecast for testing
        return "Cloudy"
    }
}

class WeatherForecast {
    let dataSource: WeatherDataSource
    
    init(dataSource: WeatherDataSource) {
        self.dataSource = dataSource
    }
    
    func getForecast() -> String {
        return dataSource.fetchForecast()
    }
}

// Usage
let api = WeatherAPI()
let mockDataSource = MockWeatherDataSource()

let forecastUsingAPI = WeatherForecast(dataSource: api)
let forecastUsingMock = WeatherForecast(dataSource: mockDataSource)

print(forecastUsingAPI.getForecast()) // Output: Sunny
print(forecastUsingMock.getForecast()) // Output: Cloudy
```
