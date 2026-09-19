[index.html](https://github.com/user-attachments/files/32421222/index.html)
<!DOCTYPE html>
<html lang="tr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Tilki - İngilizce Öğren</title>

<style>
body {
    margin: 0;
    font-family: Arial, sans-serif;
    background: #fff7ed;
    color: #333;
}

header {
    background: #f97316;
    color: white;
    text-align: center;
    padding: 25px;
}

header h1 {
    margin: 0;
    font-size: 38px;
}

nav {
    background: white;
    text-align: center;
    padding: 12px;
    box-shadow: 0 2px 8px #ddd;
}

nav button {
    border: none;
    background: #fff;
    padding: 10px 16px;
    margin: 4px;
    border-radius: 10px;
    cursor: pointer;
    font-size: 16px;
}

nav button:hover {
    background: #ffedd5;
}

section {
    display: none;
    max-width: 800px;
    margin: 30px auto;
    padding: 20px;
}

.active {
    display: block;
}

.card {
    background: white;
    padding: 25px;
    border-radius: 18px;
    box-shadow: 0 4px 15px #ddd;
    margin-bottom: 20px;
}

.levels button,
.answers button,
.game-buttons button {
    display: block;
    width: 100%;
    margin: 10px 0;
    padding: 14px;
    border: none;
    border-radius: 12px;
    background: #fb923c;
    color: white;
    font-size: 17px;
    cursor: pointer;
}

.levels button:hover,
.answers button:hover,
.game-buttons button:hover {
    background: #ea580c;
}

.score {
    font-size: 20px;
    font-weight: bold;
    color: #ea580c;
}

#result {
    font-size: 20px;
    font-weight: bold;
    margin-top: 15px;
}

.badge {
    display: inline-block;
    background: #ffedd5;
    padding: 15px;
    border-radius: 15px;
    margin: 8px;
}

.word {
    font-size: 32px;
    font-weight: bold;
    text-align: center;
    margin: 20px;
}

footer {
    text-align: center;
    padding: 25px;
    color: #777;
}
</style>
</head>

<body>

<header>
    <h1>🦊 Tilki</h1>
    <p>İngilizce öğren, soru çöz, oyun oyna!</p>
</header>

<nav>
    <button onclick="showSection('home')">🏠 Ana Sayfa</button>
    <button onclick="showSection('questions')">📚 Soru Çöz</button>
    <button onclick="showSection('games')">🎮 Oyunlar</button>
    <button onclick="showSection('achievements')">🏆 Başarımlar</button>
</nav>

<section id="home" class="active">
    <div class="card">
        <h2>🦊 Tilki'ye Hoş Geldin!</h2>
        <p>İngilizceni geliştirmenin eğlenceli yolu!</p>
        <p>Bir seviye seç, soruları çöz ve puan kazan.</p>
        <p>Sonra mini oyunlarla kelimelerini geliştir! 🎮</p>

        <p class="score">⭐ Puanın: <span id="homeScore">0</span></p>
    </div>
</section>

<section id="questions">
    <div class="card">
        <h2>📚 Soru Çöz</h2>
        <p>İngilizce seviyeni seç:</p>

        <div class="levels">
            <button onclick="startQuiz('A1')">🟢 A1 - Başlangıç</button>
            <button onclick="startQuiz('A2')">🔵 A2 - Temel</button>
            <button onclick="startQuiz('B1')">🟠 B1 - Orta</button>
            <button onclick="startQuiz('B2')">🔴 B2 - Orta Üstü</button>
        </div>
    </div>

    <div class="card" id="quizBox" style="display:none;">
        <p><b id="levelText"></b></p>
        <h2 id="question"></h2>

        <div class="answers" id="answers"></div>

        <div id="result"></div>
        <p>Soru: <span id="questionNumber">1</span></p>
    </div>
</section>

<section id="games">
    <div class="card">
        <h2>🎮 Kelime Tahmin Oyunu</h2>
        <p>İngilizce kelimenin Türkçe anlamını seç!</p>

        <div class="word" id="gameWord">cat</div>

        <div class="game-buttons" id="gameAnswers"></div>

        <div id="gameResult"></div>
        <p class="score">⭐ Puanın: <span id="gameScore">0</span></p>
    </div>
</section>

<section id="achievements">
    <div class="card">
        <h2>🏆 Başarımlar</h2>

        <div class="badge">
            ⭐ İlk 10 Puan
            <br>
            <span id="badge10">🔒</span>
        </div>

        <div class="badge">
            📚 5 Soru
            <br>
            <span id="badge5">🔒</span>
        </div>

        <div class="badge">
            🎮 Oyun Ustası
            <br>
            <span id="badgeGame">🔒</span>
        </div>
    </div>
</section>

<footer>
    🦊 Tilki - İngilizce Öğrenme Sitesi
</footer>

<script>

let score = 0;
let questionsSolved = 0;
let gamePoints = 0;
let currentQuestion = 0;
let currentQuestions = [];

