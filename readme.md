<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1,viewport-fit=cover" />
  <title>Math Quiz – Clean Mobile + Gradient + Dark Mode + US/Microsoft Voices</title>

  <style>
    :root{
      --bg1:#6a5cff;
      --bg2:#22c55e;
      --card:#ffffffcc;
      --cardSolid:#ffffff;
      --ink:#0f172a;
      --muted:#475569;
      --border:#e6e8f0;
      --pill:#f1f3ff;
      --accent:#6a5cff;

      --okbg:#e9fbef; --ok:#146c2e;
      --badbg:#ffecec; --bad:#8a1f1f;
      --infobg:#eef2ff; --info:#2b3a75;
    }

    /* Dark mode tokens */
    body.dark{
      --bg1:#0f172a;
      --bg2:#111827;
      --card:#0b1220cc;
      --cardSolid:#0b1220;
      --ink:#e5e7eb;
      --muted:#aab2c0;
      --border:#1f2a44;
      --pill:#0f1a33;
      --accent:#8b5cf6;

      --okbg:#0b2a18; --ok:#7dffb0;
      --badbg:#2a0b0b; --bad:#ff9a9a;
      --infobg:#0b1430; --info:#a7b6ff;
    }

    *{box-sizing:border-box}
    html,body{height:100%}
    body{
      margin:0;
      font-family:system-ui, -apple-system, Segoe UI, Roboto, Arial, sans-serif;
      color:var(--ink);
      padding:16px;
      display:grid;
      place-items:center;
      /* Gradient background */
      background:
        radial-gradient(1200px 600px at 20% 10%, color-mix(in oklab, var(--bg1) 70%, transparent), transparent 60%),
        radial-gradient(1200px 700px at 80% 30%, color-mix(in oklab, var(--bg2) 55%, transparent), transparent 60%),
        linear-gradient(135deg, var(--bg1), var(--bg2));
      background-attachment: fixed;
    }

    .card{
      width:min(860px, 100%);
      background:var(--card);
      border:1px solid color-mix(in oklab, var(--border) 80%, transparent);
      border-radius:20px;
      box-shadow: 0 18px 60px rgba(0,0,0,.22);
      backdrop-filter: blur(10px);
      -webkit-backdrop-filter: blur(10px);
      padding:16px;
    }

    .top{
      display:flex;
      gap:10px;
      justify-content:space-between;
      align-items:center;
      flex-wrap:wrap;
      margin-bottom:10px;
    }

    .pill{
      display:inline-flex;
      gap:8px;
      align-items:center;
      padding:8px 12px;
      border-radius:999px;
      background:var(--pill);
      border:1px solid var(--border);
      font-weight:900;
      font-size:13px;
      user-select:none;
      white-space:nowrap;
    }
    .pill .k{opacity:.8; font-weight:800; color:var(--muted)}

    /* Question: always fit on mobile */
    .q{
      text-align:center;
      font-weight:1000;
      letter-spacing:.3px;
      margin:12px 0 8px;
      font-size: clamp(34px, 8.5vw, 60px);
      line-height: 1.1;
      word-break: break-word;
      overflow-wrap: anywhere;
      padding-inline: 6px;
    }

    .subrow{
      display:flex;
      justify-content:center;
      gap:10px;
      flex-wrap:wrap;
      margin: 6px 0 10px;
    }
    .badge{
      display:inline-flex;
      gap:8px;
      align-items:center;
      padding:8px 12px;
      border-radius:14px;
      border:1px solid var(--border);
      background: color-mix(in oklab, var(--cardSolid) 92%, transparent);
      font-weight:1000;
      user-select:none;
      white-space:nowrap;
    }

    .choices{
      display:grid;
      grid-template-columns: repeat(3, 1fr);
      gap:12px;
      margin-top: 10px;
    }
    button.choice{
      border:2px solid var(--border);
      background: color-mix(in oklab, var(--cardSolid) 92%, transparent);
      border-radius:18px;
      padding:16px 10px;
      font-weight:1000;
      font-size: clamp(20px, 5vw, 30px);
      cursor:pointer;
      transition: transform .06s ease, border-color .15s ease, background .15s ease;
    }
    button.choice:hover{
      background: color-mix(in oklab, var(--accent) 10%, var(--cardSolid));
      border-color: color-mix(in oklab, var(--accent) 45%, var(--border));
    }
    button.choice:active{ transform:scale(.985); }

    .msg{
      margin-top:12px;
      padding:12px;
      border-radius:14px;
      text-align:center;
      font-weight:1000;
      border:1px solid transparent;
      min-height:22px;
      user-select:none;
    }
    .msg.ok{ background:var(--okbg); color:var(--ok); border-color: color-mix(in oklab, var(--ok) 25%, transparent); }
    .msg.bad{ background:var(--badbg); color:var(--bad); border-color: color-mix(in oklab, var(--bad) 25%, transparent); }
    .msg.info{ background:var(--infobg); color:var(--info); border-color: color-mix(in oklab, var(--info) 20%, transparent); }

    .bar-wrap{
      margin-top:10px;
      height:14px;
      background: color-mix(in oklab, var(--cardSolid) 85%, transparent);
      border-radius:999px;
      overflow:hidden;
      border:1px solid var(--border);
    }
    .bar{
      height:100%;
      width:100%;
      background: linear-gradient(90deg, var(--accent), color-mix(in oklab, var(--accent) 40%, #22c55e));
      transition: width .2s linear;
    }

    .controls{
      margin-top:14px;
      display:flex;
      gap:10px;
      justify-content:space-between;
      align-items:center;
      flex-wrap:wrap;
    }

    .tog{
      display:flex;
      gap:8px;
      align-items:center;
      padding:10px 12px;
      border-radius:14px;
      border:1px solid var(--border);
      background: color-mix(in oklab, var(--cardSolid) 92%, transparent);
      font-weight:900;
      font-size:13px;
      user-select:none;
      white-space:nowrap;
    }
    input[type="checkbox"]{ width:18px; height:18px; }

    select{
      border:1px solid var(--border);
      border-radius:14px;
      padding:10px 12px;
      font-weight:900;
      background: color-mix(in oklab, var(--cardSolid) 92%, transparent);
      color: var(--ink);
      max-width: 260px;
    }

    .btn{
      border:2px solid var(--border);
      background: color-mix(in oklab, var(--cardSolid) 92%, transparent);
      border-radius:16px;
      padding:12px 14px;
      cursor:pointer;
      font-weight:1000;
      color: var(--ink);
    }
    .btn:hover{ background: color-mix(in oklab, var(--accent) 10%, var(--cardSolid)); }

    /* Big reset */
    .btn.reset{
      border-color: color-mix(in oklab, #ff6b6b 40%, var(--border));
      background: color-mix(in oklab, #ff6b6b 15%, var(--cardSolid));
      padding:16px 22px;
      font-size:16px;
      border-radius:18px;
    }

    .disabled{ pointer-events:none; opacity:.55; }

    /* Kids mode */
    body.kids .q{ font-size: clamp(40px, 10vw, 70px); }
    body.kids button.choice{ padding:22px 10px; font-size: clamp(24px, 6vw, 34px); }

    /* Mobile: cleaner stacking + full width buttons */
    @media (max-width: 520px){
      body{ padding:12px; }
      .card{ padding:14px; border-radius:18px; }
      .choices{ grid-template-columns: 1fr; gap:12px; }
      .controls{ justify-content:center; }
      .tog, select, .btn{ width:100%; justify-content:center; }
      select{ max-width:100%; }
      .top{ justify-content:center; }
    }
  </style>
</head>

<body>
  <div class="card">
    <div class="top">
      <div class="pill"><span class="k">Level</span>: <span id="level">1</span></div>
      <div class="pill"><span class="k">Ops</span>: <span id="opsText">+</span></div>
      <div class="pill"><span class="k">Time</span>: <span id="timeLeft">15</span>s</div>
      <div class="pill"><span class="k">Score</span>: <span id="score">0</span></div>
    </div>

    <div class="subrow">
      <div class="badge">⭐ Streak: <span id="streak">0</span></div>
      <div class="badge">✨ Stars: <span id="stars">0</span></div>
      <div class="badge" id="medal">🥉 Bronze</div>
    </div>

    <div class="q" id="question"></div>

    <div class="choices" id="choices"></div>

    <div class="msg info" id="message">Pick the correct answer</div>

    <div class="bar-wrap"><div class="bar" id="bar"></div></div>

    <div class="controls">
      <div class="tog">
        <input type="checkbox" id="kidsToggle" />
        <label for="kidsToggle">Kids mode</label>
      </div>

      <div class="tog">
        <input type="checkbox" id="darkToggle" />
        <label for="darkToggle">Dark mode</label>
      </div>

      <div class="tog">
        <input type="checkbox" id="voiceToggle" checked />
        <label for="voiceToggle">Voice</label>
      </div>

      <div class="tog">
        <label for="voiceSelect">US/Microsoft voice</label>
        <select id="voiceSelect" aria-label="US/Microsoft voice"></select>
      </div>

      <button class="btn reset" id="resetBtn" type="button">🔄 Reset</button>
    </div>
  </div>

<script>
(() => {
  // -----------------------------
  // Config
  // -----------------------------
  const BASE_TIME_SECONDS = 15;      // ✅ time increased to 15s
  const LEVEL_UP_EVERY = 5;
  const ANSWER_MIN = 0;
  const ANSWER_MAX = 19;             // under 20
  const STREAK_BONUS_EVERY = 5;
  const STREAK_BONUS_STARS = 2;

  // -----------------------------
  // Helpers
  // -----------------------------
  const randInt = (min, max) => Math.floor(Math.random()*(max-min+1))+min;
  const shuffle = (arr) => {
    for (let i = arr.length - 1; i > 0; i--) {
      const j = Math.floor(Math.random() * (i + 1));
      [arr[i], arr[j]] = [arr[j], arr[i]];
    }
    return arr;
  };

  // -----------------------------
  // Elements
  // -----------------------------
  const elLevel = document.getElementById('level');
  const elOpsText = document.getElementById('opsText');
  const elTimeLeft = document.getElementById('timeLeft');
  const elScore = document.getElementById('score');
  const elStreak = document.getElementById('streak');
  const elStars = document.getElementById('stars');
  const elMedal = document.getElementById('medal');

  const elQ = document.getElementById('question');
  const elChoices = document.getElementById('choices');
  const elMsg = document.getElementById('message');
  const elBar = document.getElementById('bar');

  const kidsToggle = document.getElementById('kidsToggle');
  const darkToggle = document.getElementById('darkToggle');
  const voiceToggle = document.getElementById('voiceToggle');
  const voiceSelect = document.getElementById('voiceSelect');
  const resetBtn = document.getElementById('resetBtn');

  // -----------------------------
  // Theme + preferences (localStorage)
  // -----------------------------
  const LS = {
    kids: 'mq_kids',
    dark: 'mq_dark',
    voiceOn: 'mq_voiceOn',
    voiceId: 'mq_voiceId'
  };

  function applyKids(on){
    document.body.classList.toggle('kids', on);
    kidsToggle.checked = on;
    localStorage.setItem(LS.kids, on ? '1' : '0');
  }
  function applyDark(on){
    document.body.classList.toggle('dark', on);
    darkToggle.checked = on;
    localStorage.setItem(LS.dark, on ? '1' : '0');
  }
  function applyVoice(on){
    voiceToggle.checked = on;
    localStorage.setItem(LS.voiceOn, on ? '1' : '0');
  }

  // Load saved preferences
  applyKids(localStorage.getItem(LS.kids) === '1');
  applyDark(localStorage.getItem(LS.dark) === '1');
  applyVoice(localStorage.getItem(LS.voiceOn) !== '0'); // default ON

  kidsToggle.addEventListener('change', () => applyKids(kidsToggle.checked));
  darkToggle.addEventListener('change', () => applyDark(darkToggle.checked));
  voiceToggle.addEventListener('change', () => applyVoice(voiceToggle.checked));

  // -----------------------------
  // Voice (US + Microsoft only)
  // -----------------------------
  let voices = [];

  function isAllowedVoice(v){
    const name = (v.name || '').toLowerCase();
    const lang = (v.lang || '').toLowerCase();
    const isMicrosoft = name.includes('microsoft');
    const isUS = lang === 'en-us' || lang.startsWith('en-us');
    // Only show voices that are BOTH good standard options:
    // - Microsoft voices (Windows)
    // - US English language
    return isMicrosoft && isUS;
  }

  function loadVoices(){
    if (!('speechSynthesis' in window)){
      voiceToggle.checked = false;
      voiceToggle.disabled = true;
      voiceSelect.innerHTML = '<option>Voice not supported</option>';
      voiceSelect.disabled = true;
      return;
    }

    voices = window.speechSynthesis.getVoices() || [];
    const allowed = voices.filter(isAllowedVoice);

    voiceSelect.innerHTML = '';
    if (!allowed.length){
      voiceSelect.innerHTML = '<option>No US Microsoft voice found</option>';
      voiceSelect.disabled = true;
      return;
    }

    voiceSelect.disabled = false;

    // Put common ones first if present
    const preferredOrder = ['zira', 'david', 'mark', 'aria', 'guy', 'jenny'];
    allowed.sort((a,b) => {
      const an = (a.name||'').toLowerCase();
      const bn = (b.name||'').toLowerCase();
      const ai = preferredOrder.findIndex(k => an.includes(k));
      const bi = preferredOrder.findIndex(k => bn.includes(k));
      const aa = ai === -1 ? 999 : ai;
      const bb = bi === -1 ? 999 : bi;
      if (aa !== bb) return aa - bb;
      return an.localeCompare(bn);
    });

    allowed.forEach(v => {
      const opt = document.createElement('option');
      opt.value = String(voices.indexOf(v)); // store original index
      opt.textContent = `${v.name} (${v.lang})`;
      voiceSelect.appendChild(opt);
    });

    // Restore saved voice if exists
    const saved = localStorage.getItem(LS.voiceId);
    if (saved && [...voiceSelect.options].some(o => o.value === saved)){
      voiceSelect.value = saved;
    } else {
      voiceSelect.value = voiceSelect.options[0].value;
      localStorage.setItem(LS.voiceId, voiceSelect.value);
    }
  }

  voiceSelect.addEventListener('change', () => {
    localStorage.setItem(LS.voiceId, voiceSelect.value);
  });

  function speak(text){
    if (!voiceToggle.checked) return;
    if (!('speechSynthesis' in window)) return;

    window.speechSynthesis.cancel();

    const u = new SpeechSynthesisUtterance(text);
    const idx = parseInt(voiceSelect.value, 10);
    if (!Number.isNaN(idx) && voices[idx]) u.voice = voices[idx];
    u.rate = 1.0;
    u.pitch = 1.0;
    u.volume = 1.0;
    window.speechSynthesis.speak(u);
  }

  if ('speechSynthesis' in window){
    loadVoices();
    window.speechSynthesis.onvoiceschanged = loadVoices;
  } else {
    loadVoices();
  }

  // -----------------------------
  // Game state
  // -----------------------------
  let level = 1;
  let score = 0;
  let streak = 0;
  let stars = 0;
  let currentAnswer = 0;

  let timerId = null;
  let timeTotal = BASE_TIME_SECONDS;
  let timeLeft = BASE_TIME_SECONDS;
  let locked = false;

  function opsForLevel(lv){
    if (lv <= 1) return ['+'];          // Level 1 only +
    if (lv === 2) return ['+','−'];     // Level 2 mix +/−
    return ['+','−','×'];               // Level 3 include ×
  }

  function timeForLevel(lv){
    // Base 15 seconds, slightly faster per level, min 8 seconds
    return Math.max(8, BASE_TIME_SECONDS - (lv - 1));
  }

  function updateMedal(){
    // 1-2 bronze, 3-4 silver, 5-6 gold, 7+ diamond
    let text = '🥉 Bronze';
    if (level >= 7) text = '💎 Diamond';
    else if (level >= 5) text = '🥇 Gold';
    else if (level >= 3) text = '🥈 Silver';
    elMedal.textContent = text;
  }

  function updateStats(){
    elLevel.textContent = String(level);
    elScore.textContent = String(score);
    elStreak.textContent = String(streak);
    elStars.textContent = String(stars);
    elOpsText.textContent = opsForLevel(level).join(' ');
    updateMedal();
  }

  function setMessage(text, kind='info', lock=false){
    elMsg.textContent = text;
    elMsg.className = `msg ${kind}`;
    elMsg.dataset.locked = lock ? '1' : '';
  }

  function lockChoices(on){
    locked = on;
    elChoices.classList.toggle('disabled', on);
  }

  function stopTimer(){
    if (timerId) clearInterval(timerId);
    timerId = null;
  }

  function startTimer(){
    stopTimer();
    timeTotal = timeForLevel(level);
    timeLeft = timeTotal;
    elTimeLeft.textContent = String(timeLeft);
    elBar.style.width = '100%';

    timerId = setInterval(() => {
      timeLeft -= 1;
      if (timeLeft < 0) timeLeft = 0;
      elTimeLeft.textContent = String(timeLeft);
      elBar.style.width = ((timeLeft / timeTotal) * 100) + '%';

      if (timeLeft <= 0) onTimeUp();
    }, 1000);
  }

  function onTimeUp(){
    stopTimer();
    lockChoices(true);
    streak = 0;
    updateStats();

    setMessage("⏰ Time's up!", 'bad', true);
    speak("Time's up!");

    setTimeout(newQuestion, 900);
  }

  function maybeLevelUp(){
    const newLevel = 1 + Math.floor(score / LEVEL_UP_EVERY);
    if (newLevel !== level){
      level = newLevel;
      updateStats();
      setMessage(`🔥 Level up! Level ${level}`, 'info', true);
      speak(`Level up! Level ${level}`);
      setTimeout(() => setMessage('Pick the correct answer', 'info', false), 700);
    }
  }

  // -----------------------------
  // Question generation (answer under 20)
  // -----------------------------
  function newQuestion(){
    lockChoices(false);
    setMessage('Pick the correct answer', 'info', false);

    const ops = opsForLevel(level);
    const op = ops[randInt(0, ops.length - 1)];
    let a=0, b=0, ans=0, symbol=op;

    // Increase range a bit with level but keep answer 0..19
    const maxN = Math.min(19, 8 + level * 3);

    if (op === '+'){
      a = randInt(0, maxN);
      b = randInt(0, Math.min(maxN, ANSWER_MAX - a));
      ans = a + b;
      symbol = '+';
    } else if (op === '−'){
      a = randInt(0, maxN);
      b = randInt(0, a);
      ans = a - b;
      symbol = '−';
    } else {
      ans = randInt(0, ANSWER_MAX);
      const pairs = [];
      for (let x = 0; x <= ANSWER_MAX; x++){
        if (x === 0){
          if (ans === 0) pairs.push([0, randInt(0, 9)]);
          continue;
        }
        if (ans % x === 0){
          const y = ans / x;
          if (y <= ANSWER_MAX) pairs.push([x, y]);
        }
      }
      const filtered = pairs.filter(p => p[0] !== 1 && p[1] !== 1);
      const use = filtered.length ? filtered : pairs;
      const pick = use[randInt(0, use.length - 1)];
      a = pick[0]; b = pick[1];
      symbol = '×';
    }

    currentAnswer = ans;
    elQ.textContent = `${a} ${symbol} ${b} = ?`;

    // Options: correct + 2 wrong unique within 0..19
    const options = new Set([currentAnswer]);
    const spread = Math.min(10, 6 + level);
    while (options.size < 3){
      const delta = randInt(-spread, spread);
      const candidate = currentAnswer + delta;
      if (candidate >= ANSWER_MIN && candidate <= ANSWER_MAX) options.add(candidate);
    }

    renderChoices(shuffle(Array.from(options)));
    startTimer();
  }

  function renderChoices(list){
    elChoices.innerHTML = '';
    list.forEach(v => {
      const btn = document.createElement('button');
      btn.type = 'button';
      btn.className = 'choice';
      btn.textContent = v;

      btn.addEventListener('click', () => {
        if (locked) return;

        if (v === currentAnswer){
          stopTimer();
          lockChoices(true);

          score += 1;
          streak += 1;
          stars += 1;

          if (streak > 0 && streak % STREAK_BONUS_EVERY === 0){
            stars += STREAK_BONUS_STARS;
          }

          updateStats();
          maybeLevelUp();

          setMessage('🎉 Correct! Great job!', 'ok', true);
          speak('Correct!');

          setTimeout(newQuestion, 800);
        } else {
          streak = 0;
          updateStats();
          setMessage('❌ Try again!', 'bad', false);
          speak('Try again.');
        }
      });

      elChoices.appendChild(btn);
    });
  }

  // -----------------------------
  // Reset
  // -----------------------------
  function resetGame(){
    stopTimer();
    level = 1;
    score = 0;
    streak = 0;
    stars = 0;
    updateStats();
    elMsg.dataset.locked = '';
    newQuestion();
  }

  resetBtn.addEventListener('click', resetGame);

  // Start
  updateStats();
  newQuestion();
})();
</script>
</body>
</html>
