# Javascript DOM

### The HTML DOM \(Document Object Model\)

When a web page is loaded, the browser creates a **D**ocument **O**bject **M**odel of the page.

The **HTML DOM** model is constructed as a tree of **Objects**:

The HTML DOM is a standard **object** model and **programming interface** for HTML. It defines:

* The HTML elements as **objects**
* The **properties** of all HTML elements
* The **methods** to access all HTML elements
* The **events** for all HTML elements

In other words: **The HTML DOM is a standard for how to get, change, add, or delete HTML elements.**

\*\*\*\*

### JavaScript HTML DOM Document



| document.getElementById\(_id_\) | Find an element by element id |
| :--- | :--- |
| document.getElementsByTagName\(_name_\) | Find elements by tag name |
| document.getElementsByClassName\(_name_\) | Find elements by class name |



| _element_.innerHTML =  _new html content_ | Change the inner HTML of an element |
| :--- | :--- |
| _element_._attribute = new value_ | Change the attribute value of an HTML element |
| _element_.style._property = new style_ | Change the style of an HTML element |
| Method | Description |
| _element_.setAttribute_\(attribute, value\)_ | Change the attribute value of an HTML element |

### Adding and Deleting Elements



| Method | Description |
| :--- | :--- |
| document.createElement\(_element_\) | Create an HTML element |
| document.removeChild\(_element_\) | Remove an HTML element |
| document.appendChild\(_element_\) | Add an HTML element |
| document.replaceChild\(_new, old_\) | Replace an HTML element |
| document.write\(_text_\) | Write into the HTML output stream |



