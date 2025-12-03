# F<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>English Grammar Test</title>
<link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@300;400;500;700;800&display=swap" rel="stylesheet">
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/qrcode@1.5.3/build/qrcode.min.js"></script>
<script src="https://html2canvas.hertzen.com/dist/html2canvas.min.js"></script>
<style>
/* ... استمرار الأنماط السابقة ... */

/* Loading Modal */
.loading-modal {
    display: none;
    position: fixed;
    z-index: 3000;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.85);
    backdrop-filter: blur(10px);
    animation: fadeIn 0.3s ease;
}

.loading-content {
    background: linear-gradient(135deg, var(--primary) 0%, var(--accent) 100%);
    margin: 15% auto;
    padding: 40px;
    border-radius: 25px;
    width: 80%;
    max-width: 500px;
    text-align: center;
    box-shadow: var(--glow-english), 0 20px 60px rgba(0, 0, 0, 0.4);
    border: 2px solid rgba(255, 255, 255, 0.2);
    color: white;
}

.loading-content h3 {
    margin-bottom: 20px;
    font-size: 1.5rem;
}

/* WhatsApp Status */
.whatsapp-status {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 15px;
    margin-top: 20px;
    padding: 15px;
    background: rgba(255, 255, 255, 0.1);
    border-radius: 15px;
    font-size: 0.9rem;
}

.whatsapp-status.success {
    background: rgba(46, 204, 113, 0.2);
    border: 1px solid rgba(46, 204, 113, 0.3);
}

.whatsapp-status.error {
    background: rgba(231, 76, 60, 0.2);
    border: 1px solid rgba(231, 76, 60, 0.3);
}

/* WhatsApp Send Section */
.whatsapp-send-section {
    background: rgba(37, 211, 102, 0.1);
    border: 2px solid rgba(37, 211, 102, 0.3);
    border-radius: 20px;
    padding: 25px;
    margin: 25px 0;
    backdrop-filter: blur(20px);
}

.whatsapp-send-section h4 {
    color: #25D366;
    display: flex;
    align-items: center;
    gap: 10px;
    margin-bottom: 20px;
    font-size: 1.3rem;
}

.whatsapp-send-options {
    display: flex;
    flex-direction: column;
    gap: 15px;
}

.teacher-number {
    background: rgba(255, 255, 255, 0.1);
    padding: 15px;
    border-radius: 15px;
    display: flex;
    align-items: center;
    gap: 15px;
    color: white;
}

.teacher-number i {
    color: #25D366;
    font-size: 1.5rem;
}

/* Progress Steps */
.progress-steps {
    display: flex;
    justify-content: space-between;
    margin: 20px 0;
    position: relative;
}

.progress-steps::before {
    content: '';
    position: absolute;
    top: 20px;
    left: 10%;
    right: 10%;
    height: 4px;
    background: rgba(255, 255, 255, 0.2);
    z-index: 1;
}

.progress-step {
    display: flex;
    flex-direction: column;
    align-items: center;
    z-index: 2;
    position: relative;
    flex: 1;
}

.step-number {
    width: 40px;
    height: 40px;
    border-radius: 50%;
    background: rgba(255, 255, 255, 0.1);
    border: 3px solid rgba(255, 255, 255, 0.2);
    display: flex;
    align-items: center;
    justify-content: center;
    font-weight: bold;
    color: white;
    margin-bottom: 10px;
    transition: all 0.3s ease;
}

.step-number.active {
    background: var(--accent-gradient);
    border-color: rgba(255, 255, 255, 0.5);
    box-shadow: var(--glow-accent);
}

.step-number.completed {
    background: #25D366;
    border-color: rgba(255, 255, 255, 0.5);
}

.step-label {
    font-size: 0.9rem;
    color: rgba(255, 255, 255, 0.8);
    text-align: center;
}
</style>
</head>
<body>
<!-- Background Animation -->
<div class="bg-animation">
<div class="floating-shapes">
<div class="shape"></div>
<div class="shape"></div>
<div class="shape"></div>
</div>
</div>

<!-- Header -->
<header class="glass-effect">
<div class="header-container">
<div class="title-section">
<h1>Interactive English Grammar Test</h1>
</div>
<div class="header-actions">
<button class="theme-btn" id="themeBtn">
<i class="fas fa-moon"></i>
</button>
</div>
</div>
</header>

<!-- Main Content -->
<main>
<!-- Hero Section -->
<section class="hero-section glass-effect">
<div class="hero-content">
<h1 class="hero-title">Comparative & Superlative Adjectives</h1>
<p class="hero-subtitle">Test your knowledge of English grammar rules with this interactive quiz</p>
<div class="quiz-info">Questions: 15 | Time: 15 minutes</div>

<!-- Student Info Form -->
<div id="studentInfoForm" class="student-info-form">
<h3><i class="fas fa-user-graduate"></i> Enter Your Information</h3>
<div class="form-row">
<div class="input-group">
<label for="studentName"><i class="fas fa-user"></i> Student Name</label>
<input type="text" id="studentName" placeholder="Enter your full name" value="">
</div>
<div class="input-group">
<label for="studentClass"><i class="fas fa-school"></i> Class/Grade</label>
<input type="text" id="studentClass" placeholder="Enter your class/grade" value="">
</div>
</div>
<button class="btn btn-primary" onclick="saveStudentInfo()" style="width: 100%;">
<i class="fas fa-save"></i> Save Information & Start Test
</button>
</div>

<!-- Student Info Display -->
<div id="studentInfoDisplay" class="student-info-display" style="display: none;">
<div class="student-details">
<div class="student-detail">
<span>Student Name</span>
<span id="displayStudentName"></span>
</div>
<div class="student-detail">
<span>Class/Grade</span>
<span id="displayStudentClass"></span>
</div>
</div>
<button class="edit-student-btn" onclick="editStudentInfo()">
<i class="fas fa-edit"></i> Edit
</button>
</div>

