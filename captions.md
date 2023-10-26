# Caption

## Slide 1

## Slide 2

Before we start, you can access the slides, captions and the links I reference throughout my talk from the QR code. This goes to a Github repo, and the slides are published on the GitHub pages as well that you can find the link on the repo description. 

## Slide 3

Technology choices have ethical ramifications. This quote is from a blog post called “Modern Health, frameworks, performance, and harm” and it is written by my brilliant colleague Eric Bailey - who is a senior accessibility designer at github. 

The post mainly discusses how technology choices impact user experience and can even result in harm. 

I still remember how eye-opening I found it when I read this blog post. And I wanted to share it with every developer I know because it was making great points. After all, Eric’s blog post inspired me to give this talk. 

I encourage you to read it with Eric’s own words and emotions that are very well reflected in his writing - but today I’d like to talk about one of the main takeaways I got from the post 


## Slide 4

The choices we make everyday, as technology makers, have a direct impact on someone's quality of life. 

## Slide 5

And today, I’d like to specifically focus on how our choices impact the performance of the web applications we are building today. And how does that really reflect on our users? 

Are we building applications that can be used by anyone however they encounter it?

Or do we create inaccessible experiences because of our “not so intentional” choices? 

How world wide applications are we building today?


## Slide 6

To start with, web performance is variable. It depends on the internet speed, bandwidth and latency, because all determines how soon users can download the necessary resource to their devices. 

It is also highly dependent on the device capabilities, because after downloading these resources, they need to be processed there there as well. 

And the speed and the device capabilities varies from network to network, device to device, user to user

I'd like to think that these are the physical components that make web performance variable. 


## Slide 7

On the other hand, there are psychological factors that impact how users perceive the performance. It is more like how fast it feels to them.

And it depends on quite a lot of things too. 

For example, what are the user's expectations? Do they just want to quickly grab the phone number of a restaurant or do they want to order food online?

It is reasonable to expect a longer load time when ordering food than just wanting to access the phone number of the restaurant.

Same goes the other way around. What value are we providing? If we are rendering a data intensive page, and if the user knows this, they will be more willing to wait for it.


## Slide 8

It is also important to recognise that the content we are delivering impacts how users perceive the performance. 

For example, say our website is a platform to order party supplies, most of the time it is safe to assume people are in a happy place and they are just shopping 

but if we are developing a health platform that people check their medical results in, it is important to empathise that they are probably in an anxious state. And when we are anxious, waiting time feels slower. 


## Slide 9

When thinking about all these components that impact web performance, and how our users perceive the waiting times, I can’t help but think that we can't solve everything with just checklists. 
There are great tools out there to help us understand the performance, measure it by simulating internet speed and the devices, they provide resources to improve specific metrics but how can they take users' mental state into account? Or the content/value we are delivering.

So, for delivering truly inclusive applications, it is crucial to develop empathy for our users.

And I appreciate that building empathy for our users is not a straightforward development advice as much as writing tests but coming back to how we started, I think being intentional about our technology choices, solving the problems in a way that is specific to our users, our content rather than applying generic solutions we found on the internet all is a part of building empathy.

## Slide 10

So, where do we start then?

Web performance is already an overwhelmingly complex subject and now we are talking about building empathy, looking at how it impacts web accessibility - it is a lot - I get it. 

How about we start with javascript?

## Slide 11

Why?
Because, we as developers love it and use it, a lot.

## Slide 12

Here is a graph that shows the distribution of requests by content type. 

Javascript comes as second and at the median, there are 22 js requests on desktop and 21 on mobile per page. This is some huge number that needs a bit of an attention.

## Slide 13

Another reason that I wanted to focus on javascript today is because javascript is expensive compared to other resources

## Slide 14

Executing JavaScript demands more computational resources, because it is a CPU-bound task. And, what that means is that the time that the task is completed depends on the CPU performance.

And this task can be challenging and problematic on mobile and low-end devices due to having lower cpu speed.

it is also important to look at its impact of on the main thread.
The main thread is where a browser processes various tasks, such as parsing HTML, executing JavaScript, rendering the page, and handling user input.

