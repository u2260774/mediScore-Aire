# Aire Logic MediScore Test

## Solution

### .py program

I made a simple program in python that used the values of the observation to convert those observations into a final Medi score, using the table provided in the test portal. The function uses enums to convert respiration and consciousness observations to a Medi score. Other observations use integers and floats (rounded down to 1 decimal point) for the conversion. 

All observations pass through functions that use try and except blocks to catch user errors. The result is saved to a .json file that serves as a history for the patient's previous scores. It uses the python's json and os modules to look for/read and write to the json file, alongside the datetime module, which is used to check the time passed since the previous observation.

Depending on input, the calculate function returns either a string, which reports the error, or a tuple containing the Medi score and the flag (which is a boolean)

I have been considered adding an id parameter to the method as well, which will allow for working with multiple patients.

### Web service using flask and render

I used the function to create a web service hosted on render, and used flask for the web app. It takes in user input from forms and sends the data to the calculate function, the return value of which is used to display the result, or the error.
