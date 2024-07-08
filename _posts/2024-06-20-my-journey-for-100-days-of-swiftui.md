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
- [Day 12](#day-12): classes
- [Day 13](#day-13): protocols and extensions
- [Day 14](#day-14): optionals
- [Day 15](#day-15): Swift recap
- [Day 16](#day-16): WeSplit part 1/2
- [Day 17](#day-17): WeSplit part 2/2


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

# Day 12
Structs can hold data and perform operations through functions but OOP is much more. For this reason we need classes.

In addition to structs, classes are defined by:
1. Inheritance
2. Not having an auto-generated initializer
3. Copying an instance of a class means copying its reference
4. De-initializers
5. The possibility to change properties of an object declared as constant

## Copy means shallow copy

{% highlight swift %}
class Game {
    var score = 0 {
        didSet {
            print("Score is now \(score)")
        }
    }
}

var newGame = Game()
newGame.score += 1 // score = 1

var anotherGame = newGame
anotherGame.score += 1 // score = 2

newGame.score += 1 // score = 3
{% endhighlight %}

We have to implement our own `deepCopy` function to overcome this. 

## Inheritance
Regarding inheritance, Swift works as many other programming languages.

{% highlight swift %}
class ParentClass {
    func work() {
        print("work from ParentClass")
    }
}

final class ChildClass: ParentClass {
    override func work() {
        super.work()
        print("And then work from ChildClass")
    }
}
{% endhighlight %}

## Initializer
Initializers are a bit more complicated than struct's initializers because inheritance could be in between.

{% highlight swift %}
class ParentClass {
    var a: Int
    
    init(a: Int) {
        self.a = a
    }
}

final class ChildClass: ParentClass {
    var b: Int
    
    init(a: Int, b: Int) {
        self.b = b
        super.init(a: a)
    }
}
{% endhighlight %}
It is worth noticing that in `ChildClass`'s initializer we must initialize its own attributes before calling `ParentClass` initializer.

## De-initializer
We can define the behaviour when an object is destroyed. In Swfift we don't have to manage the memory (no `new` and `delete` keyword). So, an object is destroyed when the last variable, pointing to it, is unreachable (out of scope (`{...}`)). Swift uses **Automatic Reference Counting (ARC)** to keep trace of which objects are still reachable by some variable.

{% highlight swift %}
class A {
    var a: Int
    
    init(a: Int) {
        print("Init an object of type A")
        self.a = a
    }
    
    deinit {
        print("Destroyed an object of type A")
    }
}

func main() {
    var a = A(a:0)
    
    for i in 1...5 {
        var copyOfA = a
        copyOfA.a += 1
        print("a's new value is \(copyOfA.a)")
    }
}

main()
{% endhighlight %}

## Variables or constants?
When we declare a constant object (`let a = A(a: 0)`) we are saying that `a` will point to that area of memory and cannot be changed (`a = A(a: 1)`). The area of memory holding the object is not constant and can be changed (if properties are declared as `var` and not as `let`).

This brings another difference from structs. Classes don't have the `mutating` keyword for functions.

## Checkpoint 
Classes can be challenging. To be sure to have understood how they work an exercise is proposed: a class hierarchy for animals.

{% highlight swift %}
class Animal {
    let legs: Int
    
    init(legs: Int) {
        self.legs = legs
    }
}

class Dog: Animal {
    init() {
        super.init(legs: 4)
    }
    
    func speak() {
        print("Bau")
    }
}

class Corgi: Dog {
    override func speak() {
        print("Bau but in corgi dialect")
    }
}

class Poodle: Dog {
    override func speak() {
        print("Bau but in poddfle dialect")
    }
}

class Cat: Animal {
    var isTame: Bool
    
    init(isTame: Bool) {
        self.isTame = isTame
        super.init(legs: 4)
    }
    
    func speak() {
        print("Mio")
    }
}

class Persian: Cat {
    init() {
        super.init(isTame: true)
    }
    
    override func speak() {
        print("Miao but in persian dialect")
    }
}

class Lion: Cat {
    init() {
        super.init(isTame: false)
    }
    
    override func speak() {
        print("Miao but in lion dialect (a.k.a. roar)")
    }
}
{% endhighlight %}

# Day 13

## Protocols
Next and last step in OOP is learning interfaces (Swift calls them `protocols`).

Protocols can require also to declare variables. For each one you have to declare if they are only readable `{get}` or readable and writable `{get set}`

{% highlight swift %}
protocol Moving {
    var speed: Int { get }
    func estimateTime(for distance: Int) -> Int
    func travel(distance: Int)
}

class Car: Moving {
    var speed: Int = 50
    
    var travelledKm = 0
    
    func estimateTime(for distance: Int) -> Int {
        return distance / speed
    }
    
    func travel(distance: Int) {
        travelledKm += distance
    }
}

class Feet: Moving {
    var speed: Int = 5
    var hurt = false
    
    func estimateTime(for distance: Int) -> Int {
        return distance / speed
    }
    
    func travel(distance: Int) {
        if distance > 100 {hurt = true}
    }

}

func commute(distance: Int, using tool: Moving) {
    tool.travel(distance: distance)
}
{% endhighlight %}

## Opaque return types
Sometimes we cannot tell to the compiler what type we are returning from a function because it will complain, maybe, without reason.

{% highlight swift %}
func getRandomNumber() -> Equatable {
    return Int.random(in: 1...6)
}

func getRandomBool() -> Equatable {
    return Bool.random()
}

print(getRandomNumber() == getRandomNumber())
{% endhighlight %}

The solution is telling Swift that we return `some` of that type

{% highlight swift %}
func getRandomNumber() -> some Equatable {
    return Int.random(in: 1...6)
}

func getRandomBool() -> some Equatable {
    return Bool.random()
}

print(getRandomNumber() == getRandomNumber())
{% endhighlight %}

The `some` keyword let the compiler to know the real type reuturned but from our perspective it is only an `equatable`.

The `some` keyword can be read as: "we are returning a specific type of `equatable` but we are not saying which one".

SwiftUI uses this feature a lot.

## Extensions
With extensions we can add function(alities) to any type. 

{% highlight swift %}
extension String {
    func toStrangeFormat() -> String {
        var newString = ""
        for (i, c) in self.enumerated() {
            newString += i.isMultiple(of: 2) ? String(c) : c.uppercased()
        }
        return newString
    }
}

let myNormalString = "A normal string".toStrangeFormat()
print(myNormalString) // A nOrMaL StRiNg
{% endhighlight %}

Moreover, if we implement a custom initializer for a struct inside an extension, Swift will keep the default initializer and of our custom one.

We can extend protocols as well. In this case we can specify implementation for functions in protocols accessible everywhere. In the example before, we can specify the method `estimateTime` as an extension of the protocol `Moving` in order to provide the default implementation `return distance / speed`.

## Checkpoint
Also today has been a checkpoint-day. The challenge was about modelling a protocol for a building and implementing it for two structs.

{% highlight swift %}
protocol Building {
    var rooms: Int {get}
    var cost: Int {get set}
    var seller: String {get}
    
    func printSummary()
}

struct House: Building {
    var rooms: Int
    var cost: Int
    var seller: String
    
    func printSummary() {
        print("This house is selled by \(seller). It has \(rooms) rooms and it costs \(cost)$")
    }
}

struct Office: Building {
    var rooms: Int
    var cost: Int
    var seller: String
    
    func printSummary() {
        print("This office is selled by \(seller). It has \(rooms) rooms and it costs \(cost)$")
    }
}
{% endhighlight %}

# Day 14
Last topic about the Swift programming language: the optional type. In Swift, we can mark any type as an optional type, which means that the variable holding that type could be an instance of the type or `nil` (`null`, `None`, or `nullptr` in other languages).

In Swift, to say that a type can be `nil` we specify it in the type specification with a question mark: `Type?`.

## Unwrapping optional values
We have a couple of solutions to unwrap optional values:

### if-let
{% highlight swift %}
var maybeString: String? = nil

if let maybeString = maybeString { // Shadowing
    print("I'm sure maybeString is not nil and its value is \(maybeString)")
} else {
    print("maybeString is nil. Nothing to show")
}
{% endhighlight %}

### guard-let
{% highlight swift %}
func doSomething(a: String?) {
    guard let a = a else {
        print("a was nil. Returning")
        return
    }

    print("Here I'm sure 'a' is not nil: \(a)")
}
{% endhighlight %}

### Nil coalescing
Also known as: default value. It is achieved adding a doubble question mark `??` after the use of the optional value. 

{% highlight swift %}
let map = [
    1: "A",
    2: "B",
    3: "C"
]

let missing = map[4] ?? "N/A"
{% endhighlight %}

It is worth noticing that you can chain default values: `let a = f1() ?? f2 ?? "default"`.

## Optional chaining
We can use optional inside optionals.

{% highlight swift %}
let a = ["a", "b", "c", "d"]
let chosen = a.randomElement?.uppercased() ?? "No one"
{% endhighlight %}

You can read it as: "unwrap the value and continue the processing. If any step fails unwrapping, then fallback to the default value".

## Optional instead of exception
We can catch an exception and return a `nil` instead of handling the exception. To do so, we can use `try?` before calling the throwing function.

{% highlight swift %}
enum UserError: Error {
    case badId, networkFailed
}

func getUser(id: Int) throws -> String {
    throw UserError.networkFailed
}

if let user = try? getUser(id: 42) {
    print("User: \(user)")
}

let user = (try? getUser(id: 42)) ?? "Anonymous"
{% endhighlight %}

We can also let the program crash. When we use `try! f()` the program will crash if any exception is thrown in the function called after the `try!`

## Checkpoint
Also today was a checkpoint-day. The challenge was about coding a function that handles optional values in a single line of code.

{% highlight swift %}
func f(a: [Int]?) -> Int{
    return a?.randomElement() ?? Int.random(in: 1...100)
}
{% endhighlight %}

# Day 15
Today has been dedicated to a recap of the foundamentals learnt so far. Nothing new has been added. From tomorrow we move into SwiftUI and app development.

# Day 16
Today we start iOS app development with a running example. WeSplit is an app that allows to split the cost of a launch or a dinner among people.

## Structure of a SwiftUI app
When we create a new iOS app in XCode, the IDE will genereate a couple of file for us.

The `main` file is the file with the name of our app. It will contain the following code

{% highlight swift %}
import SwiftUI

@main
struct WeSplitApp: App {
    var body: some Scene {
        WindowGroup {
            ContentView()
        }
    }
}
{% endhighlight %}

This struct will live for the whole time our app will run.

The interface is handled by `ContentView`

{% highlight swift %}
import SwiftUI

struct ContentView: View {
    var body: some View {
        VStack {
            Image(systemName: "globe")
                .imageScale(.large)
                .foregroundStyle(.tint)
            Text("Hello, world!")
        }
        .padding()
    }
}

#Preview {
    ContentView()
}
{% endhighlight %}

For now everything will be managed by `ContentView`. At a first glance we can already see a lot of stuff we have already see in the last days.

We have:
- a `struct` representing our view which implemnts the `View` protocol
- a computed property called `body` of type `some View`

Then we have new stuff:
- a `VStack`
- an `Image`
- a `Text`
- a call to the `padding()` method

Last thing is the `#Preview` statement which initialize an object of type `ContentView` which will be showed in XCode without running our app. This feature is called **canvas**.

## Form
A `Form` is a graphical element which can be used as container for other elements (usually, for data input from the user). We can separate sections of the forms, grouping them inside a `Grouping` object.

<table>
    <tr>
        <td>{% highlight swift %}
var body: some View {
    Form {
        Section {
            Text("Hello World0")
            Text("Hello World1")
        }
        
        Section {
            Text("Hello World2")
            Text("Hello World3")
        }
    }
}
    {% endhighlight %}</td>
        <td><img src="/assets/images/2024-06-20-100-days-of-swiftui/formWithSections.png" alt="Form with sections rendered in the canvas"/></td>
    </tr>
</table>

## Navigation bar
Container which allow the navigation between views. We surround our Form with a `NavigationStack` and add some properties to it applying them to the form.

<table>
    <tr>
        <td>{% highlight swift %}
var body: some View {
        NavigationStack{
            Form {
                Section {
                    Text("Hello World0")
                    Text("Hello World1")
                }
                
                Section {
                    Text("Hello World2")
                    Text("Hello World3")
                }
            }
            .navigationTitle("SwiftUI")
            .navigationBarTitleDisplayMode(.inline)
        }
    }
    {% endhighlight %}</td>
        <td><img src="/assets/images/2024-06-20-100-days-of-swiftui/formWithSectionsAndNavigation.png" alt="Form with sections and a navigationbar rendered in the canvas"/></td>
    </tr>
</table>

## App state
What a view presents depends on its state.

In Swift, structs cannot change the value of their variables outsie `mutating` func so we **cannot** have something like this:

{% highlight swift %}
struct ContentView: View {
    var tapCount = 0
    
    var body: some View {
        Button("Tap count: \(tapCount)") {
           tapCount += 1
        }
    }
}
{% endhighlight %}

The solution is using a **property wrapper** for our varibale called `State`.

{% highlight swift %}
struct ContentView: View {
    @State var tapCount = 0
    
    var body: some View {
        Button("Tap count: \(tapCount)") {
           tapCount += 1
        }
    }
}
{% endhighlight %}

### Binding
We want our user interface being able to change the state of our app. When we write a string as input of a `TextField` we can link it to a `@State` variable but that is not enough. We have to tell to SwiftUI that we are binding that state to the graphical element which will change. To do so, we pass `$varName` instead of `varName`

The dollar sign means: be able to read and **change** the value in the state variable.

{% highlight swift %}
struct ContentView: View {
    @State var name = ""
    
    var body: some View {
        Form {
            TextField("Enter your name", text: $name)
            Text("Hello \(name)!")
        }
    }
}
{% endhighlight %}

## Loops
We can create views in a loop (maybe one for each iteration). 

{% highlight swift %}
struct ContentView: View {
    @State var name = ""
    
    var body: some View {
        Form {
            ForEach(0..<100) { number in
                Text("Row \(number)")
            }
        }
    }
}
{% endhighlight %}

We can use it in a `PickerView` to select an element from a list.

{% highlight swift %}
struct ContentView: View {
    let students = ["John", "Mark", "Tim", "Steve"]
    @State private var name = ""
    
    var body: some View {
        NavigationStack {
            Form {
                Picker("Select your student", selection: $name) {
                    ForEach(students, id: \.self) {
                        Text($0)
                    }
                }
            }
        }
    }
}
{% endhighlight %}

We can see things are becoming complex:
1. We define a `NavigationStack`
2. Inseide the `NavigationStack` we insert a `Form`
3. Insider our `Form` we insert a `Picker` which has:
    - a label ("Select your student")
    - a varibale where store the selction (`$name`)
    - a list of views (`Text`) which represent the possible selections. This list is generated with a `ForEach` "loop"
        - we iterate over `students`
        - we tell to the `ForEach` how to uniquely identify each element (`id` parameter (we use `\.self` which means each string))
        - we create the view `Text` with text the first element of the closure (the string itself)

# Day 17
Let's start developing our WeSplit application. First of all we need three state variable: `checkAmount`, `numberOfPeople`, and `tipPercentage`. Then we need an array of possible tip percentages. This is not a state variable because it will not change.

Finally, we declare the `body` computed variable which will be computed every time a state variable changes.

## First iteration
{% highlight swift %}
struct ContentView: View {
    @State private var checkAmount = 0.0
    @State private var numberOfPeople = 2
    @State private var tipPercentage = 20
    
    let tipPercenteges = [10, 15, 20, 25, 0]
    
    var body: some View {
        Form {
            Section {
                TextField("Amount", 
                            value: $checkAmount, 
                            format: .currency(code: Locale.current.currency?.identifier ?? "USD"))
                    .keyboardType(.decimalPad)
            }
            
            Section {
                Text(checkAmount, format: .currency(code: Locale.current.currency?.identifier ?? "USD"))
            }
        }
    }
}
{% endhighlight %}

![First implementation of the WeSplit app rendered in the canvas. There is just a textField to input numbers (the check amount)](/assets/images/2024-06-20-100-days-of-swiftui/weSplitV1.png)

A new element is the access to some `Locale` value. It holds the identifier for the current currency ("EUR" in my case). It is handled with nil coalescing and a default in case of errors.

Another addition is the definition of the `keyboardType` to the `TextField` object.

## Second iteration 
Next step is adding a picker for the number of people eating at out table.

We start declaring a `Picker` which will be binded to the `numberOfPeople` variable and will show `# of people` as text. In addition we can change how the view to select is shown. Adding a `NavigationStack` around our `Form` we can set the `pickerStyle` to `.navigationLink` to show a new "window".

{% highlight swift %}
struct ContentView: View {
    @State private var checkAmount = 0.0
    @State private var numberOfPeople = 2
    @State private var tipPercentage = 20
    
    let tipPercenteges = [10, 15, 20, 25, 0]
    
    var body: some View {
        NavigationStack {
            Form {
                Section {
                    TextField("Amount", value: $checkAmount, format: .currency(code: Locale.current.currency?.identifier ?? "USD"))
                        .keyboardType(.decimalPad)
                    
                    Picker("Number of people", selection: $numberOfPeople) {
                        ForEach(2..<100) {
                            Text("\($0) people")
                        }
                    }
                    .pickerStyle(.navigationLink)
                }
                
                Section {
                    Text(checkAmount, format: .currency(code: Locale.current.currency?.identifier ?? "USD"))
                }
            }
            .navigationTitle("WeSplit")
        }
    }
}
{% endhighlight %}

<table style="min-width: 50em">
    <tr>
        <td>
            <img src="/assets/images/2024-06-20-100-days-of-swiftui/weSplitV2a.png" alt="Second implementation of the WeSplit app rendered in the canvas. There is just a textField to input numbers (the check amount)"/>
        </td>
        <td>
            <img src="/assets/images/2024-06-20-100-days-of-swiftui/weSplitV2b.png" alt="Second implementation of the WeSplit app rendered in the canvas. There is just a textField to input numbers (the check amount)"/>
        </td>

    </tr>
</table>

## Third iteration
Then, we define our graphical element to input the tip percentage. We use again a `Picker` with the `pickerStyle` as `.segmented`. Moreover, we add a header text for the section holding this new picker to tell the users what they have to do  

{% highlight swift %}
struct ContentView: View {
    @State private var checkAmount = 0.0
    @State private var numberOfPeople = 2
    @State private var tipPercentage = 20
    
    let tipPercenteges = [10, 15, 20, 25, 0]
    
    var body: some View {
        NavigationStack {
            Form {
                Section {
                    TextField("Amount", value: $checkAmount, format: .currency(code: Locale.current.currency?.identifier ?? "USD"))
                        .keyboardType(.decimalPad)
                    
                    Picker("Number of people", selection: $numberOfPeople) {
                        ForEach(2..<100) {
                            Text("\($0) people")
                        }
                    }
                    .pickerStyle(.navigationLink)
                }

                Section("How much do you want to tip") {
                    Picker("Tip percentage", selection: $tipPercentage) {
                        ForEach(tipPercenteges, id: \.self) {
                            Text($0, format: .percent)
                        }
                    }
                    .pickerStyle(.segmented)
                }
                
                Section {
                    Text(checkAmount, format: .currency(code: Locale.current.currency?.identifier ?? "USD"))
                }
            }
            .navigationTitle("WeSplit")
        }
    }
}
{% endhighlight %}
![Third implementation of the WeSplit app rendered in the canvas. There is just a textField to input numbers (the check amount)](/assets/images/2024-06-20-100-days-of-swiftui/weSplitV3.png) 

## Fourth iteration
Finally, we compute the total per person. We create a new computer varible and inside it we add the computation which result will be shown in the last `Text`

{% highlight swift %}
struct ContentView: View {
    @State private var checkAmount = 0.0
    @State private var numberOfPeople = 2
    @State private var tipPercentage = 20
    
    let tipPercenteges = [10, 15, 20, 25, 0]
    
    private var totalPerPerson: Double {
        let peopleCount = Double(numberOfPeople + 2)
        let tipSelection = Double(tipPercentage)
        let tipValue = checkAmount / 100 * tipSelection
        let grandTotal = checkAmount + tipValue
        let amountPerPerson = grandTotal / peopleCount
        
        return amountPerPerson
    }
    
    var body: some View {
        NavigationStack {
            Form {
                Section {
                    TextField("Amount", value: $checkAmount, format: .currency(code: Locale.current.currency?.identifier ?? "USD"))
                        .keyboardType(.decimalPad)
                    
                    Picker("Number of people", selection: $numberOfPeople) {
                        ForEach(2..<100) {
                            Text("\($0) people")
                        }
                    }
                    .pickerStyle(.navigationLink)
                    
                }
                
                Section("How much do you want to tip") {
                    Picker("Tip percentage", selection: $tipPercentage) {
                        ForEach(tipPercenteges, id: \.self) {
                            Text($0, format: .percent)
                        }
                    }
                    .pickerStyle(.segmented)
                }
                
                Section {
                    Text(totalPerPerson, format: .currency(code: Locale.current.currency?.identifier ?? "USD"))
                }
            }
            .navigationTitle("WeSplit")
        }
    }
}
{% endhighlight %}

![Fourth implementation of the WeSplit app rendered in the canvas. There is just a textField to input numbers (the check amount)](/assets/images/2024-06-20-100-days-of-swiftui/weSplitV4.png)

## Fifth iteration
Let's fix the "bug" of the keyboard not disapearing after we edited the check amount.

We add a boolean variable `amountIsFocues` and we mark it as `FocusState`. Then, we bind this variable to the `focused` property of the `TextField` which allows the user to input the amount. Finally, we add a `toolbar` to our `Form` (which will be showed in the `NavigationStack`) with a button to toggle the focus.

{% highlight swift %}
struct ContentView: View {
    @State private var checkAmount = 0.0
    @State private var numberOfPeople = 2
    @State private var tipPercentage = 20
    @FocusState private var amountIsFocused: Bool
    
    let tipPercenteges = [10, 15, 20, 25, 0]
    
    private var totalPerPerson: Double {
        let peopleCount = Double(numberOfPeople + 2)
        let tipSelection = Double(tipPercentage)
        let tipValue = checkAmount / 100 * tipSelection
        let grandTotal = checkAmount + tipValue
        let amountPerPerson = grandTotal / peopleCount
        
        return amountPerPerson
    }
    
    var body: some View {
        NavigationStack {
            Form {
                Section {
                    TextField("Amount", value: $checkAmount, format: .currency(code: Locale.current.currency?.identifier ?? "USD"))
                        .keyboardType(.decimalPad)
                        .focused($amountIsFocused)
                    
                    Picker("Number of people", selection: $numberOfPeople) {
                        ForEach(2..<100) {
                            Text("\($0) people")
                        }
                    }
                    .pickerStyle(.navigationLink)
                    
                }
                
                Section("How much do you want to tip") {
                    Picker("Tip percentage", selection: $tipPercentage) {
                        ForEach(tipPercenteges, id: \.self) {
                            Text($0, format: .percent)
                        }
                    }
                    .pickerStyle(.segmented)
                }
                
                Section {
                    Text(totalPerPerson, format: .currency(code: Locale.current.currency?.identifier ?? "USD"))
                }
            }
            .navigationTitle("WeSplit")
            .toolbar {
                if amountIsFocused {
                    Button("Done") {
                        amountIsFocused = false
                    }
                }
            }
        }
    }
}
{% endhighlight %}
