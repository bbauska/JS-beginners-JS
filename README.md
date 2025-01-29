<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2>DOM Query Selector Methods</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<p>The Document Object Model provides a set of methods that allow 
you to select a specific element in the HTML nodes. They are the 
<b>querySelector()</b> and <b>querySelectorAll()</b> methods.</p>
<p>The <b>querySelector()</b> method is a JavaScript method from the 
document object that allows you to retrieve a single Element object 
that matches the CSS selector passed to the method.</p>
<p>The CSS selector is the pattern you use when targeting a specific
element for styling. Here’s an example of CSS selectors:</p>

```
/* Selecting all elements with the id value of box */
#box {
}

/* Selecting all elements with the class value of btn */
.btn {
}
```

<p>The pattern you need to pass to the <b>querySelector()</b> method can be 
as simple or as complex as you need.</p>
<p>For example, here’s how to use the method to retrieve an element 
with an id attribute of 'box':</p>

```
document.querySelector('#box');
```

<p>The <b>querySelector()</b> method always returns the first element that 
matches the query. The method searches for the element from the 
top to the bottom of the DOM tree.</p>
<p>The string parameter passed to the <b>querySelector()</b> method follows 
the CSS selector pattern, where class is represented by a period '.' 
and id is represented by a hash '#'.</p>
<p>Suppose you have the following HTML element on your page:</p>

```
<body>
<h1>Query Selector</h1>
<h2>Learning Query selector method</h2>
<p id="opening" class="bold">Placeholder</p>
</body>
```

<p>You can retrieve the &lt;p&gt; element by passing "p" as the method’s argument:</p>

```
let element = document.querySelector('p');
console.log(element);
// <p id="opening" class="bold">Opening</p>
```

<p>Or you can also pass the id or the class attribute, it will return the
same &lt;p&gt; element:</p>

```
document.querySelector('.bold');
// <p id="opening" class="bold">Opening</p>

document.querySelector('#opening');
// <p id="opening" class="bold">Opening</p>
```

<p>When you pass a selector that returns two elements, only the first 
element will be returned by the method. The following code tries to
fetch both &lt;h1&gt; and &lt;h2&gt; elements:</p>

```
document.querySelector('h1, h2');
// <h1>Query Selector</h1>
```

<p>Above, you can see that the method returns the first match, which is the &lt;h1&gt; 
element.</p>
<p>And that’s how the <b>querySelector()</b> method works. When you need to retrieve more 
than a single element, you need to use the alternative <b>querySelectorAll()</b> method 
instead.</p>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2>querySelectorAll() Method</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<p>The <b>querySelectorAll()</b> method is a JavaScript method from the 
DOM API that allows you to retrieve all elements that match the 
CSS selector you passed as the argument.</p>
<p>For example, here’s how to use the method to retrieve any element 
that has the class attribute of box:</p>

```
document.querySelectorAll('.box');
```

<p>The string parameter passed to the <b>querySelectorAll()</b> method 
follows the CSS selector pattern, where <b>class</b> is represented by a 
period '.' and <b>id</b> is represented by a hash '#'.</p>
<p>To retrieve all copies of a specific element, you can simply pass the
name of the element as its argument.</p>
<p>Suppose you have the following HTML element on your page:</p>

```
<body>
<p id="opening" class="bold">Opening</p>
<p id="middle">Middle</p>
<p id="closing" class="bold">Closing</p>
</body>
```

<p>You can retrieve all &lt;p&gt; elements by passing 'p' as the method’s argument:</p>

```
let elements = document.querySelectorAll('p');
console.log(elements);
// NodeList(3) [p#opening.bold, p#middle, p#closing.bold]
console.log(elements[0]);
// <p id="opening" class="bold">Opening</p>
```

<p>Or when you only need the opening and the closing <p> elements,
you can pass either the class or the `id`s as the argument:</p>

```
document.querySelectorAll('.bold');
// [p#opening.bold, p#closing.bold]
document.querySelectorAll('#opening, #closing');
// [p#opening.bold, p#closing.bold]
You can also select elements by other attributes like target or value:
// return all elements with target="_blank"
document.querySelectorAll('[target=_blank]');
// return all elements with value="red"
document.querySelectorAll('[value=red]');
```

<p>The return value of the <b>querySelectorAll()</b> method will be an 
array-like object called <b>NodeList</b>.</p>
<p>To access elements of the <b>NodeList</b> object, you can use the index 
position. You can also use the <b>forEach()</b> method to iterate over the
elements:</p>

```
let elements = document.querySelectorAll('p');
// 1. Access element at index 0
console.log(element[0]);
// 2. Iterate over the elements using forEach()
elements.forEach(function (element) {
  console.log(element);
  element.style.backgroundColor = 'yellow';
});
```

<p>The code above will log the current element inside the loop and set its 
<b>background-color</b> value to "yellow";</p>
<p>The <b>querySelectorAll()</b> method always returns a <b>NodeList</b> object 
even when you only have one matching element.</p>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2>Hide Form Steps With CSS</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<p>Back to the Wizard Form Application, we need a way to show and hide the form steps using 
CSS and JavaScript. Add the following rules in <b>style.css</b>:</p>

```
.step {
  display: none;
}
.step.active {
  display: block;
}
```

<p>This causes all the div tags with the step class to be hidden from display. To show the 
form step add the class active to the <b>step1</b> div as follows:</p>

```
<div id="step1" class="step active">
  <div class="form-group">...</div>
</div>
```

<p>Go back to the browser, and you now see only the first step of the
wizard form being displayed.</p>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="#add-btn">Adding the Next Button</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<p>Now we need some buttons to move between the form steps, so add the following button on 
<b>step1</b> div:</p>

```
<div id="step1" class="step active">
  <div class="form-group">...</div>
    <button type="button" class="btn btn-primary f-right" onclick="nextStep()">Next</button>
</div>
```

