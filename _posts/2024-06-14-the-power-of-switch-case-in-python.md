---
layout: post
title: "The power of the match statement in Python"
date: 2024-06-14 10:02:00 +0100
author: "Marco Ferrati"
categories : python
---

The `match` statement has been added to the Python programming language since version 3.10 (in 2021).

Usually, you can find it as an alternative to the `if-elif-else` statement. If so, why bother adding it to the set of Python’s statements? Let’s start with a comparison of the notation in an example where both statements do the same thing:

{% highlight python %}
def if_elif_else(n: int):
  if n == 0:
    print("n is 0")
  elif n == 1:
    print("n is 1")
  elif n == 2:
    print("n is 2")
  else:
    print("n is something else")
{% endhighlight %}

{% highlight python %}
def match_case(n: int):
  match n:
    case 0:
      print("n is 0")
    case 1:
      print("n is 1")
    case 2:
      print("n is 2")
    case _:
      print("n is something else")
{% endhighlight %}

Up to now, the `match` statement has not added anything new. Its true power comes when we use it with a concept called [Algebraic Data Type](https://en.wikipedia.org/wiki/Algebraic_data_type).

## Algebraic Data Type
An ADT is a disjoint union of tuples of types that could be mutually recursive. The advantage is when we read them, because given a type, the compiler/interpreter **can be sure of its components**. A drawback is that they are not extensible (with respect to classes).

Their idea is very similar to `Enums`, with the improvement of being able to carry data alongside.

## Usage in Python
For our example we consider the scenario where we have to send an instruction to a robot. The possible actions are:
- Go to the position P(x, y)
{% highlight json %}
{
  "type": "set_navigation_goal",
  "coordinates": "x, y"
}
{% endhighlight %}
- Send a generic message M(text)
{% highlight json %}
{
  "type": "send_message",
  "message": "stop"
}
{% endhighlight %}
- Do nothing 
{% highlight python %}
None
{% endhighlight %}

### if-elif-else
In the following listing, we check which type of actions we are handling and then retrieve the data we are interested in.
{% highlight python %}
def get_action() -> dict|None:
  # Do something to read the action to perform
  return action

def move_to(coordinates):
  # Tell the robot to move to the given coordinates
  ...

def send_message(text):
  # Send the message to the robot
  ...

action = get_action()
if action is None:
  print("No action required")
elif action.get("type") == "set_navigation_goal":
  raw_position = action.get("coordinates")
  move_to(raw_position)
elif action.get("type") == "send_message":
  message = action.get("message")
  send_message(message)
else:
  print("Action not supported")
{% endhighlight %}


### match-case
With the `match` statement, the action type checking and the data retrieval are both performed by the `case` clause.
{% highlight python %}
def get_action() -> dict|None:
  # Do something to read the action to perform
  return action

def move_to(coordinates):
  # Tell the robot to move to the given coordinates
  ...

def send_message(text):
  # Send the message to the robot
  ...

action = get_action()
match action:
  case {"type": "set_navigation_goal", "coordinate": raw_position}:
    move_to(raw_position)
  case {"type": "send_message", "message": message}:
    send_message(message)
  case None:
    print("No action required")
  case _:
    print("Action not supported")
{% endhighlight %}

## Conclusion
As you can see, the use of the match statement allows for a cleaner way to handle multiple types of actions without the complexity of data retrieval. This is possible thanks to the `match-case` statement, which is capable of "understanding" the different types of actions and creating "generic variables" on the go.
