---
layout: post
title: "PeerConnectivity"
medium_link: "https://medium.com/@rchatham/peerconnectivity-71ef96477abe#.6m15makjs"
---

## — A functional wrapper for Apple’s MultipeerConnectivity framework. —

PeerConnectivity is a framework that I wrote for simplifying the code needed to write Bluetooth/Wifi networking across iOS devices. It it currently published on Cocopods and is also available for download via Carthage.
<br><br>

If you have ever used Apple’s MultipeerConnectivity framework you know you are in for a world of hurt. There are so many moving parts that it quickly becomes difficult to manage large networking operations between devices. As I was using it in a larger application I began writing wrappers to encapsulate the functionality of the framework and to keep it contained while remaining accessible. Thus… PeerConnectivity was born.
<br><br>

## Setup Connection Manager
<br><br>

Setting up a connection manager to automatically find and connect with nearby devices is as easy as passing in the specified service type (similar to channel).

{% highlight swift %}
let pcm = PeerConnectionManager(serviceType: "local")
{% endhighlight %}

## Starting/Stopping

Start and stop with a single command.

{% highlight swift %}
pcm.start()

// Session active

pcm.stop()

// Session inactive
{% endhighlight %}

## Sending Events to Peers

Sending events is as simple as creating JSON packets and passing them to the network or specified peer.

{% highlight swift %}
let event: [String: Any] = [
    "EventKey" : Date()
]

// Sends to all connected peers
pcm.sendEvent(event)

// Access the connected peers to send to specific peer devices
if let somePeerThatIAmConnectedTo = pcm.connectedPeers.first {
   pcm.sendEvent(event, toPeers: [somePeerThatIAmConnectedTo])
}
{% endhighlight %}

## Listening for Events

Register event listeners to respond to incoming peer events.

{% highlight swift %}
// Listen to an event
pcm.listenOn({ event in
    switch event {
    case .ReceivedEvent(let peer, let eventInfo):

        guard let date = eventInfo["EventKey"] as? Date 
            else { return }
        print(date)

    default: break
    }
}, withKey: "SomeEvent")

// Stop listening to an event
pcm.removeListenerForKey("SomeEvent")
{% endhighlight %}

This makes for an extremely lightweight networking syntax that makes implementing mesh-networking in your app simple. Enjoy 😸.