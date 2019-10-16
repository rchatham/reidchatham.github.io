---
layout: post
title: why you should rewrite that old objective-c library in swift
medium_link: https://medium.com/@rchatham/why-you-should-rewrite-that-old-objective-c-library-in-swift-c922ea1416f0#.srx9rr4qz
---

## - Why you should rewrite that old Objective-C Library in Swift -


I recently came across the intersection of two Objective-C API’s that I was using from a Swift app where one was known to be rewritten in Swift soon but was very trusted and widely used (JSQMessagesViewController) while the other a much smaller but also well tested framework that had not been updated in a long time (VENTokenField). I wanted to use these two frameworks together to create a new message interface much like the one in the standard messages app but due to a few features they could not be directly used together in the situation in part because of a bug that was going to take a massive amount of fiddling to work around.
<br><br>

I took a good long look at the situation at hand. JSQMessagesViewController’s keyboard observer looks for a UITextView as opposed to VENTokenPicker using a UITextField and so to have the toolbar follow the keyboard properly I was either going to have to work a UITextView into the inner workings of the VENTokenPicker or I was going to have to do the reverse with the keyboard observer.
<br><br>

Needless to say, I felt like doing it in Swift cause I’m not super well versed in writing Objective-C and because it’s ugly and I don’t like it (saying this as I’m applying for jobs that would certainly have me writing it, oh well). I looked at the total code and figured the VENTokenPicker could be rewritten in a total of 3 files in Swift. The whole initial go took 1 day of my time to get it working and another day to smooth out most of the bugs and get the final touches right. I thought not bad. In that time I fixed the bug, rewrote a good but old Objective-C library that wasn’t getting much love into a new Swift one, converted the UITextField into a UITextView (arguably the more correct option), did not have to fiddle significantly with JSQMessagesViewController as the alternative option would’ve forced me to do, and get to feel good about myself as a member of the open source community (**pat myself on the back**).
<br><br>

Now, there are a lot of hiccups when converting code from Objective-C to Swift but at the very least this exercise will give you a better understanding of the differences between the languages and at best make you look like a Swift hero. I expect if you wrote something directly as closely as you could translate it from Objective-C to Swift it would crash immediately but,.... keep trying, you got this!!