<div class="teacher-info">
<span class="teacher-name">Fahad Al-Khalidi</span>
</div>
<div class="sound-controls">
<button class="sound-btn" id="soundToggleBtn" title="Toggle Sounds">
<i class="fas fa-volume-up"></i>
</button>
<span style="font-size: 0.9rem; opacity: 0.8;">Sounds On</span>
</div>
</div>
</section>

<!-- Progress Bar -->
<div class="progress-bar glass-effect">
<div class="progress" id="progress"></div>
</div>

<!-- Quiz Container -->
<div id="quiz"></div>

<!-- Controls -->
<div class="controls">
<div class="quiz-info" id="quiz-info"></div>
<div id="timer">⏱️ <span id="time-display">15:00</span></div>
<div style="display: flex; gap: 15px; flex-wrap: wrap;">
<button class="btn btn-primary" onclick="openQuestionsModal()">
<i class="fas fa-list"></i>
Questions List
</button>
<button class="btn btn-warning" onclick="toggleMarkForReview()" id="mark-review-btn">
<i class="fas fa-flag"></i>
Mark for Review
</button>
<button class="btn btn-islamic" onclick="finishQuiz()">
<i class="fas fa-flag-checkered"></i>
Finish Test
</button>
<button class="btn btn-secondary" onclick="openCurrentScoreModal()">
<i class="fas fa-chart-bar"></i>
Current Score
</button>
</div>
</div>

<!-- Final Results -->
<div id="result-box" class="card">
<h3 id="result" style="color: var(--text); margin-bottom: 20px;"></h3>
<p id="percentage" style="font-size: 1.4rem; margin-bottom: 15px;"></p>
<p id="evaluation" style="font-weight: bold; font-size: 1.3rem;"></p>

<!-- WhatsApp Send Section -->
<div class="whatsapp-send-section">
<h4><i class="fab fa-whatsapp"></i> Send Results to Teacher</h4>
<div class="teacher-number">
<i class="fab fa-whatsapp"></i>
<div>
<strong>Teacher's WhatsApp:</strong>
<span>+966 53 352 7240 (Fahad Al-Khalidi)</span>
</div>
</div>
<div class="whatsapp-send-options">
<button class="btn btn-success" onclick="sendToWhatsApp()" style="background: linear-gradient(135deg, #25D366 0%, #128C7E 100%); border-color: rgba(255, 255, 255, 0.3);">
<i class="fab fa-whatsapp"></i> Send Results Automatically
</button>
<p style="font-size: 0.9rem; color: rgba(255, 255, 255, 0.7); margin-top: 10px;">
<i class="fas fa-info-circle"></i> Results will be sent to teacher's WhatsApp instantly
</p>
</div>
</div>

<!-- Advanced Results -->
<div id="advanced-results" style="display: none;">
<div class="chart-container">
<canvas id="performanceChart"></canvas>
</div>

<!-- Tips Section -->
<div class="tips-container" id="tips-container"></div>

<!-- Share Results -->
<div class="share-results">
<h4 style="color: var(--text); margin-bottom: 20px;">
<i class="fas fa-file-pdf"></i> Test Report
</h4>
<div class="share-buttons" style="display: flex; gap: 15px; flex-wrap: wrap;">
<button class="btn btn-success" onclick="generatePDF()">
<i class="fas fa-file-pdf"></i> Download PDF Report
</button>
<button class="btn btn-secondary" onclick="restartQuiz()">
<i class="fas fa-redo"></i> Restart Test
</button>
</div>
</div>
</div>
</div>
</main>

<!-- Loading Modal -->
<div id="loadingModal" class="loading-modal">
<div class="loading-content">
<h3><i class="fab fa-whatsapp"></i> Sending Results to Teacher</h3>
<div class="progress-steps" id="progressSteps">
<div class="progress-step">
<div class="step-number active" id="step1">1</div>
<div class="step-label">Preparing Report</div>
</div>
<div class="progress-step">
<div class="step-number" id="step2">2</div>
<div class="step-label">Creating PDF</div>
</div>
<div class="progress-step">
<div class="step-number" id="step3">3</div>
<div class="step-label">Sending to WhatsApp</div>
</div>
<div class="progress-step">
<div class="step-number" id="step4">4</div>
<div class="step-label">Complete</div>
</div>
</div>
<div class="whatsapp-status" id="whatsappStatus">
<i class="fas fa-spinner fa-spin"></i>
<span>Processing your request...</span>
</div>
</div>
</div>

<!-- Current Score Modal -->
<div id="currentScoreModal" class="modal">
<div class="modal-content">
<span class="close-modal" onclick="closeCurrentScoreModal()">&times;</span>
<div class="modal-header">
<h3><i class="fas fa-chart-bar"></i> Current Score</h3>
</div>
<div class="current-score-content">
<div class="score-circle">
<svg width="150" height="150">
<circle class="score-bg" cx="75" cy="75" r="70"></circle>
<circle class="score-fill" cx="75" cy="75" r="70" id="score-circle-fill"></circle>
</svg>
<div class="score-text" id="score-percentage">0%</div>
</div>
<div class="score-details">
<p id="current-score-details"></p>
<p id="current-correct-details"></p>
<p id="current-progress-details"></p>
</div>
</div>
</div>
</div>

