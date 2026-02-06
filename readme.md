<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1,viewport-fit=cover" />
  <title>Math Quiz – + / − Under 15 (20s) + Voice</title>

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
      display:flex; gap:10px;
      justify-content:space-between;
      align-items:center;
      flex-wrap:wrap;
      margin-bottom:10px;
    }
    .pill{
      display:inline-flex; gap:8px; align-items:center;
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

    .q{
      text-align:center;
      font-weight:1000;
      letter-spacing:.3px;
      margin:12px 0 8px;
      font-size: clamp(34px, 9vw, 66px);
      line-height: 1.05;
      word-break: break-word;
      overflow-wrap: anywhere;
      padding-inline: 6px;
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
      font-size: clamp(20px, 5.5vw, 32px);
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
      display:flex; gap:8px; align-items:center;
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
      max-width: 320px;
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

    .btn.reset{
      border-color: color-mix(in oklab, #ff6b6b 40%, var(--border));
      background: color-mix(in oklab, #ff6b6b 15%, var(--cardSolid));
      padding:16px 22px;
      font-size:16px;
      border-radius:18px;
    }

    .disabled{ pointer-events:none; opacity:.55; }

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
      <div class="pill"><span class="k">Ops</span>: <span id="opsText">+ / −</span></div>
      <div class="pill"><span class="k">Max</span>: <span id="maxText">14</span></div>
      <div class="pill"><span class="k">Time</span>: <span id="timeLeft">20</span>s</div>
      <div class="pill"><span class="k">Score</span>: <span id="score">0</span></div>
    </div>

    <div class="q" id="question"></div>

    <div class="choices" id="choices"></div>

    <div class="msg info" id="message">Pick the correct answer</div>

    <div class="bar-wrap"><div class="bar" id="bar"></div></div>

    <div class="controls">
      <div class="tog">
        <input type="checkbox" id="darkToggle" />
        <label for="darkToggle">Dark mode</label>
      </div>

      <div class="tog">
        <input type="checkbox" id="voiceToggle" checked />
        <label for="voiceToggle">Voice</label>
      </div>

      <div class="tog">
        <label for="voiceSelect">US Microsoft voice</label>
        <select id="voiceSelect" aria-label="US Microsoft voice"></select>
      </div>

      <button class="btn reset" id="resetBtn" type="button">🔄 Reset</button>
    </div>
  </div>

<script>
(() => {
  // -----------------------------
  // Config (your request)
  // -----------------------------
  const MAX_VALUE = 14;             // ✅ random under 15 (0..14)
  const BASE_TIME_SECONDS = 20;     // ✅ time = 20s
  const OPTIONS_COUNT = 3;

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
  const elTimeLeft = document.getElementById('timeLeft');
  const elScore = document.getElementById('score');
  const elQ = document.getElementById('question');
  const elChoices = document.getElementById('choices');
  const elMsg = document.getElementById('message');
  const elBar = document.getElementById('bar');

  const darkToggle = document.getElementById('darkToggle');
  const voiceToggle = document.getElementById('voiceToggle');
  const voiceSelect = document.getElementById('voiceSelect');
  const resetBtn = document.getElementById('resetBtn');

  // -----------------------------
  // Dark mode (saved)
  // -----------------------------
  const LS_DARK = 'mq_dark';
  function applyDark(on){
    document.body.classList.toggle('dark', on);
    darkToggle.checked = on;
    localStorage.setItem(LS_DARK, on ? '1' : '0');
  }
  applyDark(localStorage.getItem(LS_DARK) === '1');
  darkToggle.addEventListener('change', () => applyDark(darkToggle.checked));

  // -----------------------------
  // Voice (US + Microsoft only) + speak selected number too
  // -----------------------------
  const LS_VOICE_ON = 'mq_voiceOn';
  const LS_VOICE_ID = 'mq_voiceId';

  function applyVoice(on){
    voiceToggle.checked = on;
    localStorage.setItem(LS_VOICE_ON, on ? '1' : '0');
  }
  applyVoice(localStorage.getItem(LS_VOICE_ON) !== '0');

  voiceToggle.addEventListener('change', () => applyVoice(voiceToggle.checked));

  let voices = [];
  function isAllowedVoice(v){
    const name = (v.name || '').toLowerCase();
    const lang = (v.lang || '').toLowerCase();
    return name.includes('microsoft') && (lang === 'en-us' || lang.startsWith('en-us'));
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
      opt.value = String(voices.indexOf(v));
      opt.textContent = `${v.name} (${v.lang})`;
      voiceSelect.appendChild(opt);
    });

    const saved = localStorage.getItem(LS_VOICE_ID);
    if (saved && [...voiceSelect.options].some(o => o.value === saved)){
      voiceSelect.value = saved;
    } else {
      voiceSelect.value = voiceSelect.options[0].value;
      localStorage.setItem(LS_VOICE_ID, voiceSelect.value);
    }
  }

  voiceSelect.addEventListener('change', () => {
    localStorage.setItem(LS_VOICE_ID, voiceSelect.value);
  });

  function speak(text){
    if (!voiceToggle.checked) return;
    if (!('speechSynthesis' in window)) return;
    if (voiceSelect.disabled) return;

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
  let currentAnswer = 0;
  let score = 0;
  let timerId = null;
  let timeLeft = BASE_TIME_SECONDS;
  let locked = false;

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
    timeLeft = BASE_TIME_SECONDS;
    elTimeLeft.textContent = String(timeLeft);
    elBar.style.width = '100%';

    timerId = setInterval(() => {
      timeLeft -= 1;
      if (timeLeft < 0) timeLeft = 0;
      elTimeLeft.textContent = String(timeLeft);
      elBar.style.width = ((timeLeft / BASE_TIME_SECONDS) * 100) + '%';

      if (timeLeft <= 0){
        onTimeUp();
      }
    }, 1000);
  }

  function onTimeUp(){
    stopTimer();
    lockChoices(true);
    setMessage("⏰ Time's up!", 'bad', true);
    speak("Time's up!");
    setTimeout(newQuestion, 900);
  }

  // -----------------------------
  // Question generation (only + and - , under 15)
  // Results kept within 0..14 for easy kids math.
  // -----------------------------
  function newQuestion(){
    lockChoices(false);
    setMessage('Pick the correct answer', 'info', false);

    const op = Math.random() < 0.5 ? '+' : '−';

    let a, b, ans;

    if (op === '+'){
      a = randInt(0, MAX_VALUE);
      b = randInt(0, MAX_VALUE - a);  // ensures ans <= 14
      ans = a + b;
    } else {
      a = randInt(0, MAX_VALUE);
      b = randInt(0, a);              // ensures non-negative
      ans = a - b;
    }

    currentAnswer = ans;
    elQ.textContent = `${a} ${op} ${b} = ?`;

    // 3 options (unique) within 0..14
    const options = new Set([currentAnswer]);
    while (options.size < OPTIONS_COUNT){
      const delta = randInt(-6, 6);
      const candidate = currentAnswer + delta;
      if (candidate >= 0 && candidate <= MAX_VALUE) options.add(candidate);
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

        // ✅ Speak the number user clicked
        speak(String(v));

        if (v === currentAnswer){
          stopTimer();
          lockChoices(true);
          score += 1;
          elScore.textContent = String(score);

          setMessage('🎉 Correct! Great job!', 'ok', true);
          // ✅ Also speak "Correct" after saying the number
          setTimeout(() => speak('Correct!'), 250);

          setTimeout(newQuestion, 900);
        } else {
          setMessage('❌ Try again!', 'bad', false);
          // ✅ Speak "Try again" after saying the number
          setTimeout(() => speak('Try again.'), 250);
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
    score = 0;
    elScore.textContent = '0';
    newQuestion();
  }

  resetBtn.addEventListener('click', resetGame);

  // Start
  document.getElementById('maxText').textContent = String(MAX_VALUE);
  newQuestion();
})();
</script>
</body>
</html>