<p>In this button, we add the <b>onclick</b> attribute so that we can run JavaScript 
code when the button is clicked. The name of the function we want to call is 
<b>nextStep()</b>, so let’s create that function in our <b>script.js</b> file. We also 
need a <b>showStep()</b> function that will:</p>

```
let currentStep = 1;
function nextStep() {
  if (currentStep < 3) {
    currentStep++;
    document.querySelectorAll('.step').forEach(function (element) {
      element.classList.remove('active');
    });
    document.querySelector(`#step${currentStep}
    `).classList.add('active');
    document.querySelector('#currentStep').textContent = currentStep;
  }
}
```

<p>In the <b>script.js</b> file, we declared a variable named <b>currentStep</b>, which is used to let us 
know in what step the form is currently in. In the <b>nextStep()</b> function, we used the 'if' 
statement to check if the <b>currentStep</b> is less than 3 because the form only has 3 steps.</p>

<p>To move to the next step, we increment the <b>currentStep</b> value by one using the "++" 
operator, then we use the <b>document.querySelectorAll()</b> method to select all elements 
containing the step class. We remove the <b>active</b> class from all form steps.</p>

<p>After that, we select the current step and add the <b>active</b> class to the 
element using the <b>classList.add()</b> method. The final task is to 
change the content of the <b>currentStep</b> paragraph to the <b>currentStep</b>.</p>
<p>Open the wizard form in the browser, and you should be able to 
navigate to step 3 using the <b>next</b> button. But notice that you can’t
go back to the previous step! This is what we’re going to implement next.</p>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="#add-prev">Adding the Previous Button</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<p>Now we need another button to move to the previous step. On <b>step2</b> and <b>step3</b> 
div tags, you can add the following buttons:</p>

```
<div id='step2' class='step'>
  <div class='form-group'>...</div>
  <button type='button' class='btn btn-secondary' onclick='prevStep()'>
    Previous
  </button>
  <button type='button' class='btn btn-primary f-right'
    onclick='nextStep()'>
    Next
  </button>
</div>
<div id="step3" class="step">
  <div class="form-group">...</div>
  <button type="button" class="btn btn-secondary" onclick="prevStep()">
    Previous
  </button>
</div>
```

<p>Next, we need to add a <b>prevStep()</b> function to the <b>script.js</b> file:</p>

```
function prevStep() {
  if (currentStep > 1) {
    currentStep--;
    document.querySelectorAll('.step').forEach(function (element) {
      element.classList.remove('active');
    });
    document.querySelector(`#step${currentStep}
    `).classList.add('active');
    document.querySelector('#currentStep').textContent = currentStep;
  }
}
```

<p>The <b>prevStep()</b> function is identical to the <b>nextStep()</b> function, except for 
the 'if statement' check and decrementing the <b>currentStep</b> part.</p>

<p>Instead of writing the same code in two different functions, we can create a new function 
that runs the query selectors part. Let’s name this function <b>showStep()</b>.
Your <b>script.js</b> file should look as follows:</p>

```
let currentStep = 1;
function showStep() {
  document.querySelectorAll('.step').forEach(function (element) {
    element.classList.remove('active');
  });
  document.querySelector(`#step${currentStep}`).classList.add('active');
  document.querySelector('#currentStep').textContent = currentStep;
}

function nextStep() {
  if (currentStep < 3) {
    currentStep++;
    showStep();
  }
}

function prevStep() {
  if (currentStep > 1) {
    currentStep--;
    showStep();
  }
}
```

<p>Back to the browser, now you can go to the next and previous steps with the buttons. 
The last thing we need to do is to style these buttons. Right now they look pretty bad:</p>

```
.f-right {
  float: right !important;
}
.btn {
  color: #fff;
  cursor: pointer;
  font-size: 1rem;
  line-height: 1.5;
  border-radius: 0.25rem;
  padding: 0.375rem 0.75rem;
  border: 1px solid transparent;
}
.btn-next {
  border-color: #007bff;
  background-color: #007bff;
}
.btn-previous {
  border-color: #6c757d;
  background-color: #6c757d;
}
```

<p>The <b>.f-right</b> style adds the float property to the element to move it to the 
right, the <b>.btn</b> is used to style the buttons. The <b>.btn-next</b> and 
<b>.btn-previous</b> styles add border and background colors to the respective elements.</p>

<p>The final task is to add the <b>submit</b> button and display the data collected by 
the form.</p>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="#add-submit">Adding a Submit Button</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<p>Back to the project, the final task we need to do on the Wizard Form is to add a <b>submit</b> 
button to the third step, so let’s do it. Add the <b>submit</b> button to the <b>step3</b> 
div as follows:</p>

```
<div id="step3" class="step">
  <div class="form-group">
    <label for="password">Password</label>
    <input class="form-control" name="password" type="password" placeholder="Enter password" />
  </div>
  <button type="button" class="btn btn-previous" onclick="prevStep()">
    Previous
  </button>
  <button type="submit" class="btn btn-submit f-right">Submit</button>
</div>
```

<p>Add the <b>CSS</b> for the <b>submit</b> button in <b>style.css</b> as follows:</p>

```
.btn-submit {
  border-color: #28a745;
} 
background-color: #28a745;
```

<p>Now we need to listen when the <b>submit</b> button is clicked.</p>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="#listen">Listening to Form Submit Events Using JavaScript</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<p>Besides the DOM API, the browser also expose signals known as events that you can use as 
a cue to run a specific code. We have done this earlier when adding the onclick attribute 
to the buttons:</p>

```
<button type='button' class='btn btn-secondary' onclick='prevStep()'>
  Previous
</button>
<button type='button' class='btn btn-primary f-right' onclick='nextStep()'>
  Next