const quizzes = {

A1: [
{
q: "What is the opposite of 'big'?",
a: ["small", "fast", "happy", "cold"],
correct: "small"
},
{
q: "I ___ a student.",
a: ["am", "is", "are", "be"],
correct: "am"
},
{
q: "What does 'cat' mean?",
a: ["Köpek", "Kedi", "Kuş", "Balık"],
correct: "Kedi"
}
],

A2: [
{
q: "She ___ to school every day.",
a: ["go", "goes", "going", "gone"],
correct: "goes"
},
{
q: "What is the past of 'eat'?",
a: ["eated", "ate", "eats", "eating"],
correct: "ate"
},
{
q: "I have lived here ___ 2020.",
a: ["for", "since", "at", "on"],
correct: "since"
}
],

B1: [
{
q: "If I had more money, I ___ a new computer.",
a: ["buy", "will buy", "would buy", "bought"],
correct: "would buy"
},
{
q: "She has already ___ her homework.",
a: ["finish", "finished", "finishing", "finishes"],
correct: "finished"
},
{
q: "What does 'although' mean?",
a: ["çünkü", "rağmen", "bu yüzden", "önce"],
correct: "rağmen"
}
],

B2: [
{
q: "If I ___ you, I would study more.",
a: ["am", "was", "were", "be"],
correct: "were"
},
{
q: "The book ___ by millions of people.",
a: ["read", "was read", "reading", "reads"],
correct: "was read"
},
{
q: "What does 'accurate' mean?",
a: ["doğru/isabetli", "hızlı", "gürültülü", "eski"],
correct: "doğru/isabetli"
}
]

};

function showSection(id) {

    document.querySelectorAll("section").forEach(section => {
        section.classList.remove("active");
    });

    document.getElementById(id).classList.add("active");

    if (id === "games") {
        newGameQuestion();
    }

    updateScore();
}

function updateScore() {
    document.getElementById("homeScore").innerText = score;
    document.getElementById("gameScore").innerText = gamePoints;

    if (score >= 10) {
        document.getElementById("badge10").innerText = "✅";
    }

    if (questionsSolved >= 5) {
        document.getElementById("badge5").innerText = "✅";
    }

    if (gamePoints >= 30) {
        document.getElementById("badgeGame").innerText = "✅";
    }
}

function startQuiz(level) {

    currentQuestions = quizzes[level];
    currentQuestion = 0;

    document.getElementById("quizBox").style.display = "block";
    document.getElementById("levelText").innerText = level + " Seviyesi";

    showQuestion();
}

function showQuestion() {

    if (currentQuestion >= currentQuestions.length) {

        document.getElementById("question").innerText =
            "🎉 Bu seviyedeki sorular bitti!";

        document.getElementById("answers").innerHTML =
            "<button onclick=\"currentQuestion=0; showQuestion();\">🔄 Tekrar Çöz</button>";

        document.getElementById("result").innerText =
            "Harika! Toplam puanın: " + score;

        return;
    }

    let q = currentQuestions[currentQuestion];

    document.getElementById("question").innerText = q.q;

    document.getElementById("questionNumber").innerText =
        (currentQuestion + 1) + " / " + currentQuestions.length;

    document.getElementById("result").innerText = "";

    let answers = document.getElementById("answers");
    answers.innerHTML = "";

    q.a.forEach(answer => {

        let button = document.createElement("button");

        button.innerText = answer;

        button.onclick = function() {
            checkAnswer(answer);
        };

        answers.appendChild(button);
    });
}

function checkAnswer(answer) {

    let correct =
        currentQuestions[currentQuestion].correct;

    if (answer === correct) {

        score += 10;
        questionsSolved++;

        document.getElementById("result").innerText =
            "✅ Doğru! +10 puan 🎉";

    } else {

        document.getElementById("result").innerText =
            "❌ Yanlış! Doğru cevap: " + correct;
    }

    updateScore();

    setTimeout(() => {

        currentQuestion++;

        showQuestion();

    }, 1000);
}

const gameQuestions = [

{
word: "cat",
answers: ["kedi", "köpek", "ev", "araba"],
correct: "kedi"
},

{
word: "book",
answers: ["kalem", "kitap", "masa", "okul"],
correct: "kitap"
},

{
word: "water",
answers: ["su", "süt", "meyve", "ekmek"],
correct: "su"
},

{
word: "school",
answers: ["hastane", "ev", "okul", "market"],
correct: "okul"
},

{
word: "friend",
answers: ["arkadaş", "öğretmen", "doktor", "komşu"],
correct: "arkadaş"
}

];

let currentGame;

function newGameQuestion() {

    currentGame =
        gameQuestions[Math.floor(Math.random() * gameQuestions.length)];

    document.getElementById("gameWord").innerText =
        currentGame.word;

    document.getElementById("gameResult").innerText = "";

    let area =
        document.getElementById("gameAnswers");

    area.innerHTML = "";

    currentGame.answers.forEach(answer => {

        let button =
            document.createElement("button");

        button.innerText = answer;

        button.onclick = function() {

            if (answer === currentGame.correct) {

                gamePoints += 10;

                document.getElementById("gameResult").innerText =
                    "🎉 Doğru! +10 puan!";

            } else {

                document.getElementById("gameResult").innerText =
                    "❌ Yanlış!";

            }

            updateScore();

            setTimeout(newGameQuestion, 900);
        };

        area.appendChild(button);
    });
}

updateScore();

</script>

</body>
</html>
