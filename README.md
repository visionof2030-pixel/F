<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<title>تقرير صورة للطالب</title>
<script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
<style>
body { font-family: Arial; direction: rtl; padding: 20px; }
input, button { margin: 5px 0; padding: 5px; }
#report { background: #f0f0f0; padding: 10px; margin-top: 20px; display: none; width: 300px; }
button { cursor: pointer; }
</style>
</head>
<body>

<h1>درس تفاعلي صغير</h1>
<p>في هذا الدرس سنتعلم عن ألوان الطبيعة.</p>

<form id="quizForm">
  <label>اسم الطالب:<br>
    <input type="text" id="studentName" required>
  </label><br>

  <p>1- ما لون السماء؟</p>
  <input type="radio" name="q1" value="أحمر" required>أحمر<br>
  <input type="radio" name="q1" value="أزرق">أزرق<br>

  <p>2- ما لون العشب؟</p>
  <input type="radio" name="q2" value="أخضر" required>أخضر<br>
  <input type="radio" name="q2" value="أصفر">أصفر<br><br>

  <button type="button" onclick="generateImage()">إنشاء تقرير كصورة + WhatsApp</button>
</form>

<!-- عنصر لتوليد الصورة -->
<div id="report"></div>

<script>
function generateImage() {
  const name = document.getElementById('studentName').value.trim();
  if(!name) { alert('اكتب اسمك'); return; }

  const answers = [
    document.querySelector('input[name="q1"]:checked').value,
    document.querySelector('input[name="q2"]:checked').value
  ];
  const correctAnswers = ["أزرق","أخضر"];

  let correctCount = 0;
  let wrongCount = 0;
  let summaryText = "";

  for(let i=0;i<answers.length;i++){
    let status = answers[i]===correctAnswers[i] ? "صحيح" : "خاطئ";
    if(status==="صحيح") correctCount++; else wrongCount++;
    summaryText += `سؤال ${i+1}: ${answers[i]} → ${status}<br>`;
  }

  // ملأ عنصر التقرير
  const reportDiv = document.getElementById('report');
  reportDiv.innerHTML = `
    <h2>تقرير الطالب: ${name}</h2>
    <p>عدد الأسئلة: ${answers.length}</p>
    <p>الإجابات الصحيحة: ${correctCount}</p>
    <p>الإجابات الخاطئة: ${wrongCount}</p>
    <p>ملخص الإجابات:</p>
    <p>${summaryText}</p>
  `;
  reportDiv.style.display = 'block';

  // توليد الصورة وحفظها
  html2canvas(reportDiv).then(canvas => {
    const link = document.createElement('a');
    link.download = `${name}_report.png`;
    link.href = canvas.toDataURL();
    link.click();
  });

  // فتح WhatsApp مع ملخص نصي
  const message = `اسم الطالب: ${name}%0Aالدرجة: ${correctCount}/${answers.length}%0Aملخص الإجابات:%0A${answers.map((a,i)=>`سؤال ${i+1}: ${a} → ${answers[i]===correctAnswers[i]?'صحيح':'خاطئ'}`).join("%0A")}`;
  const waNumber = "966533527240";
  window.open(`https://wa.me/${waNumber}?text=${message}`, '_blank');
}
</script>

</body>
</html>
