## Manual For The Quiz App Demo  
A web application written in JavaScript, CSS, and HTML. The application is a straightforward quiz where the user is asked questions about web development. 

The user is given a set amount of time to answer each question, after selecting an answer they will be shown if they are correct or not. At the end, their points will be totaled and they will be prompted to play again.  

## Functionalities and Features
- A simplistic and intuitive UI

	- The color scheme is composed of just white and purple
 
- A landing page with a start button

	- Upon clicking start an explanation panel will show up explaining how the Quiz App works

		- The user is given an option to start, which will start the questions or quit, which will bring them back to the landing page

- The quiz itself is minimalist but has many key pieces of information packed into it

	- The header includes the name of the app along with a timer letting the user know how much time they have left

	- The body features the question in bold, highly visible font, along with four possible answers to the question

		- After a user selects a possible answer (or if time runs out) the correct answer will be highlighted in green

		- If the user selected a wrong answer, that answer will be highlighted in red

	- The footer has a line dividing it from the body along with an indication to the user on how many questions are left

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
#### Importing JavaScript files
- The head is standard, the head includes links to the CSS file, an online font repository, and Javascript files
```html
	<script src="js/questions.js" defer></script>

	<script src="js/quizApp.js" defer></script>

```
<p align="right"><sub>index.html lines 14 and 17</sub></p>

- As HTML is read top to bottom, and as our JavaScript is linked at the top of the page, we want to “defer” so these lines of HTML are read after the the rest of the HTML is done loading	
  - This is done to help make load times quicker, JavaScript is much more intensive than HTML and CSS and the JavaScript is not going to be what’s immediately visible, unlike HTML and CSS

 #### Creating Elements
- The body consists of a few elements that will be important to point out for discussion on the JavaScript files later
```html
	<div class="start_btn"><button>Start Quiz</button></div>
```
<p align="right"><sub>index.html line 21</sub></p>

- The start button (“start_btn”) that shows up on the landing page
```html
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
	- The button of this box includes two buttons, wrapped in a class called “buttons”, one name “quit” and the other named “restart”
```html
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

- The “quiz_box can be broken down into a header, body section, and footer
	- The header includes both the countdown timer (“timer_sec”) and the progress bar (“time_line”)
	- The section consists of the question text and question possible answers (which will be added from the questions.js file) for each question
	- And the footer contains the question total (which will let the user know which question they are on out of five), and the next question button (“next_button”)
```html
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
	- This element is not shown right away, it will be called to later
	- Similar to that element “info-box” as “results_box” also ends in a class of buttons consisting of a restart and quit button


### /js/questions.js
- A data structure used to organize information about each question
- The file stores an array, questions, which stores multiple objects
```javascript
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
  
	1. numb: The number of the question
	2. question: The question text
	3. answer: The correct answer
	4. options: An array of possible answers (composed of 4 Strings)

- One of the options in the array will be the same as the answer listed in the array
- This data will be used by quizApp.js to dynamically change HTML elements as the user progresses through the web application 

### /js/quizApp.js
#### Creating Variables From Elements
- The file that is dynamically changing the elements on index.html
```javascript
	const start_btn = document.querySelector(".start_btn button");
	const info_box = document.querySelector(".info_box");
	const exit_btn = info_box.querySelector(".buttons .quit");
	const continue_btn = info_box.querySelector(".buttons .restart");
	const quiz_box = document.querySelector(".quiz_box");
	const result_box = document.querySelector(".result_box");
	const restart_quiz = result_box.querySelector(".buttons .restart");
	const quit_quiz = result_box.querySelector(".buttons .quit");
	const option_list = document.querySelector(".option_list");
	const time_line = document.querySelector("header .time_line");
	const timeText = document.querySelector(".timer .time_left_txt");
	const timeCount = document.querySelector(".timer .timer_sec");
	const next_btn = document.querySelector("footer .next_btn");
	const bottom_ques_counter = document.querySelector("footer .total_que");
```
<p align="right"><sub>quizApp.js lines 2 - 15</sub></p>

