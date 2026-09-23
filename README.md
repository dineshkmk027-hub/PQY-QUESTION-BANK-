<!DOCTYPE html>
<html lang="hi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>PYQ Study App</title>

<style>
body{
  margin:0;
  font-family:Arial,sans-serif;
  background:#f3f6fb;
}

.header{
  background:#1976d2;
  color:white;
  padding:25px 15px;
  text-align:center;
}

.header h1{
  margin:0;
  font-size:28px;
}

.container{
  max-width:600px;
  margin:auto;
  padding:18px;
}

.stats{
  display:flex;
  gap:12px;
}

.stat{
  flex:1;
  background:white;
  padding:18px;
  text-align:center;
  border-radius:15px;
  box-shadow:0 2px 8px #ddd;
}

.stat b{
  font-size:25px;
  color:#1976d2;
}

.card{
  background:white;
  margin-top:20px;
  padding:20px;
  border-radius:18px;
  box-shadow:0 2px 8px #ddd;
}

input, textarea, select{
  width:100%;
  box-sizing:border-box;
  padding:13px;
  margin-top:8px;
  margin-bottom:12px;
  border:1px solid #ccc;
  border-radius:10px;
  font-size:16px;
}

textarea{
  min-height:100px;
}

button{
  width:100%;
  padding:14px;
  margin-top:10px;
  border:none;
  border-radius:12px;
  background:#1976d2;
  color:white;
  font-size:17px;
}

.delete{
  background:#d32f2f;
}

.question{
  background:#f8f9ff;
  padding:15px;
  margin-top:15px;
  border-radius:12px;
  border-left:5px solid #1976d2;
}
</style>
</head>

<body>

<div class="header">
  <h1>📚 PYQ Study App</h1>
  <p>Smart Preparation</p>
</div>

<div class="container">

<div class="stats">

<div class="stat">
<b id="total">0</b>
<br>Questions
</div>

<div class="stat">
<b>0%</b>
<br>Accuracy
</div>

</div>

<div class="card">

<h2>🎯 मेरी तैयारी</h2>

<button onclick="showAdd()">➕ Add PYQ</button>

<button onclick="showQuestions()">📋 My PYQs</button>

<button onclick="mockTest()">📝 Mock Test</button>

<button onclick="performance()">📊 Performance</button>

<button onclick="weakTopics()">🔴 Weak Topics</button>

</div>

<div id="appArea"></div>

</div>

<script>

let questions =
JSON.parse(localStorage.getItem("pyqQuestions")) || [];

updateTotal();

function updateTotal(){
  document.getElementById("total").innerText =
  questions.length;
}

function showAdd(){

document.getElementById("appArea").innerHTML = `

<div class="card">

<h2>➕ Add PYQ</h2>

<label>Question</label>
<textarea id="question"
placeholder="यहाँ पूरा प्रश्न लिखें"></textarea>

<label>Option A</label>
<input id="optionA" placeholder="Option A">

<label>Option B</label>
<input id="optionB" placeholder="Option B">

<label>Option C</label>
<input id="optionC" placeholder="Option C">

<label>Option D</label>
<input id="optionD" placeholder="Option D">

<label>Correct Answer</label>
<select id="correct">
<option value="">सही उत्तर चुनें</option>
<option value="A">A</option>
<option value="B">B</option>
<option value="C">C</option>
<option value="D">D</option>
</select>

<label>Subject</label>
<input id="subject" placeholder="जैसे General Science">

<label>Topic</label>
<input id="topic" placeholder="जैसे Biology">

<label>Exam</label>
<input id="exam" placeholder="जैसे Railway Group D">

<label>Year</label>
<input id="year" placeholder="जैसे 2025">

<button onclick="savePYQ()">💾 Save PYQ</button>

</div>
`;
}

function savePYQ(){

let q = {
question: document.getElementById("question").value,
A: document.getElementById("optionA").value,
B: document.getElementById("optionB").value,
C: document.getElementById("optionC").value,
D: document.getElementById("optionD").value,
correct: document.getElementById("correct").value,
subject: document.getElementById("subject").value,
topic: document.getElementById("topic").value,
exam: document.getElementById("exam").value,
year: document.getElementById("year").value
};

if(!q.question || !q.A || !q.B || !q.C || !q.D || !q.correct){

alert("कृपया Question, सभी Options और Correct Answer भरें।");
return;
}

questions.push(q);

localStorage.setItem(
"pyqQuestions",
JSON.stringify(questions)
);

updateTotal();

alert("✅ PYQ Successfully Save हो गया!");

showQuestions();
}

function showQuestions(){

let html = `
<div class="card">
<h2>📋 My PYQs</h2>
`;

if(questions.length === 0){

html += "<p>अभी कोई PYQ Save नहीं है।</p>";

}else{

questions.forEach((q,index)=>{

html += `

<div class="question">

<b>Q${index+1}. ${q.question}</b>

<p>A. ${q.A}</p>
<p>B. ${q.B}</p>
<p>C. ${q.C}</p>
<p>D. ${q.D}</p>

<p>✅ Correct: ${q.correct}</p>

<p>📚 ${q.subject} | 📌 ${q.topic}</p>

<p>📝 ${q.exam} | 📅 ${q.year}</p>

<button class="delete"
onclick="deletePYQ(${index})">
🗑️ Delete
</button>

</div>

`;

});

}

html += "</div>";

document.getElementById("appArea").innerHTML = html;
}

function deletePYQ(index){

if(confirm("क्या यह PYQ delete करना है?")){

questions.splice(index,1);

localStorage.setItem(
"pyqQuestions",
JSON.stringify(questions)
);

updateTotal();
showQuestions();

}

}

function mockTest(){

alert("📝 Mock Test System अगला step है।");

}

function performance(){

alert("📊 Performance System अगला step है।");

}

function weakTopics(){

alert("🔴 Weak Topics System अगला step है।");

}

</script>

</body>
</html>
