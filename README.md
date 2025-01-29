# JS-beginners-JS
JavaScript for Beginners

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2>DOM Query Selector Methods</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
The Document Object Model provides a set of methods that allow
you to select a specific element in the HTML nodes. They are the
querySelector() and querySelectorAll() methods.
The querySelector() method is a JavaScript method from the
document object that allows you to retrieve a single Element object
that matches the CSS selector passed to the method.
The CSS selector is the pattern you use when targeting a specific
element for styling. Here’s an example of CSS selectors:
```
/* Selecting all elements with the id value of box */
#box {
}

/* Selecting all elements with the class value of btn */
.btn {
}
```
The pattern you need to pass to the querySelector() method can be
as simple or as complex as you need.
For example, here’s how to use the method to retrieve an element
with an id attribute of 'box':
```
document.querySelector('#box');
```
The querySelector() method always returns the first element that
matches the query. The method searches for the element from the
top to the bottom of the DOM tree.
The string parameter passed to the querySelector() method follows
the CSS selector pattern, where class is represented by a period .
and id is represented by a hash #.
Suppose you have the following HTML element on your page:
```
<body>
<h1>Query Selector</h1>
<h2>Learning Query selector method</h2>
<p id="opening" class="bold">Placeholder</p>
</body>
```
You can retrieve the <p> element by passing "p" as the method’s
argument:
```
let element = document.querySelector('p');
console.log(element);
// <p id="opening" class="bold">Opening</p>
```
Or you can also pass the id or the class attribute, it will return the
same <p> element:
```
document.querySelector('.bold');
// <p id="opening" class="bold">Opening</p>

document.querySelector('#opening');
// <p id="opening" class="bold">Opening</p>
```
When you pass a selector that returns two elements, only the first
element will be returned by the method. The following code tries to
fetch both <h1> and <h2> elements:
```
document.querySelector('h1, h2');
// <h1>Query Selector</h1>
```
Above, you can see that the method returns the first match, which
is the <h1> element.
And that’s how the querySelector() method works. When you need
to retrieve more than a single element, you need to use the
alternative querySelectorAll() method instead.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2>querySelectorAll() Method</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
The querySelectorAll() method is a JavaScript method from the
DOM API that allows you to retrieve all elements that match the
CSS selector you passed as the argument.
For example, here’s how to use the method to retrieve any element
that has the class attribute of box:
```
document.querySelectorAll('.box');
```
The string parameter passed to the querySelectorAll() method
follows the CSS selector pattern, where class is represented by a
period . and id is represented by a hash #.
To retrieve all copies of a specific element, you can simply pass the
name of the element as its argument.
Suppose you have the following HTML element on your page:
```
<body>
<p id="opening" class="bold">Opening</p>
<p id="middle">Middle</p>
<p id="closing" class="bold">Closing</p>
</body>
```
You can retrieve all <p> elements by passing "p" as the method’s
argument:
```
let elements = document.querySelectorAll('p');
console.log(elements);
// NodeList(3) [p#opening.bold, p#middle, p#closing.bold]
console.log(elements[0]);
// <p id="opening" class="bold">Opening</p>
```
Or when you only need the opening and the closing <p> elements,
you can pass either the class or the `id`s as the argument:
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
The return value of the querySelectorAll() method will be an
array-like object called NodeList.
To access elements of the NodeList object, you can use the index
position. You can also use the forEach() method to iterate over the
elements:
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
The code above will log the current element inside the loop and set
its background-color value to "yellow";
The querySelectorAll() method always returns a NodeList object
even when you only have one matching element.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2>Hide Form Steps With CSS</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
Back to the Wizard Form Application, we need a way to show and
hide the form steps using CSS and JavaScript. Add the following
rules in style.css:
```
.step {
  display: none;
}
.step.active {
  display: block;
}
```
This causes all the div tags with the step class to be hidden from
display. To show the form step add the class active to the step1 div
as follows:
```
<div id="step1" class="step active">
<div class="form-group">...</div>
</div>
```
Go back to the browser, and you now see only the first step of the
wizard form being displayed.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="#add-btn">Adding the Next Button</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
Now we need some buttons to move between the form steps, so add
the following button on step1 div:
```
<div id="step1" class="step active">
  <div class="form-group">...</div>
    <button type="button" class="btn btn-primary f-right" onclick="nextStep()">Next</button>
</div>
```
In this button, we add the onclick attribute so that we can run JavaScript code when the 
button is clicked. The name of the function we want to call is nextStep(), so let’s
create that function in our script.js file. We also need a showStep() function that will:
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
In the script.js file, we declared a variable named <b>currentStep</b>, which is used to let us 
know in what step the form is currently in. In the <b>nextStep()</b> function, we used the 'if' 
statement to check if the <b>currentStep</b> is less than 3 because the form only has 3 steps.