- The file starts with establishing variables which contain elements from index.html
	- This is done so these elements can be altered (for the case for info_box result_box etc) or to add EventListeners for buttons (start_btn restart etc)
- In some cases parent.querySelector() can be used over document.querySelector if we are getting an element that is a child of a parent we already have stored in a variable
	- See exit_btn and continue_btn
#### Adding Functionalities To Buttons
```javascript
	// if startQuiz button clicked
	start_btn.addEventListener("click", (e) => {
	  info_box.classList.add("activeInfo"); //show info box
	});
	
	// if exitQuiz button clicked
	exit_btn.addEventListener("click", (e) => {
	  info_box.classList.remove("activeInfo"); //hide info box
	});

```
<p align="right"><sub>quizApp.js lines 17 - 25</sub></p>

- While looking through index.html, there were elements listed that are not visible on the page when you first open it, that is because this application is designed around the concept of using buttons to hide or reveal information
- The sample code showcases how EventListeners are added to buttons to alter the HTML structure
- startQuiz "adds" the active
```javascript
	continue_btn.addEventListener("click", (e) => {
	  info_box.classList.remove("activeInfo"); //hide info box
	  quiz_box.classList.add("activeQuiz"); //show quiz box
	  showQuetions(0); //calling showQestions function
	  queCounter(1); //passing 1 parameter to queCounter
	  startTimer(15); //calling startTimer function
	  startTimerLine(0); //calling startTimerLine function
	});

```
<p align="right"><sub>quizApp.js lines 28 - 35</sub></p>

- This code section adds the functionality of the "start" button that becomes visible as the user is viewing the quiz info panel
- In short what this piece of code does is get rid of all the current information presented for how the quiz runs and replaces it with information pertaining to the first question, it also starts the timer up so it can countdown from 15 to 0
```javascript
	restart_quiz.addEventListener("click", (e) => {
	  quiz_box.classList.add("activeQuiz"); //show quiz box
	  result_box.classList.remove("activeResult"); //hide result box
	  timeValue = 15;
	  que_count = 0;
	  que_numb = 1;
	  userScore = 0;
	  widthValue = 0;
	  showQuetions(que_count); //calling showQestions function
	  queCounter(que_numb); //passing que_numb value to queCounter
	  clearInterval(counter); //clear counter
	  clearInterval(counterLine); //clear counterLine
	  startTimer(timeValue); //calling startTimer function
	  startTimerLine(widthValue); //calling startTimerLine function
	  timeText.textContent = "Time Left"; //change the text of timeText to Time Left
	  next_btn.classList.remove("show"); //hide the next button
	});
```
<p align="right"><sub>quizApp.js lines 47 - 63</sub></p>

- The restart_quiz button is handled slightly differently
	- Firstly, as it is being shown at the end of the quiz, it has to hide the previous resaults shown
	- Then it shows the screen for the new quiz
	- It also rests all the quiz controls back to their defaults, this helps the quiz know that it is back to number "1" for what question it needs to retrieve from the array in questions.js
```javascript
	quit_quiz.addEventListener("click", (e) => {
	  window.location.reload(); //reload the current window
	});
```
<p align="right"><sub>quizApp.js lines 66 - 68</sub></p>

- This piece of code is how the application handles the user selecting the "quit" button
- Simply the program reloads the window, this makes it so they are brought back to the landing screen
```javascript
	next_btn.addEventListener("click", (e) => {
	  //check if it does not exceed max questions
	  if (que_count < questions.length - 1) {
	    que_count++; //increment the que_count value
	    que_numb++; //increment the que_numb value
	    showQuetions(que_count); //calling showQestions function
	    queCounter(que_numb); //passing que_numb value to queCounter
	    clearInterval(counter); //clear counter
	    clearInterval(counterLine); //clear counterLine
	    startTimer(timeValue); //calling startTimer function
	    startTimerLine(widthValue); //calling startTimerLine function
	    timeText.textContent = "Time Left"; //change the timeText to Time Left
	    next_btn.classList.remove("show"); //hide the next button
	  } else {
	    clearInterval(counter); //clear counter
	    clearInterval(counterLine); //clear counterLine
	    showResult(); //calling showResult function
	  }
	});
```
<p align="right"><sub>quizApp.js lines 71 - 89</sub></p>

