# Aire Logic MediScore Test

## An issue with the table

Score 3 for '2 hours after eating' says "4.5 and below", and Score 2 says "4.5-5.8". I made the assumption that Score 3 was supposed to say "4.4 and below", similar to the row for 'When Fasting'.

![image](https://github.com/u2260774/mediScore-Aire/assets/126501906/11020b1a-a0a1-4df0-8aa7-20cbcfaec355)


## Solution

### .py program

I made a simple program in python that used the values of the observation to convert those observations into a final Medi score, using the table provided in the test portal. The function uses enums to convert respiration and consciousness observations to a Medi score. Other observations use integers and floats (rounded down to 1 decimal point) for the conversion. 

All observations pass through functions that use try and except blocks to catch user errors. The result is saved to a .json file that serves as a history for the patient's previous scores. It uses the python's json and os modules to look for/read and write to the json file, alongside the datetime module, which is used to check the time passed since the previous observation.

Depending on input, the calculate function returns either a string, which reports the error, or the mediscore as an integer. The flag can be checked using the isFlagged() function.

I have been considered adding an id parameter to the method as well, which will allow for working with multiple patients.

### Web service using flask and render

I used the function to create a web service hosted on render, and used flask for the web app. It takes in user input from forms and sends the data to the calculate function, the return value of which is used to display the result, or the error. This may take several minutes to load.

### Java

I also used java to create 2 similar versions of the solution. One uses a single class, while the other one uses a patient and a mediscore class, and is more verbose. It displays the results in a more comprehensive manner.

The java repo can be found here: github.com/u2260774/mediscore_java
