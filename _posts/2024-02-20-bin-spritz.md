---
layout: post
title: "Binary Spritz ... in binary!"
date: 2024-02-20 10:46:00 +0100
author: Team Binary Spritz
---

Do you want to know the binary ascii of Binary spritz? Here's a quick python script to print it!

{% highlight python %}
x = 'BinarySpritz'

for i in x:
    print(bin(ord(i))[2:], end=' ')
{% endhighlight %}

{% highlight bash %}
1000010 1101001 1101110 1100001 1110010 1111001 1010011 1110000 1110010 1101001 1110100 1111010
{% endhighlight %}

We are using the following functions:

- a **for loop** to iterate over the element in the **string x** 
- a print function with the space char as and to concatenate the elements in a single line
- the **ord** function to translate from char to int, eg ord('B') = 66
- the **bin** function to get a string representing the base2 value 66 = 0b1000010
- we get rid of the 0b string by selecting from the **third** element (`[2:]`) of the string
  
Nice and easy ;)