To move to the next step, we increment the <b>currentStep</b> value by one using the "++" 
operator, then we use the <b>document.querySelectorAll()</b> method to select all elements
containing the step class. We remove the <b>active</b> class from all form steps.

After that, we select the current step and add the <b>active</b> class to the 
element using the <b>classList.add()</b> method. The final task is to 
change the content of the <b>currentStep</b> paragraph to the <b>currentStep</b>.
Open the wizard form in the browser, and you should be able to 
navigate to step 3 using the <b>next</b> button. But notice that you can’t
go back to the previous step! This is what we’re going to implement next.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="#add-prev">Adding the Previous Button</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
Now we need another button to move to the previous step. On <b>step2</b> and <b>step3</b> 
div tags, you can add the following buttons:
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
Next, we need to add a <b>prevStep()</b> function to the <b>script.js</b> file:
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
The <b>prevStep()</b> function is identical to the <b>nextStep()</b> function, except for 
the 'if statement' check and decrementing the <b>currentStep</b> part.

Instead of writing the same code in two different functions, we can create a new function 
that runs the query selectors part. Let’s name this function <b>showStep()</b>.
Your <b>script.js</b> file should look as follows:
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
Back to the browser, now you can go to the next and previous steps with the buttons. 
The last thing we need to do is to style these buttons. Right now they look pretty bad:
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
The <b>.f-right</b> style adds the float property to the element to move it to the 
right, the <b>.btn</b> is used to style the buttons. The <b>.btn-next</b> and 
<b>.btn-previous</b> styles add border and background colors to the respective elements.

