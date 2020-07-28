---
layout: post
title:  "SwiftUI: A Year On"
date:   2020-07-28 15:07:54 +0100
categories: SwiftUI
---
The SwiftUI framework was released by Apple at WWDC '19, and promised [a lot](https://developer.apple.com/news/?id=06032019b). WWDC '20 saw even more in the way of SwiftUI improvements being announced, which I will talk about in a future post. When I started my most recent project, I knew that I wanted to see for myself about this new way of building user interfaces - 'better apps with less code'. After my struggles with view controllers and storyboards when creating WhyPhone - particularly with accommodating screen sizes and Dynamic Type - the prospect was appealing. I'm also passionate about making my apps more accessible, and so SwiftUI's promise of beautiful, intuitive UI was a further draw.

Unfortunately, I couldn't take advantage of most of the improvements announced at WWDC '20, as they were iOS 14 exclusive. I was setting out to build a project that was intended to end up on the App Store, and I didn't want to wait until 14's public release. Nonetheless, my first impressions were immediately positive.

One of the first things I noticed about SwiftUI was that it really was a new way of thinking. The SwiftUI view hierarchy - stacks, grids, containers, scroll views - was interesting, but the way of deploying views in code was where things truly differed from my previous experiences. Gone were the days of '@IBOutlets' for labels and '@IBActions' for buttons. Instead I found that UI elements were now contained under the auspices of 'var body: some View {'  and Labels were simply created in code using 'Label'. Buttons were a more interesting proposition, but they too seemed much simpler to create using SwiftUI than they had been. It therefore seemed that creating UI elements programatically in SwiftUI, as opposed to the strange mix of Storyboards and UIKit I had previously employed, was indeed a simpler proposition.

An example of buttons and labels from WhyPhone, 2017.

```
   @IBOutlet weak var Q4Label2: UILabel!
   @IBOutlet weak var Q4Label: UILabel!
   @IBAction func Q4Button(_ sender: Any) {

```


And an example from Stadiums using SwiftUI, 2020. This example is of a button that opens the relevant Wikipedia page for the selected stadium.

```
   Label("Stadiums")
  Button("View on Wikipedia", action: { guard let link = URL(string: self.stadium.wikiLink), UIApplication.shared.canOpenURL(link) else {
    return
          }
    // opens relevant wiki entry for stadium.
     UIApplication.shared.open(link, options: [:],
    completionHandler: nil)
                
                    })
```


As I developed my application, I encountered more and more different UI elements and new ways of doing things. These included the '.sheet' modal, a way of modally presenting a view controller over another view (like present() in UIKit) - only of course without mentioning view controllers. Instead, the simple View is the order of the day in SwiftUI, in all its many forms. One of the most common forms of this can be seen below.

```

struct StadiumDetail: View {

  // define states, environment objects and other variables here
  var body: some View {
    // define UI elements here
      VStack {
        // stacks are used to collect and lay-out UI elements
      }
  }
}
```


As I progressed, I found that this meant that my project files grew in number more than I was expecting, with a new file for almost every View. Some were re-used, like MapView, but many were single-use. As a result, I would strongly recommend a good, easy-to-understand folder structure for a SwiftUI project, to separate views and also to separate them from models or other code files. This greatly improved my own ease-of-access to my files, as well as my project organisation. The number of views was no hindrance, however, and in fact I grew to like it. I also appreciated the ease of including Views in stacks, like so:

```
VStack {
  MapView(coordinate: stadium.locationCoordinate)
                    .edgesIgnoringSafeArea(.all)
                    .frame(minWidth: 0, maxWidth: .infinity, minHeight: 0, maxHeight: .infinity)
}

```


In this example, MapView is used in the StadiumDetail view. Contained in a separate file, it is easily called with MapView() and passed the data it requires. This means that MapView itself needs only be written once - in the MapView file - and then used wherever in the project. With SwiftUI, I found that in general using Views like this was intuitive and easy enough. I also was pleased that the introduced Views conformed to the specified layouts (for example to the Stack they were in) and therefore a seamless UI could be produced.

On balance, I found that my first impressions of SwiftUI were positive. However, there were a number of things I struggled with, and a number of errors that made varying degrees of sense. I was pleased to see at WWDC that Apple plan to fix this in Xcode 12, as during my work on a not too complex project I still managed to encounter a lot of error messages that were opaque at best and misleading at worst. 

The other primary negative was NavigationView and NavigationLink. As Paul Hudson says in [Hacking With Swift](https://www.hackingwithswift.com/articles/216/complete-guide-to-navigationview-in-swiftui), NavigationView is one of the most important components of a SwiftUI app. And basic NavigationViews and Links do work well, passing data between views (in the form of parameters). Customising the navigation bar, however, is more difficult, and I found getting the changes to persist (for example hiding back buttons) extremely difficult. I also encountered a persistent, troublesome problem whereby I had two navigation bars showing on screen, for no apparent reason. At other times the space where an extra bar would be was taken up, but no bar displayed. While many such problems can be resolved by only using one NavView throughout, the fact remains that I found using NavigationView strangely difficult, particularly compared to the intuitive nature of the rest of SwiftUI. Perhaps a navigation-focused Apple tutorial, along the lines of their others on developer.apple.com, would be in order? If this does exist, please send it, because I spent way too much time getting my NavigationViews sorted.

Despite this, I have to say that I found SwiftUI mostly enjoyable to use. It massively reduced the time I would've spent creating UI elements, streamlined the process of using and reusing Views, and was generally, although not always, more intuitive than UIKit. I did note, however, that the more complex my project got, the more SwiftUI errors I ran into. In my opinion, complex projects would be better served either using SwiftUI in moderation, or by sticking with UIKit. That said, however, I would also say that less complex projects can greatly benefit from SwiftUI, even in its early iterations. I'm keenly awaiting being able to use the new features introduced at WWDC '20, and believe that in a couple of years SwiftUI may well be the way to go for all projects, big and small. It was certainly a fascinating learning experience, and as I approach the final stages of my project I'm glad I chose to use SwiftUI. Here's to the next year!

Casey



