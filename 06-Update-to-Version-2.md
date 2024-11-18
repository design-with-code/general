# Designing with Code – Why Should I?
In my article series Designing with Code, I shared [my experience](https://blogs.sap.com/2023/10/29/designing-with-code/) of spending six months working within a product design team. By stepping out of my comfort zone—my beloved design tool—and diving into creating [first prototypes](https://blogs.sap.com/2023/11/05/designing-with-code-part-2-crossing-the-bridge/) using UI5 web components, I found myself much more connected to the actual end result. Using my entry-level coding skills, I gained insights into what happens behind the pixels, which greatly improved my discussions with developers.

In [subsequent articles](https://blogs.sap.com/2023/11/13/designing-with-code-part-3-sap-web-components/), I introduced how designers can leverage web components, CSS, JavaScript, and HTML to create interactive prototypes. This hands-on approach not only deepens your understanding of components but also allows you to experience how they behave in real-world scenarios.

To clarify: I am not a front-end developer. But just as a basic understanding of design benefits developers, designers can work more efficiently by grasping the basics of coding. This is particularly helpful when exploring how components interact or how screen readers interpret your designs. For me, it was a true eye-opener.

I hope this inspires you to get started! You might want to revisit [Part 3](https://blogs.sap.com/2023/11/13/designing-with-code-part-3-sap-web-components/), where I cover a simple prototyping setup, or [Part 4](https://blogs.sap.com/2023/11/20/designing-with-code-part-4-data-document-object-model-and-events/), which introduces the model-view-controller pattern.

# An Update: Why Some Examples No Longer Work
Unfortunately, the examples in my previous articles are now outdated due to two major changes:
* *Updated UI5 Documentation*: The UI5 team migrated their documentation to a [new system](https://sap.github.io/ui5-webcomponents/), integrating a sleek playground feature. This allows you to view live example code, make modifications, and preview results directly in the browser. If you haven’t tried it yet, I highly recommend it! However, this migration rendered the old links to the UI5 web components library invalid, breaking the examples in my articles.
* *Release of UI5 Web Components Version 2*: A new version of UI5 web components introduced [several improvements](https://github.com/SAP/ui5-webcomponents/releases), including refactoring and stabilization, as well as exciting new components.
Given these changes, I’ve updated the examples in the GitHub repository to align with the latest version:
[GitHub Repository – Designing with Code](https://github.com/design-with-code/web-components)

*Disclaimer*: The prototyping setup described here is not intended for production use. For building production-grade applications, please refer to the official UI5 documentation.

# Simple Prototyping Setup
Building production-ready applications often involves complex tools like build systems, testing frameworks, and dependency management. For designers, this can be overwhelming and time-consuming. Thankfully, there are simpler alternatives for prototyping:
## Playground
The UI5 playground allows you to experiment with components by editing code and seeing instant results. This is sufficient for most exploratory tasks. However, the playground doesn’t allow for permanent saving or advanced interactions.
![UI5 Playground](01%20Playground.png)

## Local Prototyping Setup
For more complex prototypes or continuous work, a local setup offers greater flexibility. Below, I outline a minimal installation and configuration process that avoids heavy tools while providing key advantages:
* No need to manage tools or packages locally.
* No build steps—simply refresh your browser.
* Easy sharing of prototypes.

# Setting Up the Prototype: Key Changes in the New Approach

## Import Map vs. Bundle
Previously, we imported a single bundle that included all libraries, making every component available but at a performance cost. The new approach uses an import map, which loads only the components you explicitly reference, improving efficiency and compatibility with real deployments.

![Import Map](03%20Import%20Map.png)

To include a component, locate the <script> tag in the UI5 playground under the expanded code header. Copy and paste it into your HTML file.

![Import Map](02%20Locating%20Resources.png)

I recommend using the sources available on the [GitHub](https://github.com/design-with-code/web-components) repository to get started. These files might also serve you as basis for your own projects going forward. The previous examples are still available. I have added an updated version in parallel folders:
* *Old Setup*: [Part-03-SAP-Web-Components/01_button](https://github.com/design-with-code/web-components/tree/main/Part-03-SAP-Web-Components/01_button)
* *New Setup*: [Part-03-SAP-Web-Components 2.0/01_button](https://github.com/design-with-code/web-components/tree/main/Part-03-SAP-Web-Components%202.0/01_button)

## Manual Imports
With the new setup, you must manually import each required component. Create a main.js file in the same folder as your index.html and add the relevant imports. For example, to use a button component:
 
```javascript
import "@ui5/webcomponents/dist/Button.js";
``` 

If a component doesn’t render as expected, double-check your imports.
The import statement, that is needed to import a component can be found in the documentation under the section “ES6 Module Import”. Figure 3 shows the import statement in the documentation for the [Avatar](https://sap.github.io/ui5-webcomponents/components/Avatar/) component.

![Import Map](04%20Import%20Statement.png)

## Running the Prototype: HTTP Server Required
Modern browsers require HTTP servers to dynamically load resources. You can use:

### Visual Studio Code with Live Preview
Install the [Live Preview](name:%20Live%20Preview%20Id:%20ms-vscode.live-server%20Description:%20Hosts%20a%20local%20server%20in%20your%20workspace%20for%20you%20to%20preview%20your%20webpages%20on.%20Version:%200.4.15%20Publisher:%20Microsoft%20VS%20Marketplace%20Link:%20https://marketplace.visualstudio.com/items?itemName=ms-vscode.live-server) extension for an integrated HTTP server in [Visual Studio Code](https://code.visualstudio.com/).
(Recommended for simplicity)

![Import Map](06%20Preview.png)

### Node.js and http-server
[http-server](https://www.npmjs.com/package/http-server) is a lightweight alternative for more control over your setup.

# Is It Worth the Effort?
Admittedly, this new setup requires more effort compared to the old bundle-based approach. However, it offers significant advantages:

1. *Lightweight and Portable*: Avoid managing local installations while benefiting from version control. Share your prototypes easily using platforms like GitHub Pages.
2. *Realistic Testing*: Standalone prototypes allow you to test interactions like keyboard behavior, screen reader support, and resizing without playground constraints.
3. *Developer-Ready Code*: The new setup aligns more closely with production code, enabling developers to reuse your prototypes effectively.

For quick experiments, the playground remains the fastest option. But for long-term projects or detailed explorations, this setup strikes a great balance between simplicity and functionality.
