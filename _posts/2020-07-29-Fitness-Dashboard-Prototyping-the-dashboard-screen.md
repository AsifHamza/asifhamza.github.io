---
layout: single
title: Fitness Dashboard - Prototyping the dashboard screen
date: 2020-07-29 19:24:36.000000000 +02:00
tags: [ Swift, Apple, Combine, HealthKit]
classes: wide
social-share: false
header:
    overlay_image: /assets/images/Sunrise.jpeg
    overlay_filter: 0.4
    tagline: "Using SwiftUI as your prototyping tool"
    caption: "Copyright: Asif Hamza"
    show_overlay_excerpt: false
---

The first iteration of this app was my way of learning design and testing out a few technologies I was thinking of using for my day job. I taught myself Sketch and took part in the beta for new design course. That course taught me alot about how to thing about design and UX. Fast forward to today and I no longer have an active copy of sketch. I was thinking of using Figma but after realizing how much fun coding SwiftUI was, I abandoned that idea.
So the approach I am using for this iteration of the app is to do some live prototyping in SwiftUI starting with Dashboard screen which was my least liked screen. It took me hours to get the UIKit Stackviews right.

![Fitness Dashboard]({{site.url}}{{ site.baseurl }}/assets/images/Dashboard.png){: .align-center}

In contrast, it took me 30 minutes to get the following screen in SwiftUI.

![SwiftUI Dashboard]({{site.url}}{{ site.baseurl }}/assets/images/Swiftui_dashboard.png){: .align-center}

Here is the sample code. There is probably a better way to do this. This is what I cam e up with after an hour or so of playing around.

```swift 
    let title: String
    let subtitle: String
    let intensity:String
    let duration: String
    let heartRate: String
    let distance: String
    
    var body: some View {
        VStack(alignment: .center ) {
            HStack (alignment: .center, spacing: 10) {
                Image("CycleCircle")
                VStack(alignment: .leading, spacing: 0) {
                    Text(title)
                        .font(.headline)
                    Text(subtitle)
                        .font(.subheadline)
                        .foregroundColor(.gray)
                }
                Spacer()
            }
            .padding(.horizontal)
            .padding(.top)
            
            Divider()
            HStack(alignment: .center, spacing: 5) {
               
                VStack(alignment: .center, spacing: 5) {
                    Text(intensity)
                        .font(.headline)
                    Text("INTENSITY")
                        .font(.system(size:14))
                        .fixedSize()
                        .foregroundColor(.gray)
                }
                
                Divider().frame(height: 50)
                VStack(alignment: .center, spacing: 5) {
                    Text(duration)
                        .font(.headline)
                        .fixedSize()
                    Text("DURATION")
                        .fixedSize()
                       .font(.system(size:14))
                        .foregroundColor(.gray)
                }
                 Divider().frame(height: 50)
                VStack(alignment: .center, spacing: 5) {
                    Text("\(heartRate) bpm")
                        .font(.headline)
                    Text("HEART RATE")
                        .font(.system(size:14))
                        .foregroundColor(.gray)
                }
                Divider().frame(height: 50)
                VStack(alignment: .center, spacing: 5) {
                    Text("\(distance) km")
                        .font(.headline)
                        .fixedSize()
                    Text("DISTANCE")
                        .font(.system(size:14))
                        .foregroundColor(.gray)
                }
            }
            .padding(.horizontal)
            .padding(.bottom)
        }
        .fixedSize()
        .background(Color.white)
            .cornerRadius(10)
            .shadow(radius: 5)        
    }
}


struct ContentView1: View {
    var body: some View {
        NavigationView {
            ZStack {
               Color.blue.opacity(0.1)
               .edgesIgnoringSafeArea(.all)

                   VStack {
                       CardView1(title: "Last Workout", subtitle: "12 December 2020", intensity: "38", duration: "00:46", heartRate: "141", distance: "45")
                       CardView1(title: "This Week", subtitle: "18 December 2016 to 26 Dec 2016", intensity: "38", duration: "00:46", heartRate: "141", distance: "45")
                       CardView1(title: "This Month", subtitle: "December 2016", intensity: "38", duration: "02:46", heartRate: "141", distance: "300")
                       CardView1(title: "This Year", subtitle: "2016", intensity: "6976", duration: "124:46", heartRate: "141", distance: "1020")
                   }
           }
            .navigationBarTitle(Text("Dashboard"), displayMode: .large)
        }
    }
}

struct ContentView1_Previews: PreviewProvider {
    static var previews: some View {
        Group {
            ContentView1()
            ContentView1()
        }
    }
}

```