By default, the browser uses a single thread to run all the JavaScript in the page unless web and service workers are intentionally used. 
This means having many scripts running can cause delays in event processing and rendering and that will be directly reflected in the users experience. 

To have a responsive user experience, it’s important to minimize the main thread's workload. The less JavaScript is sent, the lighter the burden on the main thread.

## Slide 15

One of the first things that we can do to better understand our javascript consumption is to start looking at our bundles and see what is in them.

## Slide 16

There are great tools out there to visualise bundles to understand the contents of our bundles.
They really help with finding out what modules make up the most of the bundle size, is there anything that is not used and got there unintentionally and I think overall these resources provide a great start for optimisation. 

## Slide 17

What is interesting is that, more often than not you might find there are unused modules in your bundle.

Here is another graph that shows the distribution of unused javascript per page. 90% of the pages load over 600 KB unused javascript per page.

When contrasted with the total number of bytes loaded for mobile pages at the median, unused JavaScript accounts for 35% of all loaded scripts.

I think this is fascinating to know. 

This data might be interpreted in multiple ways but one a way could be that maybe some pages are loading scripts that may not be used on the current page, or are triggered by interactions later on in the page lifecycle or got slipped into the bundle unintentionally which is not rare.

## Slide 18

Coming back to our original angle, and looking at performance through an accessibility lens, what does unused and excessive amount of javascript actually use mean to our users?

First and foremost, Downloading unused or unnecessary javascript is a wasteful data and can even set a barrier for mobile users who don’t have unlimited data plans. 

And executing will be slower and so much worse on less capable devices or for those using assistive technologies.  

Also, use of an excess javascript resources, let alone slowing down the execution, it can even leave entire groups of people out.

These are significant ramifications that require an urgent attention to look at our javascript consumption. 

## Slide 19

One way to load javascript more intentionally is using a technique called code splitting. 

## Slide 20

Code splitting is a technique that aims to split large bundles into multiple smaller ones by leveraging dynamic imports. So that we can lazily load our javascript when we need it rather than including everything in one giant bundle.

It is supported by modern bundlers like Webpack or Rollup. 

Main motivation behind this technique is reducing the initial bundle size and minimising the startup time.

## Slide 21

Code splitting is a good alternative for optimising statically imported components. 

Here is an example of a very simplified time tracking app that shows logged times in a chosen week with the option to customise the graph style.

And in this example, we load all our components statically and especially if you pay attention to the pop up that displays a variety of graph styles, this also comes with our initial bundle but we don’t need it until the user decides to change their graph style. And they might not even change it at all. 


## Slide 22

There are various ways to split the code, for example we can do route based code splitting and load the bundle when that page is requested, or using intersection observer to load them when they become visible in the viewport.

Or like here in this example, we can load them on when the user interacts with them.

## Slides 23

Reducing the initial bundle size with code splitting helps a lot with responding to our users quickly because after all there will be less resources to download and execute in the initial load. 

And with this way, we will be able to provide some sort of content to our users sooner in the page lifecycle

This gives our users also the assurance that something is happening.  It is important, because the longer they are with a blank screen or a spinner, the more uncertain they might feel. Because they don’t know what is happening or is it even happening. And with uncertainty, similar to being anxious, waiting time feels longer. If we go back to the medical result example, imagine how anxious this waiting time will be. 

## Slide 24

If we look at tangible ways to measure how soon we render our first content, we can reference the FCP metric.

It measures the time from when the page starts loading to when any part of the page's content is rendered on the screen.


## Slide 25

Responding quickly and rendering the first content is a great start but it is very unlikely that it is what our users came to our page for. We need to render the rest of the content, especially our main content as soon as possible after we render the first content. 

I appreciate that it is a difficult task for browsers to know what the main content of our app is and there have been various metrics recommended by the Google Chrome team in the past…

## Slide 26

but these days they recommend LCP (largest contentful paint) that measures the time from when the page starts loading to when the largest element is rendered on the page.

