---
layout: single
title: Introduction - Creating a Fitness Dashboard using SwiftUI, Combine and Healthkit
date: 2020-07-28 19:24:36.000000000 +02:00
tags: [ Swift, Apple, Combine, HealthKit]
classes: wide
social-share: false
header:
    overlay_image: /assets/images/cyclingDawn.jpeg
    overlay_filter: 0.4
    caption: Photo by [Flo Karr](https://unsplash.com/photos/nCj0zBLIaAk) on [Unsplash](https://unsplash.com/)
    show_overlay_excerpt: false

---

A couple of years ago, I wrote about how I developed an app to help me be more consistent with my fitness goals. This app helped me with two main goals I had at the time - gamify my training and up my iOS Swift game. I posted some screenshots from the finished application below. I say finished, but I mean "Finished for me" as the app was never polished enough to release on the app store.

![Fitness page]({{site.url}}{{ site.baseurl }}/assets/images/HeartRate-and-Zones.png){: .align-center}

I briefly mentioned this app in my previous post on consistency. Working on the app allowed me to kill two birds with one stone. It gave me a way to investigate technologies I was proposing for a commercial app. Technologies such as Swift which seem mature enough at release 2.3 as well as using Realm (now known as [MongoDB Realm](https://realm.io)) as an on-device cache/database. It also allowed me to create something personal and useful to me, i.e. a way to track and gamify my fitness. Once the app reached an acceptable state, I ceased to work on it actively. Updates were limited to getting it to work on newer iPhone devices. 

![App Diagram]({{site.url}}{{ site.baseurl }}/assets/images/FitnessAppWorkflow.png){: .align-center}
Many thanks to my friend [Rennay](https://rennay.dev) for the diagram above.

## Time for a change?
Two things have changed in the last four years. The Swift ecosystem has grown. Swift 5.3, SwiftUI 2.0, and the reactive framework Combine are some of the technologies that I would like to try.
My fitness workflow has also changed. In 2016 my primary source of workout data was my Garmin bike computer (for outdoor rides) and my Apple Watch Series 0 (for indoor strength workouts). Garmin did not have a readily available API at the time, and so I sent the data to Strava and used its API instead. I had to manually sort workout records since they came from two disparate sources.
All of that changed when I upgraded to an Apple Watch Series 4. The better battery life and built-in GPS meant that I could record the outdoor workouts on my Apple Watch as well as on the Garmin bike computer. My Apple Watch now recorded all my workouts which meant that I no longer required the Strava API.

## Updating the app for 2020
I debated whether to alter the existing app or start from scratch. It was not clear to me whether or all the libraries I used would be viable or even necessary.

Here is the list of changes I had in mind.

- Upgrade the codebase from Xcode 10 and Swift 3 to Xcode 11 and Swift 5.3
The existing app was first written in 2016 using Xcode 8 and Swift 2.3. Swift 5 contains names changes for specific API's as well as new language constructs. The names changes would be more straightforward as XCode does offer suggestions most of the time. The newer language constructs might prove more challenging.

- Remove the Strava API
Removing the Strava API would remove a significant amount of complexity in the application. I could retrieve the workout data using HealthKit. No more network calls, rate limits and changing APIs.

- Replace the RealmDB with CoreData or perhaps no DB at all
I used Realm because I wanted to combine the Strava data with health data stored on the phone. RealmDB was sort of a local cache to prevent too many hits to the Strava API. I also liked the event-driven nature of the database. Since I planned to remove the calls to Strava, there is no real need for a separate on-device database.

- Remove the Charts Library and use SwiftUI instead
Upgrading to Swift 5 meant upgrading the Charts library to version 3.0, which had a different API. Some rework would be required if I wanted to continue using it. From what I have read, SwiftUI makes it easier to build charts, and that might be a fun thing to try. Removing the Realm and Charts libraries also meant that I could remove the entire CocoaPods file. The potential is there for a significant reduction in complexity and code.

- Improve the UI ( especially some of the icons)
I don't think I did a terrible job in creating the UI given that I'm not a designer. There were, however, instances where the design could be more consistent. As an example, consider the icons for the monthly statistics section in the image below. They don't seem to fit with the overall app design.

![Fitness Dashboard]({{site.url}}{{ site.baseurl }}/assets/images/Dashboard.png){: .align-center}

There was something also not quite right with the UX flow of the application. My original idea was to have a dashboard screen showing overall fitness statistics and then having the ability to drill down into specific areas. The actual implementation consisted of subsequent screens embedded in navigation controllers.


![Fitness Summary]({{site.url}}{{ site.baseurl }}/assets/images/Weekly-summary.png){: .align-center}

The result was an app that was not as intuitive to use (for everyone but myself).
In the end, I decided to approach the rewrite by creating a series of small experiments to test out each of the above aspects. The first of these would be to figure out how to call HealthKit from SwiftUI. 
![New App Architecture]({{site.url}}{{ site.baseurl }}/assets/images/plannedarchitecture.png){: .align-center}
The diagram below shows the planned architecture. Thank to Rennay again.