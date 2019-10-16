---
layout: post
title: SwiftyAnimate
medium_link: "https://medium.com/reid-chatham/animation-and-data-structures-in-ios-49cc69b8020c"
---

# Sweet and Swifty Animations

Sweet & Swifty Animations for iOS
Escape the Pyramid of DOOM!

“In computer science, a data structure is a particular way of organizing data in a computer so that it can be used efficiently.” — Wikipedia
These data structures and design patterns let you escape the infamous [anti-patterns](https://en.wikipedia.org/wiki/Anti-pattern) with simple and generally useful solutions. Enter [SwiftyAnimate](http://www.github.com/rchatham/SwiftyAnimate) (The Plug 🔌).

### A better way to animate…
Have you ever tried to string together multiple animations? Yes, of course you have. You wrap each subsequent animation in the completion handler of the previous one and quickly end up writing additional functions just to break up the pyramid of doom (or wormhole of death?). No matter what you end up with it’s not really what you want. Maybe something like this…?

{% highlight swift %}
UIView.animate(withDuration: time, animations: { [unowned self] in

    // animation

    self.animationFunction()

}) {  [unowned self] success in

    // non-animation function

    self.nonAnimationFunction()

    UIView.animate(withDuration: time, animations: {

        // animation

        self.animationFunction()

    }) { success in

        // function that takes time

        self.functionThatTakesTime {

            UIView.animate(withDuration: time, animations: {

                // animation

                self.animationFunction()

            }) { success in

                UIView.animate(withDuration: time, animations: {

                    // animation

                    self.animationFunction()

                })

            }

        }

    }

}
{% endhighlight %}

Pyramid of DOOM!
It’s even in the Apple Developer Documentation!!!

https://developer.apple.com/library/content/documentation/WindowsViews/Conceptual/ViewPG_iPhoneOS/AnimatingViews/AnimatingViews.html

Enter Queues to the rescue! They give you O(1) time complexity for both enqueueing and dequeueing which you DO NOT get with the standard Array type in Swift (Arrays have O(1) average time complexity for append and popLast operations, where popFirst is an O(n) operation).

{% highlight swift %}
internal class Node<T> {

    var data: T

    var next: Node<T>?

    init(data: T) {

        self.data = data

    }

}




internal struct Queue<T> {

    var first, last: Node<T>?

    mutating func dequeue() -> T? {

        let pop = first?.data

        first = first?.next

        if first == nil {

            last = nil

        }

        return pop

    }

    mutating func enqueue(data: T) {

        if last == nil {

            first = Node(data: data)

            last = first

        } else {

            last?.next = Node(data: data)

            last = last?.next

        }

    }

}
{% endhighlight %}

Now we just add our animations to the queue…

{% highlight swift %}
typealias Animation = (TimeInterval, ()->Void)




let animation: Animation = (5.0, {

    // Code to animate

})




let animations = Queue<Animation>()




animations.enqueue(animation)
{% endhighlight %}

…and recursively call the queue in each animation’s completion handler until it is empty.

{% highlight swift %}
func perform() {

    guard let animation = animations.dequeue else { return }

    UIView.animate(withDuration: animation.0, animations: animation.1) { success in

        perform()

    }

}
{% endhighlight %}

Easy enough right?
If you want to take it further check this out. In SwiftyAnimate I wrapped our Queue struct in an Animate class. The Animate class enqueues animations, with the .then(duration: TimeInterval, animations: Animation) method, to a series of operations defined by the Operation enum (with animations being one of the cases). [__the_code__](https://github.com/rchatham/SwiftyAnimate/blob/master/Sources/Animate.swift)

{% highlight swift %}
// Escape the Pyramid of DOOM!

Animate(duration: time) { [unowned self] in

    // animation

    self.animationFunction()

}.do { [unowned self] in

    // non-animation function

    self.nonAnimationFunction()

}.then(duration: time) { [unowned self] in

    // animation

    self.animationFunction()

}.wait { [unowned self] resume in

    // function that takes time

    self.functionThatTakesTime {

        resume()

    }

}.then(duration: time) { [unowned self] in

    // animation

    self.animationFunction()

}.then(duration: time) { [unowned self] in

    // animation

    self.animationFunction()

}.perform()
{% endhighlight %}

Enjoy writing beautiful code! 🎉
