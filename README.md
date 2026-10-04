<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Rene Quiz</title>

<style>
@import url('https://fonts.googleapis.com/css2?family=Cormorant+Garamond:wght@400;500;600;700&family=Montserrat:wght@400;500;600;700&display=swap');

* {
    box-sizing: border-box;
}

body {
    margin: 0;
    min-height: 100vh;
    font-family: 'Montserrat', sans-serif;
    color: #f1f5ed;
    background:
        linear-gradient(rgba(3, 24, 15, 0.88), rgba(2, 20, 13, 0.95)),
        radial-gradient(circle at top, #24543a, #061b11 70%);
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 20px;
}

body::before {
    content: "🌲  🌲  🌲  🌲  🌲";
    position: fixed;
    top: 10px;
    left: 0;
    width: 100%;
    text-align: center;
    font-size: 25px;
    opacity: 0.15;
    pointer-events: none;
}

.container {
    width: 100%;
    max-width: 600px;
}

.screen {
    display: none;
    animation: fadeIn 0.4s ease;
}

.screen.active {
    display: block;
}

@keyframes fadeIn {
    from {
        opacity: 0;
        transform: translateY(10px);
    }
    to {
        opacity: 1;
        transform: translateY(0);
    }
}

.card {
    background: rgba(5, 35, 22, 0.94);
    border: 1px solid rgba(143, 190, 157, 0.35);
    border-radius: 24px;
    padding: 30px 24px;
    box-shadow: 0 20px 60px rgba(0,0,0,0.45);
}

.logo {
    text-align: center;
    font-family: 'Cormorant Garamond', serif;
    font-size: 62px;
    font-weight: 500;
    margin: 5px 0 0;
    color: #e4efe3;
}

.subtitle {
    text-align: center;
    color: #a9c5ad;
    letter-spacing: 4px;
    font-size: 12px;
    margin-top: -5px;
    text-transform: uppercase;
}

.tree-divider {
    text-align: center;
    color: #8ebd9c;
    margin: 25px 0;
    font-size: 20px;
}

.intro {
    text-align: center;
    line-height: 1.7;
    color: #d2dfd3;
}

.name-input {
    width: 100%;
    padding: 16px;
    margin-top: 20px;
    border-radius: 14px;
    border: 1px solid #527d61;
    background: #0a291a;
    color: white;
    font-size: 16px;
    outline: none;
    text-align: center;
}

.name-input:focus {
    border-color: #91c5a0;
}

.btn {
    width: 100%;
    padding: 15px;
    margin-top: 15px;
    border-radius: 30px;
    border: 1px solid #8cbb98;
    background: #285a3b;
    color: white;
    font-size: 15px;
    font-weight: 600;
    cursor: pointer;
    transition: 0.2s;
}

.btn:hover {
    background: #37744d;
    transform: translateY(-1px);
}

.btn.secondary {
    background: transparent;
    border-color: #527d61;
}

.btn.secondary:hover {
    background: rgba(82,125,97,0.15);
}

.small-note {
    text-align: center;
    color: #829c87;
    font-size: 12px;
    margin-top: 18px;
}

/* QUESTION SCREEN */

.top-bar {
    display: flex;
    justify-content: space-between;
    align-items: center;
    color: #9db9a2;
    font-size: 13px;
    margin-bottom: 12px;
}

.progress-container {
    width: 100%;
    height: 7px;
    background: #173a26;
    border-radius: 10px;
    overflow: hidden;
    margin-bottom: 35px;
}

.progress {
    height: 100%;
    width: 0%;
    background: #91c5a0;
    border-radius: 10px;
    transition: width 0.3s ease;
}

.question {
    font-family: 'Cormorant Garamond', serif;
    font-size: 31px;
    line-height: 1.2;
    text-align: center;
    margin-bottom: 28px;
    color: #f0f4ed;
}

.options {
    display: flex;
    flex-direction: column;
    gap: 12px;
}

.option {
    width: 100%;
    text-align: left;
    padding: 16px 18px;
    border-radius: 15px;
    border: 1px solid #416c50;
    background: #092719;
    color: #e2ebe2;
    cursor: pointer;
    font-size: 14px;
    transition: 0.2s;
}

.option:hover {
    border-color: #8ebd9c;
    background: #123a24;
}

.option.selected {
    border-color: #9bc9a6;
    background: #1d5031;
}

.option.correct {
    border-color: #8dd69e;
    background: #1b5932;
}

.option.wrong {
    border-color: #d68f8f;
    background: #542727;
}

.option.disabled {
    cursor: default;
}

.feedback {
    display: none;
    text-align: center;
    margin-top: 22px;
    padding: 15px;
    border-radius: 14px;
    background: rgba(40,90,59,0.25);
    color: #c9ddcc;
    font-size: 14px;
}

.feedback.show {
    display: block;
}

/* RESULTS */

.result-score {
    text-align: center;
    font-size: 64px;
    font-family: 'Cormorant Garamond', serif;
    margin: 10px 0;
}

.result-title {
    text-align: center;
    font-family: 'Cormorant Garamond', serif;
    font-size: 36px;
}

.result-message {
    text-align: center;
    color: #b9ccb9;
    line-height: 1.7;
}

.score-box {
    border: 1px solid #527d61;
    border-radius: 18px;
    padding: 20px;
    margin: 25px 0;
    text-align: center;
}

.score-box .big {
    font-size: 40px;
    font-family: 'Cormorant Garamond', serif;
}

.score-box p {
    margin: 5px 0;
    color: #9eb5a1;
}

/* LEADERBOARD */

.leaderboard-title {
    text-align: center;
    font-family: 'Cormorant Garamond', serif;
    font-size: 40px;
}

.leaderboard {
    margin-top: 20px;
}

.player {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 15px;
    margin-bottom: 9px;
    background: #092719;
    border: 1px solid #355b42;
    border-radius: 13px;
}

.player.you {
    border-color: #91c5a0;
    background: #123b25;
}

.rank {
    width: 35px;
    color: #9fc3a5;
    font-weight: bold;
}

.player-name {
    flex: 1;
}

.player-score {
    font-weight: bold;
    color: #b9d8bd;
}

/* ANSWERS */

.answer-list {
    margin-top: 20px;
}

.answer-item {
    background: #092719;
    border: 1px solid #355b42;
    border-radius: 14px;
    padding: 15px;
    margin-bottom: 10px;
}

.answer-question {
    font-weight: 600;
    line-height: 1.4;
    margin-bottom: 8px;
}

.answer-correct {
    color: #9bd2a5;
    font-size: 13px;
}

/* MOBILE */

@media (max-width: 500px) {
    body {
        padding: 12px;
    }

    .card {
        padding: 25px 18px;
        border-radius: 20px;
    }

    .logo {
        font-size: 53px;
    }

    .question {
        font-size: 28px;
    }

    .option {
        padding: 15px;
    }
}
</style>
</head>

<body>

<div class="container">

    <!-- START SCREEN -->
    <section id="startScreen" class="screen active">
        <div class="card">

            <div class="logo">Rene</div>
            <div class="subtitle">The Quiz</div>

            <div class="tree-divider">🌲</div>

            <p class="intro">
                How well do you really know Rene?
                <br><br>
                Put your knowledge to the test and see
                whether you can make it to the top of the leaderboard.
            </p>

            <input
                id="nameInput"
                class="name-input"
                type="text"
                placeholder="Enter your name"
                maxlength="25"
            >

            <button class="btn" onclick="startQuiz()">
                Start Quiz
            </button>

            <button class="btn secondary" onclick="showLeaderboard()">
                View Leaderboard
            </button>

            <div class="small-note">
                50 questions · One Rene · How well do you know him?
            </div>

        </div>
    </section>


    <!-- QUIZ SCREEN -->
    <section id="quizScreen" class="screen">
        <div class="card">

            <div class="top-bar">
                <span id="questionNumber">1 / 50</span>
                <span id="playerDisplay"></span>
            </div>

            <div class="progress-container">
                <div id="progress" class="progress"></div>
            </div>

            <div id="question" class="question"></div>

            <div id="options" class="options"></div>

            <div id="feedback" class="feedback"></div>

            <button
                id="nextBtn"
                class="btn"
                style="display:none;"
                onclick="nextQuestion()"
            >
                Next Question
            </button>

        </div>
    </section>


    <!-- RESULT SCREEN -->
    <section id="resultScreen" class="screen">
        <div class="card">

            <div class="logo" style="font-size:48px;">Rene</div>

            <div class="tree-divider">🌲</div>

            <div class="result-title">Quiz Complete!</div>

            <p class="result-message">
                Here's how well you know Rene.
            </p>

            <div class="score-box">
                <p>Your Score</p>
                <div id="finalScore" class="big">0%</div>
                <p id="scoreFraction">0 / 50</p>
            </div>

            <div id="resultMessage" class="result-message"></div>

            <button class="btn" onclick="showAnswers()">
                View Answers
            </button>

            <button class="btn secondary" onclick="showLeaderboard()">
                View Leaderboard
            </button>

            <button class="btn secondary" onclick="restartQuiz()">
                Play Again
            </button>

        </div>
    </section>


    <!-- LEADERBOARD SCREEN -->
    <section id="leaderboardScreen" class="screen">
        <div class="card">

            <div class="leaderboard-title">
                Leaderboard
            </div>

            <p class="result-message">
                Who knows Rene best?
            </p>

            <div id="leaderboard" class="leaderboard"></div>

            <button class="btn secondary" onclick="goHome()">
                Back to Home
            </button>

        </div>
    </section>


    <!-- ANSWERS SCREEN -->
    <section id="answersScreen" class="screen">
        <div class="card">

            <div class="leaderboard-title">
                Answer Key
            </div>

            <p class="result-message">
                Rene's answers
            </p>

            <div id="answerList" class="answer-list"></div>

            <button class="btn" onclick="showResults()">
                Back to Results
            </button>

        </div>
    </section>

</div>


<script>

const questions = [

{
    q: "What’s your ideal Friday night?",
    options: ["Watching movies", "Going out with friends", "Gambling", "Staying home and gaming"],
    answer: 2
},

{
    q: "How would you describe your personality?",
    options: ["Laid-back", "Stubborn", "Outgoing", "Sensitive"],
    answer: 1
},

{
    q: "What’s your biggest strength?",
    options: ["Loyalty", "Patience", "Reassurance", "Honesty"],
    answer: 2
},

{
    q: "What’s your biggest weakness?",
    options: ["Overthinking", "Impatience", "Stoicism", "Arrogance"],
    answer: 2
},

{
    q: "What do you usually do when you’re stressed?",
    options: ["Sleep", "Go for a walk", "Sing", "Play games"],
    answer: 2
},

{
    q: "What kind of humour do you have?",
    options: ["Dark humour", "Sarcastic", "Clever wit", "Silly humour"],
    answer: 2
},

{
    q: "When do you feel most comfortable?",
    options: ["When I’m alone", "With close friends", "With family", "At home"],
    answer: 2
},

{
    q: "What’s your ideal holiday?",
    options: ["Relaxing at the beach", "Exploring nature", "Exploring historical landmarks", "Visiting theme parks"],
    answer: 2
},

{
    q: "Are you more of a morning person or a night owl?",
    options: ["Night owl", "Neither", "Depends on the day", "Morning"],
    answer: 3
},

{
    q: "How do you usually make important decisions?",
    options: ["Follow my instincts", "Ask someone for advice", "Argue the why", "Make a pros and cons list"],
    answer: 2
},

{
    q: "What’s your texting style like?",
    options: ["Fast replies", "Detailed messages", "Lots of emojis", "Lazy"],
    answer: 3
},

{
    q: "What matters most to you in a friendship?",
    options: ["Honesty", "Communication", "Loyalty", "Shared interests"],
    answer: 2
},

{
    q: "What attracts you to someone first?",
    options: ["Appearance", "Confidence", "Humour", "Intellect"],
    answer: 3
},

{
    q: "What’s your flirting style?",
    options: ["Teasing", "Complimenting", "Playful", "Non existent"],
    answer: 3
},

{
    q: "Are you more of a planner or spontaneous?",
    options: ["Planner", "Mostly a planner", "A bit of both", "Spontaneous"],
    answer: 3
},

{
    q: "Which decade would you most like to live in?",
    options: ["1920’s", "1940’s", "1960’s", "1980’s"],
    answer: 2
},

{
    q: "What would your ideal home be like?",
    options: ["Modern and spacious", "Minimalist", "Rustic", "Cosy"],
    answer: 3
},

{
    q: "What would you rather have: money, health, relationships, or luck?",
    options: ["Money", "Health", "Luck", "Relationships"],
    answer: 3
},

{
    q: "What would you do first if you suddenly became rich?",
    options: ["Travel the world", "Buy a new car", "Invest the money", "Buy a family home"],
    answer: 3
},

{
    q: "What’s your relationship with money like?",
    options: ["Careful", "Frugal", "Comfortable", "Reckless"],
    answer: 2
},

{
    q: "What’s your ideal night out?",
    options: ["Dinner and drinks", "Concert", "Movie theatre", "Arcades / 10 pin bowling"],
    answer: 3
},

{
    q: "What’s your ideal night in?",
    options: ["Reading", "Playing games", "Watching documentaries", "Watching silly movies"],
    answer: 3
},

{
    q: "What’s your biggest pet peeve?",
    options: ["Loud chewing", "People being late", "Being interrupted", "Disdain to others"],
    answer: 3
},

{
    q: "What do you usually do when someone annoys you?",
    options: ["Tell them directly", "Argue with them", "Walk away", "Go silent"],
    answer: 3
},

{
    q: "How good are you at cooking?",
    options: ["5/10", "6/10", "7/10", "8/10"],
    answer: 3
},

{
    q: "What’s your ideal morning routine?",
    options: ["Coffee and breakfast", "Exercise first", "Stay in bed for a while", "Shower first and walk"],
    answer: 3
},

{
    q: "What would you most like to experience if you could?",
    options: ["Skydiving", "Scuba diving", "Bungee jumping", "Paragliding"],
    answer: 2
},

{
    q: "What skill would you most like to master?",
    options: ["Public speaking", "Cooking", "Active listening", "Playing an instrument"],
    answer: 2
},

{
    q: "Where would you most like to live?",
    options: ["Australia", "Canada", "New Zealand", "United Kingdom"],
    answer: 2
},

{
    q: "What does your perfect weekend look like?",
    options: ["Going out with friends", "Travelling", "Staying home and relaxing", "Watching sport"],
    answer: 3
},

{
    q: "How do you usually react to criticism?",
    options: ["Defend myself", "Argue back", "Think about it immediately", "Go silent"],
    answer: 3
},

{
    q: "What makes it easier for you to forgive someone?",
    options: ["An apology", "Time", "Changed behaviour", "Authenticity"],
    answer: 3
},

{
    q: "What quality do you value most in other people?",
    options: ["Honesty", "Kindness", "Humour", "Loyalty"],
    answer: 3
},

{
    q: "What’s your love language?",
    options: ["Words of affirmation", "Acts of service", "Quality time", "Physical Touch"],
    answer: 3
},

{
    q: "What do you prefer when you’re upset?",
    options: ["Alone time", "Advice", "Distraction", "Company"],
    answer: 3
},

{
    q: "What’s your biggest fear?",
    options: ["Losing someone you love", "Failure", "Being alone", "Not giving my parents grandkids"],
    answer: 3
},

{
    q: "How would you most like to be remembered?",
    options: ["As someone successful", "As someone funny", "As someone who helped others", "Someone who people felt safe around"],
    answer: 3
},

{
    q: "What period of your life would you most like to relive?",
    options: ["Childhood", "University", "High school", "Early adulthood"],
    answer: 2
},

{
    q: "What kinds of things do you tend to hold onto?",
    options: ["Old photos", "Letters", "Clothes", "Medicine cups"],
    answer: 3
},

{
    q: "What’s one thing you’d change about yourself?",
    options: ["My stubbornness", "My impatience", "My overthinking", "My arrogance"],
    answer: 3
},

{
    q: "What motivates you the most?",
    options: ["Personal success", "Money", "Competition", "Watching others grow"],
    answer: 3
},

{
    q: "How do you usually handle problems?",
    options: [
        "Ignore them until they go away",
        "Talk about them immediately",
        "Ask someone else what to do",
        "Analyse, evaluate and then talk about it"
    ],
    answer: 3
},

{
    q: "What would make up your perfect day?",
    options: [
        "Travelling somewhere new",
        "Having the whole day to yourself",
        "Doing something adventurous",
        "Spend it with loved ones"
    ],
    answer: 3
},

{
    q: "What kind of gesture means the most to you?",
    options: [
        "Receiving a gift",
        "A handwritten letter",
        "Someone giving you advice",
        "Being there"
    ],
    answer: 3
},

{
    q: "What makes you happiest?",
    options: [
        "Winning",
        "Spending money",
        "Travelling",
        "Watching others grow and succeed"
    ],
    answer: 3
},

{
    q: "What are you most likely to spend money on?",
    options: ["Clothes", "Food", "Travel", "Horse Racing"],
    answer: 3
},

{
    q: "Who would you most like to have dinner with?",
    options: ["A celebrity", "A historical figure", "A famous athlete", "My friend"],
    answer: 3
},

{
    q: "If your life were a movie, what genre would it be?",
    options: ["Comedy", "Romance", "Psychological thriller", "Survival drama"],
    answer: 3
},

{
    q: "What would someone who knows you really well know about you?",
    options: [
        "That I secretly love attention",
        "That I overthink everything",
        "That I hate being alone",
        "That I care about others more than I should"
    ],
    answer: 3
},

{
    q: "What best describes your general approach to life?",
    options: ["Ambitious", "Cautious", "Optimistic", "Nonchalant"],
    answer: 3
}

];


let currentQuestion = 0;
let score = 0;
let playerName = "";
let answered = false;


/* START QUIZ */

function startQuiz() {

    const input = document.getElementById("nameInput");
    playerName = input.value.trim();

    if (!playerName) {
        input.style.borderColor = "#d68f8f";
        input.placeholder = "Please enter your name";
        return;
    }

    currentQuestion = 0;
    score = 0;

    document.getElementById("playerDisplay").textContent = playerName;

    showScreen("quizScreen");
    loadQuestion();
}


/* LOAD QUESTION */

function loadQuestion() {

    answered = false;

    const q = questions[currentQuestion];

    document.getElementById("questionNumber").textContent =
        `${currentQuestion + 1} / ${questions.length}`;

    document.getElementById("progress").style.width =
        `${((currentQuestion + 1) / questions.length) * 100}%`;

    document.getElementById("question").textContent = q.q;

    const optionsContainer = document.getElementById("options");
    optionsContainer.innerHTML = "";

    document.getElementById("feedback").classList.remove("show");
    document.getElementById("nextBtn").style.display = "none";

    q.options.forEach((option, index) => {

        const button = document.createElement("button");

        button.className = "option";
        button.textContent = option;

        button.onclick = () => selectAnswer(index, button);

        optionsContainer.appendChild(button);
    });
}


/* ANSWER */

function selectAnswer(index, selectedButton) {

    if (answered) return;

    answered = true;

    const q = questions[currentQuestion];
    const buttons = document.querySelectorAll(".option");

    buttons.forEach((button, i) => {

        button.classList.add("disabled");

        if (i === q.answer) {
            button.classList.add("correct");
        }
    });

    if (index === q.answer) {

        score++;

        selectedButton.classList.add("correct");

        showFeedback(
            "Correct!",
            "You know Rene pretty well."
        );

    } else {

        selectedButton.classList.add("wrong");

        showFeedback(
            "Not quite!",
            `Rene's answer was: ${q.options[q.answer]}`
        );
    }

    document.getElementById("nextBtn").style.display = "block";
}


/* FEEDBACK */

function showFeedback(title, message) {

    const feedback = document.getElementById("feedback");

    feedback.innerHTML =
        `<strong>${title}</strong><br>${message}`;

    feedback.classList.add("show");
}


/* NEXT QUESTION */

function nextQuestion() {

    currentQuestion++;

    if (currentQuestion >= questions.length) {
        finishQuiz();
        return;
    }

    loadQuestion();
}


/* FINISH */

function finishQuiz() {

    const percentage = Math.round(
        (score / questions.length) * 100
    );

    document.getElementById("finalScore").textContent =
        `${percentage}%`;

    document.getElementById("scoreFraction").textContent =
        `${score} / ${questions.length}`;

    let message = "";

    if (percentage === 100) {
        message = "Perfect score. You know Rene better than Rene knows himself.";
    } else if (percentage >= 90) {
        message = "Almost perfect. You definitely know Rene very well.";
    } else if (percentage >= 75) {
        message = "Pretty impressive. You know Rene really well.";
    } else if (percentage >= 60) {
        message = "Not bad! You know quite a bit about Rene.";
    } else if (percentage >= 40) {
        message = "You know a little about Rene, but there’s still plenty to learn.";
    } else {
        message = "Rene might need to give you a few more lessons.";
    }

    document.getElementById("resultMessage").textContent = message;

    saveScore(playerName, score, percentage);

    showScreen("resultScreen");
}


/* SAVE LEADERBOARD */

function saveScore(name, score, percentage) {

    let leaderboard =
        JSON.parse(localStorage.getItem("reneLeaderboard")) || [];

    leaderboard.push({
        name: name,
        score: score,
        percentage: percentage,
        date: new Date().toISOString()
    });

    leaderboard.sort((a, b) => {

        if (b.score !== a.score) {
            return b.score - a.score;
        }

        return new Date(a.date) - new Date(b.date);
    });

    leaderboard = leaderboard.slice(0, 50);

    localStorage.setItem(
        "reneLeaderboard",
        JSON.stringify(leaderboard)
    );
}


/* LEADERBOARD */

function showLeaderboard() {

    const leaderboard =
        JSON.parse(localStorage.getItem("reneLeaderboard")) || [];

    const container =
        document.getElementById("leaderboard");

    container.innerHTML = "";

    if (leaderboard.length === 0) {

        container.innerHTML = `
            <p class="result-message">
                No scores yet.<br>
                Be the first to take Rene's quiz.
            </p>
        `;

    } else {

        leaderboard.forEach((player, index) => {

            const div = document.createElement("div");

            div.className = "player";

            if (
                playerName &&
                player.name.toLowerCase() === playerName.toLowerCase()
            ) {
                div.classList.add("you");
            }

            div.innerHTML = `
                <span class="rank">#${index + 1}</span>
                <span class="player-name">${escapeHTML(player.name)}</span>
                <span class="player-score">
                    ${player.percentage}%
                </span>
            `;

            container.appendChild(div);
        });
    }

    showScreen("leaderboardScreen");
}


/* ANSWER KEY */

function showAnswers() {

    const container =
        document.getElementById("answerList");

    container.innerHTML = "";

    questions.forEach((q, index) => {

        const item = document.createElement("div");

        item.className = "answer-item";

        item.innerHTML = `
            <div class="answer-question">
                ${index + 1}. ${q.q}
            </div>

            <div class="answer-correct">
                ✓ ${q.options[q.answer]}
            </div>
        `;

        container.appendChild(item);
    });

    showScreen("answersScreen");
}


/* RESULTS */

function showResults() {
    showScreen("resultScreen");
}


/* RESTART */

function restartQuiz() {

    currentQuestion = 0;
    score = 0;

    showScreen("quizScreen");
    loadQuestion();
}


/* HOME */

function goHome() {

    document.getElementById("nameInput").value = "";

    showScreen("startScreen");
}


/* SCREEN SWITCHING */

function showScreen(id) {

    document.querySelectorAll(".screen").forEach(screen => {
        screen.classList.remove("active");
    });

    document.getElementById(id).classList.add("active");

    window.scrollTo({
        top: 0,
        behavior: "smooth"
    });
}


/* SECURITY */

function escapeHTML(str) {

    return str
        .replace(/&/g, "&amp;")
        .replace(/</g, "&lt;")
        .replace(/>/g, "&gt;")
        .replace(/"/g, "&quot;")
        .replace(/'/g, "&#039;");
}

</script>

</body>
</html>
