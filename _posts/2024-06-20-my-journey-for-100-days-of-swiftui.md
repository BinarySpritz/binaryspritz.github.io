---
layout: post
title: 'My journey in "The 100 days of SwiftUI"'
date: 2024-06-20 10:02:00 +0100
author: "Marco Ferrati"
categories : swift
---
In this blog post, I will log my journey in learning Swift and SwiftUI by following "[The 100 days of SwiftUI](https://www.hackingwithswift.com/100/swiftui)".

There are two reasons for this diary to exist and be publicly available: first, to share my thoughts about the language and the framework, and second, as a review of the learning process proposed by "The 100 Days of Swift," which, as the title says, you have to follow for one hundred days. Moreover, as I am a person who already knows some programming languages, I was curious about how a new language is taught.

Index:
- [Day 1](#day-1): variables and constants part 1/2
- [Day 2](#day-2): variables and constants part 2/2 and string interpolation
- [Day 3](#day-3): arrays, dictionaries, enums, 
- [Day 4](#day-4): typing
- [Day 5](#day-5): conditional statements
- [Day 6](#day-6): loops
- [Day 7](#day-7): functions part 1/2
- [Day 8](#day-8): functions part 2/2 
- [Day 9](#day-9): functional programming
- [Day 10](#day-10): struct part 1/2
- [Day 11](#day-11): struct part 2/2


# Day 1
The day started with a brief introduction to the Swift programming language and how **variables**, **constants** and **literals** work in an assignment statement (the type inference concept is briefly introduced). 

In Swift, there are both variables and constants. The former can be reassigned to a new value, while the latter cannot be reassigned (although you can probably change values inside them when objects come into play).
{% highlight swift %}
var aVariable = 0
let aConstant = "String which cannot be reassigned"
{% endhighlight %}


Regarding literals, this first day is about strings, multi-line strings, integer, and doubles.

# Day 2
The following day, the course covered Boolean variables and string interpolation.

Regarding Boolean variables, the only novelty was the `.toggle()` method, which switches the value of the variable (similar to doing `myVar = !myVar`).

Regarding string interpolation (which is achieved through the \() pattern), the course stated that it is more efficient than concatenation using the + operation. For example, `"\(s1) \(s2) \(s3)"` is faster than `s1 + s2 + s3` because concatenation requires the use of a temporary variable for each “sum” except the last.

Finally, a simple exercise was assigned: a Celsius to Fahrenheit converter that required the knowledge acquired during the first two days.
{% highlight swift %}
let temperatureInCelsius = 29.0

print("Today's temperature is \(temperatureInCelsius)C or \(temperatureInCelsius*9/5)F")
{% endhighlight %}

# Day 3
During the third day, we started looking into more complex data structures such as arrays, dictionaries, sets, and enumerations.

{% highlight swift %}
let anArray = ["Tim", "Craig", "Stever"]

let aDictionary = [
	"name": "Tim",
	"job": "CEO",
	"birthday": "November 1"
]

let aSet = Set(["Apple", "Orange", "Apple", "Pear"]) // ["Apple", "Orange", "Pear"] —> distinct items

enum WeekDays {
	case monday, tuesday, wednesday, thursday, friday, saturday, sunday
}
var weekday = WeekDays.monday
weekday = .friday

{% endhighlight %}

Two interesting facts about these data structures are:
1. Sets are incredible faster than array when you are looking for an item inside (`.contains(…)`) but they are not ordered and cannot contains duplicates
2. When working with enums you don’t have to write every time `WeekDays` because the compiler is capable of understating it by the variable type.

# Day 4
In Swift, you can specify the type of a variable when you declare it. If you don’t do ii, the compiler will infer the type. Up to now, it hasn’t been necessary to specify the type, but in the feature it could come in handy. 

Moreover, with type specification you can declare a variable or a constant without initiating it. 
{% highlight swift %}
let username: String
print(username) // Constant ‘username’ used before initialized
username = "jjocram"
print(username)
{% endhighlight %}

Finally, another checkpoint/exercise is proposed. In this checkpoint you have to declare a list with some duplicate, a set from the list and print both their .count showing that the set doesn’t have the duplicates.

{% highlight swift %}
let anArray: [String] = ["Apple", "Orange", "Apple", "Pear"]
let aSetFromAnArray: Set<String> = Set(anArray)
print("anArray has \(anArray.count) elements of which \(aSetFromAnArray.count) are unique")
{% endhighlight %}

# Day 5
Conditional statement are introduced. `if-then-else`, `switch`, and `... ? ... : ...`(ternary operator) can change the flow of your program.

## Example with `if-else if-else`
{% highlight swift %}
enum Weather {
    case sun, rain, wind, snow, unknown
}

let todaysWeather: Weather = .sun

if todaysWeather == .sun {
    print("Let's go to the park")
} else if todaysWeather == .rain || todaysWeather == .snow {
    print("Let's go to the mall")
} else if todaysWeather == .wind {
    print("Let's bring the kite with us")
} else {
    print("Something else")
}
{% endhighlight %}

## Example with `switch-case`
{% highlight swift %}
enum Weather {
    case sun, rain, wind, snow, unknown
}

let todaysWeather: Weather = .sun

switch todaysWeather {
case .sun:
    print("Let's go to the park")
case .rain, .snow:
    print("Let's go to the mall")
case .wind:
    print("Let's bring the kite with us")
default:
    print("Something else")
}
{% endhighlight %}

In addition to this simple example, the `switch-case` statement can be use with the pattern matching (we wrote an article about it for the Python programming language. [Check it out]({% post_url 2024-06-14-the-power-of-switch-case-in-python%})).

Moreover, Swift has a `fallthrough` statement. When a `case` block ends with the `fallthrough` statement, the program will execute the following `case` even though the condition doesn't match.

## Example with the ternary operator `... ? ... : ...`
{% highlight swift %}
let age = 18
let canVote = age >= 18 ? true : false
{% endhighlight %}

You can read the ternary operator as `<condition> ? <value if condition is true> : <value if condition is false>`.

# Day 6
Now it's time of iteration. `for-in` loop, and `while` loop

{% highlight swift%}
let platforms = ["iOS", "macOS", "iPadOS", "tvOS", "watchOS"]

for os in platforms {
    print("Swift is grat on \(os).")
}

for i in 1...12 {
    print("5 x \(i) = \(5*i)")
}

for i in 1...5 {
    print("Counting from 1 through 5: \(i)")
}

for i in 1..<5 {
    print("Counting from 1 up to 5: \(i)")
}

var lyrics = "Haters gonna "

for _ in 1...5{
    lyrics += "hate "
}

print(lyrics)
{% endhighlight %}

It is worh noting how ranges work in Swift: `[min]...[max (included)]` and `[min]..<[max (excluded)]`.

`while` loops have nothing new with respect to other languages.
{% highlight swift %}
var roll = 0
var times = 0

while roll != 20 {
    roll = Int.random(in: 1...20)
    times += 1
    print("I rolled \(roll)")
}

print("Crit! in \(times) roll")
{% endhighlight %}

Finally, `continue` and `break` statement:
{% highlight swift %}
let fileNames = ["A.jpg", "work.txt", "sophie.jpg"]

for fileName in fileNames {
    if fileName.hasSuffix(".jpg") == false {
        continue
    }
    
    print("Image file: \(fileName)")
}

let number1 = 4
let number2 = 14
var multiplies: [Int] = []

for i in 1...100_000 {
    if i.isMultiple(of: number1) && i.isMultiple(of: number2) {
        multiplies.append(i)
        
        if multiplies.count == 10 {
            break
        }
    }
}

print(multiplies)
{% endhighlight %}

In Swift we can also have labeled statement. In this way we can `break` an outside loop when cycling inside a nested one.

{% highlight swift %}
enum Controls {
    case up, down, left, right
}

let options: [Controls] = [.up, .down, .left, .right]
let secretCode: [Controls] = [.down, .up, .right]

outerLoop: for option1 in options {
    for option2 in options {
        for option3 in options {
            let attempt = [option1, option2, option3]
            
            if attempt == secretCode {
                print("Found the secret code \(attempt)")
                break outerLoop
            }
        }
    }
}

{% endhighlight %}

Today was also a checkpoint day. Now we know all the basic stuff to write any computer program.

The solution for the fizz-buzz problem follows.
{% highlight swift %}
for i in 1...100 {
    if i.isMultiple(of: 3) && i.isMultiple(of: 5) {
        print("FizzBuzz")
    } else if i.isMultiple(of: 3) {
        print("Fizz")
    } else if i.isMultiple(of: 5) {
        print("Buzz")
    } else {
        print(i)
    }
}
{% endhighlight %}

# Day 7
With iterations done, we reached a turning point in studying Swift. Today we step up and start studying functions. 

{% highlight swift %}
func printTimesTables(number: Int, end: Int) {
    for i in 1...end {
        print("\(i) * \(number) is \(i*number)")
    }
}

printTimesTables(number: 7, end: 20)
{% endhighlight %}

By default, Swift requires the names of the parameters when we call the function.

Returning values is as in many other programming language: `return` keyword and the type returned in the function declaration (with `-> <Type>`).

{% highlight swift %}
import Cocoa

func sameCharInStrings(stringA: String, stringB: String) -> Bool {
    return stringA.sorted() == stringB.sorted()
}

print("home has the same chars of emoh? \(sameCharInStrings(stringA: "home", stringB: "emoh"))")
{% endhighlight %}

It is not true that the `return` keyword is always needed. When the return statement is the first line of the scope we can ommit the keyword.

{% highlight swift %}
func specialHello(to: String) -> String {
    if to == "Tim" {
        "Hello Mr. Tim"
    } else {
        let normalGreet = "Hello \(to)"
        return normalGreet
    }
}
{% endhighlight %}

During this day, **tuples** are introduced as a way to return multiple values from a function:
{% highlight swift %}
func getUser() -> (firstName: String, lastName: String) {
    return (firstName: "John", lastName: "Doe")
}

let user = getUser()
print("Name: \(user.firstName) \(user.lastName)")
{% endhighlight %}

In Swift, tuples are like C's `struct` (they can only hold data) but defined in the return type. Moreover, you can also deconstruct a tuple into variables (we can use `_` to ignore some parts of the tuple).

{% highlight swift %}
func getUser() -> (firstName: String, lastName: String) {
    return (firstName: "John", lastName: "Doe")
}

let (namePart1, namePart2) = getUser()
print("Name: \(namePart1) \(namePart2)")
{% endhighlight %}

## Dive into function's parameters
In Swift, it is interesting looking into how parameters are a first-class citizen when we talk about functions.

First of all, they are integral part of the function name. It means we can have functions with the same name but different parameters' name.

{% highlight swift %}
func a(b: String) { }
func a(c: String) { }
{% endhighlight %}

Then, we can have two names for a parameter: one used inside the function body and the other used in function call (which could be `_` to have nothing)

{% highlight swift %}
func specialHello(to name: String) -> String {
    if name == "Tim" {
        return "Hello Mr. Tim"
    } else {
        return "Hello \(name)"
    }
}

print(specialHello(to: "Tim"))
{% endhighlight %}

# Day 8
In Swift, we can also have default parameters. That is done adding the default value in the parameter declarationn  `func f(a: String = "default string") { }`.

Functions can also throw exceptions and that must be added to the function definition with the `throws` keyword.

{% highlight swift %}
enum PasswordError: Error {
    case short, obvious
}

func checkPassword(password: String) throws -> String{
    if password.count < 8 {throw PasswordError.short}
    if password == "password" {throw PasswordError.obvious}
    
    if password.count < 10 {
        return "OK"
    } else if password.count < 12 {
        return "Good"
    } else {
        return "Great"
    }
}
{% endhighlight %}

To call a function which could throw an exception we have a couple of ways: `do-try-catch` block or `try!`.

{% highlight swift %}
do {
    let passwordResult = try checkPassword(password: "1234567890")
    print("The password is \(passwordResult)")
} catch PasswordError.short {
    print("You should use a longer password")
} catch PasswordError.obvious {
    print("Your password is 'password'")
} catch {
    print("Generic error: \(error)")
}

let passwordResult = try! checkPassword(password: "1234") // ! = danger. In this case it will crash the program
print("The password is \(passwordResult)")
{% endhighlight %}

Finally, to test functions in a more real use case this day's checkpoint requires to find the integer square root of an integer number.

{% highlight swift %}
enum SqrtError: Error {
    case outOfBound, noRoot
}

func sqrt(of number: Int) throws -> Int {
    if number < 1 || number > 10_000 {throw SqrtError.outOfBound}
    
    for i in 1...100 {
        if i*i == number { return i}
    }
    
    throw SqrtError.noRoot
}

let number = 10000
do {
    let root = try sqrt(of: number)
    print("sqaure root of \(number) is \(root)")
} catch SqrtError.outOfBound {
    print("Number must be grater than zero and lessere than 10_001")
} catch SqrtError.noRoot {
    print("No root has been found for \(number)")
}
{% endhighlight %}

# Day 9
After functions, it is time to go functional!

A function can be assigned to a variable and called from that variable. That is usefull when you want to let the user define a behaviour to call later.

{% highlight swift %}
func a() {
    print("Hello from a")
}

var aCaller = a
aCaller()

let bCaller = {
    print("Hello from b")
}
bCaller()
{% endhighlight %}

In the example, `bCaller` is called **closure** (a.k.a anonymous function).

To accept some values as input and return, we have to specify it in the closure with `{(<parameter list>) -> <returnType> in } (which is also the type of the function)`.
{% highlight swift %}
let sayHello: (String) -> String = { (name: String) -> String in 
    return "Hi \(name)"
}

let message = sayHello("John")
{% endhighlight %}

In a closure, we can avoid using parameters name and use `$0`, `$1`, `$2`, `...` and inline the function definition (having an anonymous function) instead. That is called **trailing closure syntax**.

{% highlight swift %}
let alphabet = ["B", "D", "X", "A", "F"]

let reverseSorted = alphabet.sorted {
    return $0 > $1
}

let onlyA = alphabet.filter { $0.hasPrefix("A") }
{% endhighlight %}

Obviously, function can be accepted as parameter by other functions (we can say that is what functional means).

{% highlight swift %}
func makeArray(size: Int, using generator: () -> Int) -> [Int] {
    var numbers: [Int] = []
    for _ in 0..<size {
        let newNumber = generator()
        numbers.append(newNumber)
    }
    return numbers
}

let intArry = makeArray(size: 10) {
    Int.random(in: 1...20)
}
{% endhighlight %}

One thing I am not really happy with is how are handled multiple closure as parameters

{% highlight swift %}
func a(first: () -> Void, second: () -> Void, third: () -> Void) {
    first()
    second()
    third()
}

a {
    print("First")
} second: {
    print("Second")
} third: {
    print("Third")
}
{% endhighlight %}

Finally, as checkpoint, here it is a program that exploits the power of closures.

{% highlight swift %}
let luckyNumbers = [7, 4, 38, 21, 16, 15, 12, 33, 31, 49]

luckyNumbers
    .filter({$0.isMultiple(of: 2)})
    .sorted()
    .map({"\($0) is lucky number"})
    .forEach({print("\($0) is a lucky number")})
{% endhighlight %}

# Day 10
After functional, object-oriented programming joins the game.

We start with `struct`s:

{% highlight swift %}
struct Album {
    let title: String
    let artist: String
    let year: Int
    
    func printInfo()  {
        print("\(title) (\(year) by \(artist)")
    }
}

let red = Album(title: "Red", artist: "Taylor Swift", year: 2012)
red.printInfo()
{% endhighlight %}

By defualt a struct instance is constant. It means you cannot change the value of its variables even if they are marked as `var`.

{% highlight swift lineos %}
struct Employee {
    let name: String
    var vacationRemaining: Int
    
    func takeVacation(days: Int) {
        if vacationRemaining > days {
            vacationRemaining -= days
            print("You can go to vacation. \(vacationRemaining) days left")
        }
    }
}
{% endhighlight %}

In the example above, when we do `vacationRemaining -= days`, the compiler will complain with the following error message: `Left side of mutating operator isn't mutable: 'self' is immutable`.

To change this behaviour we have to explicitly mark the function as `mutating`.

{% highlight swift lineos %}
struct Employee {
    let name: String
    var vacationRemaining: Int
    
    mutating func takeVacation(days: Int) {
        if vacationRemaining > days {
            vacationRemaining -= days
            print("You can go to vacation. \(vacationRemaining) days left")
        }
    }
}
{% endhighlight %}

However, when we declare the variable holding our instance it changes if we declare it as `let` or as `var`.
{% highlight swift %}
struct Employee {
    let name: String
    var vacationRemaining: Int
    
    mutating func takeVacation(days: Int) {
        if vacationRemaining > days {
            vacationRemaining -= days
            print("You can go to vacation. \(vacationRemaining) days left")
        } else {
            print("You don't have enough vacation days")
        }
    }
}

var john = Employee(name: "John", vacationRemaining: 10)
john.takeVacation(days: 5)
print(john.vacationRemaining)

let mary = Employee(name: "Mary", vacationRemaining: 10)
mary.takeVacation(days: 5)
print(mary.vacationRemaining)
{% endhighlight %}

When we declare `let mary = ...` we cannot invoke any `mutating function`. We will get the following error: `Cannot use mutating member on immutable value: 'mary' is a 'let' constant`

## Notes on properties

### Computed property
That is a fancy name for a `getter` and `setter`. For the setter the new value is hold by the automatic `newValue` parameter.
 {% highlight swift %}
struct Employee {
    let name: String
    var vacationAllocated: Int = 14
    var vacationTaken = 0
    
    var vacationRemaining: Int {
        get {
            vacationAllocated - vacationTaken
        }
        set {
            vacationAllocated = vacationTaken + newValue
        }
    }
}

var john = Employee(name: "John")
john.vacationTaken += 4
print("\(john.name) has \(john.vacationRemaining) days of vacation")

john.vacationRemaining = 10
print(print("\(john.name) has a total of \(john.vacationAllocated) days of vacation"))
{% endhighlight %}

It is worth notice that, computed properties can only be `var`.

### Observed property
In addition to `getter` and `setter` we have also `didSet` and `willSet` to observe how a variable is changed or is goining to change.

{% highlight swift %}
struct Game {
    var score = 0 {
        didSet {
            print("Someone just scored. Now it is \(score), before was \(oldValue)")
        }
    }
    
    var player: [String] = [] {
        willSet {
            print("List of player is going to change. The list of player will change from \(player) to \(newValue)")
        }
    }
}

var game = Game()
game.player = ["John", "Tim"]
game.score += 1
game.player = game.player + ["Craig"]
game.score += 1
{% endhighlight %}

## Initializer
Finally, let's talk about how to initialize our structs.

By defualt we have a generated initializer which takes in input all the properties of our struct.

{% highlight swift %}
struct Player {
    let name: String
    let number: Int
    
    init(name: String) {
        self.name = name
        self.number = Int.random(in: 1...99)
    }
}

var player = Player(name: "John")
print("\(player.name) is number \(player.number)")
{% endhighlight %}

Before calling any struct's method inside the initializer we have to initialize every property.

# Day 11

## Access modifier
By defualt the access to struct's members are `public`. There are other two access modifier:
- `private`: only by struct
- `fileprivate`: only in the same file

We can go further and use `private` and `fileprivate` also by setter.
- `private(set) var ...`

An interesting point is that Swift cannot generate the initializer when we have a mix of private and public attributes.

{% highlight swift %}
struct A {
    private var a = "a string"
}

let a = A() // OK

struct B {
    private var b = "b string"
    var c: String 
}

let b = B(c: "c string") // !Error: initializer is inaccessible due to 'private' protection level
{% endhighlight %}

## Static members
We can declare `static` members for our structs.

{% highlight swift %}
struct A {
    static var a = 0

    static func f(s: String) {
        print(s)
        a += 1
    }
}

A.f(s: "a string")
print(A.a)
{% endhighlight %}

In a static method we can access to "`self`" through the keyword `Self` (note the capital `S`).

## Checkpoint
Today has been also a checkpoint day.

Today's task was to define a struct for a car which can change gear.

{% highlight swift %}
enum GearMovement {
    case UP, DOWN
}

enum GearException: Error{
    case NO_UP, NO_DOWN
}

struct Car {
    let model: String
    let seats: Int
    private(set) var currentGear: Int = 0
    
    init(model: String, seats: Int) {
        self.model = model
        self.seats = seats
    }
    
    mutating func changeGear(_ move: GearMovement) throws {
        if currentGear == 10 && move == .UP {throw GearException.NO_UP}
        if currentGear == 0 && move == .DOWN {throw GearException.NO_DOWN}
        
        
        switch move {
        case .UP:
            currentGear += 1
        default:
            currentGear -= 1
        }
    }
}


var myCar = Car(model: "MIa", seats: 5)

do {
    try myCar.changeGear(.UP)
    print("Now you are in \(myCar.currentGear)")
} catch {
    print("Error: \(error)")
}
{% endhighlight %}