Browsers continuously work to improve heuristics to ensure that these metrics reflect our users’ expectations.

## Slide 27

How do we make sure we render our largest contentful paint, early in the life cycle of our page?

As pretty much everything, it depends on a lot of things but it is heavily influenced by how we choose to render our app

## Slide 28

Let’s have a look one of the most popular rendering patterns, Client Side Rendering.

Server sends the response..

## Slide 29

And response looks something like “ReactDOM.createroot….”

So we are rendering our entire app with Javascript.

## Slide 30

Is it bad?

Let’s see the rest of the timeline.

After the browser receives the response, it downloads and executes the javascript and then our application will be viewable and interactive. 

Because javascript is a CPU bound task, the time between the browser receiving response and the time that our page is viewable will entirely depend on how good the user’s device is. 

This doesn’t seem an inclusive and equal experience to me. 

## Slide 31

And if we take this further, and look at another case where

Server sends a response, browser downloads the js 

## Slide 32

But what if something happens and the browser fails to execute the javascript?

We will end up pretty much with a broken blank useless page.

## Slide 33

And I can’t help but think - you had one job.

Just rendering the page. We are not even trying to make it interactive yet. Just viewable. 

We failed to provide to our users and we have no idea what kind of inconvenience we caused to them.

Is there an alternative?

## Slide 34

With a different rendering strategy we can eliminate the possibility of failing to render our page. And it is generating our HTML on the server.

## Slide 35

Let’s see how it is different from the client side rendering

Again, server sends a response.. 

## Slide 36

But this time our response looks more like this. Return open tag html and the rest of the markup.

## Slide 37

After the browser receives the response that includes our pre-generated static HTML, browser parses it ,renders and our page will be viewable way earlier in the page lifecycle. 

## Slide 38

Compared to the client side rendering

## Slide 39

It is a huge gain for our users 

Because they will receive the main content quickly

And It is a compassionate practice, we don’t leave them long in uncertainty with blank screens or spinners

Also because we are taking care of the rendering of the page in “our” servers, this takes us a step further to provide a more equal and inclusive experience. 

Because how soon our application becomes accessible to users won’t depend entirely on their device capabilities anymore.

## Slide 40

Server side rendering really helps with making the page viewable as early as possible, but this doesn’t solve our entire problem. We want to provide more interactive and richer user interfaces to our users, so to be able to do that we still have some javascript to execute on the client side.

## Slide 41

This stage is called hydration. It mainly means attaching Dom events to our static html that we generated on our servers to make the page more interactive.  
It is crucial for our users to be able to view the page as early as possible regardless how powerful their devices are but we need to be mindful of the time between when our page looks ready and when our page is interactive.

## Slide 42

There are a few metrics that specifically track interactivity. TTI is a helpful metric to refer to understand when our applications get responsive and interactive.

The TTI metric measures the time from when the page starts loading to when its main sub-resources have loaded and it is capable of reliably responding to user input quickly.

## Slide 43

And the time that our application becomes interactive depends on our hydration strategy we choose. Do we want to fully hydrate the page or progressive hydration, there are quite a lot of patterns out there and can really depend on the type of application we are building and that is a whole other topic.

One thing doesn’t really depend on the type of application though, is the amount of javascript needs to be hydrated.

## Slide 44

And this brings me to my next point - is less javascript possible?

Surely, but what I mean here is that is there a way to achieve the same level of interactivity with less javascript?

## Slide 45

The solution is not another futuristic library that takes up less space in the bundle, it is actually the opposite. Going back to basics, using native solutions. 

Although it sounds no brainer, I don’t think we leverage the native solutions as much as we should.

Most of the time, opting in for a native solution won’t only help with our javascript bundle size but it will bring us a whole lot of benefits that will make our page more accessible out of the box. 

There has been really cool releases recently in browser apis and css space. If you had a chance to watch the “What's New in CSS in 2023” talk yesterday, Steve’s talked about really cool CSS features as well including trigonometric function, has property, container queries, you should check out the recording if you missed the talk.

## Slide 46

One of them that I was very excited about is the popover API. 

