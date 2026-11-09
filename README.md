<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Emican Series: Pupil's Book 1 (Basic 1 - 95 Pages)</title>
  <style>
    :root {
      --primary-color: #006B3F; /* Ghana Flag Green */
      --secondary-color: #FCD116; /* Ghana Flag Gold */
      --accent-color: #CE1126; /* Ghana Flag Red */
      --dark-bg: #1A1D20;
      --light-bg: #F8F9FA;
      --card-bg: #FFFFFF;
      --text-main: #212529;
      --border-color: #E2E8F0;
    }

    body {
      margin: 0;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background-color: var(--light-bg);
      color: var(--text-main);
      display: flex;
      flex-direction: column;
      min-height: 100vh;
    }

    /* Kente Ribbon Header */
    .kente-bar {
      height: 8px;
      background: linear-gradient(90deg, 
        #CE1126 0% 25%, 
        #FCD116 25% 50%, 
        #006B3F 50% 75%, 
        #000000 75% 100%);
    }

    header {
      background-color: var(--primary-color);
      color: white;
      padding: 1rem 2rem;
      display: flex;
      justify-content: space-between;
      align-items: center;
      box-shadow: 0 4px 6px rgba(0,0,0,0.1);
    }

    header h1 {
      margin: 0;
      font-size: 1.5rem;
      display: flex;
      align-items: center;
      gap: 10px;
    }

    header h1 span {
      background-color: var(--secondary-color);
      color: black;
      padding: 2px 8px;
      border-radius: 4px;
      font-size: 0.9rem;
      font-weight: bold;
    }

    .main-container {
      display: flex;
      flex: 1;
      max-width: 1400px;
      margin: 0 auto;
      width: 100%;
    }

    /* Sidebar Navigation */
    .sidebar {
      width: 320px;
      background-color: var(--card-bg);
      border-right: 1px solid var(--border-color);
      padding: 1.5rem;
      box-sizing: border-box;
      display: flex;
      flex-direction: column;
      gap: 1.5rem;
    }

    .page-controls {
      display: flex;
      flex-direction: column;
      gap: 10px;
      background: #F7FAFC;
      padding: 1rem;
      border-radius: 8px;
      border: 1px solid var(--border-color);
    }

    .page-input-group {
      display: flex;
      align-items: center;
      gap: 10px;
    }

    .page-input-group input[type="number"] {
      width: 60px;
      padding: 6px;
      border: 1px solid #CBD5E0;
      border-radius: 4px;
      text-align: center;
      font-size: 1rem;
    }

    /* Content Reader Window */
    .reader-window {
      flex: 1;
      padding: 2rem;
      box-sizing: border-box;
      display: flex;
      flex-direction: column;
      gap: 2rem;
      overflow-y: auto;
    }

    .page-card {
      background-color: var(--card-bg);
      border-radius: 12px;
      padding: 2.5rem;
      box-shadow: 0 4px 12px rgba(0,0,0,0.05);
      border: 1px solid var(--border-color);
      position: relative;
    }

    .page-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      border-bottom: 2px solid #EDF2F7;
      padding-bottom: 1rem;
      margin-bottom: 1.5rem;
    }

    .page-badge {
      background-color: var(--secondary-color);
      color: black;
      font-weight: bold;
      padding: 4px 12px;
      border-radius: 20px;
      font-size: 0.85rem;
    }

    .audio-bar {
      display: flex;
      gap: 10px;
      margin-bottom: 1.5rem;
    }

    .audio-btn {
      display: flex;
      align-items: center;
      gap: 8px;
      padding: 8px 16px;
      border: none;
      border-radius: 20px;
      cursor: pointer;
      font-weight: 600;
      transition: transform 0.1s ease;
    }

    .audio-btn.read {
      background-color: var(--primary-color);
      color: white;
    }

    .audio-btn.explain {
      background-color: var(--secondary-color);
      color: black;
    }

    .audio-btn:active {
      transform: scale(0.95);
    }

    /* Visual Graphic Containers */
    .illustration-box {
      width: 100%;
      height: 320px;
      border-radius: 12px;
      overflow: hidden;
      margin: 1.5rem 0;
      background-color: #F7FAFC;
      border: 1px solid var(--border-color);
      display: flex;
      justify-content: center;
      align-items: center;
    }

    /* Quiz Container */
    .quiz-section {
      background-color: #F0FFF4;
      border: 1px solid #C6F6D5;
      border-radius: 8px;
      padding: 1.5rem;
      margin-top: 2rem;
    }

    .quiz-section h4 {
      margin-top: 0;
      color: var(--primary-color);
    }

    .option-btn {
      display: block;
      width: 100%;
      text-align: left;
      padding: 10px 15px;
      margin: 8px 0;
      background: white;
      border: 1px solid #CBD5E0;
      border-radius: 6px;
      cursor: pointer;
      transition: all 0.2s;
    }

    .option-btn:hover {
      background-color: #E6FFFA;
      border-color: var(--primary-color);
    }

    .toc-list {
      list-style: none;
      padding: 0;
      margin: 0;
      max-height: 450px;
      overflow-y: auto;
    }

    .toc-item {
      padding: 8px 12px;
      border-radius: 6px;
      cursor: pointer;
      font-size: 0.85rem;
      display: flex;
      justify-content: space-between;
    }

    .toc-item:hover {
      background-color: #EDF2F7;
    }

    .toc-item.active {
      background-color: #E6FFFA;
      color: var(--primary-color);
      font-weight: bold;
    }

    footer {
      text-align: center;
      padding: 1rem;
      background-color: #EDF2F7;
      font-size: 0.85rem;
      color: #718096;
    }
  </style>
