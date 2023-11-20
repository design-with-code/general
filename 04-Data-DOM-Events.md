# Designing with Code (Part 4) – Data, Document Object Model, and Events

Creating prototypes in code allows designers to gain a deeper understanding of the way user interfaces are constructed. This can help us become more sensitive towards concerns from engineers, but it can also strengthen the designer's position in discussions with development.

In the [previous article of this series](https://blogs.sap.com/2023/11/13/designing-with-code-part-3-sap-web-components), we created a first simple static prototype. We created a very simple setup with no installation required, and we added all parts of our simple application in a single HTML file. This allowed us to combine web components and place them into layouts we created using flex layouts.

The important thing about prototypes of course is that the display of components isn’t static, and that we can add interactivity much more easily to it with our design tools.

This article will address the most important aspects that are required to add interactivity. It is helpful if you already have some experience with web technologies, but I will attempt to add sufficient information for everyone to follow.

The following topics are necessary to create interactive prototypes:

* **Data model**: our prototype will display a list of addresses with a flag indicating whether we are allowed to send ads to that address. We will allow the user to change this flag and store this in the data model. To make sure the data is consistent, we will encapsulate the data model in a single class that is used by the application to read and change the data.
* **Document object model**: we will create the table rows dynamically from the list of addresses. For this purpose, we will add, remove, and change elements in the HTML document using the document object model operations.
* **Events**: to make the user interface interactive and react to user input, we must listen to the events initiated by the interface components. If a user for instance clicks a button, the button initiates a click event to which we register a method that is then called on click. Event handling is the basis for making user interfaces interactive.

In this article, we will shed some light on each of these aspects.

> [!NOTE]
> All code examples, the full article text, and additional detailed explanations on how to set up the text editor and other topics can be found on the GitHub page for this series: [Design with Code](https://github.com/design-with-code).

## Application

Let's first look at the application we want to build. We want to create a simple application that displays a list of addresses. Each address will have a flag that indicates whether we are allowed to send ads to that address. When the user selects an address from the list, they will see the address details in a dialog. In this dialog, the flag whether ads are allowed or not will be displayed as a checkbox. The user can change this flag by clicking the checkbox and the change is saved.

*Figure 1 - Screen-flow of our simple address application. The application shows a list of addresses. When selecting an entry, the details are shown in a dialog. In the dialog, the user can change the ads flag which will then be saved back into the data model.*

As we can see, the application is about displaying and manipulating the address data. The first step therefore will be to define the address data model.

### Setup

For the examples in this article, we will create four empty files:

* ``index.html`` - The main entry point of the application containing the HTML document and the references to the other resources.
* ``style.css`` - Contains the CSS styles that were in the main document in the styles tag. Putting it in a separate file allows for reuse and better readability.
* ``data.js`` – The JavaScript file that contains the data structure and all methods to access and modify the data.
* ``index.js`` – The JavaScript file that controls the lifecycle and interactivity of the application.

The ``index.html`` looks almost like the one we created in the previous article. We only remove the form elements from the panel, extract the styles into the ``style.css``, and we add additional references to the related files in the header as shown below. It is important to reference the ``data.js`` **before** the ``index.js`` to make sure the data model is available to application logic.

```html
<head>
  ...
  <link rel="stylesheet" href="style.css"/>
  <script src="data.js"></script>
  <script src="index.js"></script>
  ...
</head>
``````

*Listing 1 - Links to the related files in the header element of the HTML document.*

## Data

The data model is the basis for every application. All information displayed in the application and all interaction in the application is related to this data model. It is good practice to encapsulate all functionality used to retrieve or manipulate data in a single class which exists only once in the application.

> [!HINT]
> All examples in this chapter can be found in the [GitHub repository](https://github.com/design-with-code/web-components/tree/main/Part-04-Data-DOM-And-Events/01_data) on "Design with Code".

As you are starting to work with JavaScript now, you might want to make sure that the right information is processed in your application or you need to identify errors in your code. This process is called *debugging* and there are various tools built into your browser to support this. Have a look at the [article on debugging](https://github.com/design-with-code/general/blob/main/A3-Debugging.md) on the GitHub repository.

### Defining the Model

We will now open the ``data.js`` to create the data model. In our application, we want to display a list of addresses and a flag showing whether we are allowed to send advertisements to these addresses or not.

```js
{
  id: 1, 
  name:"Anna Arendt", 
  street:"Kleine Strasse 12", 
  city:"Walldorf", 
  zip: "69190", 
  advertisment: true
}
```

*Listing 2 - A single address shown as a JSON structure.*

Above, you can see an example of a single address as a JSON structure. Our address list will contain an array of multiple such addresses. JSON stands for Java Script Object Notation and is a way to represent JavaScript objects as a string (*serialization*) and convert them back into an object (*deserialization*) again.

To separate the data model from the rest of the application, we are going to create a class that contains all functions to access and modify the data. This class will be instantiated by the application, and the application will only use these functions to access or modify the data to make sure that the data remains consistent and that no invalid changes are applied. We could use these functions to validate or format the changes before writing them into the data structure.

Below, you will find the signature of the ``AddressList`` class. The implementation details can be found in the example code.

```js
class AddressList{
  static getInstance()  // Get an instance of the data model AddressList
  getList()             // Get the actual address list as array [ ]     
  getSortedList(ascending) // Get list sorted ascending (true) 
  getAddress(id).       // Retrieve a specific address by id
  addAddress(name, street, city, zip, ads)
                        // Create a new address by providing the required fields
  removeAddress(id).    // Removing an address from the list
  updateAddress(address)  // Change an existing address
}
```

*Listing 3 - Signature of the AddressList class that is used to encapsulate data access.*

As you can see above, the ``AddressList`` class implements all basic access functions to the data. Apart from that, we don't have to take any care that the data is correct because it is all taken care of by the data model itself. The application can only call these functions and rely on them to work.

*Figure 2 - Data model test. To make sure the data model and all accessor methods work properly, it is helpful to include a little test routine. This is the output in Chrome developer tools console.*

This is very similar to how data access in backend systems can be wrapped by data access objects. The great thing about this is that the consumer of the data doesn't have to know where the data comes from. The access is always the same through the same interface.

If you create such a data model, it is also helpful to create test cases to see whether the methods work in the way you expect them to. In the example code, you also find multiple test cases in the ``index.js``.

### Singleton

To avoid that there are multiple instances of the ``AddressList`` in your application, each with different address lists, we use a *singleton* pattern. Instead of calling the constructor directly with ``new AddressList()``, we use the static ``AddressList.getInstance()`` method, which will always return the same instance with the same data, no matter when and from where we call it in the application. You will see examples for this in the test cases.

### Copy vs. Reference

You will want to make sure that the data in the model is only accessed via the functions of the data model. Therefore, you must ensure that the data that is given out never contains references to the original variables but only copies. In JavaScript as in other programming languages, there is a difference whether you give access to the variable by handing over the reference to it or whether you create a copy of the data and hand over only that.

In the first example, if you call the function ``getList()`` you get a reference to the list. This means that if you change something in the list, it is also changed inside of the ``AddressList`` class by passing the accessor functions, making it hard to control which changes are applied when.

```js
class AddressList{
  list = [];          // The list array

  getList(){
    return this.list; // Returns a reference to the list
  }
}
```

*Listing 4 - The getList function returns a reference to the list. This allows every consumer to modify the list directly.*

Therefore, it is important that we hand over a copy of the original list instead. Now, any change the caller makes on the list only affects their local copy. The spread operator ``[...array]`` can be used to copy the values of an array into a new array.

```js
class AddressList{
  list = [];

  getList(){
    return [...this.list]; // Returns a copy of the list
  }
}
```

* Listing 5 - The spread operator copies the contents of the list into a new object and create a copy. Then a consumer modifies its copy of the list, this does not affect the original list.*

### Summary

Above, we have discussed some important aspects of the data model that is used to hold the application data. The application doesn't access this data directly but uses the access functions provided by the model to ensure consistency. By encapsulating all data into a single model, we can also test the access functions and apply corrections in a single place which makes it much easier to maintain.

Now, as we have the data defined, we can take a look at the user interface elements and how they can be handled in the document object model.

## Document Object Model

Inside the browser, an HTML document is represented as a hierarchical element structure. All elements displayed in the browser are part of the document body. Each element has different properties that determine their appearance and behavior depending on the type of element. Our web components are part of this structure just as any standard HTML elements (e.g., ``div``). Each element is added as a child of another element, and the parent of all elements is the document's ``body``.

All examples in this chapter can be found in the [GitHub repository](https://github.com/design-with-code/web-components/tree/main/Part-04-Data-DOM-And-Events/02_dom) on "Design with Code".

### Setting Element Properties

Inside of the JavaScript code, we can reference elements in the document a function like ``document.getElementById(id)``. On this reference we can now access and change all properties this element has. It is important, that an element has the ``id`` attribute set to get a reference to it, otherwise the function will not return a result.

Let’s assume you have an empty ``span`` element in your document.

You can get a reference to this element via its id. Then you set the element content via the property ``innerHTML``.

```html
<span id="myText"></span>
```

If you now look at this element in the browser, you will see that the element has been changed containing the text.

```js
// Get the html element with the id myText
const span = document.getElementById("myText");

// Set the text between the start and element to Hello
span.innerHTML = "Hello"; 
```

It is important to know that this doesn't change any file permanently, but just changes the document model at runtime in the browser. If you reload the page, all changes will be gone.

```html
<span id="myText">Hello</span>
```

We can use the same mechanism to access the properties of the web components.

```html
<ui5-checkbox id="adsCB" checked="false" text="Allow ads"></ui5-checkbox>
```

We can now get a reference to this element in our code and set the checkbox to checked.

```js
// Get the checkbox in the html document
const cb = document.getElementById("adsCB");

// Set the checked attribute to true
cb.checked = true;
```

This way, we can programmatically control all elements on the page and change labels, contents, or functionality as we need it.

### Accessing Element Methods

We can also access methods of an element to execute some internal logic. For instance, calling the function ``myDialog.show()`` on a reference to a dialog element, will open the dialog overlaying the other contents on the screen. **Please note that in JavaScript we access properties and functions using camelCase (e.g., ``headerText``) that is shown in the documentation and not the hyphenated style (e.g., ``header-text`` used in HTML).**

### Adding and Removing Elements

We can't only access existing elements in the document, but we can also create new elements or remove existing elements from the document. We use this to populate a table with the addresses from our data model.

First, let’s create an empty table with the id ``addressTable`` in our application and define columns for the different data fields.

```html
...
<ui5-table id="addressTable">
  <ui5-table-column slot="columns">Name</ui5-table-column>
  <ui5-table-column slot="columns">Street</ui5-table-column>
  <ui5-table-column slot="columns">City</ui5-table-column>
  <ui5-table-column slot="columns">ZIP</ui5-table-column>
  <ui5-table-column slot="columns">Ads</ui5-table-column>
</ui5-table>
...
```

When we open this table in the browser, it will be empty and just display the column headers. We could manually create the table rows by adding a ``ui5-table-row`` for each address in the address list. But as we want to be able to change the contents, we will create these rows using code.

In the ``index.js`` we create the logic that generates the rows. You will find the commented code in the example files.

First, as the document is loaded completely and all static parts of the document are available, the ``onload`` event will be triggered. We use this event to initialize our table with the sorted address list.

```js
// When the document is loaded this lifecycle hook is called
onload = () => {

  // We use this to update the data rows in the table.

  // Instead of using the list as is, we use the sorted list
  const sortedList = addressList.getSortedList(true);
  
  // We now call the update function
  updateAddressTable(sortedList);
} 
```

In the ``updateAddressTable(list)`` function, we iterate over the list of addresses and add a new row for each address as a child to the table.

```js
// Function to update the table contents
function updateAddressTable(list) {
  // Do some clean up first
  ...

  // Retrieve the table element from the html document
  const table = document.getElementById("addressTable");
  
  // Iterate the list and create a row for each item
  list.forEach((address) => {

    // Call the function that creates the row
    const row = createTableRow(address);
    // Append the row to the table
    table.appendChild(row);
  });
}
```

New elements are created using the ``document.createElement(elementName)`` function. Here, a new ``ui5-table-row`` is created for each address.

```js
// Function to create a new table row for an address
function createTableRow(address){

  // Creating the html element with the name ui5-table-row
  const row = document.createElement("ui5-table-row");
  row.id = address.id;  // Set the id
  row.type = "Active";  // Set the active property to be able to trigger events
  ...
  
  // Create the table cells for the address fields
  const nameCell = document.createElement("ui5-table-cell");
  nameCell.innerHTML = address.name; // The cell content is the address name
  
  // Append the cell to the row
  row.appendChild(nameCell);
  ...
  
  // Return the row that has been create to the caller
  return row;
}
```

Inside of this function we create the ``ui5-table-cells`` that contain the actual data. The cells are added as children to the row so that in the end we have created a table row for each address and a table cell for each field within the address.

*Figure 3 - The application with a row appended to the address table for each address.*

Now, as we begin to generate the UI from the data instead of manually adding table rows, it is not important how many rows we want to display anymore. Also, we can adjust and enhance the way we render our information in one place, and this change will become effective everywhere.

For instance, if we want to display whether ads are allowed or not as a checkbox instead of a string, we just need to adjust the way this cell is rendered in one place, and it will be available everywhere.

```js
// Inside of the create table row function
...

const adsCell = document.createElement("ui5-table-cell");

// Create a check box 
const cb = document.createElement("ui5-checkbox");
cb.checked = address.advertisment; // Is checked if advertiment is true
cb.readonly = true;                // We don't want to change this value
adsCell.appendChild(cb);           // Add the checkbox into the cell

row.appendChild(adsCell);
...
```

*Figure 4 - The flag indicating whether ads are allowed is now displayed as a read-only checkbox.*

### Shadow DOM

Web components hide their internal structure by placing it in a so-called shadow DOM. This hidden part of the document is protected from access via the document object model, and you normally shouldn’t have to care about it. In some cases, a web component offers access to specific elements of the hidden structure using the parts so that you can apply certain styles. We use this for instance in the ``style.css`` to remove the padding from the panel content area for the table.

### Summary

We have added logic to our application that generates parts of the user interface based on the data model. This means that we can also adjust the user interface when the data model changes. In the first two parts of this article, we have laid the foundation for an interactive prototype. Now, we need to add event handling to make the prototype interactive by responding to user input.

## Events

User interface elements are designed to display data as well as to offer means to interact with the data. Each user interface element has a specific purpose (e.g., button -&gt; initiate action) and according to that purpose offers certain events. Most events are based on user input (e.g., ``click``) but can also be based on system events (e.g., ``onload``).

All examples in this chapter can be found in the [GitHub repository](https://github.com/design-with-code/web-components/tree/main/Part-04-Data-DOM-And-Events/03_events) on "Design with Code".

If we want a certain function to be initiated by a user input, we must register this function as an event listener in the element. The element will then inform every event listener if the event is triggered.

```js
// Get the button from the document
const btn = document.getElementById("myButton");

// Use the addEventListener method to tell the button which function should
// be called when the user clicks. Here, we use an anonymous function that is
// declared inline. Here, the handleClick function will be called.
btn.addEventListener("click", (event) => handleClick(event)); 
```

We have now registered the ``handleClick()`` function to be called when the event is caused. The event parameter that is handed to the ``handleClick()`` function contains the event context, e.g., what control has caused the event or what row in the table has been clicked. In this example, the ``event.target`` property is a reference to the button that initiated the event.

```js
// Function called on click
function handleClick(event){
  const btn = event.target; // getting a reference to the button
}
```

In many cases, we don't need the information of the event in the event handler function, because the purpose of the function is clear.

### Button Event

We could for instance offer a button that switches the form factor between cozy and compact mode.

```js
// Getting a reference to the button element from the document
const formFactorButton = document.getElementById(“formFactorButton”);

// Register an event listener to the buttons click event
formFactorButton.addEventListener(“click”, (e) => toggleFormFactor(e));
// On click, the toggleFormFactor function will be called
```

As the user clicks the button, the event handler function is called and either sets or removes the <code>ui5-content-density-compact</code> class from the document body element.

```js
// Function holding the functionality to toggle between cozy and compact mode
function toggleFormFactor(e){

  // By adding the content density class to the HTML body, the entire
  // application will be displayed in compact mode (using less space)
  document.body.classList.toggle("ui5-content-density-compact");
}
```

As we can see in the figure below, the dimensions of some elements are adjusted and optimized for either touch (cozy) or desktop (compact) devices.

*Figure 5 - Application switched from cozy to compact form factor.*

### Table Event

In our address list application, we want to display a dialog with the address details when a user selects a table row. To allow the table row to create an event on click, we need to set the mode to ``active``, otherwise, we will not receive any events, even if we set an event listener. Then, we add and event listener to the table, which collects the events from all rows.

```js
// Getting a reference to the table
const table = document.getElementById("addressTable");

// Adding an event listener for the row-click event
table.addEventListener("row-click", (e) => showDetails(e));
```

In this event handler function we then open and populate the data into the details dialog. We use the event context to find out which table row has been selected using the ``event.detail.row.id``. As the row id is the same as the id of the address display in this row, we can get the address from the data model and set the address values in the dialog.

```js
// This function is called when a user clicked a table row
function showDetails(e){
  // Get a reference to the dialog element, which currently still is hidden
  const dialog = document.getElementById("detailsDialog");

  // Get the row id that has been clicked from the event context
  const selectedId = e.detail.row.id;

  // Get the address for the id from the data model
  selectedAddress = AddressList.getInstance().getAddress(selectedId);

  // Set the respective texts and values in the dialog
  ...
    
  dialog.show();
}
```

Before that, we have already added the dialog to the ``index.html``, so that here we only need to show it.

To complete the functionality of the application, we make sure that when the user closes the dialog, we compare whether they have changed the state of some of the checkboxes and update the data model if this is the case. If the data model has been updated, we also update the table and show a message toast.

*Figure 6 - Final application flow where the user can select an address, sees the details, changes the agreement and where changes are applied and confirmed by a message toast.*

### Summary

With events, our application can now react to user input and is finally interactive. Based on the user input, we can change the user interface and the data model and with that, cover a large part of what an interactive prototype is supposed to do.

## Summary and Outlook

This article addressed some of the most important concepts of web-based frontend development:

* How to handle **data** that we want to display in the application. Having a single data model is important to allow for interactivity and user input as the prototype progresses. Initially, if you only want to assemble components to a static prototype, this is not necessary.
* How to manipulate the **document object model (DOM)** of the application, which in the end is just an HTML document. This is important to dynamically create contents or react to user interaction. If you want to construct parts of the prototype based on the data model, like for instance the table we used, this is a very powerful way.
* How to make the application interactive by registering **event** listener methods that run code based on user input like a button click or a table selection. This is crucial to make a prototype interactive and requires both, understanding of the DOM-handling and a data model to work efficiently.

There are other things that you will need as you want to create more and more detailed and powerful prototypes like using stylesheets with CSS and using the [theme variables](https://github.com/design-with-code/general/blob/main/A2-Theme-Variables.md) but for now, the most important thing is that you try to get an understanding of these basic concepts that you will need going forward. If it is too overwhelming for a start, just play around with the code you can download from the [GitHub repository](https://github.com/design-with-code/web-components/tree/main/Part-04-Data-DOM-And-Events) and apply smaller changes to see what happens. Take your time! :-)

In the [previous article](https://blogs.sap.com/2023/11/13/designing-with-code-part-3-sap-web-components) of this series, you learned how to set up a simple prototyping environment for [SAP web components](https://sap.github.io/ui5-webcomponents/). In this article, you have learned how you can make an interactive prototype using a data model, the document object model, and event handling to react to user input and programmatically control all elements of your application.

While the articles can't go into all the details, you can find detailed listings and comments in the [GitHub repository "Design with Code"](https://github.com/design-with-code). You can download the examples from there and run them on your own computer. You can use the examples as a basis for your own prototypes and explorations.

Acquaint yourself more deeply with the [SAP Fiori Design Guidelines](https://experience.sap.com/fiori-design/) and the [SAP Web Component documentation](https://sap.github.io/ui5-webcomponents/) to get more information about how to design SAP Fiori applications using the web component library. For all the other topics that you need there is plenty of documentation and tutorial guidance available, so that it will be easy for you to find some that best serves your needs. I can recommend the [Mozilla Developer Network](https://developer.mozilla.org/) documentation for every question related to JavaScript and CSS. In many cases, it can also be useful to ask [ChatGPT](https://openai.com/), which can create detailed listings and instructions for your specific questions.

In the upcoming articles, we will describe prototyping with other UI technologies offered by SAP, such as SAPUI5 and SAP Web Components for Angular, and how these frameworks add complexity, but also support to your prototyping efforts. We will also take a look at specific topics related to prototyping and interactivity.
