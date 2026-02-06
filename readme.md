<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1,viewport-fit=cover" />
  <title>Math Quiz – Levels (Beginner/Primary/Upper) + Voice</title>

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
      width:min(920px, 100%);
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
      gap:14px;
      margin-top: 10px;
    }
    /* ✅ Bigger answers */
    button.choice{
      border:2px solid var(--border);
      background: color-mix(in oklab, var(--cardSolid) 92%, transparent);
      border-radius:18px;
      padding:22px 10px;
      font-weight:1000;
      font-size: clamp(28px, 6.2vw, 44px);  /* bigger */
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
      font-size: 16px;
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
      max-width: 360px;
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
      <div class="pill"><span class="k">Level</span>:
        <strong id="levelName">Beginner</strong>
      </div>
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
        <label for="levelSelect">Choose Level</label>
        <select id="levelSelect" aria-label="Choose level">
          <option value="beginner">Beginner (under 15)</option>
          <option value="primary">Primary (under 25)</option>
          <option value="upper">Upper (under 55, + − × ÷)</option>
        </select>
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
        <label for="voiceSelect">Voice</label>
        <select id="voiceSelect" aria-label="Voice"></select>
      </div>

      <button class="btn reset" id="resetBtn" type="button">🔄 Reset</button>
    </div>
  </div>

<script>
(() => {
  // ---------------------------------------------------
  // Level configs (your request)
  // ---------------------------------------------------
  const LEVELS = {
    beginner: { name: "Beginner", max: 14, ops: ['+','−'], allowDivide: false },
    primary:  { name: "Primary",  max: 24, ops: ['+','−'], allowDivide: false },
    upper:    { name: "Upper",    max: 54, ops: ['+','−','×','÷'], allowDivide: true }
  };

  const TIME_SECONDS = 20;
  const OPTIONS_COUNT = 3;

  // ---------------------------------------------------
  // Helpers
  // ---------------------------------------------------
  const randInt = (min, max) => Math.floor(Math.random()*(max-min+1))+min;
  const shuffle = (arr) => {
    for (let i = arr.length - 1; i > 0; i--) {
      const j = Math.floor(Math.random() * (i + 1));
      [arr[i], arr[j]] = [arr[j], arr[i]];
    }
    return arr;
  };

  // Number-to-words (0..60) for TTS quality
  const ones = ["zero","one","two","three","four","five","six","seven","eight","nine"];
  const teens = ["ten","eleven","twelve","thirteen","fourteen","fifteen","sixteen","seventeen","eighteen","nineteen"];
  const tens = ["","","twenty","thirty","forty","fifty","sixty"];
  function sayNumber(n){
    n = Math.round(n);
    if (n < 0) return "minus " + sayNumber(-n);
    if (n < 10) return ones[n];
    if (n < 20) return teens[n - 10];
    if (n < 70){
      const t = Math.floor(n/10);
      const r = n%10;
      return r === 0 ? tens[t] : `${tens[t]} ${ones[r]}`;
    }
    return String(n);
  }

  // ---------------------------------------------------
  // Elements
  // ---------------------------------------------------
  const elLevelName = document.getElementById('levelName');
  const elOpsText = document.getElementById('opsText');
  const elMaxText = document.getElementById('maxText');
  const elTimeLeft = document.getElementById('timeLeft');
  const elScore = document.getElementById('score');

  const elQ = document.getElementById('question');
  const elChoices = document.getElementById('choices');
  const elMsg = document.getElementById('message');
  const elBar = document.getElementById('bar');

  const levelSelect = document.getElementById('levelSelect');
  const darkToggle = document.getElementById('darkToggle');
  const voiceToggle = document.getElementById('voiceToggle');
  const voiceSelect = document.getElementById('voiceSelect');
  const resetBtn = document.getElementById('resetBtn');

  // ---------------------------------------------------
  // Dark mode (saved)
  // ---------------------------------------------------
  const LS_DARK = 'mq_dark';
  function applyDark(on){
    document.body.classList.toggle('dark', on);
    darkToggle.checked = on;
    localStorage.setItem(LS_DARK, on ? '1' : '0');
  }
  applyDark(localStorage.getItem(LS_DARK) === '1');
  darkToggle.addEventListener('change', () => applyDark(darkToggle.checked));

  // ---------------------------------------------------
  // Voice (cross-device)
  // ---------------------------------------------------
  const LS_VOICE_ON = 'mq_voiceOn';
  const LS_VOICE_ID = 'mq_voiceId';

  voiceToggle.checked = (localStorage.getItem(LS_VOICE_ON) !== '0');
  voiceToggle.addEventListener('change', () => {
    localStorage.setItem(LS_VOICE_ON, voiceToggle.checked ? '1' : '0');
  });

  let voices = [];

  function isEnglish(v){
    const lang = (v.lang || '').toLowerCase();
    return lang.startsWith('en');
  }
  function isEnUS(v){
    const lang = (v.lang || '').toLowerCase();
    return lang === 'en-us' || lang.startsWith('en-us');
  }

  function voiceRank(v){
    const name = (v.name || '').toLowerCase();
    const microsoft = name.includes('microsoft');
    const google = name.includes('google');
    const siri = name.includes('siri');
    const apple = name.includes('com.apple') || name.includes('apple');

    if (microsoft && isEnUS(v)) return 1;
    if ((siri || apple) && isEnUS(v)) return 2;
    if (google && isEnUS(v)) return 3;
    if (isEnUS(v)) return 4;
    if ((siri || apple) && isEnglish(v)) return 5;
    if (microsoft && isEnglish(v)) return 6;
    if (google && isEnglish(v)) return 7;
    if (isEnglish(v)) return 8;
    return 999;
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
    const english = voices
      .filter(v => voiceRank(v) < 999)
      .sort((a,b) => voiceRank(a) - voiceRank(b) || (a.name||'').localeCompare(b.name||''));

    voiceSelect.innerHTML = '';
    if (!english.length){
      voiceSelect.innerHTML = '<option>No English voice found</option>';
      voiceSelect.disabled = true;
      return;
    }

    voiceSelect.disabled = false;

    english.slice(0, 12).forEach(v => {
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

  // iOS: unlock TTS after first gesture
  let ttsUnlocked = false;
  function unlockTTS(){
    if (ttsUnlocked) return;
    ttsUnlocked = true;
    if ('speechSynthesis' in window){
      const u = new SpeechSynthesisUtterance(' ');
      u.volume = 0;
      window.speechSynthesis.speak(u);
      window.speechSynthesis.cancel();
    }
    document.removeEventListener('touchend', unlockTTS);
    document.removeEventListener('click', unlockTTS);
  }
  document.addEventListener('touchend', unlockTTS, { once:true });
  document.addEventListener('click', unlockTTS, { once:true });

  // ---------------------------------------------------
  // Game state
  // ---------------------------------------------------
  let currentLevelKey = 'beginner';
  let currentAnswer = 0;
  let score = 0;
  let timerId = null;
  let timeLeft = TIME_SECONDS;
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
    timeLeft = TIME_SECONDS;
    elTimeLeft.textContent = String(timeLeft);
    elBar.style.width = '100%';

    timerId = setInterval(() => {
      timeLeft -= 1;
      if (timeLeft < 0) timeLeft = 0;
      elTimeLeft.textContent = String(timeLeft);
      elBar.style.width = ((timeLeft / TIME_SECONDS) * 100) + '%';

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

  function applyLevelUI(){
    const cfg = LEVELS[currentLevelKey];
    elLevelName.textContent = cfg.name;
    elMaxText.textContent = String(cfg.max);
    elOpsText.textContent = cfg.ops.join(' ');
  }

  // ---------------------------------------------------
  // Question generation for each level
  // - Beginner/Primary: +/−, answers 0..max
  // - Upper: +/−/×/÷, answers kept integer and within 0..max
  // ---------------------------------------------------
  function newQuestion(){
    lockChoices(false);
    setMessage('Pick the correct answer', 'info', false);

    const cfg = LEVELS[currentLevelKey];
    const max = cfg.max;
    const op = cfg.ops[randInt(0, cfg.ops.length - 1)];

    let a=0, b=0, ans=0, symbol=op;

    if (op === '+'){
      a = randInt(0, max);
      b = randInt(0, max - a);   // keep ans <= max
      ans = a + b;
      symbol = '+';
    } else if (op === '−'){
      a = randInt(0, max);
      b = randInt(0, a);         // keep ans >= 0
      ans = a - b;
      symbol = '−';
    } else if (op === '×'){
      // pick answer <= max, then choose factor pair
      ans = randInt(0, max);
      const pairs = [];
      for (let x = 0; x <= max; x++){
        if (x === 0){ if (ans === 0) pairs.push([0, randInt(0, Math.min(10,max))]); continue; }
        if (ans % x === 0){
          const y = ans / x;
          if (y <= max) pairs.push([x, y]);
        }
      }
      const filtered = pairs.filter(p => p[0] !== 1 && p[1] !== 1);
      const use = filtered.length ? filtered : pairs;
      const pick = use[randInt(0, use.length - 1)];
      a = pick[0]; b = pick[1];
      symbol = '×';
    } else {
      // ÷ : ensure integer result, within 0..max
      ans = randInt(0, max);
      b = randInt(1, Math.min(12, max)); // divisor (avoid 0)
      a = ans * b;
      // ensure a within reasonable range; if too big, retry once
      if (a > max) { // keep displayed numbers not too large
        // rebuild with smaller b
        b = randInt(1, Math.max(1, Math.floor(max / Math.max(ans,1))));
        a = ans * b;
      }
      symbol = '÷';
    }

    currentAnswer = ans;
    elQ.textContent = `${a} ${symbol} ${b} = ?`;

    // Options: correct + 2 wrong within 0..max (unique)
    const options = new Set([currentAnswer]);
    const spread = Math.max(6, Math.floor(max / 6));
    while (options.size < OPTIONS_COUNT){
      const delta = randInt(-spread, spread);
      const candidate = currentAnswer + delta;
      if (candidate >= 0 && candidate <= max) options.add(candidate);
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

        const spokenNumber = sayNumber(v);

        if (v === currentAnswer){
          stopTimer();
          lockChoices(true);
          score += 1;
          elScore.textContent = String(score);

          setMessage('🎉 Correct! Great job!', 'ok', true);

          // Speak "number + correct" together
          speak(`${spokenNumber}. Correct!`);

          setTimeout(newQuestion, 900);
        } else {
          setMessage('❌ Try again!', 'bad', false);
          speak(`${spokenNumber}. Try again.`);
        }
      });

      elChoices.appendChild(btn);
    });
  }

  // ---------------------------------------------------
  // Level select + reset
  // ---------------------------------------------------
  levelSelect.addEventListener('change', () => {
    currentLevelKey = levelSelect.value;
    applyLevelUI();
    // restart question, keep score (or reset if you want)
    newQuestion();
  });

  function resetGame(){
    stopTimer();
    score = 0;
    elScore.textContent = '0';
    applyLevelUI();
    newQuestion();
  }

  resetBtn.addEventListener('click', resetGame);

  // Start
  applyLevelUI();
  newQuestion();
})();
</script>
</body>
</html>
