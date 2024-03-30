# Quiz-website
its a basic programming related quiz website.

index.html
<!DOCTYPE html>
<html>
<head>
  <title>Quiz App - Easy Tutorials</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
<div class="app">
  <h1>programming related quiz  </h1>
  <div class="quiz">
    <h2 id="question">Question goes here</h2>
    <div id="answer-buttons">
      <button class="btn">Answer 1</button>
      <button class="btn">Answer 2</button>
      <button class="btn">Answer 3</button>
      <button class="btn">Answer 4</button>
    </div>
    <button id="next-btn">Next</button>
  </div>
</div>
<a href="https://www.youtube.com/channel/UCkjoHfkLEy7ZT4bA2myJ8xA?sub_confirmation=1" class="watch-link">Watch More Videos</a>
<script src="script.js"></script>
</body>
</html>


script.js
const questions = [
    {
        question: "who is the father of java programming language?",
        answers: [
            { text: "Dennis MacAlistair Ritchie", correct: false},
            { text: "James Gosling", correct: true},
            { text: "Tim Berners-Lee", correct: false},
            { text: "none of them", correct: false},
        ]
    },
    {
        question: "the java programming language is released in_ ?",
        answers: [
            { text: "May 1995", correct: true},
            { text: "May 1991", correct: false},
            { text: "May 1998", correct: false},
            { text: "May 2000", correct: false},
        ]
    },
    {
        question: "in this which one is not the programming language?",
        answers: [
            { text: "Python", correct: false},
            { text: "C++", correct: false},
            { text: "java", correct: false},
            { text: "HTML", correct: true},
        ]
    },
    {
        question: "which programming language is used for youtube?",
        answers: [
            { text: "C++", correct: false},
            { text: "Python", correct: true},
            { text: "JavaScript", correct: false},
            { text: "none of them", correct: false},
        ]
    }  
];

const questionElement = document.getElementById("question");
const answerButtons = document.getElementById("answer-buttons");
const nextButton = document.getElementById("next-btn");

let currentQuestionIndex = 0;
let score = 0;

function startQuiz(){
    currentQuestionIndex = 0;
    score = 0;
    nextButton.innerHTML = "Next";
    showQuestion();
}

function showQuestion(){
    resetState();
    let currentQuestion = questions[currentQuestionIndex];
    let questionNo = currentQuestionIndex + 1;
    questionElement.innerHTML = questionNo + ". " + currentQuestion.question;

    currentQuestion.answers.forEach(answer => {
        const button = document.createElement("button");
        button.innerHTML = answer.text;
        button.classList.add("btn");
        answerButtons.appendChild(button);
        if(answer.correct){
            button.dataset.correct = answer.correct;
        }
        button.addEventListener("click", selectAnswer);
    });
}


function resetState(){
    nextButton.style.display = "none";
    while(answerButtons.firstChild){
        answerButtons.removeChild(answerButtons.firstChild);
    }
}

function selectAnswer(e){
    const selectedBtn = e.target;
    const isCorrect = selectedBtn.dataset.correct === "true";
    if(isCorrect){
        selectedBtn.classList.add("correct");
        score++;
    }else{
        selectedBtn.classList.add("incorrect");
    }
    Array.from(answerButtons.children).forEach(button => {
        if(button.dataset.correct === "true"){
            button.classList.add("correct");
        }
        button.disabled = true;
    });
    nextButton.style.display = "block";
}

function showScore(){
    resetState();
    questionElement.innerHTML = `You scored ${score} out of ${questions.length}!`;
    nextButton.innerHTML = "Play Again";
    nextButton.style.display = "block";
}

function handleNextButton(){
    currentQuestionIndex++;
    if(currentQuestionIndex < questions.length){
        showQuestion();
    }else{
        showScore();
    }
}


nextButton.addEventListener("click", ()=>{
    if(currentQuestionIndex < questions.length){
        handleNextButton();
    }else{
        startQuiz();
    }
});



style.css
startQuiz();

* {
    margin: 0;
    padding: 0;
    font-family: 'Poppins', sans-serif;
    box-sizing: border-box;
  }
  body{
    background: #446dc0;
  }
  .app{
    background: #dd699f;
    width: 90%;
    max-width: 600px;
    margin: 100px auto 0;
    border-radius: 10px;
    padding: 30px;
  }
  .app h1{
    font-size: 25px;
    color: #001e4d;
    font-weight: 600;
    border-bottom: 1px solid #333;
    padding-bottom: 30px;
  }
  .quiz{
    padding: 20px 0;
  }
  .quiz h2{
    font-size: 18px;
    color: #001e4d;
    font-weight: 600;
  }
  .btn{
    background: #fff;
    color: #222;
    font-weight: 500;
    width: 100%;
    border: 1px solid #222;
    padding: 10px;
    margin: 10px 0;
    text-align: left;
    border-radius: 4px;
    cursor: pointer;
    transition: all 0.3s;
  }
  .btn:hover:not([disabled]){
    background: #222;
    color: #fff;
  }
  .btn:disabled{
    cursor: no-drop;
  }
  #next-btn{
    background: #001e4d;
    color: #fff;
    font-weight: 500;
    width: 150px;
    border: 0;
    padding: 10px;
    margin: 20px auto 0;
    border-radius: 4px;
    cursor: pointer;
    display: none;
  }
  .correct{
    background: #9aeabc;
  }
  .incorrect{
    background: #ff9393;
  }
  
   .watch-link{
     position: absolute;
     bottom: 5%;
     right: 5%;
     color: #fff;
     text-decoration: none;
   }
