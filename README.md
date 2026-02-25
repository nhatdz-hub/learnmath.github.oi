# learnmath.github.oi
<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Học Toán THCS - Lớp 6 đến 9</title>
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600&display=swap" rel="stylesheet">

  <style>
    body {
      font-family: 'Poppins', Arial, sans-serif;
      background: linear-gradient(to bottom, #ffffff 0%, #e3f2fd 60%, #bbdefb 100%);
      margin: 0;
      padding: 20px;
      color: #2c3e50;
      min-height: 100vh;
    }
    .container {
      max-width: 850px;
      margin: 0 auto;
      background: rgba(255, 255, 255, 0.96);
      padding: 35px;
      border-radius: 16px;
      box-shadow: 0 8px 30px rgba(0, 0, 0, 0.08);
    }
    h1 { color: #1565c0; text-align: center; font-size: 2.3rem; margin-bottom: 25px; }
    h2 { color: #0d47a1; font-size: 1.7rem; margin-bottom: 20px; }
    h3 { color: #1976d2; font-size: 1.35rem; }

    #auth-screen {
      background: linear-gradient(135deg, #42a5f5 0%, #ec407a 100%);
      padding: 40px 30px;
      border-radius: 16px;
      color: white;
      margin-bottom: 20px;
    }
    #auth-screen h1, #auth-screen h2 { color: white; }
    #auth-screen input {
      background: rgba(255,255,255,0.9);
      border: none;
      color: #333;
    }
    #auth-screen button {
      background: rgba(255,255,255,0.25);
      border: 2px solid white;
      color: white;
      font-weight: 600;
    }
    #auth-screen button:hover { background: rgba(255,255,255,0.4); }
    #message { color: #ffe082; font-weight: 500; text-align: center; margin-top: 15px; }

    input, button {
      display: block;
      width: 90%;
      max-width: 420px;
      margin: 16px auto;
      padding: 14px;
      font-size: 1.05rem;
      border-radius: 10px;
      border: 2px solid #90caf9;
      transition: all 0.3s;
    }
    input:focus {
      border-color: #42a5f5;
      box-shadow: 0 0 0 4px rgba(66,165,245,0.2);
      outline: none;
    }
    button {
      background: #2196f3;
      color: white;
      border: none;
      cursor: pointer;
      font-weight: 600;
    }
    button:hover { background: #1976d2; transform: translateY(-2px); }

    /* Phần chọn lớp - thẳng hàng ngang */
    #class-screen { text-align: center; }
    .class-grid {
      display: flex;
      flex-direction: row;
      flex-wrap: nowrap;
      justify-content: center;
      align-items: center;
      gap: 20px;
      margin: 40px 0;
      overflow-x: auto;
      padding: 10px 0;
    }
    .class-btn {
      flex: 0 0 180px;
      height: 100px;
      font-size: 1.5rem;
      font-weight: 600;
      color: white;
      border: none;
      border-radius: 12px;
      cursor: pointer;
      transition: all 0.3s ease;
      min-width: 160px;
      box-shadow: 0 4px 12px rgba(0,0,0,0.1);
      background: #4caf50;
    }
    .class-btn:hover {
      background: linear-gradient(135deg, #ffffff 0%, #c8e6c9 100%);
      transform: translateY(-5px);
      box-shadow: 0 10px 25px rgba(76,175,80,0.3);
      color: #1b5e20;
    }

    /* Màn hình lý thuyết mới */
    #theory-screen {
      background: #f9fff9;
      border: 1px solid #c8e6c9;
      border-radius: 16px;
      padding: 30px;
      margin: 20px 0;
      line-height: 1.7;
    }
    #theory-screen h2 { color: #2e7d32; text-align: center; }
    #theory-content { font-size: 1.1rem; color: #333; }
    .theory-btn {
      margin: 30px auto 0;
      width: 220px;
      background: #4caf50;
    }
    .theory-btn:hover { background: #388e3c; }

    .lesson-list { margin: 25px 0; }
    .lesson-item {
      background: #f0f9ff;
      border: 1px solid #bbdefb;
      border-radius: 10px;
      padding: 16px;
      margin: 12px 0;
      cursor: pointer;
      transition: all 0.3s;
      color: #1565c0;
      font-weight: 500;
    }
    .lesson-item:hover {
      background: #e3f2fd;
      transform: translateX(6px);
      box-shadow: 0 4px 15px rgba(33,150,243,0.15);
    }

    #quiz-content .question {
      background: white;
      padding: 16px;
      border-radius: 10px;
      margin-bottom: 20px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.05);
      font-size: 1.1rem;
    }
    .option { margin: 10px 0; padding: 10px; border-radius: 8px; transition: background 0.2s; }
    .option:hover { background: #e8f4fd; }

    #progress {
      margin: 25px 0;
      font-weight: bold;
      color: #2e7d32;
      text-align: center;
      font-size: 1.2rem;
    }

    .hidden { display: none !important; }

    button[onclick="logout()"],
    button[onclick="backToLessons()"],
    button[onclick="backToClasses()"] {
      background: #757575;
      display: block;
      margin: 25px auto;
      width: 220px;
    }
    button[onclick="logout()"]:hover { background: #616161; }
  </style>
</head>
<body>
<div class="container">

  <!-- Đăng ký / Đăng nhập -->
  <div id="auth-screen">
    <h1>LearnMath</h1>
    <h2 id="form-title">Đăng ký / Đăng nhập</h2>
    <input type="text" id="username" placeholder="Tên đăng nhập" required>
    <input type="password" id="password" placeholder="Mật khẩu" required>
    <button onclick="register()">Đăng ký</button>
    <button onclick="login()">Đăng nhập</button>
    <p id="message"></p>
  </div>

  <!-- Chọn lớp -->
  <div id="class-screen" class="hidden">
    <h1>Chọn lớp học</h1>
    <div class="class-grid">
      <button class="class-btn" onclick="selectClass(6)">Lớp 6</button>
      <button class="class-btn" onclick="selectClass(7)">Lớp 7</button>
      <button class="class-btn" onclick="selectClass(😎">Lớp 8</button>
      <button class="class-btn" onclick="selectClass(9)">Lớp 9</button>
    </div>
    <button onclick="logout()">Đăng xuất</button>
  </div>

  <!-- Danh sách bài học -->
  <div id="lessons-screen" class="hidden">
    <h2 id="class-title"></h2>
    <div id="lesson-list" class="lesson-list"></div>
    <button onclick="backToClasses()">← Quay lại chọn lớp</button>
  </div>

  <!-- Màn hình LÝ THUYẾT (mới thêm) -->
  <div id="theory-screen" class="hidden">
    <h2 id="theory-title"></h2>
    <div id="theory-content"></div>
    <button class="theory-btn" onclick="startQuizAfterTheory()">Bắt đầu làm bài</button>
    <button onclick="backToLessons()" style="margin-top:15px;">Quay lại danh sách bài học</button>
  </div>

  <!-- Màn hình trắc nghiệm -->
  <div id="quiz-screen" class="hidden">
    <h2 id="quiz-title"></h2>
    <div id="progress"></div>
    <div id="quiz-content"></div>
    <button id="submit-btn" onclick="checkQuiz()" style="margin-top:25px;">Nộp bài</button>
    <button onclick="backToLessons()" style="margin-left:20px;">Quay lại</button>
  </div>

</div>

<script>
// Dữ liệu bài học - bổ sung phần lý thuyết
const lessonsData = {
  6: [
    { chapter: "Chương 1", title: "Số nguyên", lessons: [
      { 
        title: "Số nguyên dương, âm và số 0", 
        key: "61",
        theory: `
          <p><strong>Số nguyên</strong> là tập hợp các số ..., -3, -2, -1, 0, 1, 2, 3, ...</p>
          <ul>
            <li><strong>Số nguyên dương</strong>: 1, 2, 3, ... (các số lớn hơn 0)</li>
            <li><strong>Số nguyên âm</strong>: -1, -2, -3, ... (các số nhỏ hơn 0)</li>
            <li><strong>Số 0</strong>: không dương cũng không âm</li>
          </ul>
          <p>Trên <strong>trục số</strong>, số càng lớn nằm càng bên phải, số càng nhỏ nằm càng bên trái.</p>
        `
      },
      { title: "So sánh số nguyên", key: "62", theory: "Nội dung lý thuyết so sánh số nguyên..." },
      { title: "Cộng trừ số nguyên", key: "63", theory: "Quy tắc cộng trừ số nguyên..." }
    ]},
    { chapter: "Chương 2", title: "Phân số", lessons: [
      { title: "Khái niệm phân số", key: "64", theory: "Phân số là gì? Tử số, mẫu số..." },
      { title: "Rút gọn phân số", key: "65", theory: "Cách tìm ước chung lớn nhất để rút gọn..." }
    ]}
  ],
  7: [
    { chapter: "Chương 1", title: "Biểu thức đại số", lessons: [
      { title: "Hằng số và biến số", key: "71", theory: "Hằng số là giá trị không đổi, biến số thay đổi được..." }
    ]}
  ],
  8: [{ chapter: "Chương 1", title: "Đang cập nhật", lessons: [] }],
  9: [{ chapter: "Chương 1", title: "Đang cập nhật", lessons: [] }]
};

const questionsData = {
  "61": [
    { q: "Số nguyên âm nhỏ nhất trong các số sau là?", options: ["-5", "0", "3", "-1"], answer: 0 },
    { q: "-8 nằm ở đâu trên trục số?", options: ["Bên phải 0", "Bên trái 0", "Tại gốc", "Không xác định"], answer: 1 }
    // Thêm đủ 10 câu khi cần
  ],
};

let currentUser = null;
let currentClass = null;
let currentLessonKey = null;
let currentLessonTitle = null;
let currentTheory = null;
let currentQuestions = [];
let userAnswers = [];

// Các hàm register, login, showMessage, showClassSelection giữ nguyên
function register() {
  const user = document.getElementById("username").value.trim();
  const pass = document.getElementById("password").value.trim();
  if (!user || !pass) {
    showMessage("Vui lòng nhập đủ thông tin!", "red");
    return;
  }
  if (localStorage.getItem("user_" + user)) {
    showMessage("Tên đăng nhập đã tồn tại!", "red");
    return;
  }
  const data = { password: pass, progress: {} };
  localStorage.setItem("user_" + user, JSON.stringify(data));
  showMessage("Đăng ký thành công! Bạn có thể đăng nhập ngay.", "#fff59d");
}

function login() {
  const user = document.getElementById("username").value.trim();
  const pass = document.getElementById("password").value.trim();
  const saved = localStorage.getItem("user_" + user);
  if (!saved) {
    showMessage("Tài khoản không tồn tại!", "red");
    return;
  }
  const data = JSON.parse(saved);
  if (data.password !== pass) {
    showMessage("Mật khẩu không đúng!", "red");
    return;
  }
  currentUser = user;
  showMessage("Đăng nhập thành công!", "#c8e6c9");
  setTimeout(showClassSelection, 800);
}

function showMessage(text, color = "#ef5350") {
  const el = document.getElementById("message");
  el.textContent = text;
  el.style.color = color;
}

function showClassSelection() {
  document.getElementById("auth-screen").classList.add("hidden");
  document.getElementById("class-screen").classList.remove("hidden");
}

function selectClass(cls) {
  currentClass = cls;
  document.getElementById("class-title").textContent = Lớp ${cls};
  renderLessons(cls);
  document.getElementById("class-screen").classList.add("hidden");
  document.getElementById("lessons-screen").classList.remove("hidden");
}

function renderLessons(cls) {
  const container = document.getElementById("lesson-list");
  container.innerHTML = "";
  const chapters = lessonsData[cls] || [];
  if (chapters.length === 0) {
    container.innerHTML = "<p style='color:#777; text-align:center;'>Chưa có bài học nào cho lớp này...</p>";
    return;
  }
  chapters.forEach(chap => {
    const chapDiv = document.createElement("div");
    chapDiv.innerHTML = <h3>${chap.chapter} - ${chap.title}</h3>;
    chap.lessons.forEach(les => {
      const item = document.createElement("div");
      item.className = "lesson-item";
      item.textContent = les.title;
      item.onclick = () => startTheory(les.key, les.title, les.theory || "Chưa có nội dung lý thuyết.");
      chapDiv.appendChild(item);
    });
    container.appendChild(chapDiv);
  });
}

// Mở màn hình lý thuyết
function startTheory(key, title, theory) {
  currentLessonKey = key;
  currentLessonTitle = title;
  currentTheory = theory;

  document.getElementById("theory-title").textContent = title + " - Lý thuyết";
  document.getElementById("theory-content").innerHTML = theory;

  document.getElementById("lessons-screen").classList.add("hidden");
  document.getElementById("theory-screen").classList.remove("hidden");
}

// Chuyển từ lý thuyết sang bài kiểm tra
function startQuizAfterTheory() {
  currentQuestions = questionsData[currentLessonKey] || [];
  if (currentQuestions.length === 0) {
    alert("Chưa có câu hỏi cho bài này!");
    backToLessons();
    return;
  }

  document.getElementById("quiz-title").textContent = currentLessonTitle;
  document.getElementById("progress").textContent = Câu hỏi 1 / ${currentQuestions.length};
  userAnswers = new Array(currentQuestions.length).fill(-1);
  renderQuiz();

  document.getElementById("theory-screen").classList.add("hidden");
  document.getElementById("quiz-screen").classList.remove("hidden");
}

function renderQuiz() {
  const container = document.getElementById("quiz-content");
  container.innerHTML = "";
  currentQuestions.forEach((q, i) => {
    const div = document.createElement("div");
    div.className = "question";
    div.innerHTML = <strong>Câu ${i+1}:</strong> ${q.q}<br>;
    q.options.forEach((opt, j) => {
      const label = document.createElement("label");
      label.className = "option";
      label.innerHTML = `
        <input type="radio" name="q${i}" value="${j}" ${userAnswers[i] === j ? "checked" : ""}>
        ${opt}
      `;
      label.querySelector("input").onchange = () => { userAnswers[i] = j; };
      div.appendChild(label);
    });
    container.appendChild(div);
  });
}

function checkQuiz() {
  let correct = 0;
  userAnswers.forEach((ans, i) => {
    if (ans === currentQuestions[i].answer) correct++;
  });
  const total = currentQuestions.length;
  alert(Bạn trả lời đúng ${correct}/${total} câu!\n${correct >= 8 ? "Hoàn thành bài học!" : "Cần làm lại để qua bài nhé!"});
  if (correct >= 8 && currentUser) {
    const data = JSON.parse(localStorage.getItem("user_" + currentUser));
    if (!data.progress) data.progress = {};
    data.progress[currentLessonKey] = true;
    localStorage.setItem("user_" + currentUser, JSON.stringify(data));
  }
}

function backToLessons() {
  document.getElementById("theory-screen").classList.add("hidden");
  document.getElementById("quiz-screen").classList.add("hidden");
  document.getElementById("lessons-screen").classList.remove("hidden");
}

function backToClasses() {
  document.getElementById("lessons-screen").classList.add("hidden");
  document.getElementById("class-screen").classList.remove("hidden");
}

function logout() {
  currentUser = null;
  document.getElementById("lessons-screen").classList.add("hidden");
  document.getElementById("quiz-screen").classList.add("hidden");
  document.getElementById("theory-screen").classList.add("hidden");
  document.getElementById("class-screen").classList.add("hidden");
  document.getElementById("auth-screen").classList.remove("hidden");
  showMessage("");
}
</script>
</body>
</html>
