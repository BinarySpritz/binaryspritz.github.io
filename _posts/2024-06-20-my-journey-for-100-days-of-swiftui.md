---
layout: post
title: 'My journey in "The 100 days of SwiftUI"'
date: 2024-06-20 10:02:00 +0100
author: "Marco Ferrati"
categories : swift
---
In this blog post, I will log my journey in learning Swift and SwiftUI by following "[The 100 days of SwiftUI](https://www.hackingwithswift.com/100/swiftui)".

There are two reasons for this diary to exist and be publicly available: first, to share my thoughts about the language and the framework, and second, as a review of the learning process proposed by "The 100 Days of Swift," which, as the title says, you have to follow for one hundred days. Moreover, as I am a person who already knows some programming languages, I was curious about how a new language is taught.

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
print("anArray has \(anArray.count) elmennts of which \(aSetFromAnArray.count) are unique")
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

