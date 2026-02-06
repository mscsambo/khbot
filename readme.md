<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Math Quiz (Levels + Timer + Sounds + Voice)</title>
  <style>
    body{
      font-family:system-ui, Arial, sans-serif;
      background:#f6f7fb;
      margin:0; padding:24px;
      min-height:100vh;
      display:grid; place-items:center;
    }
    .card{
      width:min(720px, 100%);
      background:#fff;
      border-radius:16px;
      padding:20px;
      box-shadow:0 10px 30px rgba(0,0,0,.08);
    }
    .top{
      display:flex;
      gap:12px;
      justify-content:space-between;
      flex-wrap:wrap;
      align-items:center;
      margin-bottom:10px;
    }
    .pill{
      display:inline-flex;
      gap:8px;
      align-items:center;
      padding:8px 12px;
      border-radius:999px;
      background:#f1f3ff;
      border:1px solid #e6e8f0;
      font-weight:800;
      font-size:13px;
      color:#27304a;
    }
    .q{
      font-size:44px;
      font-weight:900;
      text-align:center;
      margin:16px 0 16px;
    }
    .choices{
      display:grid;
      grid-template-columns: repeat(3, 1fr);
      gap:12px;
    }
    button.choice{
      border:2px solid #e6e8f0;
      background:#fafbff;
      border-radius:12px;
      padding:16px 10px;
      font-size:22px;
      font-weight:900;
      cursor:pointer;
      transition: transform .05s ease, border-color .15s ease, background .15s ease;
    }
    button.choice:active{ transform:scale(.98); }
    button.choice:hover{ border-color:#cfd6ff; background:#f3f5ff; }

    .msg{
      margin-top:14px;
      padding:12px;
      border-radius:12px;
      text-align:center;
      font-weight:900;
      min-height:22px;
      border:1px solid transparent;
    }
    .msg.ok{ background:#e9fbef; color:#146c2e; border-color:#bfe9cc; }
    .msg.bad{ background:#ffecec; color:#8a1f1f; border-color:#ffd0d0; }
    .msg.info{ background:#eef2ff; color:#2b3a75; border-color:#d6ddff; }

    .bar-wrap{
      margin-top:10px;
      height:12px;
      background:#eef0f6;
      border-radius:999px;
      overflow:hidden;
      border:1px solid #e6e8f0;
    }
    .bar{
      height:100%;
      width:100%;
      background:#6a5cff;
      transition: width .2s linear;
    }

    .row{
      display:flex;
      justify-content:space-between;
      align-items:center;
      margin-top:14px;
      gap:10px;
      flex-wrap:wrap;
    }
    .btn{
      border:1px solid #e6e8f0;
      background:#fff;
      border-radius:10px;
      padding:10px 12px;
      cursor:pointer;
      font-weight:900;
    }
    .btn:hover{ background:#f7f7fb; }
    .btn.danger{
      background:#fff5f5;
      border-color:#ffd0d0;
    }
    .tog{
      display:flex; gap:8px; align-items:center;
      font-weight:800; font-size:13px; color:#344054;
    }
    input[type="checkbox"]{ width:18px; height:18px; }
    select{
      border:1px solid #e6e8f0;
      border-radius:10px;
      padding:10px 12px;
      font-weight:900;
      background:#fff;
    }
    .small{ color:#667085; font-size:13px; font-weight:800; }
    .disabled { opacity:.55; pointer-events:none; }
  </style>
</head>
<body>
  <div class="card">
    <div class="top">
      <div class="pill">Level: <span id="level">1</span></div>
      <div class="pill">Ops: <span id="opsText">+</span></div>
      <div class="pill">Time: <span id="timeLeft">10</span>s</div>
      <div class="pill">Score: <span id="score">0</span> / <span id="count">0</span></div>
    </div>

    <div class="q" id="question">3 + 7 = ?</div>

    <div class="choices" id="choices"></div>

    <div class="msg info" id="message">Pick the correct answer</div>

    <div class="bar-wrap" aria-label="timer progress">
      <div class="bar" id="bar"></div>
    </div>

    <div class="row">
      <div class="tog">
        <input type="checkbox" id="soundToggle" checked />
        <label for="soundToggle">Beep sounds</label>
      </div>

      <div class="tog">
        <input type="checkbox" id="voiceToggle" checked />
        <label for="voiceToggle">Voice</label>
      </div>

      <div class="tog">
        <label for="voiceSelect">Voice:</label>
        <select id="voiceSelect" title="Choose a voice"></select>
      </div>

      <button class="btn" id="nextBtn" type="button">Next</button>
      <button class="btn danger" id="resetBtn" type="button">Reset</button>
    </div>

    <div class="row">
      <div class="small">
        Level up every <span id="levelUpEvery">5</span> correct answers •
        Level 1: + • Level 2: +/− • Level 3+: +/−/×
      </div>
    </div>
  </div>

  <script>
    // -------------------------------
    // Helpers
    // -------------------------------
    function randInt(min, max) {
      return Math.floor(Math.random() * (max - min + 1)) + min;
    }
    function shuffle(arr) {
      for (let i = arr.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [arr[i], arr[j]] = [arr[j], arr[i]];
      }
      return arr;
    }

    // -------------------------------
    // Sounds (WebAudio, no files)
    // -------------------------------
    let audioCtx = null;
    function ensureAudio() {
      if (!audioCtx) audioCtx = new (window.AudioContext || window.webkitAudioContext)();
    }
    function beep(freq, durationMs, type = "sine", gain = 0.06) {
      if (!document.getElementById("soundToggle").checked) return;

      ensureAudio();
      const ctx = audioCtx;
      if (ctx.state === "suspended") ctx.resume();

      const osc = ctx.createOscillator();
      const g = ctx.createGain();

      osc.type = type;
      osc.frequency.value = freq;
      g.gain.value = gain;

      osc.connect(g);
      g.connect(ctx.destination);

      osc.start();
      setTimeout(() => osc.stop(), durationMs);
    }
    function sfxCorrect() {
      beep(880, 90, "triangle", 0.07);
      setTimeout(() => beep(1175, 110, "triangle", 0.07), 90);
    }
    function sfxWrong() {
      beep(220, 130, "sawtooth", 0.06);
      setTimeout(() => beep(180, 160, "sawtooth", 0.05), 90);
    }
    function sfxTimeUp() {
      beep(300, 140, "square", 0.05);
      setTimeout(() => beep(260, 180, "square", 0.05), 120);
      setTimeout(() => beep(220, 220, "square", 0.05), 260);
    }

    // -------------------------------
    // Voice (SpeechSynthesis)
    // -------------------------------
    const voiceToggle = document.getElementById("voiceToggle");
    const voiceSelect = document.getElementById("voiceSelect");
    let voices = [];

    function loadVoices() {
      voices = window.speechSynthesis ? window.speechSynthesis.getVoices() : [];
      voiceSelect.innerHTML = "";

      if (!voices.length) {
        const opt = document.createElement("option");
        opt.value = "";
        opt.textContent = "No voices found";
        voiceSelect.appendChild(opt);
        voiceSelect.disabled = true;
        return;
      }

      voiceSelect.disabled = false;

      // Prefer English voices first (works well for "Correct / Try again")
      const preferred = voices
        .slice()
        .sort((a,b) => {
          const ae = (a.lang || "").toLowerCase().startsWith("en") ? 0 : 1;
          const be = (b.lang || "").toLowerCase().startsWith("en") ? 0 : 1;
          return ae - be;
        });

      preferred.forEach((v, idx) => {
        const opt = document.createElement("option");
        opt.value = String(voices.indexOf(v)); // store original index
        opt.textContent = `${v.name} (${v.lang})`;
        voiceSelect.appendChild(opt);
        if (idx === 0) voiceSelect.value = opt.value; // default
      });
    }

    // Some browsers load voices async
    if ("speechSynthesis" in window) {
      loadVoices();
      window.speechSynthesis.onvoiceschanged = loadVoices;
    } else {
      voiceToggle.checked = false;
      voiceToggle.disabled = true;
      voiceSelect.disabled = true;
    }

    function speak(text) {
      if (!voiceToggle.checked) return;
      if (!("speechSynthesis" in window)) return;

      // stop previous speech so it feels responsive
      window.speechSynthesis.cancel();

      const u = new SpeechSynthesisUtterance(text);
      const selectedIndex = parseInt(voiceSelect.value, 10);
      if (!Number.isNaN(selectedIndex) && voices[selectedIndex]) {
        u.voice = voices[selectedIndex];
      }
      u.rate = 1.0;
      u.pitch = 1.0;
      u.volume = 1.0;

      window.speechSynthesis.speak(u);
    }

    // -------------------------------
    // UI elements
    // -------------------------------
    const elQ = document.getElementById("question");
    const elChoices = document.getElementById("choices");
    const elMsg = document.getElementById("message");
    const elScore = document.getElementById("score");
    const elCount = document.getElementById("count");
    const elLevel = document.getElementById("level");
    const elOpsText = document.getElementById("opsText");
    const elTimeLeft = document.getElementById("timeLeft");
    const elBar = document.getElementById("bar");
    const nextBtn = document.getElementById("nextBtn");
    const resetBtn = document.getElementById("resetBtn");

    // -------------------------------
    // Game state
    // -------------------------------
    let currentAnswer = 0;
    let score = 0;           // correct answers
    let count = 0;           // questions shown
    let level = 1;

    const LEVEL_UP_EVERY = 5;
    document.getElementById("levelUpEvery").textContent = LEVEL_UP_EVERY;

    // Timer
    let timerId = null;
    let timeTotal = 10;
    let timeLeft = 10;
    let locked = false;

    function setMessage(text, type) {
      elMsg.textContent = text || "";
      elMsg.className = "msg" + (type ? " " + type : "");
    }

    function updateStats() {
      elScore.textContent = String(score);
      elCount.textContent = String(count);
      elLevel.textContent = String(level);
      elOpsText.textContent = getOpsForLevel(level).join(" ");
    }

    function getOpsForLevel(lv) {
      // Level rules:
      // 1 => [+]
      // 2 => [+, -]
      // 3+ => [+, -, ×]
      if (lv <= 1) return ["+"];
      if (lv === 2) return ["+", "−"];
      return ["+", "−", "×"];
    }

    function getTimeForLevel(lv) {
      // Faster as level increases, min 3 seconds
      return Math.max(3, 11 - lv);
    }

    function stopTimer() {
      if (timerId) clearInterval(timerId);
      timerId = null;
    }

    function startTimer() {
      stopTimer();
      timeTotal = getTimeForLevel(level);
      timeLeft = timeTotal;
      elTimeLeft.textContent = String(timeLeft);
      elBar.style.width = "100%";

      timerId = setInterval(() => {
        timeLeft -= 1;
        if (timeLeft < 0) timeLeft = 0;

        elTimeLeft.textContent = String(timeLeft);
        elBar.style.width = ((timeLeft / timeTotal) * 100) + "%";

        if (timeLeft <= 0) onTimeUp();
      }, 1000);
    }

    function lockChoices(lock) {
      locked = lock;
      if (lock) elChoices.classList.add("disabled");
      else elChoices.classList.remove("disabled");
    }

    function onTimeUp() {
      stopTimer();
      lockChoices(true);
      setMessage("⏰ Time’s up! Click Next for a new question.", "bad");
      sfxTimeUp();
      speak("Time's up!");
    }

    function maybeLevelUp() {
      const newLevel = 1 + Math.floor(score / LEVEL_UP_EVERY);
      if (newLevel !== level) {
        level = newLevel;
        updateStats();
        setMessage(`🔥 Level up! You are now Level ${level}`, "info");
        sfxCorrect();
        speak(`Level up! Level ${level}`);
      }
    }

    // -------------------------------
    // Question generation (answers under 20)
    // -------------------------------
    function generateQuestion() {
      // ensure audio context can start (some browsers need user action)
      ensureAudio();

      lockChoices(false);
      setMessage("Pick the correct answer", "info");

      const ops = getOpsForLevel(level);
      const op = ops[randInt(0, ops.length - 1)];

      // Difficulty scaling: increase number range as level rises, still keep answer 0..19
      const maxN = Math.min(19, 8 + level * 3);

      let a, b, ans, symbol;

      if (op === "+") {
        symbol = "+";
        a = randInt(0, maxN);
        b = randInt(0, Math.min(maxN, 19 - a));
        ans = a + b;
      } else if (op === "−") {
        symbol = "−";
        a = randInt(0, maxN);
        b = randInt(0, a); // non-negative result
        ans = a - b;
      } else {
        // × (multiplication) but keep answer under 20
        symbol = "×";
        // Pick an answer 0..19 then choose a factor pair
        ans = randInt(0, 19);

        // Collect factor pairs (a*b = ans) with small numbers
        const pairs = [];
        for (let x = 0; x <= 19; x++) {
          if (x === 0 && ans !== 0) continue;
          if (x === 0 && ans === 0) {
            pairs.push([0, randInt(0, 9)]);
            continue;
          }
          if (x > 0 && ans % x === 0) {
            const y = ans / x;
            if (y <= 19) pairs.push([x, y]);
          }
        }

        // Prefer non-trivial pairs (avoid too many 1s) if possible
        const filtered = pairs.filter(p => p[0] !== 1 && p[1] !== 1);
        const use = (filtered.length ? filtered : pairs);
        const pick = use[randInt(0, use.length - 1)];
        a = pick[0];
        b = pick[1];
      }

      currentAnswer = ans;
      count += 1;
      updateStats();

      elQ.textContent = `${a} ${symbol} ${b} = ?`;

      // Create 3 options: correct + 2 unique wrong answers (0..19)
      const options = new Set([currentAnswer]);
      while (options.size < 3) {
        const delta = randInt(-(6 + level), (6 + level));
        const candidate = currentAnswer + delta;
        if (candidate >= 0 && candidate <= 19) options.add(candidate);
      }

      renderChoices(shuffle(Array.from(options)));
      startTimer();
    }

    function renderChoices(list) {
      elChoices.innerHTML = "";
      list.forEach((value) => {
        const btn = document.createElement("button");
        btn.type = "button";
        btn.className = "choice";
        btn.textContent = value;

        btn.addEventListener("click", () => {
          if (locked) return;

          if (value === currentAnswer) {
            stopTimer();
            lockChoices(true);

            score += 1;
            updateStats();
            setMessage("🎉 Correct! Great job!", "ok");
            sfxCorrect();
            speak("Correct!");

            maybeLevelUp();

            // auto-next
            setTimeout(generateQuestion, 700);
          } else {
            setMessage("❌ Wrong answer. Try again!", "bad");
            sfxWrong();
            speak("Try again.");
            // allow reselect
          }
        });

        elChoices.appendChild(btn);
      });
    }

    function resetGame() {
      stopTimer();
      score = 0;
      count = 0;
      level = 1;
      updateStats();
      setMessage("Pick the correct answer", "info");
      generateQuestion();
    }

    nextBtn.addEventListener("click", generateQuestion);
    resetBtn.addEventListener("click", resetGame);

    // Start
    resetGame();
  </script>
</body>
</html>
