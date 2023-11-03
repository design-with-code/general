# Designing with Code – Part 1: Change of Perspective

You are a designer. You know every little trick of your design tools and you use them every day for ideation, exploration, prototyping, testing, and specification. You work diligently to create a great design that is usable, desirable, technically feasible and compliant to all standards and guidelines. You get as prepared as you can.
But there is this moment of truth where you show your designs to engineering and wait for their verdict...

> “This is not feasible” has been the death sentence to many great design ideas.

You can mitigate this risk by working together with your engineers very early on, iterate together with them if they have time for you and investigate the technical documentation, samples, and sandboxes. The availability of great UI kits in your design tools as well as detailed design guidelines also prevent you from going too far, and many design tools invest into the design-to-developer handover to bridge this gap.

Still, wouldn’t it be great to be more independent as a designer? Wouldn’t it be good to really know what is feasible instead of guessing? Want to discuss on eye-level?

The only way of getting there is by making your hands dirty and start designing with code. This might sound intimidating at first, but with a bit of help, this is not too hard, and it gets extremely satisfying in the long run.

This series of articles is directed towards designers, that want to learn a bit more about the technology behind the SAP design system and how it can be used as one tool to bring our practice further.

## Travel broadens the mind

In 2023, after many years working as a design system expert on the SAP Fiori design system, I had the opportunity to join one of your product areas for six months as a fellow product designer. I was excited to change perspective from someone who provides design guidelines to someone consuming those guidelines. I was tasked to create a new application which is a rare and lucky situation as the bulk of work consists of incremental enhancements of existing applications.

To say this right away - it was a great experience and I wish I had done this much earlier. It was so rewarding to work together with and learn from product managers who were deep experts of their domain. We had regular reviews with customers who would help us validate our ideas and correct our course immediately. I was able to tap into the wealth of experience of my design colleagues who supported me in understanding the background of many design decisions in the product and in finding solutions. And finally, we were lucky to be co-located with the engineering team that also was very supportive and helped clarify technical issues as they occurred. Optimal conditions for a designer to thrive! [Thank you!]

## Explore

After I had gained a first understanding of the task at hand and after I had done the information architecture, persona, use cases and process flows, the design exploration phase could start. The use case mapped very well to an established floorplan in the SAP Fiori Design Guidelines. I used this floorplan as basis and focused on the information and functionality inside.

It is amazing, how fast the number of frames can grow during exploration, especially, if you don’t spend sufficient time on componentization. Keeping the files clean is extremely hard during the exploration phase as everything still is in flux. Even the slightest change can result in touching many frames to carry those changes through. Also, in customer reviews I was always under pressure to have a consistent screen flow available for presentation. As I refined more and more of the interactivity, the prototype became even more complex and harder to maintain.

At a certain point, I was so frustrated with keeping all parts of the prototype in sync that I was looking for an alternative that would save me work. While I have some programming skills in HTML and JavaScript, I would not claim that I am even close to being a developer. I wasn’t sure at all whether I would be able to create the prototype functionality in code. The pain was big enough to make me try. Using the SAP Web Components helped me a lot, as it comes with more than 60 components that already implement our design system. The library also contains the CSS-variables from the Horizon theme so that the parts I had to take care of was mainly content, layout, and interactivity.

As I was only trying to get a frontend prototype and no productive application, I could set up a very simple environment that would fit into a folder and could be shared as a zip file.

From this moment on, the iteration speed increased tremendously. Especially for the interactive parts, improvements could be applied very fast, and I would always be able to present a working prototype to customers. By being able to interact with the prototype, people felt much more like interacting with the final product. People were able to spot issues much easier and got inspired to think about enhancements. The most satisfying thing for me was the fact that table contents were generated from data, which means that changes in the design had to be made in one place only and would be consistently available throughout the application. This saved me a huge amount of time. By having access to the original UI components and theme variables it was easy to stay within the design system.

## Define

As the design stabilized, detailed specification work started. I used my design tool to document the design details for later handover to engineering. This allowed me to share more context and reasoning behind the design decisions and receive comments. I was also able to document alternatives.