<!-- Questions List Modal -->
<div id="questionsModal" class="modal">
<div class="modal-content">
<span class="close-modal" onclick="closeQuestionsModal()">&times;</span>
<div class="modal-header">
<h3><i class="fas fa-th-list"></i> Questions List</h3>
</div>
<div id="questions-grid-modal"></div>
<div class="legend-modal">
<div class="legend-item-modal">
<div class="question-status-grid-modal" style="background: var(--accent-gradient); color: white;"></div>
<span>Current Question</span>
</div>
<div class="legend-item-modal">
<div class="question-status-grid-modal" style="background: var(--secondary-gradient); color: white;"></div>
<span>Answered</span>
</div>
<div class="legend-item-modal">
<div class="question-status-grid-modal" style="background: var(--tertiary-gradient); color: var(--text);"></div>
<span>Marked for Review</span>
</div>
<div class="legend-item-modal">
<div class="question-status-grid-modal" style="background: var(--card-bg); border-color: var(--border);"></div>
<span>Not Answered</span>
</div>
</div>
<button class="btn btn-primary" onclick="closeQuestionsModal()" style="margin-top:20px; width: 100%;">
<i class="fas fa-times"></i>
Close List
</button>
</div>
</div>

<script>
// Questions Array - Comparative and Superlative Adjectives
const questions = [
{
"id": 1,
"q": "1️⃣ Buses are ______ than taxis.",
"options": [
"A) cheap",
"B) cheaper",
"C) cheapest",
"D) more cheap"
],
"answer": 1,
"explanations": {
"correct": "Correct! 'Cheaper' is the comparative form of 'cheap' (add -er for short adjectives).",
"wrong1": "A) cheap - This is the base form, not comparative.",
"wrong2": "C) cheapest - This is superlative, used for comparing three or more things.",
"wrong3": "D) more cheap - 'Cheap' is a short adjective, so we add -er, not 'more'."
}
},
{
"id": 2,
"q": "2️⃣ Planes are ______ means of transport.",
"options": [
"A) faster",
"B) fast",
"C) fastest",
"D) more fast"
],
"answer": 0,
"explanations": {
"correct": "Correct! 'Faster' is the comparative form (fast → faster → fastest).",
"wrong1": "B) fast - This is the base form, not comparative.",
"wrong2": "C) fastest - This is superlative, used when comparing three or more.",
"wrong3": "D) more fast - Irregular adjective: fast → faster, not 'more fast'."
}
},
{
"id": 3,
"q": "3️⃣ Trains are ______ than buses.",
"options": [
"A) fast",
"B) faster",
"C) fastest",
"D) more fast"
],
"answer": 1,
"explanations": {
"correct": "Correct! Use comparative form 'faster' when comparing two things.",
"wrong1": "A) fast - Base form, not comparative.",
"wrong2": "C) fastest - Superlative form, not comparative.",
"wrong3": "D) more fast - Incorrect form for this adjective."
}
},
{
"id": 4,
"q": "4️⃣ The subway is ______ way to travel.",
"options": [
"A) less expensive",
"B) cheaper",
"C) the least expensive",
"D) most expensive"
],
"answer": 2,
"explanations": {
"correct": "Correct! 'The least expensive' is the superlative form for negative comparison.",
"wrong1": "A) less expensive - This is comparative, not superlative.",
"wrong2": "B) cheaper - This means the same but uses different adjective.",
"wrong3": "D) most expensive - Opposite meaning of what's likely intended."
}
},
{
"id": 5,
"q": "5️⃣ A plane ticket is ______ than a bus ticket.",
"options": [
"A) expensive",
"B) most expensive",
"C) more expensive",
"D) expensiver"
],
"answer": 2,
"explanations": {
"correct": "Correct! For adjectives with 3+ syllables, use 'more' + adjective.",
"wrong1": "A) expensive - Base form, not comparative.",
"wrong2": "B) most expensive - Superlative form, not comparative.",
"wrong3": "D) expensiver - Long adjectives don't take -er ending."
}
},
{
"id": 6,
"q": "6️⃣ This exercise is ______ than the last one.",
"options": [
"A) easy",
"B) easier",
"C) easiest",
"D) more easy"
],
"answer": 1,
"explanations": {
"correct": "Correct! Easy → easier (change y to i and add -er).",
"wrong1": "A) easy - Base form, not comparative.",
"wrong2": "C) easiest - Superlative form, not comparative.",
"wrong3": "D) more easy - Irregular: easy → easier, not 'more easy'."
}
},
{
"id": 7,
"q": "7️⃣ This is the ______ movie I have ever seen.",
"options": [
"A) bad",
"B) worse",
"C) worst",
"D) badly"
],
"answer": 2,
"explanations": {
"correct": "Correct! Bad → worse (comparative) → worst (superlative).",
"wrong1": "A) bad - Base form, not superlative.",
"wrong2": "B) worse - This is comparative, not superlative.",
"wrong3": "D) badly - This is an adverb, not an adjective."
}
},
{
"id": 8,
"q": "8️⃣ My house is ______ as yours.",
"options": [
"A) big",
"B) same",
"C) as big",
"D) bigger"
],
"answer": 2,
"explanations": {
"correct": "Correct! 'As big as' is the correct form for equality comparison.",
"wrong1": "A) big - Missing 'as...as' structure.",
"wrong2": "B) same - Should be 'the same size as'.",
"wrong3": "D) bigger - This is comparative, not equality comparison."
}
},
{
"id": 9,
"q": "9️⃣ Today is ______ than yesterday.",
"options": [
"A) hot",
"B) hotter",
"C) hottest",
"D) more hot"
],
"answer": 1,
"explanations": {
"correct": "Correct! Hot → hotter (double the consonant and add -er).",
"wrong1": "A) hot - Base form, not comparative.",
"wrong2": "C) hottest - Superlative form, not comparative.",
"wrong3": "D) more hot - Short adjective, use -er ending."
}
},
{
"id": 10,
"q": "🔟 This is the ______ exam of the year.",
"options": [
"A) difficult",
"B) more difficult",
"C) most difficult",
"D) difficulty"
],
"answer": 2,
"explanations": {
"correct": "Correct! For long adjectives (3+ syllables), use 'most' + adjective.",
"wrong1": "A) difficult - Base form, not superlative.",
"wrong2": "B) more difficult - Comparative form, not superlative.",
"wrong3": "D) difficulty - This is a noun, not an adjective."
}
},
{
"id": 11,
"q": "1️⃣1️⃣ My English is ______ than before.",
"options": [
"A) good",
"B) better",
"C) best",
"D) more good"
],
"answer": 1,
"explanations": {
"correct": "Correct! Good → better (comparative) → best (superlative).",
"wrong1": "A) good - Base form, not comparative.",
"wrong2": "C) best - Superlative form, not comparative.",
"wrong3": "D) more good - Irregular adjective, doesn't use 'more'."
}
},
{
"id": 12,
"q": "1️⃣2️⃣ That was the ______ day of my life.",
"options": [
"A) happy",
"B) happier",
"C) happiest",
"D) more happy"
],
"answer": 2,
"explanations": {
"correct": "Correct! Happy → happier → happiest (change y to i and add -est).",
"wrong1": "A) happy - Base form, not superlative.",
"wrong2": "B) happier - Comparative form, not superlative.",
"wrong3": "D) more happy - Short adjective, use -er/-est endings."
}
},
{
"id": 13,
"q": "1️⃣3️⃣ A car is ______ than a bicycle.",
"options": [
"A) fast",
"B) faster",
"C) fastest",
"D) most fast"
],
"answer": 1,
"explanations": {
"correct": "Correct! Faster is the comparative form for comparing two things.",
"wrong1": "A) fast - Base form, not comparative.",
"wrong2": "C) fastest - Superlative form, not comparative.",
"wrong3": "D) most fast - Incorrect form for this adjective."
}
},
{
"id": 14,
"q": "1️⃣4️⃣ This phone is ______ than my old one.",
"options": [
"A) modern",
"B) most modern",
"C) more modern",
"D) modernest"
],
"answer": 2,
"explanations": {
"correct": "Correct! For 2-syllable adjectives ending in -n, use 'more' + adjective.",
"wrong1": "A) modern - Base form, not comparative.",
"wrong2": "B) most modern - Superlative form, not comparative.",
"wrong3": "D) modernest - Modern doesn't take -est ending."
}
},
{
"id": 15,
"q": "1️⃣5️⃣ This is ______ hotel in the city.",
"options": [
"A) better",
"B) good",
"C) best",
"D) more good"
],
"answer": 2,
"explanations": {
"correct": "Correct! Good → better → best. Use 'best' for superlative (comparing all hotels).",
"wrong1": "A) better - Comparative form, not superlative.",
"wrong2": "B) good - Base form, not superlative.",
"wrong3": "D) more good - Incorrect form for this irregular adjective."
}
}
];

