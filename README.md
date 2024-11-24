# Manual For The Quiz App Demo

## Abstract

A web application written in JavaScript (using React), CSS, and HTML. The application is a straightforward quiz where the user is asked questions about web programming or development concepts. The user is given a set amount of time to answer questions, after selecting an answer they will be shown if they are correct or not. At the end their points will be totaled and they will be prompted to play again.

## Functions and features
- A simplistic and intuitive UI
- A landing page with a start button
    - Upon clicking start an explanation panel will show up explaining how the Quiz App works
        - The user is given an option to start, which will start the questions or quit, which will bring them back to the landing page
- The quiz itself is minimalist but has many key pieces of information packed into it
    - The color scheme is composed of just white and purple
    - The header includes the name of the app along with a timer letting the user know how much time they have left
        - The separation between the header and body is used as a progress bar, the line will fill with purple to match how much time the user has left (a good indicator for the user as it is quicker to interpret than the time number in the corner, especially when they are under pressure)
        - Upon clicking an answer both the timer and progress bar will stop
    - The body features the question in bold, highly visible font, along with four possible answers to the question
        - Each answer is placed into a container that is lightly shaded blue
        - Upon clicking on an answer the correct answer will be shaded green and a green check mark icon will appear at the right edge of the correct answer’s container
            - If the user fails to pick an answer on time, the same thing will happen, the correct answer will be highlighted in green
        - If the user picked an answer that was incorrect, the correct answer will be displayed in the same way, but the answer that the user picked will be shaded in red with a red “x” symbol at the right edge of the container
    - The footer has a line dividing it from the body along with an indication to the user one how many questions are left
        - If the user has answered the question (or if time has run out) and the quiz is currently on pause, there will be a button in the corner prompting the user to go to the next question
- Upon completion the user will be shown an ending screen
    - The user will be told how many questions they got correct out of the five
    - The user will be prompted with button to replay the quiz or quit the quiz
        - The replay button is colored purple and much more noticeable than the quit button, incentivizing users to play more
        - Replaying will bring the user straight to the quiz start and not the landing page with the start button
            - Upon replay the quiz will be exact the same as it was presented before, the question order will not change

## The Directory and Files
- The root directory consists of four items
    - css folder
        - A folder used for organizing CSS files, only stores a single file
            - style.css
                - A CSS file used for formatting and designing the webpage
    - js folder
    - A folder used for organizing JavaScript files, stores two files
        - questions.js
            - A simple JavaScript file that acts more so as a database than a program
            - Stores an array consisting of information pertaining to each question
        - quizApp.js
            - The actual program that runs the web application 
                - Stores functions that add events to buttons 
                - At the start of the file variables are created from elements in the HTML file that quizApp.js is calling to
    - .gitignore file
        - Used by GIT to know which files to ignore when uploading to GitHub
    - index.html
        - The file that stores the HTML structure for the project, it consists of elements whose visibility will change depending on what needs to be shown to the user at a given time
        - It is linked to both the CSS and JS files

## Explaination
- index.html
    - The head is standard, the header includes links to the CSS file, an online font repository, and Javascript files
    ```
    <!-- Add questions list -->
	<script src="js/questions.js" defer></script>

	<!-- Main logic of the app -->
	<script src="js/quizApp.js" defer></script>
    ```
    - The JavaScript links include a “defer” tag
        - As HTML is read top to bottom, and as our JavaScript is linked at the top of the page, we want to “defer” so these lines of HTML are read after the the rest of the HTML is done loading	
            - This is done to help make load times quicker, JavaScript is much more intensive than HTML and CSS and the JavaScript is not going to be what’s immediately visible, unlike HTML and CSS