Popovers are very common and we see them in tooltips, menus, dialogs. Even though they are super common, building them is still a lot of manual work. You need to add scripting to manage focus, open and close states, accessible hooks into the components, keyboard bindings to enter and exit the experience

But with the new popover api, all this really comes out of the box

Default focus management. Opening the popover takes the next tab inside the popover
Light-dismiss functionality. Clicking outside of the popover area will close the popover and return focus to the popover trigger. 
Accessible keyboard bindings. Hitting the esc key will close the popover and return focus to the trigger element. No more globally listening esc key press events
Promotion to the top layer. Popovers will appear on a separate layer above the rest of the page, so rest in peace z-index:10000


## Slide 47

The Popover example comes from my favourite design system Primer. Github’s design system that I feel very lucky to be a part of. 
We recently refactored our react tooltip component to use the popover API, and I witnessed all of the benefits of this native solution from the first hand.

Shout out to my colleague, Keith Cirkel who tremendously helped me with this work. 


## Slide 48

And the browser support is pretty good. And Firefox is working on releasing it soon without the flag. 

## Slide 49

How about no js?
I know it doesn’t sound very practical especially for rich user interfaces but hear me out. 

I think  we should care about how our applications behave if JS fails to execute.

I believe it would be an inclusive practice to provide at least the main content and the functionality of our applications even if javascript is failed to load or it is disabled. 

For example if my app is making doctor appointments, I think my users should be able to at least fill up that appointment form and submit. 

And this is possible without JS.

Forms or links can definitely be enhanced by JavaScript, but preferably should function without it.

## Slide 50

There are common industry patterns that support this purpose and they are Progressive enhancement and graceful degradation.

In a nutshell, Progressive enhancement aims to provide a baseline of the essential functionality and the content to as many users as possible, while delivering enhanced experiences to users who have access to more modern devices and browsers.

On the other hand, Graceful degradation is centered around building modern web applications and rich user interfaces that will work in higher technology devices and newest browsers, but still falls back to delivering essential content and functionality in older browsers and low end devices.

Both great strategies but totally depends on the case and the state of the application. 

## Slide 51

Inclusive web applications don’t become that way overnight. We need to put in the work and consistently show up every single day for change.

Here are a couple of practises that I think might be helpful to develop with performance in mind

Check in at a PR time

## Slide 52

Integrating an automated job that reports the bundle size into your CI could be really helpful as a regular reminder.

For example we use this GitHub action in my team and it reports the bundle size changes everytime when a PR is created. 

You can’t practically maybe take an action in every time when there is an unexpected bundle increase, 
But still good practice to create awareness around the changes in the bundle size.

## Slide 53

There are even more advanced tools out there that generate very detailed performance reports at a PR time. This is from Calibre, they are an Australian based company and they do really cool work in This space

## Slide 54

Include in your code review. This could be adding a merge checklist item to our pull request template to make sure that we do our tests and don’t introduce any performance regression with that PR, if not we are improving.

Or as a code reviewer, we can try to review the code from a performance lens. Is there an alternative native solution to this new npm module or if not maybe a smaller one? Is there an opportunity to load this component dynamically when it is actually needed? Just adding a few questions to your code review belt, can make a huge difference, 

Educate yourself and your team if you are a manager. This is our web, this is our responsibility, we gotta do the work.

And test. Test it with trotting the network, simulating devices that are less capable - run lighthouse regularly to check in and read through the recommended resources. To see if there's anything to optimise.


## Slide 55

Tech Choices matter - they have a power to shape how people experience the web
Executing Javascript is a CPU bound task - its performance is heavily dependant on the device capabilities
Be mindful of Javascript consumption - because it doesn’t come for free
Check your bundle - what is in there? 

## Slide 56

Leverage code splitting to dynamically load javascript on demand - look for opportunities. 
Opt in for native solutions where possible - HTML and CSS are so much cooler than we aware 
Aim for applications to function even JS fails - remember no.js is the coolest javascript framework :)

## Slide 57

Develop inclusivity in mind, this is our web.

## Slide 58

Thank you