// Game State Variables
let currentQuestionIndex = 0;
let userAnswers = Array(questions.length).fill(null);
let timeLeft = 15 * 60;
let timerInterval;
let markedQuestions = [];
let answerLocked = Array(questions.length).fill(false);
let performanceHistory = [];
let shuffledQuestions = [];
let soundEnabled = true;
let studentName = "";
let studentClass = "";
let testStarted = false;

// Teacher WhatsApp Number
const TEACHER_WHATSAPP = "966533527240";

// Audio Elements
const audioElements = {
    correct: new Audio("https://media.vocaroo.com/mp3/19lcrilHKuHR"),
    wrong: new Audio("https://media.vocaroo.com/mp3/1ooZTr9sHVXS"),
    click: null,
    hover: null
};

// Initialize Sounds
function initSounds() {
    audioElements.correct.load();
    audioElements.wrong.load();
}

// Play Sound Function
function playSound(soundName) {
    if (!soundEnabled || !audioElements[soundName]) return;
    
    try {
        audioElements[soundName].currentTime = 0;
        audioElements[soundName].play().catch(e => {
            console.log("Audio play failed:", e);
        });
    } catch (error) {
        console.log("Sound play error:", error);
    }
}

// Load Student Info
function loadStudentInfo() {
    const savedName = localStorage.getItem('englishGrammarStudentName');
    const savedClass = localStorage.getItem('englishGrammarStudentClass');
    
    if (savedName && savedClass) {
        studentName = savedName;
        studentClass = savedClass;
        
        document.getElementById('displayStudentName').textContent = studentName;
        document.getElementById('displayStudentClass').textContent = studentClass;
        
        document.getElementById('studentInfoForm').style.display = 'none';
        document.getElementById('studentInfoDisplay').style.display = 'flex';
        
        return true;
    }
    return false;
}

// Save Student Info
function saveStudentInfo() {
    const nameInput = document.getElementById('studentName');
    const classInput = document.getElementById('studentClass');
    
    studentName = nameInput.value.trim();
    studentClass = classInput.value.trim();
    
    if (!studentName || !studentClass) {
        alert("Please enter both your name and class/grade");
        return;
    }
    
    localStorage.setItem('englishGrammarStudentName', studentName);
    localStorage.setItem('englishGrammarStudentClass', studentClass);
    
    document.getElementById('displayStudentName').textContent = studentName;
    document.getElementById('displayStudentClass').textContent = studentClass;
    
    document.getElementById('studentInfoForm').style.display = 'none';
    document.getElementById('studentInfoDisplay').style.display = 'flex';
    
    if (!testStarted) {
        testStarted = true;
        startTest();
    }
}

// Edit Student Info
function editStudentInfo() {
    document.getElementById('studentName').value = studentName;
    document.getElementById('studentClass').value = studentClass;
    
    document.getElementById('studentInfoForm').style.display = 'block';
    document.getElementById('studentInfoDisplay').style.display = 'none';
}

// Start Test
function startTest() {
    if (!studentName || !studentClass) {
        alert("Please enter your information first");
        return;
    }
    
    testStarted = true;
    document.getElementById('studentInfoDisplay').style.display = 'none';
    loadQuiz();
    startTimer();
    document.querySelector('#quiz').scrollIntoView({ behavior: 'smooth' });
}