</button>
```

<p>The <b>onclick</b> HTML attribute is a shortcut to listen to the click event.</p>
<p>When the previous button is clicked, we run the <b>prevStep()</b> function. When the next 
button is clicked, we run the <b>nextStep()</b> function.</p>
<p>Aside from using the <b>onclick</b> attribute, we can also add event listeners using the 
<b>addEventListener()</b> method.</p>
<p>Let’s add an <b>event listener</b> so that we know when a form is submitted. The Wizard 
Form we created has an id attribute, so you can select that form using JavaScript.</p>

```
const wizardForm = document.querySelector('#wizard-form');
```

<p>Next, you need to call the addEventListener() method and listen to
the 'submit' event as follows:</p>

```
const wizardForm = document.querySelector('#wizard-form');
  wizardForm.addEventListener('submit', function (event) {
  // TODO: handle the submit event
});
```

<p>Now that we can listen to the submit event, we need to interrupt the default behavior of 
the form so that JavaScript can take over. To do so, we need to call the 
<b>event.preventDefault()</b> method inside the function we passed to the 
<b>event listener</b>:</p>

```
const wizardForm = document.querySelector('#wizard-form');
wizardForm.addEventListener('submit', function (event) {
  event.preventDefault();
});
```

<p>The <b>preventDefault()</b> method interrupts the default flow of the submit event, 
which will cause the browser to refresh the current page.
From here, you can instruct JavaScript to do specific tasks to the form data submitted 
by the user.</p>
<p>The form object has an object property named elements that store all input elements you 
define inside the form. Inside the object, you can access the value of input fields by 
specifying its name attribute, followed by the value property.</p>
<p>Here’s how to get the values for our Wizard Form:</p>

```
event.preventDefault();
const email = wizardForm.elements.email.value;
const username = wizardForm.elements.username.value;
const password = wizardForm.elements.password.value;
```

<p>Finally, we display the data using the JavaScript <b>alert()</b> function, which;</p>

```
const email = wizardForm.elements.email.value;
const username = wizardForm.elements.username.value;
const password = wizardForm.elements.password.value;
alert(`Registration complete! Your details: \n
Email: ${email} \n
Username: ${username} \n
Password: ${password}`);
```

<p>You can test the Wizard Form in the browser. Fill in the <b>textboxes</b> and you’ll 
get an alert when clicking the submit button:</p>
<p>Just to make the application smarter, we can reset the form after it has been submitted 
by the user:</p>

```
const email = wizardForm.elements.email.value;
const username = wizardForm.elements.username.value;
const password = wizardForm.elements.password.value;
// alert(...);
wizardForm.reset();
currentStep = 1;
showStep();
```

<p>The <b>reset()</b> method from the form will reset all <b>textboxes</b>, then we 
set the <b>currentStep</b> variable to 1 and run the <b>showStep()</b> function to 
reset the interface.</p>

<h2>Taking Care of Repeating Code</h2>

<p>If you look closely, you might notice that the code for the Next and Previous buttons 
in the steps are identical. Instead of writing them in the HTML file, we can use 
JavaScript to add them dynamically.</p>
<p>First, select all the steps <b>div</b> using <b>querySelector()</b> as follows:</p>

```
const stepsDiv = document.querySelectorAll('.step');
stepsDiv.forEach((element, index) => {
  if (index === 0) {
    element.innerHTML += nextButton;
  } else if (index === stepsDiv.length - 1) {
    element.innerHTML += previousButton;
    element.innerHTML += registerButton;
  } else {
    element.innerHTML += previousButton;
    element.innerHTML += nextButton;
  }
});
```

<p>Next, declare three variables containing the HTML buttons tag:</p>

```
const stepsDiv = document.querySelectorAll('.step');
const previousButton =
  '<button class="btn btn-secondary" onclick="prevStep()"
type="button">Previous</button>';
const nextButton =
  '<button class="btn btn-primary f-right" onclick="nextStep()"
type="button">Next</button>';
const registerButton =
  '<button type="submit" class="btn btn-success f-right">Register</