- This code section adds the functionality of the "next question" button that becomes visible after the user selects an answer or the timer runs out
- If the program still has questions to show (i.e. the current question number isn't 5) increment the question number and count and use those new values to update the screen to show the next quiz question and possible answers
- If the quiz is currently on question 5, go to the results screen to show the user their score
```javascript
	function showQuetions(index) {
  		const que_text = document.querySelector(".que_text");
		...
		...
	}
```
<p align="right"><sub>quizApp.js lines 93 - 126</sub></p>

- showQuetions is a bigger function written later on in the code
- It's purpose is to show the question and possible answers for the current question number
```javascript
	  let que_tag =
	    "<span>" +
	    questions[index].numb +
	    ". " +
	    questions[index].question +
	    "</span>";
	  let option_tag =
	    '<div class="option"><span>' +
	    questions[index].options[0] +
	    "</span></div>" +
	    '<div class="option"><span>' +
	    questions[index].options[1] +
	    "</span></div>" +
	    '<div class="option"><span>' +
	    questions[index].options[2] +
	    "</span></div>" +
	    '<div class="option"><span>' +
	    questions[index].options[3] +
	    "</span></div>";
	  que_text.innerHTML = que_tag; //adding new (child) span tag inside que_tag
	  option_list.innerHTML = option_tag; //adding new (child) div tag inside option_tag
```
<p align="right"><sub>quizApp.js lines 98 - 118</sub></p>

- showQuetions uses the index given (which corresponds to the current question number) to create HTML elements
	- Firstly, it gets the number and question from the questions array, this data is formed into HTML (in the form of a JavaScript string) and then placed into a variable
	- This variable is called to add it to the HTML of que_text, an element that correspond with the HTML element "que_text", making this variable a child of que_text
 	- This process is repeated to get a list of possible answers as well, these elements are added to the "option_list" element as a child
```javascript
	for (i = 0; i < option.length; i++) {
		option[i].setAttribute("onclick", "optionSelected(this)");
	}
```
<p align="right"><sub>quizApp.js lines 123 - 125</sub></p>  

- At the end of this function, an array is used to go through all the elements in options (which is the list of possible answers), this array calls to a function that will add an EventListener to each option
#### Running The Quiz
```javascript
	function optionSelected(answer) {
		clearInterval(counter); //clear counter
		clearInterval(counterLine); //clear counterLine
		let userAns = answer.textContent; //getting user selected option
		let correcAns = questions[que_count].answer; //getting correct answer from array
		const allOptions = option_list.children.length; //getting all option items
		...
		...
	}
```
<p align="right"><sub>quizApp.js lines 132 - 164</sub></p>  

- This function takes in an "answer" paramater (an answer the user selected out of four on the quiz)
- As the user selected an aswer, the timer stops
```javascript
	if (userAns == correcAns) {
	    userScore += 1; //update total score value increment by 1
	    answer.classList.add("correct"); //add green color to correct selected option
	    answer.insertAdjacentHTML("beforeend", tickIconTag); //add tick icon to correct selected option
	    console.log("Correct Answer");
	    console.log("Your correct answers = " + userScore);
	  } else {
	    answer.classList.add("incorrect"); //add red color to correct selected option
	    answer.insertAdjacentHTML("beforeend", crossIconTag); //add cross icon to correct selected option
	    console.log("Wrong Answer");
	
	    for (i = 0; i < allOptions; i++) {
	      if (option_list.children[i].textContent == correcAns) {
	        //if there is an option which is matched to an array answer
	        option_list.children[i].setAttribute("class", "option correct"); //add green color to matched option
	        option_list.children[i].insertAdjacentHTML("beforeend", tickIconTag); //add tick icon to matched option
	        console.log("Auto selected correct answer.");
	      }
	    }
	  }
	  for (i = 0; i < allOptions; i++) {
	    option_list.children[i].classList.add("disabled"); //once user select an option, disable all options
	  }
	  next_btn.classList.add("show"); //show the next button if user selected any option
	}
```
<p align="right"><sub>quizApp.js lines 140 - 163</sub></p>  

- The function first checks if the user answered correctly or not
	- If the user answered correctly, their tracked score will go up and the answer button they clicked will turn green
 	- If the user answered incorrectly, the answer button they clicked will turn red
- The program also goes through the options and adds in the green color to the correct answer manually
	- This is done for the case where the user does not select the right answer, they still need to be shown what the correct one was even if they did not select it
- The final for loop is the function preventing the user from clicking another button (by disabling all the other answer buttons) after the user has selected an answer
```javascript
	function showResult() {
	  info_box.classList.remove("activeInfo"); //hide info box
	  quiz_box.classList.remove("activeQuiz"); //hide quiz box
	  result_box.classList.add("activeResult"); //show result box
	  const scoreText = result_box.querySelector(".score_text");
	  if (userScore > 3) {
	    // if user scored more than 3
	    //create a new span tag and pass the user score number and total question number
	    let scoreTag =
	      "<span>and congrats! , You got <p>" +
	      userScore +
	      "</p> out of <p>" +
	      questions.length +
	      "</p></span>";
	    scoreText.innerHTML = scoreTag; //add new span tag inside score_Text
	  } else if (userScore > 1) {
	    // if user scored more than 1
	    let scoreTag =
	      "<span>and nice , You got <p>" +
	      userScore +
	      "</p> out of <p>" +
	      questions.length +
	      "</p></span>";
	    scoreText.innerHTML = scoreTag;
	  } else {
	    // if user scored less than 1
	    let scoreTag =
	      "<span>and sorry , You got only <p>" +
	      userScore +
	      "</p> out of <p>" +
	      questions.length +
	      "</p></span>";
	    scoreText.innerHTML = scoreTag;
	  }
	}
```
<p align="right"><sub>quizApp.js lines 167 - 201</sub></p>  

- After question 5 the results will be shown to the user, the program will remove the quiz screen to show the results
- The application will check what the users score is and alter what it says to discuss the users score (a higher score corresponds to a more celebratory message), along with returning said score to the user
#### Showing Changing Elements
```javascript
	function startTimer(time) {
	  ...
	  if (time < 9) {
	      //if timer is less than 9
	      let addZero = timeCount.textContent;
	      timeCount.textContent = "0" + addZero; //add a 0 before time value
          }
          ...
	}
	function startTimerLine(time) {
	  ...
          time_line.style.width = time + "px"; //increasing width of time_line with px by time value
          ...
	}
```
<p align="right"><sub>quizApp.js lines 204 - 247</sub></p>  

- Some of the final methods are handling the timer operations
- startTimer takes in an input and counts down from that input to zero, all while dymaically altering the text on screen to match
	- For styling, the function will check if the time is lower than ten, and add a zero in front of the current time, if so, to keep the "##" format
- startTimerLine starts a timer so it can dynamically display a progress bar to visually show the user how much time they have left
```javascript
	function queCounter(index) {
	  //creating a new span tag and passing the question number and total question
	  let totalQueCounTag =
	    "<span><p>" +
	    index +
	    "</p> of <p>" +
	    questions.length +
	    "</p> Questions</span>";
	  bottom_ques_counter.innerHTML = totalQueCounTag; //adding new span tag inside bottom_ques_counter
	}
```
<p align="right"><sub>quizApp.js lines 249 - 258</sub></p>  

- The final code piece in quizApp.js updates the HTML on screen to show the current question the user is on
	- This is done by creating a variable which holds a String containing HTML, this variable is added as a child element to the bottom_ques_counter

### /css/style.css
- The CSS  for the program is standard, it is all stored in one file
- The CSS starts with setting the margin and padding to zero (to make styling more controllable) as well as importing a font from a font repository
- From there each element is individually styled to give the quiz app a cohesive aesthetic