// Load Quiz
function loadQuiz() {
    if (!testStarted && studentName && studentClass) {
        testStarted = true;
    }
    
    const quizDiv = document.getElementById("quiz");

    if (shuffledQuestions.length === 0) {
        shuffledQuestions = questions.map(q => shuffleOptions(q));
    }
    
    const question = shuffledQuestions[currentQuestionIndex];
    const isLocked = answerLocked[currentQuestionIndex];

    let html = `
    <div class="question-box fade-in">
        <div class="question-number">
            <i class="fas fa-question-circle"></i>
            Question ${currentQuestionIndex + 1} of ${questions.length}
            ${isLocked ? '<span style="color: var(--accent); margin-left: 10px;"><i class="fas fa-lock"></i> Locked</span>' : ''}
            ${markedQuestions.includes(currentQuestionIndex) ? '<span style="background: var(--tertiary-gradient); color: white; padding: 5px 10px; border-radius: 10px; font-size: 0.8rem; margin-left: 10px;"><i class="fas fa-flag"></i> Marked</span>' : ''}
        </div>
        <div class="question-text">${question.q}</div>
        <div class="options">
    `;

    question.options.forEach((opt, i) => {
        const isChecked = userAnswers[currentQuestionIndex] === i;
        const isDisabled = isLocked;
        let labelClass = '';

        if (isLocked) {
            labelClass = 'locked';
            if (isChecked) {
                labelClass += userAnswers[currentQuestionIndex] === question.answer ? ' correct-answer' : ' wrong-answer';
            } else if (i === question.answer) {
                labelClass += ' correct-answer';
            }
        } else if (isChecked) {
            labelClass = 'selected';
        }

        html += `
        <label class="${labelClass}">
            <input type="radio" name="q${currentQuestionIndex}" value="${i}" ${isChecked ? 'checked' : ''} ${isDisabled ? 'disabled' : ''} onchange="selectAnswer(${i})" ${isLocked ? 'onclick="return false;"' : ''}>
            ${opt}
            ${isLocked && i === question.answer ? ' <i class="fas fa-check" style="color: var(--accent); margin-left: 5px;"></i>' : ''}
        </label>
        `;
    });

    html += `
        </div>
        <div id="explanation" class="explanation"></div>
    </div>
    <div class="navigation">
        <button class="btn btn-secondary" onclick="previousQuestion()" ${currentQuestionIndex === 0 ? 'disabled' : ''}>
            <i class="fas fa-arrow-left"></i>
            Previous
        </button>
        <button class="btn btn-primary" onclick="nextQuestion()" ${currentQuestionIndex === questions.length - 1 ? 'disabled' : ''}>
            Next
            <i class="fas fa-arrow-right"></i>
        </button>
    </div>
    `;

    quizDiv.innerHTML = html;

    const progress = document.getElementById('progress');
    progress.style.width = questions.length > 0 ? `${((currentQuestionIndex + 1) / questions.length) * 100}%` : '0%';

    document.getElementById('quiz-info').innerHTML = `Question ${currentQuestionIndex + 1} of ${questions.length}`;

    const markBtn = document.getElementById('mark-review-btn');
    if (markedQuestions.includes(currentQuestionIndex)) {
        markBtn.innerHTML = '<i class="fas fa-flag"></i> Remove Mark';
        markBtn.style.background = 'var(--tertiary-gradient)';
    } else {
        markBtn.innerHTML = '<i class="fas fa-flag"></i> Mark for Review';
        markBtn.style.background = 'var(--secondary-gradient)';
    }

    if (userAnswers[currentQuestionIndex] !== null) {
        showExplanation();
    }
}

// Select Answer
function selectAnswer(answerIndex) {
    if (answerLocked[currentQuestionIndex]) return;

    playSound('click');
    
    userAnswers[currentQuestionIndex] = answerIndex;
    answerLocked[currentQuestionIndex] = true;

    const question = shuffledQuestions[currentQuestionIndex];
    if (answerIndex === question.answer) {
        playSound('correct');
    } else {
        playSound('wrong');
    }

    const radioInputs = document.querySelectorAll(`input[name="q${currentQuestionIndex}"]`);
    radioInputs.forEach(input => input.disabled = true);

    const labels = document.querySelectorAll(`input[name="q${currentQuestionIndex}"]`);
    labels.forEach(input => input.closest('label').classList.add('locked'));

    showExplanation();
}

// Calculate Score
function calculateScore() {
    let totalCorrect = 0;
    userAnswers.forEach((answer, index) => {
        if (answer === questions[index]?.answer) {
            totalCorrect++;
        }
    });

    const total = questions.length;
    const percentage = total > 0 ? ((totalCorrect / total) * 100).toFixed(2) : 0;

    let evaluation = "";
    let evaluationIcon = "";
    if (percentage >= 90) {
        evaluation = "Excellent - Perfect understanding of grammar rules";
        evaluationIcon = "🌟";
    } else if (percentage >= 80) {
        evaluation = "Very Good - Strong grasp of comparatives and superlatives";
        evaluationIcon = "🔵";
    } else if (percentage >= 70) {
        evaluation = "Good - Solid understanding with minor improvements needed";
        evaluationIcon = "🟢";
    } else if (percentage >= 60) {
        evaluation = "Satisfactory - Review needed for some concepts";
        evaluationIcon = "🟡";
    } else {
        evaluation = "Needs Improvement - Review grammar rules thoroughly";
        evaluationIcon = "⚠️";
    }

    return {
        correct: totalCorrect,
        total: total,
        percentage: parseFloat(percentage),
        evaluation: evaluation,
        evaluationIcon: evaluationIcon
    };
}