I had used the SAP web components in my prototype as it was easy to set up and use for me. But the final product would use a different frontend technology called SAPUI5. SAPUI5 is one of the reference technologies for SAP Fiori and I knew it by heart from a design perspective, but I had never looked at it from a developer’s perspective. SAPUI5 offers a wealth of floorplans, patterns and components implementing the SAP design system but at the same time it is more restrictive on designs outside of this system.

In the process of creating the specification, I had to evaluate the feasibility of my designs in SAPUI5 by creating smaller code snippets in a sandbox environment. Going back and forth between the sandbox, design tool and my older prototype was tedious and time-consuming.

The experience with the previous prototype had given me confidence, so I decided to create another prototype in SAPUI5 to make sure my specification would work out.

Again, I found a way to set up an environment with minimal dependencies and installation. I gathered my sand box snippets and other examples that I could use as basis from my prototype. After some initial issues and a lot of help, I managed to build up a version of my application in the actual target technology SAPUI5. My initial fears of the complexity and steep learning curve turned out to be unjustified.

In this stage, my discussion with engineering intensified and we were able to correct some of the wrong assumptions I had made in my first iteration. Detailed work on interactive behaviors, refinements of the responsive behavior, user validations as well as reviews with accessibility experts and screen reader users could now be done in the target technology revealing also some bugs and enhancement requests for the standard components. Many of the issues they were able to spot would normally only have come up much later during implementation and were now cleared out upfront.

## Limitations

I am not claiming that the prototypes I had created would replace the work of a frontend developer. I believe that my code quality was terrible and many aspects that experienced frontend-developers take for granted have been completely ignored by me.

However, getting my hands into the code and putting together the actual components into a running prototype felt extremely powerful to me. The magic moment when code turns into experience is something I don’t want to miss anymore. I envy you developers for that power, seriously ;-)

My initial fears of the complexity of the setup and implementation turned out to be baseless and the efforts of scanning through documentations and tutorials were offset multiple times by the efficiency I gained. Had I been given more guidance in the beginning; these efforts would have been much smaller, and I would have been able to avoid many of the pitfalls on the way.

I know that one reason for me having the time to take this extra effort was also because I was a fellow in another organization and didn’t have the workload, designers are usually covered with. It is hard to take the risk of diving into a new approach while you have development teams waiting for your specifications.

To make this step easier for other designers I decided to create a series of articles that would help getting started designing with code.

* I will investigate the interplay between design tools and code and how you can make the most out of combining both when designing SAP Fiori applications.
* I will give you an overview of three different ways how you can build prototypes for SAP Fiori applications using either plain vanilla HTML, JavaScript + SAP Web Components, or the SAPUI5 framework, or the popular Angular NG JavaScript framework.
* Later-on I will address specific topics like accessibility or responsiveness and how designing with code can help coming to good solutions.

## Summary and Outlook

Design tools have improved tremendously over the past years, and we can expect them to become even more powerful soon. However, there is nothing compared to the real thing. Like a sculptor who creates exploratory clay models, this is merely an approximation of the genuine bronze piece, with its unique tactile sensations, radiance, mass, and solidity.

Creating prototypes in code can’t replace the design tool but it can complement your design process with a more realistic picture of the final product.

* Realistic interactivity that matches exactly the timing and motions of the actual components gives you a better impression of how these components play together in an interaction flow. This can also include simulating loading times and system failures.
* Building out an interactive prototype helps you identify gaps in your specification you might have missed out and that would usually be raised later by the engineers, such as error handling, empty states, extreme contents, etc.
* Accessibility and keyboard interactions can be tested and refined with different users and interaction devices. Some interactions that seem to be clear before will turn out to be unusable for a screen reader user.
* Using an underlying data structure for the information displayed in the prototype reduces the effort for modifications as changes usually must be applied in a single place to take effect everywhere, as opposed to fixing multiple screens in a screen flow.
* Ensuring the feasibility of designs by using the actual components and their features improves the communication with engineering. This can also include the identifications of specific improvements and enhancements that are outside of the standard functionality.

Designing with code deepens your understanding of the actual matter our products are made of. This can be hard in the beginning but will be extremely rewarding in the long run as it makes you feel more empowered. This hopefully motivates you to read through the next article in this series that tries to build a bridge from your design tool into the development environment.
