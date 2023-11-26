# Designing with Code (Part 5) - Team Player

This is the fifth part of the article series Designing with Code , which has the goal to make a case for designers to get more deeply involved with prototyping their designs with the actual UI technologies at hand. Getting some hands-on experience is so important to understand what it is that you are designing for. To put it in Chris Connors’ words: “Someone designing a chair wouldn’t attempt it without deep understanding of wood, plastic, steel, how they are made, joined, shaped. Code is no different.”

In the past articles, I presented the first steps using web components including some basics of data handling and interactivity. As already described in the first article, during my fellowship in a product design team, the web components were my door opener into prototyping:  

While working on the design for a content-heavy application, I soon got frustrated by the redundant work that was necessary to keep screen flows and variations up to date to reflect changes. Especially the table, which formed the main part of my application was a nightmare for me to handle. Looking for ways to speed things up, I started using web components. After some initial frustration, I became much faster at creating the interactive application using code than any of my design tools. In many cases, the turn-around time from feedback to revised prototype took minutes rather than hours, as often the change had to be applied in a single function rather than in multiple frames or components. That was extremely powerful. 

Also, getting a much better feeling of what the design changes meant in terms of UI implementation helped me to better anticipate the questions that inevitably would come from development when starting to work on it.

As I already had a basic understanding of HTML, JavaScript, and CSS, it was much easier for me to integrate web components than learning a complete framework like Angular, React, or even SAPUI5. And this is the actual beauty of web components: 

**Web components are team players.** 

They integrate into existing HTML applications effortlessly. You can decide to include individual components or you can build up an entire application using web components as well as anything in between, and you can change your opinion at any time during the process. 
Web components are forgiving to sloppy code and lack of architecture; they are just right for every level of proficiency because they let you choose the strictness of the implementation around them. 

There is no decision that can’t be revisited along the way, and that’s extremely powerful when you know as little as I did at the time.

## Lowering Expectations

And this is one of the most important learnings that I took away from my first time of trial and error: 

**Being an experienced designer doesn’t mean I am a good UI developer, and that’s okay.**

I made a lot of mistakes (and I still do), and I was frustrated by the fact that I was not able to lean on the professional experience I normally can when acting as a designer. 

In fact, I was afraid of asking for help because my code was so terrible that I would rather search forever in documentation than ask one of my development colleagues and risk to show them my spaghetti code. But after a while, I noticed that instead of bursting out in laughter, they appreciated my efforts and responded with friendly support. The way our discussions went changed, and I noticed that I started to understand aspects I hadn’t been aware of before. 

I was so used to being the design expert with the mandate to fight for the interests of the user that reacting to push back from development already had become a reflex. And that’s not unjustified, because often we demand additional efforts and create complexity from our engineers to make life easier for our users. Challenging development is part of our profession and so is the suspicion: don’t they build it because it’s not feasible or because they don’t want to?

I will never reach the level of our engineering colleagues, but the more I learn, the more I understand. My questions become more targeted, my suggestions become more valuable, and the discussions happen more on eye-level.

I don’t expect ever to become a good UI developer, but I can already tell that I have become a better designer by better understanding the technical side of what we do.

## Overdo

Another thing I noticed was that I started bypassing the actual design phase. As it was so easy to iterate on the coded prototype, I hardly opened my design tool anymore. That’s both a risk and an opportunity, since it also opens this perspective to you. Have you ever wondered why an implementation seemed short-sighted and not fitting to the rest? Have you ever seen an implementation where things didn’t fit together?

You just have to overdo it and skip the design phase, et voilá!