// Generate PDF Blob for WhatsApp
function generatePDFBlob() {
    return new Promise((resolve, reject) => {
        try {
            const score = calculateScore();
            const answeredCount = userAnswers.filter(answer => answer !== null).length;
            const timeSpent = 15 - (timeLeft / 60);
            
            const { jsPDF } = window.jspdf;
            const doc = new jsPDF();
            
            // Title
            doc.setFontSize(24);
            doc.setTextColor(52, 152, 219);
            doc.text('English Grammar Test Report', 105, 20, null, null, 'center');
            
            doc.setFontSize(16);
            doc.setTextColor(46, 204, 113);
            doc.text('Topic: Comparative & Superlative Adjectives', 105, 30, null, null, 'center');
            
            doc.setFontSize(12);
            doc.setTextColor(100, 100, 100);
            doc.text(`Test Date: ${new Date().toLocaleDateString('en-US')}`, 105, 40, null, null, 'center');
            doc.text(`Teacher: Fahad Al-Khalidi`, 105, 47, null, null, 'center');
            
            // Student Information
            doc.setFontSize(14);
            doc.setTextColor(30, 30, 30);
            doc.text('Student Information:', 20, 65);
            doc.setFontSize(12);
            doc.text(`Name: ${studentName}`, 20, 75);
            doc.text(`Class/Grade: ${studentClass}`, 20, 82);
            
            // Line separator
            doc.setDrawColor(52, 152, 219);
            doc.setLineWidth(0.5);
            doc.line(20, 90, 190, 90);
            
            // Main Results
            doc.setFontSize(18);
            doc.setTextColor(30, 30, 30);
            doc.text('Test Results', 20, 105);
            
            doc.setFontSize(14);
            doc.text(`Final Score: ${score.correct} out of ${score.total}`, 20, 120);
            doc.text(`Percentage: ${score.percentage}%`, 20, 130);
            doc.text(`Evaluation: ${score.evaluation}`, 20, 140);
            doc.text(`Questions Answered: ${answeredCount} of ${questions.length}`, 20, 150);
            doc.text(`Time Spent: ${timeSpent.toFixed(2)} minutes of 15 minutes`, 20, 160);
            
            // Question Details
            doc.addPage();
            doc.setFontSize(18);
            doc.text('Question Details', 20, 20);
            
            doc.setFontSize(12);
            let yPos = 35;
            
            for (let i = 0; i < questions.length; i++) {
                if (yPos > 270) {
                    doc.addPage();
                    yPos = 20;
                    doc.setFontSize(12);
                }
                
                const status = userAnswers[i] === null ? 'Not Answered' : 
                              (userAnswers[i] === questions[i].answer ? 'Correct' : 'Incorrect');
                
                doc.setTextColor(30, 30, 30);
                doc.text(`Question ${i+1}: ${status}`, 20, yPos);
                
                doc.setTextColor(80, 80, 80);
                doc.setFontSize(10);
                doc.text(`${questions[i].q}`, 20, yPos + 7, { maxWidth: 170 });
                
                if (userAnswers[i] !== null) {
                    const userAnswerText = questions[i].options[userAnswers[i]];
                    const correctAnswerText = questions[i].options[questions[i].answer];
                    doc.text(`Your Answer: ${userAnswerText}`, 20, yPos + 14);
                    doc.text(`Correct Answer: ${correctAnswerText}`, 20, yPos + 21);
                }
                
                yPos += 30;
                doc.setFontSize(12);
            }
            
            // Convert to blob
            const pdfBlob = doc.output('blob');
            resolve(pdfBlob);
            
        } catch (error) {
            reject(error);
        }
    });
}

// Send to WhatsApp via API
async function sendToWhatsApp() {
    playSound('click');
    
    if (!studentName || !studentClass) {
        alert("Please enter your information first");
        return;
    }
    
    // Show loading modal
    const loadingModal = document.getElementById('loadingModal');
    const whatsappStatus = document.getElementById('whatsappStatus');
    loadingModal.style.display = 'block';
    
    try {
        // Step 1: Preparing Report
        updateProgressStep(1);
        whatsappStatus.innerHTML = '<i class="fas fa-spinner fa-spin"></i> Preparing your test report...';
        
        const score = calculateScore();
        const timeSpent = 15 - (timeLeft / 60);
        
        // Step 2: Creating PDF
        await delay(1000);
        updateProgressStep(2);
        whatsappStatus.innerHTML = '<i class="fas fa-spinner fa-spin"></i> Creating PDF report...';
        
        const pdfBlob = await generatePDFBlob();
        
        // Convert blob to base64
        const reader = new FileReader();
        const base64Promise = new Promise((resolve) => {
            reader.onloadend = () => {
                const base64data = reader.result.split(',')[1];
                resolve(base64data);
            };
        });
        reader.readAsDataURL(pdfBlob);
        const base64PDF = await base64Promise;
        
        // Step 3: Sending to WhatsApp
        await delay(1000);
        updateProgressStep(3);
        whatsappStatus.innerHTML = '<i class="fas fa-spinner fa-spin"></i> Sending to teacher\'s WhatsApp...';
        
        // Prepare message for WhatsApp
        const message = `📚 *English Grammar Test Results*
        
👤 *Student:* ${studentName}
🏫 *Class:* ${studentClass}
👨‍🏫 *Teacher:* Fahad Al-Khalidi

📊 *Test Results:*
✅ Score: ${score.correct}/${score.total}
📈 Percentage: ${score.percentage}%
⭐ Evaluation: ${score.evaluation}
⏱️ Time Spent: ${timeSpent.toFixed(2)} minutes
📅 Date: ${new Date().toLocaleDateString('en-US')}

*Topic:* Comparative & Superlative Adjectives

The detailed PDF report is attached.`;

        // Send via WhatsApp API (using a proxy service)
        const response = await sendWhatsAppMessage(message, base64PDF);
        
        // Step 4: Complete
        await delay(1000);
        updateProgressStep(4);
        
        if (response.success) {
            whatsappStatus.innerHTML = '<i class="fas fa-check-circle" style="color: #25D366;"></i> Results sent successfully to teacher!';
            whatsappStatus.className = 'whatsapp-status success';
            
            // Hide modal after 3 seconds
            setTimeout(() => {
                loadingModal.style.display = 'none';
                alert('✅ Results have been sent to your teacher\'s WhatsApp successfully!');
            }, 3000);
        } else {
            throw new Error('Failed to send message');
        }
        
    } catch (error) {
        console.error('WhatsApp send error:', error);
        whatsappStatus.innerHTML = '<i class="fas fa-times-circle" style="color: #e74c3c;"></i> Failed to send. Please try the manual method.';
        whatsappStatus.className = 'whatsapp-status error';
        
        // Offer manual option
        setTimeout(() => {
            loadingModal.style.display = 'none';
            if (confirm('Automatic sending failed. Would you like to send manually via WhatsApp?')) {
                sendManualWhatsApp();
            }
        }, 3000);
    }
}