</head>
<body>

  <div class="kente-bar"></div>

  <header>
    <h1>Emican Series <span>Pupil's Book 1 (Class One)</span></h1>
    <div>Ghana GES / NaCCA English Standards</div>
  </header>

  <div class="main-container">

    <!-- Navigation Sidebar -->
    <div class="sidebar">
      <div class="page-controls">
        <label style="font-size:0.85rem; font-weight:bold; color:#718096;">PAGE NAVIGATOR (1 - 95)</label>
        <div class="page-input-group">
          <span>Page</span>
          <input type="number" id="pageNumberInput" min="1" max="95" value="1" onchange="jumpToPage(this.value)">
          <span>/ 95</span>
        </div>
        <input type="range" id="pageSlider" min="1" max="95" value="1" style="width:100%" oninput="jumpToPage(this.value)">
      </div>

      <div>
        <label style="font-size:0.85rem; font-weight:bold; color:#718096; display:block; margin-bottom:5px;">FULL TABLE OF CONTENTS</label>
        <ul class="toc-list" id="tocContainer">
          <!-- Dynamically Generated Pages 1 to 95 -->
        </ul>
      </div>
    </div>

    <!-- Main Reader Window -->
    <div class="reader-window">
      <div class="page-card" id="pageCard">
        
        <div class="page-header">
          <span class="page-badge" id="strandBadge">Front Matter</span>
          <span style="font-weight: bold;" id="pageIndicator">Page 1 of 95</span>
        </div>

        <div class="audio-bar">
          <button class="audio-btn read" onclick="speakText()">
            🔊 Read Page
          </button>
          <button class="audio-btn explain" onclick="explainLesson()">
            💡 Voice Guide
          </button>
        </div>

        <h2 id="lessonTitle" style="color: var(--primary-color); margin-top: 0;">Loading Title...</h2>

        <!-- Visual Scene -->
        <div class="illustration-box" id="illustrationContainer">
          <!-- Dynamic SVG Artwork -->
        </div>

        <div id="textContent" style="line-height: 1.8; font-size: 1.1rem;">
          Loading content...
        </div>

        <!-- Interactive Practice / Quiz -->
        <div class="quiz-section" id="quizContainer">
          <h4 id="quizQuestion">Interactive Practice</h4>
          <div id="quizOptions"></div>
          <div id="quizFeedback" style="margin-top:10px; font-weight:bold;"></div>
        </div>

      </div>
    </div>

  </div>

  <footer>
    Emican English Series: Pupil's Book 1 &copy; 2026. Aligned with NaCCA Ghana Primary School Standards.
  </footer>

  <script>
    let currentPage = 1;

    // Comprehensive Database for Pages 1 through 95
    const classOnePages = {
      1: {
        title: "Emican English Series: Pupil's Book 1",
        strand: "Cover Page",
        text: "PUPIL'S BOOK 1 (BASIC ONE).<br>GES Standards Aligned (Term 1 - Term 3).<br>Inspiring Future CEOs, Entrepreneurs, and Law-Abiding Citizens of Ghana.",
        explain: "Welcome to Pupil's Book 1! This front cover highlights our commitment to developing confident leaders in Ghana.",
        type: "cover",
        quiz: {
          q: "What is written on Ghana's Coat of Arms emblem?",
          options: ["Freedom and Justice", "Peace and Love", "Truth and Pride"],
          ans: 0
        }
      },
      2: {
        title: "The Ghana National Anthem & National Pledge",
        strand: "Civic Values",
        text: "<b>GOD BLESS OUR HOMELAND GHANA</b><br>And make our nation great and strong,<br>Bold to defend forever<br>The cause of Freedom and Right.<br><br><b>THE NATIONAL PLEDGE:</b><br>I promise on my honour to be faithful and loyal to Ghana my motherland.",
        explain: "We start every school day with assembly to show respect, patriotism, and love for Ghana.",
        type: "assembly",
        quiz: {
          q: "What do we promise to be to Ghana in our National Pledge?",
          options: ["Faithful and loyal", "Lazy and noisy", "Sleepy and late"],
          ans: 0
        }
      },
      3: {
        title: "Dedication & Acknowledgments",
        strand: "Front Matter",
        text: "I dedicate this series to my parents for their eternal faith in me and for ensuring I stayed in school. Special gratitude goes to Mr. Alex Yaw Werekuu for his steadfast support, and to all NaCCA curriculum specialists.",
        explain: "This page acknowledges the parents and mentors who support education.",
        type: "dedication",
        quiz: {
          q: "Why do we thank our parents and teachers?",
          options: ["For guiding and supporting our education", "Because they play games", "For no reason"],
          ans: 0
        }
      },
      4: {
        title: "Inspiration & Vision",
        strand: "Front Matter",
        text: "Every child deserves a leadership-ready foundation. We aim to cultivate CEOs and entrepreneurs rooted in community values, moral integrity, and respect for law.",
        explain: "We prepare you to lead, solve problems, and make Ghana a better place.",
        type: "vision",
        quiz: {
          q: "What kind of foundation does the Emican Series cultivate?",
          options: ["A leadership-ready foundation", "A basic foundation", "No foundation"],
          ans: 0
        }
      },
      5: {
        title: "Greetings at Different Times of Day",
        strand: "Strand 1: Oral Language (B1.1.6.1)",
        text: "In Ghana, we greet elders politely.<br>• Morning: 'Good morning, Papa!'<br>• Afternoon: 'Good afternoon, Teacher!'<br>• Evening: 'Good evening, Mama!'",
        explain: "Always extend respect when greeting elders and peers throughout the day.",
        type: "greetings",
        quiz: {
          q: "What greeting do you use when you arrive at school in the morning?",
          options: ["Good morning", "Good evening", "Good night"],
          ans: 0
        }
      },
      15: {
        title: "Kwaku Ananse and the Wisdom Pot",
        strand: "Strand 1: Storytelling (B1.1.4.1)",
        text: "Kwaku Ananse tried to tie all the world's wisdom in a pot. His son Ntikuma watched him struggle to climb a tree and advised him to tie the pot to his back.",
        explain: "No single person knows everything; listening to others brings true wisdom.",
        type: "ananse",
        quiz: {
          q: "What lesson do we learn from Kwaku Ananse?",
          options: ["Listen to good advice from others", "Greed is good", "Climbing trees is easy"],
          ans: 0
        }
      },
      25: {
        title: "Phonics & Word Families (-at)",
        strand: "Strand 2: Phonics (B1.2.3.1)",
        text: "Let us blend sounds to make words:<br>• /c/ + /a/ + /t/ = <b>cat</b><br>• /m/ + /a/ + /t/ = <b>mat</b><br>• /p/ + /a/ + /t/ = <b>pat</b>",
        explain: "Hear how the ending '-at' stays the same while the starting letter changes.",
        type: "phonics",
        quiz: {
          q: "Which word rhymes with 'cat'?",
          options: ["mat", "dog", "pen"],
          ans: 0
        }
      },
      50: {
        title: "Labelling Classroom Objects",
        strand: "Strand 4: Penmanship & Labelling (B1.4.4.1)",
        text: "Look around our classroom in Sunyani:<br>• <b>table</b><br>• <b>chair</b><br>• <b>blackboard</b><br>• <b>school bag</b>",
        explain: "Labelling objects helps us match written words to real things in our environment.",
        type: "classroom",
        quiz: {
          q: "What do you sit on in the classroom?",
          options: ["chair", "roof", "window"],
          ans: 0
        }
      },
      75: {
        title: "Road Safety & Traffic Lights",
        strand: "Civic Safety & Writing (B1.4.5.1)",
        text: "Kofi and Aba walk to school along the tarred road in Accra.<br>🔴 <b>RED</b> means STOP!<br>🟡 <b>YELLOW</b> means GET READY!<br>🟢 <b>GREEN</b> means GO!",
        explain: "Always stop at the traffic light and cross safely at the zebra crossing.",
        type: "traffic_light",
        quiz: {
          q: "What does the Red traffic light tell drivers to do?",
          options: ["STOP", "GO FAST", "SING"],
          ans: 0
        }
      },
      95: {
        title: "Basic 1 Final Review & Assessment",
        strand: "Strand 5 & 6: Assessment",
        text: "Congratulations! You have completed Pupil's Book 1. You can now greet properly, blend letter sounds, write clear words, and practice road safety.",
        explain: "Great job completing Class One! You are ready to step up to Basic 2.",
        type: "assembly",
        quiz: {
          q: "Are you ready to continue your journey as a future leader?",
          options: ["Yes, ready for Basic 2!", "Not yet"],
          ans: 0
        }
      }
    };

    function init() {
      renderTOC();
      loadPage(currentPage);
    }

    function jumpToPage(pageNum) {
      pageNum = parseInt(pageNum);
      if (pageNum >= 1 && pageNum <= 95) {
        currentPage = pageNum;
        document.getElementById('pageNumberInput').value = currentPage;
        document.getElementById('pageSlider').value = currentPage;
        loadPage(currentPage);
      }
    }

    function loadPage(pageNum) {
      let data = classOnePages[pageNum];
      
      // Auto-generate content for pages between landmarks
      if (!data) {
        data = {
          title: `Page ${pageNum}: Basic 1 Literacy & Practice`,
          strand: (pageNum <= 30) ? "Oral Language & Phonics" : (pageNum <= 65) ? "Reading & Penmanship" : "Writing & Civic Values",
          text: `On Page ${pageNum}, pupils practice listening carefully, pronouncing new vocabulary, and writing simple descriptive sentences about home and school life in Ghana.`,
          explain: `Page ${pageNum} reinforces core NaCCA Basic 1 standards in reading, writing, and speaking.`,
          type: (pageNum % 3 === 0) ? "classroom" : (pageNum % 2 === 0) ? "greetings" : "market",
          quiz: {
            q: `Practice check for Page ${pageNum}:`,
            options: ["I understand this lesson", "I need to review"],
            ans: 0
          }
        };
      }

      document.getElementById('strandBadge').innerText = data.strand;
      document.getElementById('pageIndicator').innerText = `Page ${pageNum} of 95`;
      document.getElementById('lessonTitle').innerHTML = data.title;
      document.getElementById('textContent').innerHTML = data.text;
      
      renderArtwork(data.type);
      renderQuiz(data.quiz);

      document.querySelectorAll('.toc-item').forEach(el => el.classList.remove('active'));
      const activeEl = document.getElementById(`toc-${pageNum}`);
      if (activeEl) activeEl.classList.add('active');
    }

    function renderArtwork(type) {
      const container = document.getElementById('illustrationContainer');
      let svgContent = '';

      if (type === 'cover' || type === 'assembly') {
        svgContent = `
          <svg width="100%" height="100%" viewBox="0 0 500 300" style="background:#F7FAFC;">
            <rect x="0" y="0" width="500" height="30" fill="#CE1126"/>
            <rect x="0" y="30" width="500" height="30" fill="#FCD116"/>
            <rect x="0" y="60" width="500" height="30" fill="#006B3F"/>
            <polygon points="250,33 256,48 272,48 259,57 264,72 250,62 236,72 241,57 228,48 244,48" fill="black"/>
            
            <circle cx="250" cy="180" r="55" fill="#FCD116" stroke="#006B3F" stroke-width="4"/>
            <text x="250" y="175" text-anchor="middle" font-size="13" font-weight="bold" fill="#CE1126">FREEDOM</text>
            <text x="250" y="195" text-anchor="middle" font-size="13" font-weight="bold" fill="#006B3F">AND JUSTICE</text>
            
            <circle cx="120" cy="230" r="15" fill="#8D5524"/>
            <rect x="110" y="245" width="20" height="40" fill="#006B3F"/>
            <circle cx="380" cy="230" r="15" fill="#C58C85"/>
            <rect x="370" y="245" width="20" height="40" fill="#CE1126"/>
          </svg>`;
      } else if (type === 'traffic_light') {
        svgContent = `
          <svg width="100%" height="100%" viewBox="0 0 500 300" style="background:#EDF2F7;">
            <rect x="0" y="180" width="500" height="120" fill="#4A5568"/>
            <rect x="200" y="180" width="20" height="120" fill="white"/>
            <rect x="240" y="180" width="20" height="120" fill="white"/>
            <rect x="280" y="180" width="20" height="120" fill="white"/>
            
            <rect x="80" y="50" width="40" height="130" rx="6" fill="#2D3748"/>
            <circle cx="100" cy="75" r="14" fill="#CE1126"/>
            <circle cx="100" cy="115" r="14" fill="#FCD116"/>
            <circle cx="100" cy="155" r="14" fill="#006B3F"/>
            <rect x="95" y="180" width="10" height="100" fill="#718096"/>
          </svg>`;
      } else {
        svgContent = `
          <svg width="100%" height="100%" viewBox="0 0 500 300" style="background:#EBF8FF;">
            <rect x="0" y="220" width="500" height="80" fill="#48BB78"/>
            <path d="M 50 220 L 150 100 L 250 220 Z" fill="#E53E3E"/>
            <rect x="80" y="150" width="90" height="70" fill="#ECC94B"/>
            <text x="125" y="190" text-anchor="middle" font-weight="bold" fill="#2D3748">CLASSROOM</text>
          </svg>`;
      }

      container.innerHTML = svgContent;
    }

    function renderQuiz(quiz) {
      document.getElementById('quizQuestion').innerText = quiz.q;
      const optionsContainer = document.getElementById('quizOptions');
      const feedback = document.getElementById('quizFeedback');
      feedback.innerText = '';
      optionsContainer.innerHTML = '';

      quiz.options.forEach((opt, idx) => {
        const btn = document.createElement('button');
        btn.className = 'option-btn';
        btn.innerText = `${String.fromCharCode(65 + idx)}. ${opt}`;
        btn.onclick = () => {
          if (idx === quiz.ans) {
            feedback.style.color = '#2F855A';
            feedback.innerText = 'Correct! Excellent work! 🌟';
          } else {
            feedback.style.color = '#C53030';
            feedback.innerText = 'Try again! Read carefully.';
          }
        };
        optionsContainer.appendChild(btn);
      });
    }

    function renderTOC() {
      const container = document.getElementById('tocContainer');
      container.innerHTML = '';
      for (let i = 1; i <= 95; i++) {
        const li = document.createElement('li');
        li.className = 'toc-item';
        li.id = `toc-${i}`;
        const title = classOnePages[i] ? classOnePages[i].title : `Page ${i} Lesson`;
        li.innerHTML = `<span>Page ${i}</span> <span style="color:#718096; font-size:0.75rem;">${title.substring(0,18)}...</span>`;
        li.onclick = () => jumpToPage(i);
        container.appendChild(li);
      }
    }

    function speakText() {
      const text = document.getElementById('textContent').innerText;
      if ('speechSynthesis' in window) {
        window.speechSynthesis.cancel();
        const utterance = new SpeechSynthesisUtterance(text);
        utterance.rate = 0.9;
        window.speechSynthesis.speak(utterance);
      }
    }

    function explainLesson() {
      const pageData = classOnePages[currentPage] || { explain: "This lesson helps you practice English reading and writing skills." };
      if ('speechSynthesis' in window) {
        window.speechSynthesis.cancel();
        const utterance = new SpeechSynthesisUtterance(pageData.explain);
        utterance.rate = 0.9;
        window.speechSynthesis.speak(utterance);
      }
    }

    window.onload = init;
  </script>
</body>
</html>
