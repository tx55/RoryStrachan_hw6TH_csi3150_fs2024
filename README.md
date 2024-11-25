## Manual For The Quiz App Demo  
A web application written in JavaScript (using React), CSS, and HTML. The application is a straightforward quiz where the user is asked questions about web programming or development concepts. 

The user is given a set amount of time to answer questions, after selecting an answer they will be shown if they are correct or not. At the end their points will be totaled and they will be prompted to play again.  

## Functionalities and Features
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

</td><td valign="center" width="50%">

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

## CodeBase

### /index.html
- The head is standard, the header includes links to the CSS file, an online font repository, and Javascript files
```
	<script src="js/questions.js" defer></script>

	<script src="js/quizApp.js" defer></script>

```
<p align="right"><sub>index.html lines 14 and 17</sub></p>

- As HTML is read top to bottom, and as our JavaScript is linked at the top of the page, we want to “defer” so these lines of HTML are read after the the rest of the HTML is done loading	
  - This is done to help make load times quicker, JavaScript is much more intensive than HTML and CSS and the JavaScript is not going to be what’s immediately visible, unlike HTML and CSS

 
- The body consists of a few elements that will be important to point out for discussion on the JavaScript files later
```
	<div class="start_btn"><button>Start Quiz</button></div>
```
<p align="right"><sub>index.html line 21</sub></p>

- The start button (“start_btn”) that shows up on the landing page
```
	<div class="info_box">
	    	...
		...
	    	<div class="buttons">
	        	<button class="quit">Exit Quiz</button>
	        	<button class="restart">Continue</button>
	    	</div>
	</div>

```
<p align="right"><sub>index.html lines 24 - 37</sub></p>

- The instructions (“info_box”) that describe to the user how the quiz works
	- The button of this box includes two buttons, wrapped in a class called “buttons:”, one name “quit” and the other named “restart”
```
	<div class="quiz_box">
	    	<header>
	        	<div class="title">Demo Quiz App in JavaScript</div>
	        	<div class="timer">
	            	<div class="time_left_txt">Time Left</div>
	            	<div class="timer_sec">15</div>
	        	</div>
	        	<div class="time_line"></div>
	    	</header>
	    	<section>
	        	<div class="que_text">
	            	<!-- Insert questions from ./js/questions.js -->
	        	</div>
	        	<div class="option_list">
	            	<!-- Insert options to questions from ./js/questions.js -->
	        	</div>
	    	</section>
	
	    	<!-- footer of Quiz Box -->
	    	<footer>
	        	<div class="total_que">
	            	<!-- insert Question Count Number dynamically from JavaScript App logic -->
	        	</div>
	        	<button class="next_btn">Next Que</button>
	    	</footer>
	</div>
```
<p align="right"><sub>index.html lines 40 - 65</sub></p>

- The “quiz_box which can be broken down into a header, body section, and footer
	- The header includes both the countdown timer (“timer_sec”) and the progress bar (“time_line”)
	- The section consists of the question text and question possible answers (which will be added from the questions.js file) for each question
	- And the footer contains the question total (which will let the user know which question they are on out of five), and the next question button (“next_button”)
```
	<div class="result_box">
		<div class="icon">
			<i class="fas fa-crown"></i>
		</div>
		<div class="complete_text">You've completed the Quiz!</div>
		 	<div class="score_text">
			<!-- insert dynamic user score as Result from JavaScript -->
	        </div>
	        <div class="buttons">
	            	<button class="restart">Replay Quiz</button>
	            	<button class="quit">Quit Quiz</button>
	        </div>
	</div>
```
<p align="right"><sub>index.html lines 68 - 80</sub></p>

- The bottom of the body contains the “results_box” which will be used to tell the user what score they got
	- Similar to that element “info-box” as “results_box” also ends in a class of buttons consisting of a restart and quit button


### /js/questions.js
- A data structure to organize information about each question
- The file stores an array, questions, which stores multiple objects
```
	let questions = [
  	{
		numb: 1,
		question: "What does HTML stand for?",
		answer: "Hyper Text Markup Language",
		options: [
		  	"Hyper Text Preprocessor",
		  	"Hyper Text Markup Language",
		  	"Hyper Text Multiple Language",
		  	"Hyper Tool Multi Language",
		],
  	},

```
<p align="right"><sub>questions.js lines 3 - 14</sub></p>

- Each array element consists of the following information
  
1. numb: The number the question is
2. question: The question text
3. answer: The correct answer
4. options: An array of possible answers (composed of 4 strings)

- One of the answers in the array will be the same as the answer listed in the array
- This data will be used by quizApp.js to dynamically change HTML elements as the user progresses through the web application 