![02-designer-coder](https://github.com/design-with-code/general/assets/46745939/0eb4693b-de56-4aaa-a376-e9381efe8d84)

*Figure 1 – If you don’t find your Figma shortcut anymore you should be concerned. (Image generated by DALL-E-3)*

Finding myself stuck in the implementation of my prototype taught me the lesson of how important it is to regularly take a step back and look at my work from a distance. Freeing yourself from the “how can I solve this” mindset and getting into the thought process of “what is needed” again reflects the exact same conversation you usually have with development.

**Don’t give up being a designer just because you enjoy coding.**

During the refinement phase, I forced myself into this by regularly updating the design specification, and in that way having to take this more holistic perspective. Describing what I did in code often made me rethink and rework the design and then feed that back in. I also think you shouldn’t open the code editor before you have the first design iteration finished to avoid getting into the solution space right away.

## One Step at a Time

An important learning from working my way into the world of coding was that most setup instructions are targeting developers. As a designer who simply wants to create prototypes, I can keep it simple.

**Don’t let complex setup get into your way.**

Setting up a development environment requires the orchestration of several independent tools and projects into a single development pipeline. A professional developer spends a lot of time on writing test cases, documentation, and so on, and many of the tools are designed to run those tests, control code quality, and detect issues. 

![02-tools](https://github.com/design-with-code/general/assets/46745939/6501b0e3-cfd2-4d0c-9d9b-865ef180ad90)

*Figure 2 - Various tools for HTML and JavaScript*

In other words, much of this is not relevant when creating design prototypes. Now, the setup instructions for UI libraries such as SAP Web Components are not meant for nosy designers but for developers building products. For many, this already means an insurmountable hurdle.

Same here. Getting access to web components wasn’t as easy as I had hoped. Seeing the potential, I wanted to get started with examples that I took from the web components playground (the old non-storybook version). But I was intimidated by the setup instructions that included things that I had never heard of and of which I didn’t understand the purpose. There are only few things as frustrating as spending hours on setting up and installing things you don’t understand and then not being able to change anything because you don’t understand what you are doing and if things don’t work… see above. Learning how to use something is already hard enough, who wants to spend even more effort on the setup?

I learned to avoid any complexity I couldn’t handle. Instead, it is better to start with the simplest setup possible and then slowly add any additions needed. A proper code editor can save a lot of time with code completion and formatting. I also learned to value GitHub, which took me a long time to understand and use. I still didn’t see a need to go for the full setup recommended for application developers, and I will stay away from it until I understand it and understand why I should use it.

## Motivation

Of course, I am passionate about creating business applications, as they hold the hardest design challenges to solve, but many of these challenges are not so much UI challenges rather than process, data, or integration challenges. Solving such challenges is just not as straight forward as fixing the design and can take much more time. In other words, our everyday work as designers often doesn’t give us enough opportunity to spend time working on prototypes and exploring options. 

**So where can we purposefully practice our skills?**

Having meaningful side projects that allow you practicing your skills at your own pace can help a lot. They give you the freedom to try out things without pressure and without limitations. Depending on the type of project, seeing the results of your work immediately and being able to iterate fast can be very rewarding. 
For me, this is a home automation application I use to optimize our energy consumption with my family as an extremely critical user group. 

![03-openhab](https://github.com/design-with-code/general/assets/46745939/537ac2f8-a7b4-4360-a85d-92fd6ed4d0ba)

*Figure 3 – UI of my home automation system built with SAP web components.*

Now, in version 7, I have implemented the entire application using our web components library enjoying the capabilities of the components and the polished design in both light and dark mode. 

If you want to get deeper into the different aspects of development, I can only recommend looking for such a side project you can use to motivate and challenge yourself, be it a Raspberry Pi project or building on a smart home platform like OpenHAB, this can easily grow into a time-consuming hobby.

## Summary and Outlook

In the first set of articles in this series, I have explained why it might pay off for designers to get a deeper understanding of the UI technologies they use. I have tried to show how modern design tools like Figma already prepare you for this step and how discipline in using components and layout can help bridging the gap. In the last two articles I gave you some help to set up a simple development environment and create a first application using our web components library.

What you have seen is that web components are open and flexible, but at the same time they leave a lot to the developer. Currently, there is very little support regarding layout and even component-internal behaviors, manipulating table contents, for example, requires a lot of scripting. If you want to focus on prototyping certain screen flows and interactions without going too deep on the development side, this can be inefficient. 

This is, where a more opinionated framework such as SAPUI5 can be more suitable for you. SAPUI5 is optimized to build SAP Fiori applications and provides a lot of out-of-the-box functionality that takes this burden off your shoulders. Even though it appears extremely intimidating in the beginning, once you have understood how things belong together, you can be much faster with much less effort if you stick with the predefined options. In the next part of this series, which will start after the Holidays, I will introduce SAPUI5 and how it can be easily set up for prototyping.