The final task is to add the <b>submit</b> button and display the data collected by the form.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="#add-submit">Adding a Submit Button</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
Back to the project, the final task we need to do on the Wizard Form is to add a <b>submit</b> 
button to the third step, so let’s do it. Add the <b>submit</b> button to the <b>step3</b> 
div as follows:
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
Add the <b>CSS</b> for the <b>submit</b> button in <b>style.css</b> as follows:
```
.btn-submit {
  border-color: #28a745;
} 
background-color: #28a745;
```
Now we need to listen when the <b>submit</b> button is clicked.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="#listen">Listening to Form Submit Events Using JavaScript</h2
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
Besides the DOM API, the browser also expose signals known as
events that you can use as a cue to run a specific code. We have
done this earlier when adding the onclick attribute to the buttons:
```
<button type='button' class='btn btn-secondary' onclick='prevStep()'>
Previous
</button>
<button type='button' class='btn btn-primary f-right'
onclick='nextStep()'>
Next
</button>
```
The onclick HTML attribute is a shortcut to listen to the click event.
When the previous button is clicked, we run the prevStep()
function. When the next button is clicked, we run the nextStep() function.
Aside from using the onclick attribute, we can also add event listeners using the addEventListener() method.
Let’s add an event listener so that we know when a form is submitted. The Wizard Form we created has an id attribute, so you
can select that form using JavaScript.
```
const wizardForm = document.querySelector('#wizard-form');
```
Next, you need to call the addEventListener() method and listen to
the 'submit' event as follows:
```
const wizardForm = document.querySelector('#wizard-form');
  wizardForm.addEventListener('submit', function (event) {
  // TODO: handle the submit event
});
```
Now that we can listen to the submit event, we need to interrupt
the default behavior of the form so that JavaScript can take over.
To do so, we need to call the event.preventDefault() method inside
the function we passed to the event listener:
```
const wizardForm = document.querySelector('#wizard-form');
wizardForm.addEventListener('submit', function (event) {
event.preventDefault();
});
```
The preventDefault() method interrupts the default flow of the
submit event, which will cause the browser to refresh the current
page.
From here, you can instruct JavaScript to do specific tasks to the
form data submitted by the user.
The form object has an object property named elements that store
all input elements you define inside the form. Inside the object, you
can access the value of input fields by specifying its name attribute,
followed by the value property.
Here’s how to get the values form our Wizard Form:
```
event.preventDefault();
const email = wizardForm.elements.email.value;
const username = wizardForm.elements.username.value;
const password = wizardForm.elements.password.value;
```
Finally, we display the data using the JavaScript alert() function, which
```
const email = wizardForm.elements.email.value;
const username = wizardForm.elements.username.value;
const password = wizardForm.elements.password.value;
alert(`Registration complete! Your details: \n
Email: ${email} \n
Username: ${username} \n
Password: ${password}`);
```
You can test the Wizard Form in the browser. Fill in the textboxes
and you’ll get an alert when clicking the submit button:
Just to make the application smarter, we can reset the form after it
has been submitted by the user:
```
const email = wizardForm.elements.email.value;
const username = wizardForm.elements.username.value;
const password = wizardForm.elements.password.value;
// alert(...);
wizardForm.reset();
currentStep = 1;
showStep();
```
The reset() method from the form will reset all textboxes, then we
set the currentStep variable to 1 and run the showStep() function to
reset the interface.
Taking Care of Repeating Code
If you look closely, you might notice that the code for the Next and
Previous buttons in the steps are identical. Instead of writing them
in the HTML file, we can use JavaScript to add them dynamically.
First, select all the steps div using querySelector() as follows:
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
Next, declare three variables containing the HTML buttons tag:
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
Now, we need to iterate over the elements using the forEach()
method. We can check if the element is the first or the last step
from the index value.
For the first element at index 0, we only add the next button. For
the last element, we add the previous and submit buttons, for all
the middle elements, we add the previous and next buttons:
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
To check if the element is the last step of the Wizard Form, we
compare the index value with the stepsDiv.length - 1 value.
To add an element to existing elements, we use the += assignment
operator.
Now we can remove all <button> elements from the HTML file. Run
the Wizard Form in the browser again, and you’ll see the buttons
added using JavaScript.
The Wizard Form is finished. You can check the completed
application at https://github.com/nathansebhastian/js-wizard-form/
tree/main/complete
Summary
Congratulations on finishing your first JavaScript project! The
Wizard Form application helps you learn the idea of using
JavaScript to manipulate what you see on the screen.
Although a Wizard Form looks complex, it’s actually pretty easy
when you have the steps mechanism created using JavaScript.
Let’s recap what we’ve learned in this project:

  1. How to select HTML elements using <b>document.querySelector()</b> and document.querySelectorAll()
  2. Show and hide elements using CSS and JavaScript
  3. Conditionally display HTML elements using variables, if statements, and functions
  4. An introduction to browser events
  5. Handling a form submit event with addEventListener()
  6. Retrieve, display, and reset form data with the event object
  7. Add elements to specific parts of the HTML document with the innerHTML property
  
And the most important thing is that you’ve seen how an application can be built 
step-by-step and gradually becomes more complex.
In the next chapter, we’re going to learn how to use JavaScript to send and receive data 
from a backend service.
