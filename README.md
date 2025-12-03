<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>اختبار القواعد الإنجليزية - تجربة</title>
    <link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@300;400;500;700;800&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary: #3498db;
            --accent: #2ecc71;
            --secondary: #9b59b6;
            --bg: linear-gradient(135deg, #3498db 0%, #2ecc71 100%);
            --card-bg: rgba(255, 255, 255, 0.95);
            --text: #1F2937;
        }

        * {
            font-family: 'Tajawal', sans-serif;
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: var(--bg);
            color: var(--text);
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 800px;
            margin: 0 auto;
        }

        .card {
            background: var(--card-bg);
            border-radius: 20px;
            padding: 30px;
            margin: 20px 0;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
        }

        h1 {
            text-align: center;
            color: white;
            margin-bottom: 30px;
            font-size: 2.5rem;
        }

        h2 {
            color: var(--primary);
            margin-bottom: 20px;
        }

        .form-group {
            margin-bottom: 20px;
        }

        label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
            color: #333;
        }

        input {
            width: 100%;
            padding: 12px;
            border: 2px solid #ddd;
            border-radius: 10px;
            font-size: 16px;
        }

        .btn {
            background: var(--accent);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 10px;
            font-size: 18px;
            font-weight: bold;
            cursor: pointer;
            width: 100%;
            margin: 10px 0;
            transition: all 0.3s;
        }

        .btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 5px 15px rgba(46, 204, 113, 0.4);
        }

        .btn-primary {
            background: var(--primary);
        }

        .btn-success {
            background: #25D366; /* WhatsApp color */
        }

        .question {
            background: white;
            padding: 20px;
            margin: 15px 0;
            border-radius: 10px;
            border-left: 5px solid var(--primary);
        }

        .options {
            margin-top: 15px;
        }

        .option {
            display: block;
            padding: 12px;
            margin: 8px 0;
            background: #f8f9fa;
            border: 2px solid #dee2e6;
            border-radius: 8px;
            cursor: pointer;
        }

        .option.selected {
            background: #d4edda;
            border-color: var(--accent);
        }

        .option.correct {
            background: #d4edda;
            border-color: var(--accent);
        }

        .option.wrong {
            background: #f8d7da;
            border-color: #dc3545;
        }

        .results {
            text-align: center;
            padding: 30px;
        }

        .score {
            font-size: 48px;
            font-weight: bold;
            color: var(--accent);
            margin: 20px 0;
        }

        .whatsapp-section {
            background: rgba(37, 211, 102, 0.1);
            border: 2px solid rgba(37, 211, 102, 0.3);
            border-radius: 15px;
            padding: 20px;
            margin: 20px 0;
        }

        .teacher-info {
            background: rgba(52, 152, 219, 0.1);
            padding: 15px;
            border-radius: 10px;
            margin: 15px 0;
        }

        .hidden {
            display: none;
        }

        .status {
            padding: 10px;
            border-radius: 5px;
            margin: 10px 0;
            text-align: center;
        }

        .success {
            background: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
        }

        .error {
            background: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
        }

        .loading {
            text-align: center;
            padding: 20px;
        }

        .spinner {
            border: 4px solid #f3f3f3;
            border-top: 4px solid var(--accent);
            border-radius: 50%;
            width: 40px;
            height: 40px;
            animation: spin 1s linear infinite;
            margin: 0 auto;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>📚 اختبار القواعد الإنجليزية</h1>
        
        <!-- Student Info Form -->
        <div id="studentForm" class="card">
            <h2>معلومات الطالب</h2>
            <div class="form-group">
                <label for="studentName">اسم الطالب:</label>
                <input type="text" id="studentName" placeholder="أدخل اسمك الكامل">
            </div>
            <div class="form-group">
                <label for="studentClass">الفصل/الصف:</label>
                <input type="text" id="studentClass" placeholder="أدخل فصلك">
            </div>
            <button class="btn" onclick="startTest()">بدء الاختبار</button>
        </div>

        <!-- Test Section -->
        <div id="testSection" class="hidden">
            <div class="card">
                <div class="teacher-info">
                    <strong>👨‍🏫 المعلم:</strong> فهد الخالدي<br>
                    <strong>📱 الواتساب:</strong> 966533527240
                </div>
                
                <div id="questionsContainer"></div>
                
                <button id="submitBtn" class="btn hidden" onclick="submitTest()">إنهاء الاختبار</button>
            </div>
        </div>

        <!-- Results Section -->
        <div id="resultsSection" class="hidden">
            <div class="card results">
                <h2>📊 نتائج الاختبار</h2>
                <div id="resultsContent"></div>
                
                <div class="whatsapp-section">
                    <h3><i class="fab fa-whatsapp"></i> إرسال النتائج إلى المعلم</h3>
                    <p>سيتم إرسال النتائج تلقائياً إلى واتساب المعلم</p>
                    <button class="btn btn-success" onclick="sendToWhatsApp()">
                        <i class="fab fa-whatsapp"></i> إرسال النتائج الآن
                    </button>
                    <div id="whatsappStatus" class="status hidden"></div>
                </div>
                
                <button class="btn btn-primary" onclick="restartTest()">إعادة الاختبار</button>
            </div>
        </div>

        <!-- Loading Modal -->
        <div id="loadingModal" class="hidden">
            <div class="card loading">
                <h3>جاري إرسال النتائج...</h3>
                <div class="spinner"></div>
                <p id="loadingText">جاري إعداد التقرير وإرساله إلى المعلم</p>
            </div>
        </div>
    </div>

    <script>
        // الأسئلة (سؤالين فقط للاختبار)
        const questions = [
            {
                id: 1,
                question: "1️⃣ Buses are ______ than taxis.",
                options: ["A) cheap", "B) cheaper", "C) cheapest", "D) more cheap"],
                correct: 1,
                explanation: "الإجابة الصحيحة هي 'cheaper' لأنها صيغة المقارنة لـ 'cheap'"
            },
            {
                id: 2,
                question: "2️⃣ This is the ______ movie I have ever seen.",
                options: ["A) bad", "B) worse", "C) worst", "D) badly"],
                correct: 2,
                explanation: "الإجابة الصحيحة هي 'worst' لأنها صيغة التفضيل لـ 'bad'"
            }
        ];

        // بيانات الطالب
        let studentName = '';
        let studentClass = '';
        let userAnswers = [];
        let testStarted = false;

        // بدء الاختبار
        function startTest() {
            studentName = document.getElementById('studentName').value.trim();
            studentClass = document.getElementById('studentClass').value.trim();
            
            if (!studentName || !studentClass) {
                alert('الرجاء إدخال الاسم والفصل');
                return;
            }
            
            document.getElementById('studentForm').classList.add('hidden');
            document.getElementById('testSection').classList.remove('hidden');
            
            loadQuestions();
        }

        // تحميل الأسئلة
        function loadQuestions() {
            const container = document.getElementById('questionsContainer');
            container.innerHTML = '';
            
            questions.forEach((q, index) => {
                const questionDiv = document.createElement('div');
                questionDiv.className = 'question';
                questionDiv.innerHTML = `
                    <h3>${q.question}</h3>
                    <div class="options" id="options${q.id}">
                        ${q.options.map((opt, optIndex) => `
                            <label class="option" onclick="selectAnswer(${q.id}, ${optIndex})">
                                ${opt}
                            </label>
                        `).join('')}
                    </div>
                `;
                container.appendChild(questionDiv);
            });
            
            document.getElementById('submitBtn').classList.remove('hidden');
        }

        // اختيار إجابة
        function selectAnswer(questionId, optionIndex) {
            const options = document.querySelectorAll(`#options${questionId} .option`);
            options.forEach(opt => opt.classList.remove('selected'));
            options[optionIndex].classList.add('selected');
            
            userAnswers[questionId - 1] = optionIndex;
        }

        // إنهاء الاختبار
        function submitTest() {
            const answered = userAnswers.filter(a => a !== undefined).length;
            
            if (answered < questions.length) {
                alert(`الرجاء الإجابة على جميع الأسئلة (تمت الإجابة على ${answered} من ${questions.length})`);
                return;
            }
            
            calculateResults();
        }

        // حساب النتائج
        function calculateResults() {
            let score = 0;
            let resultsHTML = '';
            
            questions.forEach((q, index) => {
                const userAnswer = userAnswers[index];
                const isCorrect = userAnswer === q.correct;
                
                if (isCorrect) {
                    score++;
                }
                
                // تلوين الإجابات
                const options = document.querySelectorAll(`#options${q.id} .option`);
                options.forEach((opt, optIndex) => {
                    opt.classList.remove('correct', 'wrong');
                    if (optIndex === q.correct) {
                        opt.classList.add('correct');
                    } else if (optIndex === userAnswer && !isCorrect) {
                        opt.classList.add('wrong');
                    }
                });
            });
            
            const percentage = (score / questions.length) * 100;
            const evaluation = percentage >= 50 ? 'ممتاز! 👍' : 'تحتاج للمزيد من المذاكرة 📚';
            
            resultsHTML = `
                <div class="score">${score}/${questions.length}</div>
                <p><strong>النسبة:</strong> ${percentage.toFixed(0)}%</p>
                <p><strong>التقييم:</strong> ${evaluation}</p>
                <p><strong>الطالب:</strong> ${studentName}</p>
                <p><strong>الفصل:</strong> ${studentClass}</p>
            `;
            
            document.getElementById('resultsContent').innerHTML = resultsHTML;
            document.getElementById('testSection').classList.add('hidden');
            document.getElementById('resultsSection').classList.remove('hidden');
        }

        // إرسال إلى واتساب
        async function sendToWhatsApp() {
            const loadingModal = document.getElementById('loadingModal');
            const loadingText = document.getElementById('loadingText');
            const statusDiv = document.getElementById('whatsappStatus');
            
            loadingModal.classList.remove('hidden');
            loadingText.textContent = 'جاري إعداد التقرير...';
            
            try {
                // حساب النتائج
                let score = 0;
                questions.forEach((q, index) => {
                    if (userAnswers[index] === q.correct) score++;
                });
                const percentage = (score / questions.length) * 100;
                
                // إنشاء الرسالة
                const date = new Date().toLocaleDateString('ar-SA');
                const time = new Date().toLocaleTimeString('ar-SA');
                
                const message = `📚 *نتيجة اختبار القواعد الإنجليزية*
                
👤 *الطالب:* ${studentName}
🏫 *الفصل:* ${studentClass}
👨‍🏫 *المعلم:* فهد الخالدي

📊 *النتيجة:*
✅ الإجابات الصحيحة: ${score}/${questions.length}
📈 النسبة المئوية: ${percentage.toFixed(0)}%
⭐ التقييم: ${percentage >= 50 ? 'ممتاز' : 'يحتاج تحسين'}

⏰ تاريخ الاختبار: ${date}
🕒 وقت الاختبار: ${time}

*تفاصيل الأسئلة:*
${questions.map((q, i) => {
    const userAnswer = userAnswers[i];
    const isCorrect = userAnswer === q.correct;
    const answerText = q.options[userAnswer] || 'لم يتم الإجابة';
    return `\n${q.question}\nإجابة الطالب: ${answerText} ${isCorrect ? '✅' : '❌'}\n`;
}).join('')}

تم إنشاء هذا التقرير تلقائياً من نظام الاختبار التفاعلي.`;

                // رقم المعلم
                const teacherNumber = '966533527240';
                
                // ترميز الرسالة
                const encodedMessage = encodeURIComponent(message);
                
                // رابط واتساب
                const whatsappURL = `https://wa.me/${teacherNumber}?text=${encodedMessage}`;
                
                // محاكاة التأخير للواجهة
                await new Promise(resolve => setTimeout(resolve, 2000));
                
                // فتح واتساب في نافذة جديدة
                loadingText.textContent = 'جاري فتح واتساب...';
                await new Promise(resolve => setTimeout(resolve, 1000));
                
                // فتح الرابط
                window.open(whatsappURL, '_blank');
                
                // إظهار رسالة النجاح
                loadingModal.classList.add('hidden');
                statusDiv.innerHTML = '<div class="success"><i class="fas fa-check-circle"></i> تم إرسال النتائج بنجاح إلى المعلم!</div>';
                statusDiv.classList.remove('hidden');
                
                // إخفاء الرسالة بعد 5 ثوان
                setTimeout(() => {
                    statusDiv.classList.add('hidden');
                }, 5000);
                
            } catch (error) {
                console.error('Error:', error);
                loadingModal.classList.add('hidden');
                statusDiv.innerHTML = '<div class="error"><i class="fas fa-exclamation-circle"></i> حدث خطأ في الإرسال. حاول مرة أخرى.</div>';
                statusDiv.classList.remove('hidden');
            }
        }

        // إعادة الاختبار
        function restartTest() {
            userAnswers = [];
            testStarted = false;
            
            document.getElementById('resultsSection').classList.add('hidden');
            document.getElementById('whatsappStatus').classList.add('hidden');
            document.getElementById('studentName').value = '';
            document.getElementById('studentClass').value = '';
            
            document.getElementById('studentForm').classList.remove('hidden');
        }

        // بدء التطبيق
        window.onload = function() {
            // تعطيل خاصية الإدخال التلقائي
            document.getElementById('studentName').autocomplete = 'off';
            document.getElementById('studentClass').autocomplete = 'off';
        };
    </script>
</body>
</html>
