<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Romantic Couple Quiz</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha3/dist/css/bootstrap.min.css" rel="stylesheet">
    <style>
        body {
            background: url('https://i.imgur.com/QlWuEYY.jpg') no-repeat center center fixed;
            background-size: cover;
            font-family: Arial, sans-serif;
            color: #fff;
        }
        .game-container {
            max-width: 700px;
            margin: auto;
            background: rgba(0, 0, 0, 0.7);
            padding: 20px;
            border-radius: 15px;
            box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.4);
        }
        h1, .lead {
            color: #ffebcd;
        }
        .btn {
            font-size: 16px;
        }
        .score {
            font-size: 18px;
            font-weight: bold;
            color: #fdd835;
        }
        .romantic-message {
            font-size: 24px;
            color: #ff6f61;
            font-weight: bold;
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <div class="game-container text-center">
        <h1>Romantic Couple Quiz</h1>
        <p class="lead">Let’s play and make things a little spicy!</p>

        <div id="questionBox">
            <h4 id="question">Click 'Start' to begin!</h4>
            <p id="asker" class="mt-2" style="font-style: italic; font-size: 18px;"></p>
        </div>

        <div id="buttons" class="mt-3">
            <button id="startBtn" class="btn btn-primary w-100" onclick="startGame()">Start Game</button>
            <button id="answer1" class="btn btn-outline-light mt-2 w-100 d-none" onclick="checkAnswer(1)"></button>
            <button id="answer2" class="btn btn-outline-light mt-2 w-100 d-none" onclick="checkAnswer(2)"></button>
        </div>

        <div id="scoreBoard" class="mt-4">
            <p class="score">Your Score: <span id="playerScore">0</span></p>
            <p class="score">Girlfriend's Score: <span id="girlfriendScore">0</span></p>
        </div>

        <div id="romanticMessage" class="romantic-message d-none">
            I love you, I want to hug you, and kiss you passionately.
        </div>
    </div>

    <script>
        const questions = [
            { 
                question: "Would you rather kiss me for 10 minutes or cuddle me for an hour?", 
                options: ["Kiss for 10 minutes", "Cuddle for an hour"], 
                correct: 1, 
                player: "girlfriend", 
                asker: "You are asking this question" 
            },
            { 
                question: "Where would you like to go on a romantic date?", 
                options: ["Beach at sunset", "Candlelight dinner"], 
                correct: 2, 
                player: "player", 
                asker: "She is asking this question" 
            },
            { 
                question: "What’s my favorite part of your body?", 
                options: ["Your lips", "Your eyes"], 
                correct: 1, 
                player: "girlfriend", 
                asker: "You are asking this question" 
            },
            { 
                question: "What turns you on the most about me?", 
                options: ["My smile", "My touch"], 
                correct: 2, 
                player: "player", 
                asker: "She is asking this question" 
            },
            { 
                question: "What’s something we should try together for the first time?", 
                options: ["A new adventure", "A sensual dance"], 
                correct: 2, 
                player: "girlfriend", 
                asker: "You are asking this question" 
            },
            { 
                question: "If we had a whole day to ourselves, what would you want to do?", 
                options: ["Stay in bed all day", "Go on an adventure"], 
                correct: 1, 
                player: "player", 
                asker: "She is asking this question" 
            },
            { 
                question: "What’s your favorite memory of us so far?", 
                options: ["Our first kiss", "Our first date"], 
                correct: 1, 
                player: "girlfriend", 
                asker: "You are asking this question" 
            },
            { 
                question: "Would you rather whisper sweet nothings or exchange naughty texts?", 
                options: ["Sweet nothings", "Naughty texts"], 
                correct: 2, 
                player: "player", 
                asker: "She is asking this question" 
            },
            { 
                question: "If I were to surprise you, what would make you happiest?", 
                options: ["A romantic getaway", "A steamy night together"], 
                correct: 2, 
                player: "girlfriend", 
                asker: "You are asking this question" 
            },
            { 
                question: "What’s the most romantic thing you’d love me to do?", 
                options: ["A surprise date", "Write you a love letter"], 
                correct: 1, 
                player: "player", 
                asker: "She is asking this question" 
            },
            { 
                question: "What’s one thing I do that makes your heart race?", 
                options: ["My smile", "When I get close to you"], 
                correct: 2, 
                player: "girlfriend", 
                asker: "You are asking this question" 
            },
            { 
                question: "If we were alone on a deserted island, what would we do first?", 
                options: ["Build a shelter", "Make out"], 
                correct: 2, 
                player: "player", 
                asker: "She is asking this question" 
            },
            { 
                question: "What’s one naughty secret you’ve been wanting to share with me?", 
                options: ["What I dream about us", "What I fantasize about"], 
                correct: 2, 
                player: "girlfriend", 
                asker: "You are asking this question" 
            },
            { 
                question: "What do you love most about me?", 
                options: ["My body", "My soul"], 
                correct: 2, 
                player: "player", 
                asker: "She is asking this question" 
            },
            { 
                question: "What’s one thing we’ve never done that you’d love to try?", 
                options: ["A romantic getaway", "An intimate spa night"], 
                correct: 2, 
                player: "girlfriend", 
                asker: "You are asking this question" 
            }
        ];

        let currentQuestionIndex = -1;
        let playerScore = 0;
        let girlfriendScore = 0;

        function startGame() {
            currentQuestionIndex = -1;
            playerScore = 0;
            girlfriendScore = 0;
            document.getElementById("playerScore").textContent = playerScore;
            document.getElementById("girlfriendScore").textContent = girlfriendScore;
            document.getElementById("romanticMessage").classList.add("d-none");
            loadNextQuestion();
        }

        function loadNextQuestion() {
            currentQuestionIndex++;
            if (currentQuestionIndex >= questions.length) {
                document.getElementById("question").textContent = "Game Over! Thank you for playing!";
                document.getElementById("answer1").classList.add("d-none");
                document.getElementById("answer2").classList.add("d-none");
                document.getElementById("startBtn").classList.remove("d-none");
                document.getElementById("startBtn").textContent = "Play Again";
                document.getElementById("romanticMessage").classList.remove("d-none");
                return;
            }

            const currentQuestion = questions[currentQuestionIndex];
            document.getElementById("question").textContent = currentQuestion.question;
            document.getElementById("asker").textContent = currentQuestion.asker;
            document.getElementById("answer1").textContent = currentQuestion.options[0];
            document.getElementById("answer2").textContent = currentQuestion.options[1];
            document.getElementById("answer1").classList.remove("d-none");
            document.getElementById("answer2").classList.remove("d-none");
            document.getElementById("startBtn").classList.add("d-none");
        }

        function checkAnswer(selected) {
            const currentQuestion = questions[currentQuestionIndex];
            if (selected === currentQuestion.correct) {
                if (currentQuestion.player === "player") {
                    playerScore++;
                } else {
                    girlfriendScore++;
                }
            }

            document.getElementById("playerScore").textContent = playerScore;
            document.getElementById("girlfriendScore").textContent = girlfriendScore;

            loadNextQuestion();
        }
    </script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha3/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>
