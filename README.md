## Manual For The Quiz App Demo  
A web application written in JavaScript (using React), CSS, and HTML. The application is a straightforward quiz where the user is asked questions about web programming or development concepts. 

The user is given a set amount of time to answer questions, after selecting an answer they will be shown if they are correct or not. At the end their points will be totaled and they will be prompted to play again.  

## Languages and Tools  
- A simplistic and intuitive UI

	- The color scheme is composed of just white and purple
 
- A landing page with a start button

	- Upon clicking start an explanation panel will show up explaining how the Quiz App works

		- The user is given an option to start, which will start the questions or quit, which will bring them back to the landing page

- The quiz itself is minimalist but has many key pieces of information packed into it

	- The header includes the name of the app along with a timer letting the user know how much time they have left

	- The body features the question in bold, highly visible font, along with four possible answers to the question

		- After a user selects a possible answer (of if time runs out) the correct answer will be highlighted in green

		- If the user selected a wrong answer, that answer will be highlighted in red

	- The footer has a line dividing it from the body along with an indication to the user one how many questions are left

- Upon completion the user will be shown an ending screen

	- The user will be told how many questions they got correct out of the five

	- The user will be prompted with button to replay the quiz or quit the quiz

## Directory and Files
<table><tr><td valign="center" width="60%">

The root directory consists of four items:

- css folder
  - A folder used for organizing CSS files, only stores a single file
   - style.css


- js folder
  - A folder used for organizing JavaScript files, stores two files
  - questions.js
  - quizApp.js


- .gitignore file
  - Used by GIT to know which files to ignore when uploading to GitHub


- README.md
  - What you are currently reading, used to inform the user about the repository and its functions


- index.html
  - The file that stores the HTML structure for the project, it consists of elements whose visibility will change depending on what needs to be shown to the user at a given time
    - It is linked to both the CSS and JS files  

</td><td valign="top" width="50%">

        Quiz App Demo 
	      	├─── css
	      	|    └─── style.css
	      	├─── js
	      	|    ├─── question.js
          	|    └─── quizApp.js
    	├─── .gitignore
    	├─── README.md
	      	└─── index.html  


</td></tr></table>  
