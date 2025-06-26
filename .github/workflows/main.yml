<!DOCTYPE html>
<html lang="th">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Greek God Quiz</title>
  <link href="https://fonts.googleapis.com/css2?family=Sarabun&display=swap" rel="stylesheet">
  <style>
    :root {
      --bg-color: #ffffff;
      --text-color: #222;
      --card-color: #f4f4f4;
      --button-color: #ffffff;
      --button-border: #ccc;
      --button-hover: #007acc;
      --button-text-hover: #fff;
    }
    [data-theme="dark"] {
      --bg-color: #121212;
      --text-color: #f4f4f4;
      --card-color: #1e1e1e;
      --button-color: #2a2a2a;
      --button-border: #555;
      --button-hover: #2196f3;
      --button-text-hover: #fff;
    }
    body {
      font-family: 'Sarabun', sans-serif;
      background: var(--bg-color);
      color: var(--text-color);
      margin: 0;
      padding: 2rem;
      display: flex;
      flex-direction: column;
      align-items: center;
    }
    .container {
      max-width: 700px;
      width: 100%;
      background: var(--card-color);
      border-radius: 10px;
      padding: 2rem;
      box-shadow: 0 2px 10px rgba(0,0,0,0.1);
    }
    h1 {
      text-align: center;
    }
    .question-box {
      font-size: 1.1rem;
      margin: 1.5rem 0;
    }
    .answers {
      display: flex;
      flex-direction: column;
      gap: 0.5rem;
    }
    button {
      background: var(--button-color);
      border: 1px solid var(--button-border);
      padding: 0.75rem;
      border-radius: 6px;
      cursor: pointer;
      transition: 0.2s;
      color: var(--text-color);
    }
    button:hover {
      background: var(--button-hover);
      color: var(--button-text-hover);
    }
    #result {
      margin-top: 2rem;
      text-align: center;
    }
    #result img {
      max-width: 200px;
      margin: 1rem 0;
    }
    .top-controls {
      display: flex;
      justify-content: space-between;
      width: 100%;
      max-width: 700px;
      margin-bottom: 1rem;
    }
    .top-controls select, .top-controls button {
      padding: 0.5rem;
      border-radius: 5px;
      border: 1px solid var(--button-border);
      background: var(--button-color);
      color: var(--text-color);
    }
  </style>
</head>
<body data-theme="light">
  <div class="top-controls">
    <select id="langToggle">
      <option value="th">ภาษาไทย</option>
      <option value="en">English</option>
    </select>
    <button onclick="toggleTheme()">Toggle Theme</button>
  </div>
  <div class="container">
    <h1 id="title">คุณเป็นเทพเจ้าองค์ใดในตำนานกรีก?</h1>
    <div id="quiz-container">
      <div class="question-box" id="question-box"></div>
      <div class="answers" id="buttons"></div>
    </div>
    <div id="result"></div>
  </div>

  <script>
    const translations = {
      th: {
        title: "คุณเป็นเทพเจ้าองค์ใดในตำนานกรีก?",
        questions: [
          { q: "คุณคิดว่าคุณเป็นคนแบบไหน?", a: ["ฉลาด รอบคอบ", "เด็ดขาด มีอำนาจ", "ใจดี ดูแลคนอื่น", "เงียบขรึม รักสันโดษ"] },
          { q: "สถานที่โปรดของคุณคือที่ไหน?", a: ["ห้องสมุดหรือเวิร์คช็อป", "ป่าเขาหรือธรรมชาติ", "ชายทะเลหรือแม่น้ำ", "บนเวทีหรือคาเฟ่ศิลปะ"] },
          { q: "คุณมีข้อดีเด่นด้านใด?", a: ["ความกล้าหาญ", "ความรักและความเข้าใจ", "ความยุติธรรม", "การสื่อสาร"] },
        ],
        resultPrefix: "คุณเหมือนกับเทพเจ้า"
      },
      en: {
        title: "Which Greek God Are You?",
        questions: [
          { q: "How would you describe yourself?", a: ["Smart and thoughtful", "Decisive and powerful", "Kind and caring", "Quiet and reserved"] },
          { q: "What's your favorite place?", a: ["Library or workshop", "Forest or nature", "Beach or river", "Stage or art cafe"] },
          { q: "What is your greatest strength?", a: ["Bravery", "Love and empathy", "Justice", "Communication"] },
        ],
        resultPrefix: "You are like the god"
      }
    };

    const types = ["Athena", "Zeus", "Demeter", "Hades"];
    const godData = {
      Athena: { name: {th: "อธีนา", en: "Athena"}, img: "https://upload.wikimedia.org/wikipedia/commons/thumb/1/1f/Athena_Lemnia_Louvre_Ma5145_n1.jpg/300px-Athena_Lemnia_Louvre_Ma5145_n1.jpg" },
      Zeus: { name: {th: "ซูส", en: "Zeus"}, img: "https://upload.wikimedia.org/wikipedia/commons/thumb/4/4c/Zeus_smiting_typhon.jpg/300px-Zeus_smiting_typhon.jpg" },
      Demeter: { name: {th: "ดีมีเทอร์", en: "Demeter"}, img: "https://upload.wikimedia.org/wikipedia/commons/thumb/e/e1/Demeter_Altemps_Inv8596.jpg/300px-Demeter_Altemps_Inv8596.jpg" },
      Hades: { name: {th: "ฮาเดส", en: "Hades"}, img: "https://upload.wikimedia.org/wikipedia/commons/thumb/e/e4/Hades_with_Cerberus_-_Altemps_Inv8599.jpg/300px-Hades_with_Cerberus_-_Altemps_Inv8599.jpg" },
    };

    let lang = "th";
    const scores = {};
    let current = 0;

    function toggleTheme() {
      const body = document.body;
      body.dataset.theme = body.dataset.theme === "light" ? "dark" : "light";
    }

    document.getElementById("langToggle").addEventListener("change", (e) => {
      lang = e.target.value;
      document.getElementById("title").textContent = translations[lang].title;
      current = 0;
      Object.keys(scores).forEach(k => scores[k] = 0);
      showQuestion();
    });

    function showQuestion() {
      const q = translations[lang].questions[current];
      document.getElementById("question-box").textContent = q.q;
      const btns = document.getElementById("buttons");
      btns.innerHTML = "";
      q.a.forEach((txt, i) => {
        const btn = document.createElement("button");
        btn.textContent = txt;
        btn.onclick = () => selectAnswer(types[i]);
        btns.appendChild(btn);
      });
    }

    function selectAnswer(type) {
      scores[type] = (scores[type] || 0) + 1;
      current++;
      if (current < translations[lang].questions.length) {
        showQuestion();
      } else {
        showResult();
      }
    }

    function showResult() {
      let top = null, max = 0;
      for (let god in scores) {
        if (scores[god] > max) {
          max = scores[god];
          top = god;
        }
      }
      const g = godData[top];
      document.getElementById("quiz-container").style.display = "none";
      document.getElementById("result").innerHTML = `
        <h2>${translations[lang].resultPrefix} ${g.name[lang]}</h2>
        <img src="${g.img}" alt="${g.name[lang]}" />
      `;
    }

    showQuestion();
  </script>
</body>
</html>
