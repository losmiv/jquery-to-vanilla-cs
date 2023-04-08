source for CheatSheet [here](https://tobiasahlin.com/blog/move-from-jquery-to-vanilla-javascript/ "https://tobiasahlin.com/blog/move-from-jquery-to-vanilla-javascript/")

This is cheatsheet for DOM manipulation differences between jquery and vanilla.

## 1. Selecting Elements
```javascript
  // jQuery, select all instances of .box
  $(".box");

  // Instead, select the first instance of .box
  document.querySelector(".box");

  // …or select all instances of .box  
  document.querySelectorAll(".box");
```

## 2. Running Function on all selected elements
```javascript
  // with jQuery
  // Hide all instances of .box
  $(".box").hide();

  // Without jQuery
  // Iterate over the nodelist of elements to hide all instances of .box
  document.querySelectorAll(".box").forEach(box => { box.style.display = "none" })
```


## 3. Finding one element within another
```javascript
  // With jQuery
  // Select the first instance of .box within .container
  var container = $(".container");
  // Later...
  container.find(".box");


  // Without jQuery
  // Select the first instance of .box within .container
  var container = document.querySelector(".container");
  // Later...
  container.querySelector(".box");
```

## 4. Traversing the tree with parent(), next() and prev()
```javascript
  // with jQuery
  // Return the next, previous, and parent element of .box
  $(".box").next();
  $(".box").prev();
  $(".box").parent();

  // Without jQuery
  // Return the next, previous, and parent element of .box
  var box = document.querySelector(".box");
  box.nextElementSibling;
  box.previousElementSibling;
  box.parentElement;
```


## 5. Working with Events
```javascript
  // With jQuery
  $(".button").click(function(e) { /* handle click event */ });
  $(".button").mouseenter(function(e) {  /* handle click event */ });
  $(document).keyup(function(e) {  /* handle key up event */  });

  // Without jQuery
  document.querySelector(".button").addEventListener("click", (e) => { /* ... */ });
  document.querySelector(".button").addEventListener("mouseenter", (e) => { /* ... */ });
  document.addEventListener("keyup", (e) => { /* ... */ });
```


## 6. Event Listening for Dynamically added Elements
```javascript
  // With jQuery
  // Handle click events .search-result elements, 
  // even when they're added to the DOM programmatically
  $(".search-container").on("click", ".search-result", handleClick);

  // Without jQuery
  // Create and add an element to the DOM
  var searchElement = document.createElement("div");
  document.querySelector(".search-container").appendChild(searchElement);
  // Add an event listener to the element
  searchElement.addEventListener("click", handleClick);
```


## 7. Triggering and Creating Event
```javascript
  // With jQuery
  // Trigger myEvent on document and .box
  $(document).trigger("myEvent");
  $(".box").trigger("myEvent");

  // Without jQuery
  // Create and dispatch myEvent
  document.dispatchEvent(new Event("myEvent"));
  document.querySelector(".box").dispatchEvent(new Event("myEvent"));
```


## 8. Styling Elements
```javascript
  // With jQuery
  // Select .box and change text color to #000
  $(".box").css("color", "#000");

  // Without jQuery
  // Select the first .box and change its text color to #000
  document.querySelector(".box").style.color = "#000";

  // With jQuery
  // Pass multiple styles
  $(".box").css({
    "color": "#000",
    "background-color": "red"
  });

  // Without jQuery
  // Set color to #000 and background to red
  var box = document.querySelector(".box");
  box.style.color = "#000";
  box.style.backgroundColor = "red";

  // Set all styles at once (and override any existing styles)
  box.style.cssText = "color: #000; background-color: red";
```


## 9. hide() and show()
```javascript
  // With jQuery
  // Hide and show and element
  $(".box").hide();
  $(".box").show();

  // Without jQuery
  // Hide and show an element by changing "display" to block and none
  document.querySelector(".box").style.display = "none";
  document.querySelector(".box").style.display = "block"
```


## 10. document ready
```javascript
  // With jQuery
  $(document).ready(function() { 
    /* Do things after DOM has fully loaded */
  });

  // Without jQuery
  // Define a convenience method and use it
  var ready = (callback) => {
    if (document.readyState != "loading") callback();
    else document.addEventListener("DOMContentLoaded", callback);
  }

  ready(() => { 
    /* Do things after DOM has fully loaded */ 
  });
```

## 11. Working with classes
```javascript
  // With jQuery
  // Add, remove, and the toggle the "focus" class
  $(".box").addClass("focus");
  $(".box").removeClass("focus");
  $(".box").toggleClass("focus");

  // Without jQuery
  // Add, remove, and the toggle the "focus" class
  var box = document.querySelector(".box");
  box.classList.add("focus");
  box.classList.remove("focus");
  box.classList.toggle("focus");

  // Add "focus" and "highlighted" classes, and then remove them
  var box = document.querySelector(".box");
  box.classList.add("focus", "highlighted");
  box.classList.remove("focus", "highlighted");

  // Remove the "focus" class and add "blurred"
  document.querySelector(".box").classList.replace("focus", "blurred");
```


## 12. Checking if Element has a Class
```javascript
  // With jQuery
  // Check if .box has a class of "focus", and do something
  if ($(".box").hasClass("focus")) {
    // Do something...
  }

  // Without jQuery
  // Check if .box has a class of "focus", and do something
  if (document.querySelector(".box").classList.contains("focus")) {
    // Do something...
  }
```

## 13. Network requests with .get() or .ajax()
```javascript
  // With jQuery
  $.ajax({
      url: "data.json"
    }).done(function(data) {
      // ...
    }).fail(function() {
      // Handle error
    });

  // Without jQuery
  fetch("data.json")
    .then(data => {
      // Handle data
    }).catch(error => {
      // Handle error
    });
```


## 14. Creating Elements
```javascript
  // Create a div & span
  $("<div/>");
  $("<span/>");

  // Create a div and a span
  document.createElement("div");
  document.createElement("span");

  var element = document.createElement("div");
  element.textContent = "Text"
  // or create a textNode and append it
  var text = document.createTextNode("Text");
  element.appendChild(text);
```

## 15. Updating DOM
```javascript
  // With jQuery
  // Update the text of a .button
  $(".button").text("New text");
  // Read the text of a .button
  $(".button").text(); // Returns "New text"

  // Without jQuery
  // Update the text of a .button
  document.querySelector(".button").textContent = "New text";
  // Read the text of a .button
  document.querySelector(".button").textContent; // Returns "New text"

  // Create div element and append it to .container
  $(".container").append($("<div/>"));

  // Create a div and append it to .container
  var element = document.createElement("div");
  document.querySelector(".container").appendChild(element);

  // Create a div
  var element = document.createElement("div");

  // Update its class
  element.classList.add("box");

  // Set its text
  element.textContent = "Text inside box";

  // Append the element to .container
  document.querySelector(".container").appendChild(element);
```
