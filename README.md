# voight-kampff
~A very advanced form of lie detector that measures contractions of the iris muscle and the presence of invisible airborne particles emitted from the body. The bellows were designed for the latter function and give the machine the menacing air of a sinister intent. The VK is used primarily by Blade Runners to determine if a suspect is truly human by measuring the degree of his empathic response through carefully worded questions and statements.~

A technical test for Android development.

## Introduction:

First off, thanks for taking the time to apply to our organization. We really appreciate the interest, and we know your time is valuable. We hope that this test will give you a little insight into some of the technologies and systems we deal with on an everyday basis, in addition to helping us get a better idea of your strengths and how what you can bring to our team.

## Your Toolbox:

There are two pieces of knowledge you will need to effectively complete the assignment.

### 1. [A Brief Introduction to FHIR](fhir.md)

### 2. [The Test Server](server.md)
 
## The Assignment:

#### Your job is to create a basic Android health application that does the following core tasks:

1. Downloads the 10 most recently updated patients from the test server.
  * Just as a note, patient objects are complicated...ignore all the fields you do not need when you pull the data from the server. Don't create a tonne of POJOs to cover every field when you download the patient object.
2. Displays a list of these patients to the user, with Name. 
3. Allows the user to do the following to a patient object:
  * View the family name, gender, and birthday of each patient if they want.
  * Update the family name, gender, or birthday of each patient, and update the patient on the FHIR test server with the new information. 
4. Refresh the list and fetch the new latest 10 patients. 
5. Change the order of patients displayed, based on birthday, or name (alphabetical).
6. Upload the project to a public GitHub repository so we can clone and look at what you've done.

##### Bonus points for:

1. Being able to adjust the number of patients that are downloaded at one time.
2. Storing the patient data locally. (In whatever persistence tool you want)
3. Implementing other CRUD operations with the test server.

## What are we looking for?

 1. Functionality first and foremost. Does the app accurately do what it's supposed to do?
 2. Error handling, and code comments/documentation. We deal with some of peoples most sensitive data, their personal health information. The code we write needs to be readable, dependable, and well documented.
 3. Unit tests. How do you know that the code is doing what it's supposed to do? At minimum, I would expect you to test that you can get and set the patient fields correctly.
 4. Does it look good? It doesn't have to be a piece of art, but it would be good if the application followed the [google material design guidelines](https://material.io/guidelines/) to some degree. Medical apps don't work if people think they're ugly, unintuitive, and don't use them.
 5. What libraries are you using? We don't expect you to home roll your own REST framework, or JSON deserializer. How familiar are you with the most commonly used Android development tools available?
 6. You can do this in Java or Kotlin, whichever you prefer.
 
Typically, we give one week for this assignment to be done. If you feel like this is too short, or have special accommodations you want us to be aware of, please do not hesitate to let us know. 
 
Just keep in mind, that like most programming problems, there is rarely a single right or wrong answer. Do the work to the best of your abilities. If there is a section or part you are uncertain of, make an assumption and be sure to document it in the solution you provide. We're not here to try and trick you. If you cannot complete everything, submit what you have, and we can talk about the solution you've provided.

We wish you the best of luck, and thanks again for your interest!
