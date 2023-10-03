# Software Engineering Week5 submission

## The Task

First, choose six rules of clean code and explain them. For each one,

* Summarise the rule in your own words.
* Provide an example from the code that you wrote in week 2 and then refined in week 4.
* Explain how your code implements the rule. 

Second, copy the doxygen comments from your code into your portfolio and provide some 
descriptive commentary on their purpose and structure. Use screenshots showing the HTML 
content that is generated from your code to illustrate your explanation.

Finally, highlight three examples from your code where you have eliminated the need
for comments by adhering to the principles of clean code.


## Six Rules


### Meaningful Names
Descriptive names for variables, functions and classes to make the code more self explanatory.
In my code, the class "AllNotesPage" and method names like "Add_Clicked" and "notesCollection_SelectionChanged" are descriptive and meaningful.


### DRY (Don't Repeat Yourself)
Avoid duplicating code by extracting common functionality into reusable methods or classes.
In my code, i have implemented DRY by centralizing the navigation logic to "NotePage" in both the "Add_Clicked" and "notesCollection_SelectionChanged" methods.
This avoided code duplication by using the same navigation code in multiple places.


### Single Responsibility Principle (SRP)
Each class and method should have a single task, well-defined single responsibility.
The class constructor "AllNotesPage" is focused on initializing the page, It is not handling multiple tasks.


### Comments and Documentation
Comments and documentation is to explain the purpose and usage of code when it's not immediately obvious.
My code lacks comments due to the meaningful names i have created. The comments that i did provide 
make it easier for someone reading the code to understand its intent and functionality.

// Get the note model: This comment explains that the code is obtaining a note model from the current selection,
clarifying the purpose of the code.

// Should navigate to "NotePage?ItemId=path\on\device\XYZ.notes.txt": This comment describes the expected outcome of the navigation code,
specifying the format of the URL that the navigation should produce.

// Unselect the UI: This comment indicates that the code is deselecting an item in the UI,
which is helpful for understanding the code's behavior.


### Consistent Formatting
Maintaining a consistent and readable code style throughout the project with spacing.
My code follows a consistent formatting style, which is good for readability. I have seperated the functions with
spaces to make it more readable.


### Keep Functions/Methods Small
Splitting up large complex functions or methods into smaller, more manageable ones to improve readability and maintainability.
Add_Clicked Method method handles the "Add" button click event and navigates to the NotePage. It's a concise method with a clear purpose.
The method is focused and do not contain an excessive amount of code, which promotes readability and maintainability.