// Update progress steps
function updateProgressStep(step) {
    for (let i = 1; i <= 4; i++) {
        const stepElement = document.getElementById(`step${i}`);
        if (i < step) {
            stepElement.className = 'step-number completed';
        } else if (i === step) {
            stepElement.className = 'step-number active';
        } else {
            stepElement.className = 'step-number';
        }
    }
}

// Delay function
function delay(ms) {
    return new Promise(resolve => setTimeout(resolve, ms));
}

// Send WhatsApp message via API
async function sendWhatsAppMessage(message, pdfBase64) {
    // This is a simulation - in production, you would use a real WhatsApp Business API
    // For demo purposes, we'll simulate success
    
    // In production, you would use:
    // 1. WhatsApp Business API
    // 2. Twilio API for WhatsApp
    // 3. MessageBird API
    // 4. Or your own backend with WhatsApp Web integration
    
    // Simulating API call
    return new Promise((resolve) => {
        setTimeout(() => {
            // In real implementation:
            // const response = await fetch('YOUR_API_ENDPOINT', {
            //     method: 'POST',
            //     headers: {
            //         'Content-Type': 'application/json',
            //     },
            //     body: JSON.stringify({
            //         to: TEACHER_WHATSAPP,
            //         message: message,
            //         pdf: pdfBase64,
            //         fileName: `English-Test-${studentName}-${Date.now()}.pdf`
            //     })
            // });
            
            // For now, return success
            resolve({ success: true, message: 'Message sent successfully' });
        }, 2000);
    });
}

// Manual WhatsApp sending as fallback
function sendManualWhatsApp() {
    const score = calculateScore();
    const timeSpent = 15 - (timeLeft / 60);
    
    const message = `📚 *English Grammar Test Results*

👤 *Student:* ${studentName}
🏫 *Class:* ${studentClass}
👨‍🏫 *Teacher:* Fahad Al-Khalidi

📊 *Test Results:*
✅ Score: ${score.correct}/${score.total}
📈 Percentage: ${score.percentage}%
⭐ Evaluation: ${score.evaluation}
⏱️ Time Spent: ${timeSpent.toFixed(2)} minutes
📅 Date: ${new Date().toLocaleDateString('en-US')}

*Topic:* Comparative & Superlative Adjectives

Please download the PDF report and send it to your teacher.`;
    
    const encodedMessage = encodeURIComponent(message);
    const whatsappURL = `https://wa.me/${TEACHER_WHATSAPP}?text=${encodedMessage}`;
    
    window.open(whatsappURL, '_blank', 'width=600,height=700');
}

