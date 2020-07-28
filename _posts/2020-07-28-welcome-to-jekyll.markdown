---
layout: post
title:  "SwiftUI: A Year On"
date:   2020-07-28 15:07:54 +0100
categories: SwiftUI, jekyll updarte
---
The SwiftUI framework was released by Apple at WWDC '19, and promised [a lot](https://developer.apple.com/news/?id=06032019b). WWDC '20 saw even more in the way of SwifUI improvements being announced, which I'll talk about in a future post. When I started my most recent project, I knew that I wanted to see for myself about this new way of building user interfaces - 'better apps with less code'. After my struggles with view controllers and storyboards when creating WhyPhone - particularly with accomodating screen sizes and Dynamic Type - the prospect was appealing.

Unfortunately, I couldn't take advantage of most of the improvements announced at WWDC '20, as they were iOS 14 eexclusive. I was setting out to build a project that was intended to end up on the App Store, and I didn't want to wait until 14's public release. Nonetheless, my first impressions were immediately positive.

One of the first things I noticed about SwiftUI was that it really was a new way of thinking. The SwiftUI view hierarchy - stacks, grids, containers, scroll views - was interesting, but the way of deploying views in code was where things truly differed from my previous experiences. Gone were the days of '@IBOutlets' for labels and '@IBActions' for buttons. Instead I found that UI elements were now contained under the auspices of 'var body: some View {'  and Labels were simply created in code using 'Label'. Buttons were a more interesting proposition, but they too seemed much simpler to create using SwiftUI than they had been. It therefore seemed that creating UI elements programatically in SwiftUI, as opposed to the strange mix of Storyboards and UIKit I had previously employed, was indeed a simpler proposition.

An example of buttons and labels from WhyPhone, 2017.

'''
   @IBOutlet weak var Q4Label2: UILabel!
   @IBOutlet weak var Q4Label: UILabel!
   @IBAction func Q4Button(_ sender: Any) {

'''

And an example from Stadiums using SwiftUI, 2020. This example is of a button that opens the relevant Wikipedia page for the selected stadium.

'''
   Label("Stadiums")
  Button("View on Wikipedia", action: { guard let link = URL(string: self.stadium.wikiLink), UIApplication.shared.canOpenURL(link) else {
    return
          }
    // opens relevant wiki entry for stadium.
     UIApplication.shared.open(link, options: [:],
    completionHandler: nil)
                
                    })
'''


Jekyll requires blog post files to be named according to the following format:

`YEAR-MONTH-DAY-title.MARKUP`

Where `YEAR` is a four-digit number, `MONTH` and `DAY` are both two-digit numbers, and `MARKUP` is the file extension representing the format used in the file. After that, include the necessary front matter. Take a look at the source for this post to get an idea about how it works.

Jekyll also offers powerful support for code snippets:

{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