button>';
```

<p>Now, we need to iterate over the elements using the <b>forEach()</b> 
method. We can check if the element is the first or the last step 
from the index value.</p>
<p>For the first element at <b>index 0</b>, we only add the next button. For 
the last element, we add the previous and submit buttons, for all 
the middle elements, we add the previous and next buttons:</p>

```
stepsDiv.forEach((element, index) => {
  if (index === 0) {
    element.innerHTML += nextButton;
  } else if (index === stepsDiv.length - 1) {
    element.innerHTML += previousButton;
    element.innerHTML += registerButton;
  } else {
    element.innerHTML += previousButton;
    element.innerHTML += nextButton;
  }
});
```

<p>To check if the element is the last step of the Wizard Form, we compare the index value 
with the <b>stepsDiv.length - 1</b> value.</p>
<p>To add an element to existing elements, we use the '+=' assignment operator.</p>
<p>Now we can remove all &lt;button&gt; elements from the HTML file. Run 
the Wizard Form in the browser again, and you’ll see the buttons added using JavaScript.</p>
<p>The Wizard Form is finished. You can check the completed
application at https://github.com/nathansebhastian/js-wizard-form/tree/main/complete</p>

<h2>Summary</h2>
<p>Congratulations on finishing your first JavaScript project! The Wizard Form application 
helps you learn the idea of using JavaScript to manipulate what you see on the screen.
Although a Wizard Form looks complex, it’s actually pretty easy when you have the steps 
mechanism created using JavaScript.</p>
<p>Let’s recap what we’ve learned in this project:</p>

  1. How to select HTML elements using <b>document.querySelector()</b> and <b>document.querySelectorAll()</b>
  2. Show and hide elements using CSS and JavaScript
  3. Conditionally display HTML elements using variables, if statements, and functions
  4. An introduction to browser events
  5. Handling a form submit event with <b>addEventListener()</b>
  6. Retrieve, display, and reset form data with the event object
  7. Add elements to specific parts of the HTML document with the <b>innerHTML</b> property
  
<p>And the most important thing is that you’ve seen how an application can be built 
step-by-step and gradually becomes more complex.</p>
<p>In the next chapter, we’re going to learn how to use JavaScript to send and receive data 
from a backend service.</p>

<h2>Chapter 13: Asynchronous JavaScript and Callbacks</h2>
JavaScript is a non-blocking, synchronous programming language.
What does this even mean? It means that JavaScript doesn’t wait
until a code finished running before running the next one (non-
blocking)
Synchronous means sequential, and we know this because
JavaScript runs code line by line from the top to the bottom.
Why is this important? Let me show you an easy example.
The window object of the DOM has a method called setTimeout() that
you can use to run a function after a specific amount of time.
The method accepts two arguments:
1. The function to execute after the timeout
2. The amount of time to wait in milliseconds
For example, here’s how to wait 3 seconds before running a
console log:
setTimeout(function () {
console.log('Hello!');
}, 3000);
Run the code above from the console, and after 3 seconds, you
should see the 'Hello!' string printed.
Now, let’s add some console log before and after the setTimeout()
method as follows:
console.log('Start');
setTimeout(function () {
console.log('Hello!');
}, 3000);
console.log('End');
Now we have 'Start' and 'End' strings which should be printed
before and after the setTimeout() method has finished executing.
When you run the code above, you will see this output:
image::images/3-4-example-settimeout.png
Surprise! The 'End' string got printed ahead of the 'Hello!' string.
This is because of the non-blocking nature of JavaScript.
The synchronous nature of JavaScript makes it read the code line
by line from top to bottom. But because it’s non-blocking,
JavaScript executes the setTimeout() method, then continue code
execution to the next line.
This is not a bug. It’s an expected behavior of JavaScript because of
the way it’s designed.
And this is important to know because when you’re developing a
website or application, there will be times when you send data to a
server, and you need to wait for the response before continuing
code execution.
To make JavaScript wait until a specific operation has been
completed, we need to use what’s known as the callback function.
Callback Functions Explained
A callback function is simply a function passed into another
function as an argument. The callback function would then be used
by the function when the situation is right.
The function we passed into the setTimeout() method above is a
callback function. So does the function we passed into the
addEventListener() method.
Back to the example above, we can make JavaScript wait for the
setTimeout() method to finish before printing the 'End' string by
moving the console log line below 'Hello!' as follows:
console.log('Start');
setTimeout(function () {
console.log('Hello!');
console.log('End!');
}, 3000);
But of course, we can do this because we’re the ones who added the
setTimeout() method.
If we imagine the setTimeout() method as a part of code that we
can’t touch, like the addEventListener() method, how do we make
sure that it runs a certain instruction after the timeout?
The answer is to use a callback, just like the addEventListener()
method. In the example below, imagine that you can’t modify the
content of the processData() function:
function processData(data, callbackFn) {
setTimeout(function () {
console.log('Sending data back');
const response = {
data: data + 'abc',
};
callbackFn(response);
}, 3000);
}
Here, the processData() function accepts two parameters:
1. The data parameter to process
2. The callback function to execute after the process
To get the response from the function above, we need to call that
function and pass both data and a callback function.
Here’s how you do it:
processData('Nathan', function (response) {
console.log(`Response given: ${response}`);
});
This callback pattern is used not only when responding to events,
but also when sending data to another server.
We don’t know in advance how long a server needs to process the
data, so we put a callback function that will be executed when the
response is ready.
Summary
In this chapter, you’ve learned that JavaScript is a programming
language that doesn’t stop to wait for a function that takes time to
finish. It will continue to run the next line of code when the
previous line isn’t completed yet.
The callback function is a way to make JavaScript run in an
asynchronous manner. The next step of the operation starts only
when the previous operation is completed.

Chapter 14: Promises
A Promise is an alternative way to deal with the non-blocking
nature of JavaScript while running asynchronous operations. It’s a
modern feature released in 2015 (that is 20 years after the first
release of JavaScript)
Basically, a Promise object represents a "pending state" in the most
common sense: The promise will eventually be fulfilled at a later
date.
To give you an illustration, suppose you want to buy a new phone
to replace your old phone, so you open a messaging app to contact
a phone store. This is similar to how you access a variable or a
function that returns a promise:
After you send a message explaining what you want, you get an
automated message saying that a representative will answer your
message shortly. This is similar to receiving a Promise object:
A minute later, you get a new message from a human
representative, saying that the phone model you want to buy is
available for purchase. This is when the Promise was resolved:
Or, in a completely different scenario, the representative tells you
that the store doesn’t sell phones, because the store is a food store
and not a phone store. This means the Promise was rejected:
This illustration shows how the Promise object in JavaScript works:
​▪​A Promise is like the automated message that we’ve seen earlier,
it represents a pending state that must be fulfilled by later.
​▪​The human representative saying that the phone model is
available is similar to the resolve() method, which shows that
the Promise is fulfilled.
​▪​The representative telling you that you’re contacting the wrong
store is like the reject() method, which is the method used to
show that the Promise can’t be fulfilled because of an error.
A typical promise implementation would look as follows:
let p = new Promise((resolve, reject) => {
let isTrue = true;
if (isTrue) {
resolve('Promise resolved');
} else {
reject('Promise rejected');
}
});
When creating a new Promise object, we need to pass a callback
function that will be called immediately with two arguments: the
resolve() and reject() functions
Depending on the result of the Promise, either the resolve() or the
reject() function will be called to end the pending state.
To handle the Promise object, you need to chain the function call
with then() and catch() functions as shown below:
let p = new Promise((resolve, reject) => {
let isTrue = true;
if (isTrue) {
resolve('Success');
} else {
reject('Error');
}
});
p
.then(message => console.log(`Promise resolved: ${message}`))
.catch(message => console.log(`Promise rejected: ${message}`));
The resolve() function corresponds to the then() function, while
reject() corresponds to the catch() function. You can change the
isTrue value to false to test this.
Here’s an illustration of the promise process:
Using the promise pattern, you can call your functions sequentially
by placing the next process inside the then() method.
Callbacks vs Promises
The promise pattern is created to replace the use of callbacks. By
using promises, the code we write would be more intuitive and
maintainable.
Going back to the messaging illustration, let’s create an example of
using callbacks to handle the situation. First, we declare the two
variables required for this situation, called isPhoneStore and
isPhoneAvailable:
const isPhoneStore = true;
const isPhoneAvailable = true;
Next, we write a function that will process incoming messages. This
function will mimic the promise pattern, and it will resolve only
when isPhoneStore and isPhoneAvailable are true:
function processMessage(resolveCallback, rejectCallback) {
if (!isPhoneStore) {
rejectCallback({
name: 'Wrong store',
message: 'Sorry, this is a food store!',
});
} else if (!isPhoneAvailable) {
rejectCallback({
 name: 'Out of stock',
message: 'Sorry, the X phone is out of stock!',
});
} else {
resolveCallback({
name: 'OK',
message: 'The X phone is available! How many you want to buy?',
});
}
}
Here, you can see that the function processMessage accepts two
callback functions: resolveCallback and rejectCallback.
When we call the function, we need to provide the callback
functions, similar to how we need to chain the then() and catch()
methods when accessing a promise:
processMessage(
value => console.log(value),
reason => console.log(reason)
);
In the call to the processMessage above, the first argument is the
resolveCallback() function, and the second argument is the
rejectCallback() function.
If you run the code above, then the resolveCallback() function will
be called. You can change one of the two variables to false to
trigger the rejectCallback() function.
Now that we have a working callback example, let’s rewrite the
code using a promise as follows:
const isPhoneStore = true;
const isPhoneAvailable = true;
function processMessage() {
return new Promise((resolve, reject) => {
if (!isPhoneStore) {
reject({
name: 'Wrong store',
message: 'Sorry, this is a food store!',
});
} else if (!isPhoneAvailable) {
reject({
 name: 'Out of stock',
message: 'Sorry, the X phone is out of stock!',
});
} else {
resolve({
name: 'OK',
message: 'The X phone is available! How many you want to buy?',
});
}
});
}
processMessage()
.then(response => console.log(response))
.catch(error => console.log(error));
Here, you can see that the processMessage() function returns a
Promise object that gets resolved only when both isPhoneStore and
isPhoneAvailable are true.
When one of the two variables is false, then the Promise object will
be rejected.
Here you can see that you don’t need to add two extra parameters
to the processMessage() function just for the callbacks, and when
calling the function, you also use the then() and catch() methods to
handle the result of the promise.
The use of a promise makes the code easier to understand. Here’s
the comparison of the two side by side:
Summary
In this chapter, you’ve learned how the Promise object works in
JavaScript. A promise is easy to understand when you realize the
three states that can be generated by the promise: pending,
resolved, and rejected.
When facing a promise, you need to define what’s going to happen
next inside the .then() and .catch() methods
You’ve also learned how promises can be used to replace callbacks.

Chapter 15: The Fetch API
In this chapter, we’re going to learn about the Fetch API. But before
we start, let’s quickly review what we mean by API.
What is an API?
API stands for Application Programming Interface, but this fancy
term doesn’t really tell you what an API is, so let me explain it in
simpler terms.
An API is simply a program that’s exposed by the developer. The
intention of exposing this program is so that other applications can
call and use the program to achieve a specific result.
For example, imagine you’re going to a restaurant to have lunch.
You don’t directly go to the kitchen and prepare the food.
Instead, you order food from the waiter, who takes the order to the
kitchen. In the kitchen, the chef will make the food, and when it’s
done, the waiter brings the food to your table.
You know nothing about what’s happening in the kitchen. All you
know is that you specify what you want to the waiter, and the
waiter takes care of the rest.
In a similar way, an API serve as the gateway that you can access to
achieve a specific result. You don’t really know how the API works
under the hood. All you know is that you get what you wanted
from the API.
There are two kinds of APIs: the web API (also known as REST API),
or library API.
The web API is created by exposing certain endpoints that you can
access to send and receive data.
The library API is a piece of code written by other people. This code
usually has a bunch of objects, methods, and properties that you
can access to do something. You don’t need to know how they work
under the hood.
The document object exposed by the browser is an example of a
library API, also known as the DOM API. You don’t write the
document
object
from
scratch,
and
when
you
call
the
querySelector() method, you don’t know exactly what code is
written in that method.
The Fetch API we’re going to learn next is also a library API.
How Fetch API works
The Fetch API is a function that you can use to send a request to
any web API URL and get some response.
To send a GET request similar to that of an HTML form, you only
need to pass the URL where you want to send the data as an
argument to the fetch() function:
fetch('<Your URL>');
The fetch() function accepts two parameters:
1. The URL to send the request to
2. The options to set in the request. You can set the request
method to GET or POST here.
Under the hood, the fetch() function returns a promise, so you
need to add the .then() and .catch() methods.
When the request returns a response, the then() method will be
called. If the request returns an error, then the catch() method will
be executed.
Inside the .then() and .catch() methods, you pass a callback
function to execute when the respective methods are called. In the
following example, we’re going to hit a dummy URL located in
jsonplaceholder.typicode.com:
fetch('https://jsonplaceholder.typicode.com/todos/1')
.then(response => console.log(response))
.catch(error => console.log(error));
The code above will give the following response:
Here, you can see that the body property contains a ReadableStream.
To use the ReadableStream in our JavaScript application, we need to
convert it to JSON format first, so let’s do it:
fetch('https://jsonplaceholder.typicode.com/todos/1')
.then(response => response.json())
.then(data => console.log(data))
The json() method converts the ReadableStream into a JavaScript
object. The data variable above will be printed as follows:
{
userId: 1,
id: 1,
title: "delectus aut autem",
completed: false
}
If you want to send a POST request instead of a GET request, pass
an object containing a method property as follows:
fetch('https://jsonplaceholder.typicode.com/todos', {
method: 'POST',
}).then(response => response.json())
.then(data => console.log(data))
When you send a POST method, you need to set the request header
and body properties to ensure a smooth process.
For the header, you need to add the Content-Type property and set
it to application/json. The data you want to send should be put
inside the body property in a JSON format. See the example below:
fetch('https://jsonplaceholder.typicode.com/todos', {
method: 'POST',
headers: {
'Content-Type': 'application/json',
},
body: JSON.stringify({ title: 'Learn JavaScript' }),
}).then(response => response.json())
.then(data => console.log(data))
In the example above, we send a POST request to create a new todo
task. The title of the task is Learn JavaScript. The response from the
typicode API would be similar as follows:
{
title: 'Learn JavaScript',
id: 201
}
Summary
The Fetch API allows you to access APIs and perform a network
request using standard request methods such as GET, POST, PUT,
PATCH, and DELETE.
The Fetch API returns a promise, so you need to chain the function
call with .then() and .catch() methods, as shown in the previous
chapter.
Here, we only see the GET and POST methods in action, but don’t
worry because we’re going to use the rest in the following project.

Chapter 16: Project 2 - Creating a
To-do List Application
As the final project of this book, we’re going to create a To-do List
application.
In this application, we can add, edit, delete, and mark a task as
completed.
The finished application looks as follows:
To start building this application, we need to create a simple server
that’s going to store our task data. To do so, we need to install
Node.js
Installing Node.js
Node.js is a JavaScript runtime application that enables you to run
JavaScript outside of the browser. We need to install this
application on our computer to create a simple server.
You can download and install Node.js from https://nodejs.org. Pick
the recommended LTS version because it has long-term support.
Creating the Server and Database
To set up this project, let’s create a new folder named todo-list.
Open this folder in VSCode, then create a new file named db.json
and put the following content in it:
{
"tasks": [
{
"title": "Learn Swimming",
"completed": true,
"id": 1
},
{
"title": "Learn Cooking",
"completed": false,
"id": 2
}
]
}
This JSON file will serve as the database of our application. When
we add a new task, this file will be updated.
The next step is to run this JSON file as a server. To do so, you need
to use Node Package Manager (or NPM for short) to install a json
server.
First, right-click on the todo-list folder and select the Open in
Integrated Terminal option. This will open the terminal from which
you can run some commands.
The command I want you to run is npm install -g json-server.
This command will install the json-server package globally on your
computer.
Once the installation is finished, you should see the following
output:
The next step is to run the json-server package. Run this command
in your terminal:
json-server db.json
If you see the following output, it means the JSON server is running
successfully:
You can open the browser and access the URL at http://
localhost:3000/tasks to see the JSON data we created earlier.
The To-do List application we’re going to create is going to access
this API endpoint for fetching, adding, removing, and updating the
tasks.
You’ve created a simple server that exposes an API endpoint
successfully. Nice work!
Let’s Start the Project: HTML and CSS First
The next step is to write the front-end part of the project. Open the
client folder in VSCode, then create two files named index.html and
script.js.
Open the index.html file and write the standard HTML document
structure just like when we create the Wizard Form:
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"
/>
<title>To-do List</title>
</head>
<body></body>
</html>
To focus our attention on the JavaScript part, we’re going to use
Bootstrap to style our HTML tags. Bootstrap is a library containing
pre-written CSS rules that you can apply to your project.
To use Bootstrap styles, you just add specific classes to your HTML
elements. Add Bootstrap to our project by creating a link that
fetches the Bootstrap CSS from the CDN server as follows:
<title>To-do List</title>
<link
rel="stylesheet"
href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.0/dist/css/
bootstrap.min.css"
/>
CDN stands for Content Delivery Network, and it’s a server that
allows you to fetch popular libraries. By using a CDN, you don’t
need to download the Bootstrap CSS file onto your computer and
load it locally.
The last step is to add the script.js file to the HTML file. As always,
add the defer attribute so that the browser loads the script after the
HTML document has been rendered:
<script src="script.js" defer></script>
</head>
Now we need to add some HTML to the <body> tag. First, write the
container that’s going to contain all our HTML content. I’m going to
add some comments to help you put the HTML in the right place:
<body>
<div class="container m-5 rounded mx-auto bg-light shadow">
<!-- App title section START-->
<div class="row p-4">
<div class="col">
<h1 class="text-center">
<u>My Todo List ✅</u>
</h1>
</div>
</div>
<!-- App title section END -->
</div>
</body>
Under the 'App title section END' comment, add an input and a
button we’re going to use to create a task. The divs around the
input and the button is created only to apply Bootstrap style:
<!-- Create task section START -->
<div class="row p-3">
<div class="col col-11 mx-auto">
<div class="row bg-white rounded shadow-sm p-2">
<div class="col">
<input
type="text"
id="task-title"
class="form-control border-0 rounded"
placeholder="Enter the task here.."
/>
</div>
<div class="col-auto">
<button type="button" class="btn btn-primary"
onClick="addTask()">
Add Task
</button>
</div>
</div>
</div>
</div>
<div class="my-2 mx-4 border-bottom"></div>
<!-- Create task section END -->
Next, we’re going to add the filter section under the 'Create task
section'. This filter section will contain a select input:
<!-- Filter options section START -->
<div class="row p-3 justify-content-end">
<div class="col-auto d-flex align-items-center">
<label class="text-secondary my-2 me-2">Filter</label>
<select class="form-select form-select-sm"
onChange="filterTasks(event)">
<option value="all" selected>All</option>
<option value="completed">Completed</option>
<option value="active">Active</option>
</select>
</div>
</div>
<!-- Filter options section END -->
The last step is to display the tasks. We’re going to use table
element here:
<!-- Tasks list section START -->
<div class="row px-5">
<div class="col">
<div class="table-responsive">
<table class="table table-striped table-bordered table-hover">
<tbody id="tbody-tasks">
<tr>
<td><input class="form-check-input" type="checkbox" checked /
></td>
<td>Learn JavaScript</td>
<td>
<button type="button" class="btn btn-link">Edit</button>
</td>
<td>
<button type="button" class="btn btn-link">Delete</button>
</td>
</tr>
<tr>
<td><input class="form-check-input" type="checkbox" /></td>
<td>Learn HTML</td>
<td>
<button type="button" class="btn btn-link">Edit</button>
</td>
<td>
<button type="button" class="btn btn-link">Delete</button>
</td>
</tr>
</tbody>
</table>
</div>
</div>
</div>
<!-- Tasks list section END -->
And now the HTML part is completed. Right-click on the index.html
file and select Open with Live Server to see the result.
If you need to check your code, you can get the code used in this
chapter
at
https://github.com/nathansebhastian/js-todo-list/tree/
main/check-point-1
Summary
In this chapter, we’ve installed Node.js and created a simple server
using the json-server package. The database we use in this project
is a simple JSON file named db.json.
We’ve also created the HTML file for our To-do application and
used Bootstrap to style the elements.

Chapter 17: Adding CRUD
Functionalities to the Application
Create, Read, Update, and Delete (CRUD) are four basic
functionalities that make the core of a web application. We’re going
to learn how to implement them using JavaScript in this chapter.
Before we start creating the functionalities for the To-do List, we
need to edit the Live Server settings and prevent server reload
when the db.json file changes.
If we don’t do this, the application will be interrupted when we
add, edit, or delete a task.
Open the VSCode Settings menu by pressing Ctrl + , or Command +
, and search for 'live server ignore'. You should see the following
output:
Click the Edit in settings.json link, and add db.json to the Live
Server ignore files settings as shown below:
"liveServer.settings.ignoreFiles": [
 "db.json",
".vscode/**",
"**/*.scss",
"**/*.sass",
"**/*.ts"
]
Save the changes. Now Live Server won’t reload when there’s a
change in the db.json file.
Use Fetch to Get and Display Tasks from the
API
Now that we have the database and the interface ready, the next
step is to use JavaScript to get tasks data and display it in our table.
We’re going to use the Fetch API for that.
Open the script.js file, and write the following getTask() function:
const BASE_API_URL = 'http://localhost:3000/tasks';
function getTasks() {
const tableElement = document.querySelector('#tasks-table');
fetch(BASE_API_URL)
.then(response => response.json())
.then(tasks => {
console.log(tasks);
});
}
getTasks();
In the code above, we declared a constant variable to store the API
URL we’re going to hit with requests.
Below the constant, we created a function called getTasks() that
will execute a network request using fetch(). To check if we
successfully retrieved the data, we printed the tasks to the console.
If you open the browser console, you should see the following
output:
This means we successfully retrieved the tasks data. The next step
is to display those data on our To-do List. We need to query the
<tbody> element in our HTML page and put the tasks as rows there.
Recall that in our previous chapter, we put the id attribute to the
<tbody> tag as follows:
<tbody id="tbody-tasks">
...
</tbody>
This means we can get the element using the query selector:
const BASE_API_URL = 'http://localhost:3000/tasks';
const tableElement = document.querySelector('#tbody-tasks');
Then we go back into the getTasks() function, remove the
console.log() method and create table rows based on the tasks
data.
Below, you can see that the code for creating the elements is quite
long, but it’s essentially the same as when we create buttons for the
Wizard Form:
function getTasks() {
let tableRows = '';
fetch(BASE_API_URL)
.then(response => response.json())
.then(tasks => {
tasks.forEach(task => {
const element = `<tr class=${
 task.completed ? 'table-success' : ''
}><td><input class="form-check-input" type="checkbox" ${
task.completed ? 'checked' : ''
} onclick="toggleTask(event, ${task.id})"></td><td>${
task.title
}</td><td><button type="button" class="btn btn-link"
onclick="editTask(${
task.id
})">Edit</button></td><td><button type="button" class="btn btn-
link" onclick="deleteTask(${
task.id
})">Delete</button></td></tr>`;
tableRows += element;
});
tableElement.innerHTML = tableRows;
});
}
In the above code, we create a variable named tableRows that starts
as an empty string. Next, we iterate over the tasks array using the
forEach() method, and create an element variable for each task
data.
This element variable uses the data from the array to dynamically
adjust the HTML output. If the task is marked as completed, then
the table-success class is added to the <tr> tag, and the checked
attribute is added to the checkbox.
When the checkbox is clicked, then the toogleTask() function will
be called. When the Edit button is clicked, then the editTask()
function will be called, and when the Delete button is clicked, the
deleteTask() button is called.
The elements are stored in the tableRows variable, and when the
forEach() process is finished, we set the innerHTML value of the
tableElement to the tableRows value.
If you open the browser, you should see the tasks appear on the
table like this:
Since we’re able to display the data, we can remove the hard-coded
<tr> elements in our index.html file. Remove the highlighted lines
below:
<!-- remove this from index.html -->
<tr>
... Learn JavaScript ...
</tr>
<tr>
... Learn HTML ...
</tr>
Now that we successfully displayed the data, the next step is to
enable adding a new task to the database.
Adding a New Task
To add a new task to the database, we need to define the addTask()
function that has been defined in the previous chapter for the 'Add
Task' button:
<button type="button" class="btn btn-primary" onClick="addTask()">
Add Task
</button>
Back to the script.js file, create a new function named addTask()
and write the following code into it:
function addTask() {
const taskTitle = document.querySelector('#task-title');
const data = {
title: taskTitle.value,
completed: false,
};
fetch(BASE_API_URL, {
method: 'POST',
headers: {
'Content-Type': 'application/json',
},
body: JSON.stringify(data),
}).then(response => {
if (response.ok) {
alert('Task added');
getTasks();
taskTitle.value = '';
}
});
}
First, we query the input text, which has an id of task-title, then
we create an object called data that stores the title and completed
status of the task.
After that, we send a POST request using fetch(), adding the
required options. When the response comes, we call the alert()
function to notify the user that the task has been added to the
database.
Because there’s a new task on the database, we called the
getTasks() data to reload the task lists and display it to the user.
Then we empty the input text just to make it intuitive.
Now you can test adding a new task from the browser. The next
step is to add the delete functionality.
Deleting a Task
To delete a task from the database, we need to define the
deleteTask() function in our script.js file. Here’s the function in
full:
function deleteTask(id) {
const confirmation = confirm('Are you sure you want to delete the
task?');
if (confirmation) {
fetch(BASE_API_URL + '/' + id, {
method: 'DELETE',
}).then(response => {
if (response.ok) {
alert('Task deleted');
getTasks();
}
});
}
}
First, we confirm the decision to delete the task with the user using
the confirm() function, which is part of the browser API.
When the user confirms, we send a DELETE request using the
fetch() function, and we put the id value of the task we want to
delete in the API URL (BASE_API_URL + '/' + id)
When we got a response back, we just call the alert() function to
notify the user, then refresh the tasks list with getTasks().
Now You can test the delete button from the browser. It should be
working.
Editing a Task
To edit a task, we need to declare the editTask() function in our
script.js file as follows:
function editTask(id) {
const newTitle = prompt('Enter the new task title');
if (newTitle) {
const data = { title: newTitle };
fetch(BASE_API_URL + '/' + id, {
method: 'PATCH',
headers: {
'Content-Type': 'application/json',
},
 body: JSON.stringify(data),
}).then(response => {
if (response.ok) {
alert('Task updated');
getTasks();
}
});
}
}
To edit a task, we need to call the prompt() function to ask the user
a new title for the task. When the new title is received, we put the
title as an object inside the data variable.
The next step is to perform a network request using fetch(), add
the id of the task to the URL, and set the method to PATCH.
When we receive a response, we notify the user and refresh the
list.
Marking a Task as Completed
To mark a task as completed or not completed, we need to check if
the checkbox input has the checked attribute.
To do so, we need to access the event property when the input is
clicked. This is why we pass the event property on the checkbox
onclick attribute:
<input ... type="checkbox" onclick="toggleTask(event, id)">
Create a toggleTask() function in the script.js file as shown below:
function toggleTask(event, id) {
const checked = event.target.checked;
const data = {
completed: checked,
};
fetch(BASE_API_URL + '/' + id, {
method: 'PATCH',
headers: {
'Content-Type': 'application/json',
},
body: JSON.stringify(data),
}).then(response => {
 if (response.ok && checked) {
alert('Hurray! You finished the task');
}
getTasks();
});
}
The checked attribute returns true when the checkbox is checked,
or false otherwise.
We wrap this value in a data object and then send a PATCH request
using fetch(), similar to the editTask() function we created earlier.
When the task is marked as completed, we notify the user with an
alert() call. To refresh the list, we call the getTasks() function.
Now we have all core functionalities created using JavaScript. The
last step is to enable the filter function.
Filtering Tasks
The select input that we’ve created will serve as a filter function.
We can refresh the list to see only completed or active tasks.
In JSON server, you can filter the returned data by adding a query
parameter. To filter by the completed property value, the URL is
http://localhost:3000/tasks?completed=true or http://localhost:3000/
tasks?completed=false.
You can test this by opening the URL on the browser.
Since we already have a getTasks() function, we can create a
filterTasks() function that simply calls on getTasks():
function filterTasks(event) {
const filterValue = event.target.value;
if (filterValue === 'all') {
getTasks();
} else if (filterValue === 'completed') {
getTasks('completed');
} else {
getTasks('active');
} }
Here, we use the event property again to get the value of the select
input.
Next, we check the value of the filterValue and add the relevant
argument when calling the getTasks() function.
If we want to see only completed tasks, then we send the
'completed' value to the getTasks() function.
To accommodate the filter argument, we need to add a parameter
to the getTasks() function. Let’s update the function as shown
below:
function getTasks(filter) {
let parameter = '';
if (filter === 'completed') {
parameter = '?completed=true';
} else if (filter === 'active') {
parameter = '?completed=false';
}
const API_URL = BASE_API_URL + parameter;
fetch(API_URL)
...
}
Here, we add the filter parameter to the getTasks() function.
Then, we create a query parameter for the URL using an if-else
check.
Next, we add the parameter to the BASE_API_URL and use it when
calling the fetch() function.
This way, the GET request corresponds to the filter value you
selected.
And now the application is complete! You can try all the
functionalities on your browser.
If you encounter an error and need some help, you can compare
your code with mine at https://github.com/nathansebhastian/js-
todo-list/tree/main/check-point-2
or
email
me
at
nathan@codewithnathan.com
Summary
Well done! You’ve just finished your second JavaScript project.
Hopefully, this project has shown you how JavaScript is the secret
ingredient that makes a web application interactive.
In JavaScript, we define functions that respond to user actions, and
then plug those functions into the HTML onclick attribute.
When the user performs an action, JavaScript will respond by
running the relevant process. The CRUD operations are the core
functionalities of a web application, and you’ll see them no matter
what applications you use.

...the end