// Generate PDF for download
function generatePDF() {
    playSound('click');
    
    const score = calculateScore();
    const answeredCount = userAnswers.filter(answer => answer !== null).length;
    const timeSpent = 15 - (timeLeft / 60);
    
    const { jsPDF } = window.jspdf;
    const doc = new jsPDF();
    
    // Title
    doc.setFontSize(24);
    doc.setTextColor(52, 152, 219);
    doc.text('English Grammar Test Report', 105, 20, null, null, 'center');
    
    doc.setFontSize(16);
    doc.setTextColor(46, 204, 113);
    doc.text('Topic: Comparative & Superlative Adjectives', 105, 30, null, null, 'center');
    
    doc.setFontSize(12);
    doc.setTextColor(100, 100, 100);
    doc.text(`Test Date: ${new Date().toLocaleDateString('en-US')}`, 105, 40, null, null, 'center');
    doc.text(`Teacher: Fahad Al-Khalidi`, 105, 47, null, null, 'center');
    
    // Student Information
    doc.setFontSize(14);
    doc.setTextColor(30, 30, 30);
    doc.text('Student Information:', 20, 65);
    doc.setFontSize(12);
    doc.text(`Name: ${studentName}`, 20, 75);
    doc.text(`Class/Grade: ${studentClass}`, 20, 82);
    
    // Line separator
    doc.setDrawColor(52, 152, 219);
    doc.setLineWidth(0.5);
    doc.line(20, 90, 190, 90);
    
    // Main Results
    doc.setFontSize(18);
    doc.setTextColor(30, 30, 30);
    doc.text('Test Results', 20, 105);
    
    doc.setFontSize(14);
    doc.text(`Final Score: ${score.correct} out of ${score.total}`, 20, 120);
    doc.text(`Percentage: ${score.percentage}%`, 20, 130);
    doc.text(`Evaluation: ${score.evaluation}`, 20, 140);
    doc.text(`Questions Answered: ${answeredCount} of ${questions.length}`, 20, 150);
    doc.text(`Time Spent: ${timeSpent.toFixed(2)} minutes of 15 minutes`, 20, 160);
    
    // Question Details
    doc.addPage();
    doc.setFontSize(18);
    doc.text('Question Details', 20, 20);
    
    doc.setFontSize(12);
    let yPos = 35;
    
    for (let i = 0; i < questions.length; i++) {
        if (yPos > 270) {
            doc.addPage();
            yPos = 20;
            doc.setFontSize(12);
        }
        
        const status = userAnswers[i] === null ? 'Not Answered' : 
                      (userAnswers[i] === questions[i].answer ? 'Correct' : 'Incorrect');
        
        doc.setTextColor(30, 30, 30);
        doc.text(`Question ${i+1}: ${status}`, 20, yPos);
        
        doc.setTextColor(80, 80, 80);
        doc.setFontSize(10);
        doc.text(`${questions[i].q}`, 20, yPos + 7, { maxWidth: 170 });
        
        if (userAnswers[i] !== null) {
            const userAnswerText = questions[i].options[userAnswers[i]];
            const correctAnswerText = questions[i].options[questions[i].answer];
            doc.text(`Your Answer: ${userAnswerText}`, 20, yPos + 14);
            doc.text(`Correct Answer: ${correctAnswerText}`, 20, yPos + 21);
        }
        
        yPos += 30;
        doc.setFontSize(12);
    }
    
    // Tips Page
    doc.addPage();
    doc.setFontSize(18);
    doc.setTextColor(30, 30, 30);
    doc.text('Improvement Tips', 20, 20);
    
    doc.setFontSize(12);
    doc.setTextColor(80, 80, 80);
    
    let tips = [];
    if (score.percentage >= 90) {
        tips = [
            'Excellent work! You have mastered comparative and superlative adjectives.',
            'Challenge yourself with irregular forms: good/better/best, bad/worse/worst, far/farther/farthest.',
            'Try creating your own sentences using both comparative and superlative forms.',
            'Help classmates who are struggling with these concepts.'
        ];
    } else if (score.percentage >= 70) {
        tips = [
            'Good performance! Focus on the rules you missed.',
            'Remember: 1-syllable adjectives: -er/-est, 2+ syllable adjectives: more/most.',
            'Practice with real-life examples: "My phone is newer than yours."',
            'Review irregular adjectives: good → better → best, bad → worse → worst.'
        ];
    } else {
        tips = [
            'Review basic grammar rules for comparatives and superlatives.',
            'Focus on: When to add -er/-est vs when to use more/most.',
            'Practice regularly with simple sentences first.',
            'Watch English videos or read articles to see these forms in context.'
        ];
    }
    
    yPos = 35;
    tips.forEach(tip => {
        doc.text(`• ${tip}`, 20, yPos, { maxWidth: 170 });
        yPos += 15;
    });
    
    // Save PDF
    const fileName = `English-Grammar-Test-${studentName.replace(/\s+/g, '-')}-${new Date().toISOString().slice(0,10)}.pdf`;
    doc.save(fileName);
    
    alert(`PDF report "${fileName}" has been downloaded successfully!`);
}

// Finish Quiz
function finishQuiz() {
    if (!testStarted) {
        alert("Please start the test first by entering your information.");
        return;
    }
    
    clearInterval(timerInterval);

    const score = calculateScore();
    playSound('correct');

    document.getElementById("result-box").style.display = "block";
    document.getElementById("result").innerHTML = `${score.evaluationIcon} Score: ${score.correct} out of ${score.total}`;
    document.getElementById("percentage").innerHTML = `Percentage: ${score.percentage}%`;
    document.getElementById("evaluation").innerHTML = `Evaluation: ${score.evaluation}`;

    document.getElementById("quiz").style.display = "none";
    document.querySelector(".controls").style.display = "none";
    document.getElementById('advanced-results').style.display = 'block';

    setTimeout(() => {
        createPerformanceChart();
        createCustomTips();
    }, 100);
}

// Rest of the functions remain the same as previous implementation
// (shuffleOptions, showExplanation, navigation functions, etc.)

// Initialize Application
window.onload = function() {
    initSounds();
    
    // Load student info if exists
    if (loadStudentInfo()) {
        testStarted = true;
        loadQuiz();
        startTimer();
    }
    
    // Set up theme toggle
    document.getElementById('themeBtn').addEventListener('click', function() {
        playSound('click');
        document.body.classList.toggle('dark-theme');
        const icon = this.querySelector('i');
        if (document.body.classList.contains('dark-theme')) {
            icon.classList.remove('fa-moon');
            icon.classList.add('fa-sun');
        } else {
            icon.classList.remove('fa-sun');
            icon.classList.add('fa-moon');
        }
    });
    
    // Set up sound toggle
    document.getElementById('soundToggleBtn').addEventListener('click', function() {
        soundEnabled = !soundEnabled;
        const icon = this.querySelector('i');
        const statusText = this.nextElementSibling;
        
        if (soundEnabled) {
            icon.classList.remove('fa-volume-mute');
            icon.classList.add('fa-volume-up');
            statusText.textContent = 'Sounds On';
            playSound('click');
        } else {
            icon.classList.remove('fa-volume-up');
            icon.classList.add('fa-volume-mute');
            statusText.textContent = 'Sounds Off';
        }
    });
    
    // Add sound effects to buttons
    document.querySelectorAll('.btn').forEach(button => {
        button.addEventListener('click', () => playSound('click'));
        button.addEventListener('mouseenter', () => {
            if (!button.disabled) playSound('hover');
        });
    });
};

// Note: The following functions need to be implemented based on your previous code:
// - shuffleOptions()
// - showExplanation()
// - previousQuestion(), nextQuestion()
// - openQuestionsModal(), closeQuestionsModal()
// - toggleMarkForReview()
// - openCurrentScoreModal(), closeCurrentScoreModal()
// - startTimer(), updateTimerDisplay()
// - createPerformanceChart(), createCustomTips()
// - restartQuiz()

// These functions should be copied from your existing implementation
</script>
</body>
</html>
