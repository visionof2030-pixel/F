<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>اختبار القواعد الإنجليزية</title>
    <link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@300;400;500;700;800&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Tajawal', sans-serif;
        }

        body {
            background: linear-gradient(135deg, #3498db, #2ecc71);
            min-height: 100vh;
            padding: 20px;
            color: #333;
        }

        .container {
            max-width: 800px;
            margin: 0 auto;
        }

        header {
            text-align: center;
            background: white;
            padding: 20px;
            border-radius: 15px;
            margin-bottom: 20px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }

        h1 {
            color: #2c3e50;
            margin-bottom: 10px;
        }

        .card {
            background: white;
            padding: 30px;
            border-radius: 15px;
            margin-bottom: 20px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }

        .btn {
            background: #2ecc71;
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 10px;
            font-size: 18px;
            cursor: pointer;
            width: 100%;
            margin: 10px 0;
            transition: 0.3s;
        }

        .btn:hover {
            background: #27ae60;
            transform: translateY(-2px);
        }

        .btn-whatsapp {
            background: #25D366;
        }

        .btn-whatsapp:hover {
            background: #128C7E;
        }

        input {
            width: 100%;
            padding: 12px;
            margin: 10px 0;
            border: 2px solid #ddd;
            border-radius: 8px;
            font-size: 16px;
        }

        .question {
            padding: 20px;
            border: 2px solid #e0e0e0;
            border-radius: 10px;
            margin: 15px 0;
        }

        .option {
            padding: 12px;
            margin: 8px 0;
            background: #f8f9fa;
            border: 2px solid #dee2e6;
            border-radius: 8px;
            cursor: pointer;
            transition: 0.3s;
        }

        .option:hover {
            background: #e9ecef;
        }

        .option.selected {
            background: #d4edda;
            border-color: #28a745;
        }

        .result-card {
            text-align: center;
            padding: 40px 20px;
        }

        .score {
            font-size: 48px;
            font-weight: bold;
            color: #2ecc71;
            margin: 20px 0;
        }

        .whatsapp-info {
            background: rgba(37, 211, 102, 0.1);
            border: 2px solid #25D366;
            padding: 15px;
            border-radius: 10px;
            margin: 20px 0;
            text-align: center;
        }

        .hidden {
            display: none;
        }

        .loading {
            text-align: center;
            padding: 30px;
        }

        .spinner {
            border: 4px solid #f3f3f3;
            border-top: 4px solid #3498db;
            border-radius: 50%;
            width: 40px;
            height: 40px;
            animation: spin 1s linear infinite;
            margin: 20px auto;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- Step 1: Student Info -->
        <div id="step1">
            <header>
                <h1>📚 اختبار القواعد الإنجليزية</h1>
                <p>اختبار قصير - سؤالين فقط</p>
            </header>
            
            <div class="card">
                <h2>معلومات الطالب</h2>
                <input type="text" id="studentName" placeholder="أدخل اسمك الكامل">
                <input type="text" id="studentClass" placeholder="أدخل فصلك / صفك">
                <button class="btn" onclick="startTest()">بدء الاختبار</button>
            </div>
        </div>

        <!-- Step 2: Test Questions -->
        <div id="step2" class="hidden">
            <div class="card">
                <h2>اختبار القواعد</h2>
                
                <!-- Question 1 -->
                <div class="question" id="q1">
                    <h3>السؤال 1: Buses are ______ than taxis.</h3>
                    <div class="option" onclick="selectAnswer(1, 0)">A) cheap</div>
                    <div class="option" onclick="selectAnswer(1, 1)">B) cheaper</div>
                    <div class="option" onclick="selectAnswer(1, 2)">C) cheapest</div>
                    <div class="option" onclick="selectAnswer(1, 3)">D) more cheap</div>
                </div>

                <!-- Question 2 -->
                <div class="question" id="q2">
                    <h3>السؤال 2: This is the ______ movie I have ever seen.</h3>
                    <div class="option" onclick="selectAnswer(2, 0)">A) bad</div>
                    <div class="option" onclick="selectAnswer(2, 1)">B) worse</div>
                    <div class="option" onclick="selectAnswer(2, 2)">C) worst</div>
                    <div class="option" onclick="selectAnswer(2, 3)">D) badly</div>
                </div>

                <button class="btn" onclick="submitTest()">إنهاء الاختبار</button>
            </div>
        </div>

        <!-- Step 3: Results -->
        <div id="step3" class="hidden">
            <div class="card result-card">
                <h2>🎉 نتائج الاختبار</h2>
                <div id="resultsContent"></div>
                
                <div class="whatsapp-info">
                    <h3>📱 إرسال النتائج إلى المعلم</h3>
                    <p><strong>المعلم:</strong> فهد الخالدي</p>
                    <p><strong>رقم الواتساب:</strong> 966533527240</p>
                    <button class="btn btn-whatsapp" onclick="sendWhatsApp()">
                        <span style="font-size: 20px;">📤</span> إرسال النتائج الآن
                    </button>
                </div>
                
                <button class="btn" onclick="restartTest()">إعادة الاختبار</button>
            </div>
        </div>

        <!-- Loading Screen -->
        <div id="loadingScreen" class="hidden">
            <div class="card loading">
                <h3>جاري إرسال النتائج...</h3>
                <div class="spinner"></div>
                <p>سيفتح واتساب تلقائياً خلال ثواني</p>
            </div>
        </div>
    </div>

    <script>
        // Answers storage
        const answers = {
            q1: null,
            q2: null
        };

        // Correct answers
        const correctAnswers = {
            q1: 1,  // B) cheaper
            q2: 2   // C) worst
        };

        // Student info
        let studentName = '';
        let studentClass = '';

        function startTest() {
            studentName = document.getElementById('studentName').value.trim();
            studentClass = document.getElementById('studentClass').value.trim();
            
            if (!studentName || !studentClass) {
                alert('الرجاء إدخال الاسم والفصل');
                return;
            }
            
            document.getElementById('step1').classList.add('hidden');
            document.getElementById('step2').classList.remove('hidden');
        }

        function selectAnswer(questionNum, optionIndex) {
            const questionId = `q${questionNum}`;
            const options = document.querySelectorAll(`#${questionId} .option`);
            
            // Remove selected class from all options in this question
            options.forEach(option => {
                option.classList.remove('selected');
            });
            
            // Add selected class to clicked option
            options[optionIndex].classList.add('selected');
            
            // Save answer
            answers[questionId] = optionIndex;
        }

        function submitTest() {
            // Check if all questions are answered
            if (answers.q1 === null || answers.q2 === null) {
                alert('الرجاء الإجابة على جميع الأسئلة');
                return;
            }
            
            // Calculate score
            let score = 0;
            let resultsHTML = '';
            
            if (answers.q1 === correctAnswers.q1) score++;
            if (answers.q2 === correctAnswers.q2) score++;
            
            const percentage = (score / 2) * 100;
            const grade = percentage >= 50 ? 'ناجح' : 'يراجع';
            
            // Show results
            resultsHTML = `
                <div class="score">${score}/2</div>
                <p><strong>النسبة:</strong> ${percentage}%</p>
                <p><strong>التقييم:</strong> ${grade}</p>
                <p><strong>الطالب:</strong> ${studentName}</p>
                <p><strong>الفصل:</strong> ${studentClass}</p>
                
                <div style="margin-top: 20px; text-align: left;">
                    <p><strong>تفاصيل الإجابات:</strong></p>
                    <p>1. Buses are ______ than taxis.</p>
                    <p style="color: ${answers.q1 === correctAnswers.q1 ? '#27ae60' : '#e74c3c'}">
                        إجابتك: ${getOptionText(1, answers.q1)} ${answers.q1 === correctAnswers.q1 ? '✅' : '❌'}
                    </p>
                    <p>2. This is the ______ movie I have ever seen.</p>
                    <p style="color: ${answers.q2 === correctAnswers.q2 ? '#27ae60' : '#e74c3c'}">
                        إجابتك: ${getOptionText(2, answers.q2)} ${answers.q2 === correctAnswers.q2 ? '✅' : '❌'}
                    </p>
                </div>
            `;
            
            document.getElementById('resultsContent').innerHTML = resultsHTML;
            document.getElementById('step2').classList.add('hidden');
            document.getElementById('step3').classList.remove('hidden');
        }

        function getOptionText(questionNum, optionIndex) {
            const options = {
                1: ['A) cheap', 'B) cheaper', 'C) cheapest', 'D) more cheap'],
                2: ['A) bad', 'B) worse', 'C) worst', 'D) badly']
            };
            return options[questionNum][optionIndex];
        }

        function sendWhatsApp() {
            // Calculate score again
            let score = 0;
            if (answers.q1 === correctAnswers.q1) score++;
            if (answers.q2 === correctAnswers.q2) score++;
            const percentage = (score / 2) * 100;
            const grade = percentage >= 50 ? 'ناجح' : 'يراجع';
            
            // Show loading
            document.getElementById('step3').classList.add('hidden');
            document.getElementById('loadingScreen').classList.remove('hidden');
            
            // Create the message
            const date = new Date().toLocaleDateString('ar-SA');
            const time = new Date().toLocaleTimeString('ar-SA');
            
            const message = `📚 *نتيجة اختبار القواعد الإنجليزية*

👤 *الطالب:* ${studentName}
🏫 *الفصل:* ${studentClass}
👨‍🏫 *المعلم:* فهد الخالدي

📊 *النتائج:*
✅ الإجابات الصحيحة: ${score}/2
📈 النسبة المئوية: ${percentage}%
⭐ التقييم: ${grade}

📝 *تفاصيل الإجابات:*
1. Buses are ______ than taxis.
   إجابة الطالب: ${getOptionText(1, answers.q1)} ${answers.q1 === correctAnswers.q1 ? '✅ صحيحة' : '❌ خاطئة'}
   الإجابة الصحيحة: B) cheaper

2. This is the ______ movie I have ever seen.
   إجابة الطالب: ${getOptionText(2, answers.q2)} ${answers.q2 === correctAnswers.q2 ? '✅ صحيحة' : '❌ خاطئة'}
   الإجابة الصحيحة: C) worst

⏰ *تاريخ الاختبار:* ${date}
🕒 *وقت الاختبار:* ${time}

تم إنشاء هذا التقرير تلقائياً من نظام الاختبار التفاعلي.`;

            // WhatsApp number
            const whatsappNumber = '966533527240';
            
            // Encode the message
            const encodedMessage = encodeURIComponent(message);
            
            // Create WhatsApp URL
            const whatsappURL = `https://wa.me/${whatsappNumber}?text=${encodedMessage}`;
            
            // Open WhatsApp after short delay
            setTimeout(() => {
                window.open(whatsappURL, '_blank');
                
                // Hide loading and show results again
                setTimeout(() => {
                    document.getElementById('loadingScreen').classList.add('hidden');
                    document.getElementById('step3').classList.remove('hidden');
                    alert('تم فتح واتساب بنجاح! الرجاء الضغط على زر الإرسال لإرسال النتائج إلى المعلم.');
                }, 1000);
            }, 2000);
        }

        function restartTest() {
            // Reset everything
            answers.q1 = null;
            answers.q2 = null;
            studentName = '';
            studentClass = '';
            
            // Reset selections
            document.querySelectorAll('.option').forEach(option => {
                option.classList.remove('selected');
            });
            
            // Reset inputs
            document.getElementById('studentName').value = '';
            document.getElementById('studentClass').value = '';
            
            // Show first step
            document.getElementById('step3').classList.add('hidden');
            document.getElementById('loadingScreen').classList.add('hidden');
            document.getElementById('step1').classList.remove('hidden');
        }

        // Initialize
        window.onload = function() {
            // Prevent form submission
            document.getElementById('studentName').addEventListener('keypress', function(e) {
                if (e.key === 'Enter') {
                    e.preventDefault();
                    startTest();
                }
            });
            
            document.getElementById('studentClass').addEventListener('keypress', function(e) {
                if (e.key === 'Enter') {
                    e.preventDefault();
                    startTest();
                }
            });
        };
    </script>
</body>
</html>
