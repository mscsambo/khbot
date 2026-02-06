<html lang="km">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1,viewport-fit=cover" />
  <title>Math Quiz – Kids Mode + Levels + Stars + Voice + Fullscreen</title>
  <style>
    :root{
      --bg:#f6f7fb; --card:#fff; --ink:#111827; --muted:#6b7280;
      --border:#e6e8f0; --pill:#f1f3ff; --accent:#6a5cff;
      --okbg:#e9fbef; --ok:#146c2e; --badbg:#ffecec; --bad:#8a1f1f; --infobg:#eef2ff; --info:#2b3a75;
    }
    *{box-sizing:border-box}
    body{
      font-family:system-ui, -apple-system, Segoe UI, Roboto, Arial, "Noto Sans Khmer", sans-serif;
      background:var(--bg); margin:0; padding:18px;
      min-height:100vh; display:grid; place-items:center;
    }
    .card{
      width:min(860px, 100%);
      background:var(--card);
      border-radius:18px;
      padding:18px;
      box-shadow:0 10px 30px rgba(0,0,0,.08);
      border:1px solid rgba(0,0,0,.04);
    }
    .top{
      display:flex; gap:10px; justify-content:space-between; align-items:center; flex-wrap:wrap;
      margin-bottom:10px;
    }
    .pill{
      display:inline-flex; gap:8px; align-items:center;
      padding:8px 12px; border-radius:999px; background:var(--pill); border:1px solid var(--border);
      font-weight:900; font-size:13px; color:#27304a;
      user-select:none;
    }
    .pill .k{opacity:.7; font-weight:800}
    .status{
      display:flex; gap:10px; flex-wrap:wrap; align-items:center; justify-content:space-between;
      margin-top:8px;
    }
    .q{
      font-weight:1000; text-align:center; letter-spacing:.5px;
      font-size:44px; margin:14px 0 12px;
    }
    .stars{
      display:flex; align-items:center; justify-content:center; gap:10px; flex-wrap:wrap;
      margin:6px 0 4px;
    }
    .stars .badge{
      display:inline-flex; gap:8px; align-items:center;
      padding:8px 12px; border-radius:14px; border:1px solid var(--border); background:#fff;
      font-weight:1000;
    }
    .stars .emoji{font-size:18px}
    .stars .text{font-size:14px}
    .medal{
      font-size:18px;
      padding:8px 12px;
      border-radius:14px;
      border:1px solid var(--border);
      background:#fff;
      font-weight:1000;
    }

    .choices{
      display:grid;
      grid-template-columns: repeat(3, 1fr);
      gap:12px;
      margin-top:10px;
    }
    button.choice{
      border:2px solid var(--border);
      background:#fafbff;
      border-radius:16px;
      padding:16px 10px;
      font-weight:1000;
      cursor:pointer;
      transition: transform .06s ease, border-color .15s ease, background .15s ease;
    }
    button.choice:hover{ background:#f3f5ff; border-color:#cfd6ff; }
    button.choice:active{ transform:scale(.985); }

    .msg{
      margin-top:12px;
      padding:12px 12px;
      border-radius:14px;
      text-align:center;
      font-weight:1000;
      border:1px solid transparent;
      min-height:22px;
      user-select:none;
    }
    .msg.ok{ background:var(--okbg); color:var(--ok); border-color:#bfe9cc; }
    .msg.bad{ background:var(--badbg); color:var(--bad); border-color:#ffd0d0; }
    .msg.info{ background:var(--infobg); color:var(--info); border-color:#d6ddff; }

    .bar-wrap{
      margin-top:10px;
      height:14px;
      background:#eef0f6;
      border-radius:999px;
      overflow:hidden;
      border:1px solid var(--border);
    }
    .bar{
      height:100%;
      width:100%;
      background:var(--accent);
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
      padding:8px 10px;
      border-radius:14px;
      border:1px solid var(--border);
      background:#fff;
      font-weight:900;
      font-size:13px;
      color:#1f2937;
      user-select:none;
    }
    input[type="checkbox"]{ width:18px; height:18px; }
    select{
      border:1px solid var(--border);
      border-radius:14px;
      padding:10px 12px;
      font-weight:1000;
      background:#fff;
      max-width:240px;
    }

    .btn{
      border:2px solid var(--border);
      background:#fff;
      border-radius:16px;
      padding:12px 14px;
      cursor:pointer;
      font-weight:1000;
    }
    .btn:hover{ background:#f7f7fb; }
    .btn.full{
      border-color:#d6ddff;
      background:#eef2ff;
      color:#2b3a75;
    }
    .btn.full:hover{ background:#e3e8ff; }

    /* BIG reset (your request) */
    .btn.reset{
      border-color:#ffb3b3;
      background:#ffeded;
      color:#8a1f1f;
      padding:18px 26px;
      font-size:18px;
      border-radius:18px;
    }
    .btn.reset:hover{ background:#ffdada; }

    .disabled{ pointer-events:none; opacity:.55; }

    /* Kids Mode (bigger + more spacing) */
    body.kids .card{ padding:20px; }
    body.kids .q{ font-size:58px; margin:18px 0 14px; }
    body.kids .choices{ gap:14px; }
    body.kids button.choice{ padding:22px 10px; font-size:28px; border-radius:18px; }
    body.kids .msg{ font-size:18px; padding:14px; }
    body.kids .pill{ font-size:14px; padding:10px 14px; }
    body.kids .btn.reset{ font-size:20px; padding:20px 30px; }
    body.kids .stars .text{ font-size:15px; }

    /* Mobile layout: stack controls nicely */
    @media (max-width: 520px){
      body{ padding:10px; }
      .choices{ grid-template-columns: 1fr; }
      .controls{ justify-content:center; }
      select{ width:100%; max-width:100%; }
      .tog{ width:100%; justify-content:center; }
      .btn{ width:100%; }
    }

    /* Fullscreen feel */
    body.fullscreen .card{
      width:min(1100px, 100%);
    }
  </style>
</head>
<body>
  <div class="card">
    <div class="top">
      <div class="pill"><span class="k" id="t_level_k">Level</span>: <span id="level">1</span></div>
      <div class="pill"><span class="k" id="t_ops_k">Ops</span>: <span id="opsText">+</span></div>
      <div class="pill"><span class="k" id="t_time_k">Time</span>: <span id="timeLeft">15</span>s</div>
      <div class="pill"><span class="k" id="t_score_k">Score</span>: <span id="score">0</span></div>
    </div>

    <div class="stars">
      <div class="badge">
        <span class="emoji">⭐</span>
        <span class="text"><span id="t_streak_k">Streak</span>: <span id="streak">0</span></span>
      </div>
      <div class="badge">
        <span class="emoji">✨</span>
        <span class="text"><span id="t_stars_k">Stars</span>: <span id="stars">0</span></span>
      </div>
      <div class="medal" id="medal">🥉</div>
    </div>

    <div class="q" id="question"></div>

    <div class="choices" id="choices"></div>

    <div class="msg info" id="message"></div>

    <div class="bar-wrap" aria-label="timer progress">
      <div class="bar" id="bar"></div>
    </div>

    <div class="controls">
      <div class="tog">
        <input type="checkbox" id="kidsToggle" />
        <label for="kidsToggle" id="t_kids">Kids mode</label>
      </div>

      <div class="tog">
        <input type="checkbox" id="voiceToggle" checked />
        <label for="voiceToggle" id="t_voice">Voice</label>
      </div>

      <div class="tog">
        <label for="langSelect" id="t_lang">Language</label>
        <select id="langSelect" aria-label="Language">
          <option value="en">English</option>
          <option value="km">ខ្មែរ</option>
        </select>
      </div>

      <div class="tog">
        <label for="voiceSelect" id="t_voice_sel">Voice</label>
        <select id="voiceSelect" aria-label="Voice"></select>
      </div>

      <button class="btn full" id="fsBtn" type="button">⛶ Fullscreen</button>
      <button class="btn reset" id="resetBtn" type="button">🔄 Reset</button>
    </div>
  </div>

<script>
(() => {
  // -----------------------------
  // Config (your request)
  // -----------------------------
  const BASE_TIME_SECONDS = 15;      // ✅ base timer = 15s
  const LEVEL_UP_EVERY = 5;          // level up each 5 correct
  const ANSWER_MIN = 0;
  const ANSWER_MAX = 19;             // answers under 20

  // Stars system:
  // +1 star per correct
  // +2 bonus stars each 5-streak
  const STREAK_BONUS_EVERY = 5;
  const STREAK_BONUS_STARS = 2;

  // -----------------------------
  // Simple utilities
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
  const voiceToggle = document.getElementById('voiceToggle');
  const langSelect = document.getElementById('langSelect');
  const voiceSelect = document.getElementById('voiceSelect');
  const fsBtn = document.getElementById('fsBtn');
  const resetBtn = document.getElementById('resetBtn');

  // Labels that change language
  const t = {
    en: {
      levelK:'Level', opsK:'Ops', timeK:'Time', scoreK:'Score',
      streakK:'Streak', starsK:'Stars',
      kids:'Kids mode', voice:'Voice', lang:'Language', voiceSel:'Voice',
      pick:'Pick the correct answer',
      correct:'Correct! Great job!',
      tryAgain:'Try again!',
      timeUp:"Time's up!",
      levelUp:(n)=>`Level up! Level ${n}`,
      fs:'Fullscreen', exitFs:'Exit Fullscreen',
      reset:'Reset',
      medalBronze:'Bronze', medalSilver:'Silver', medalGold:'Gold', medalDiamond:'Diamond'
    },
    km: {
      levelK:'កម្រិត', opsK:'ប្រតិបត្តិការ', timeK:'ពេល', scoreK:'ពិន្ទុ',
      streakK:'ជាប់ៗ', starsK:'ផ្កាយ',
      kids:'ម៉ូដកុមារ', voice:'សំឡេង', lang:'ភាសា', voiceSel:'សំឡេង',
      pick:'ជ្រើសចម្លើយត្រឹមត្រូវ',
      correct:'ត្រឹមត្រូវ! ល្អណាស់!',
      tryAgain:'ព្យាយាមម្តងទៀត!',
      timeUp:'អស់ពេលហើយ!',
      levelUp:(n)=>`ឡើងកម្រិត! កម្រិត ${n}`,
      fs:'ពេញអេក្រង់', exitFs:'ចេញពីពេញអេក្រង់',
      reset:'កំណត់ឡើងវិញ',
      medalBronze:'សំរិទ្ធ', medalSilver:'ប្រាក់', medalGold:'មាស', medalDiamond:'ពេជ្រ'
    }
  };

  function currentLang(){ return langSelect.value === 'km' ? 'km' : 'en'; }

  function setUITexts(){
    const L = t[currentLang()];
    document.getElementById('t_level_k').textContent = L.levelK;
    document.getElementById('t_ops_k').textContent = L.opsK;
    document.getElementById('t_time_k').textContent = L.timeK;
    document.getElementById('t_score_k').textContent = L.scoreK;
    document.getElementById('t_streak_k').textContent = L.streakK;
    document.getElementById('t_stars_k').textContent = L.starsK;

    document.getElementById('t_kids').textContent = L.kids;
    document.getElementById('t_voice').textContent = L.voice;
    document.getElementById('t_lang').textContent = L.lang;
    document.getElementById('t_voice_sel').textContent = L.voiceSel;

    fsBtn.textContent = (isFullscreen() ? `⛶ ${L.exitFs}` : `⛶ ${L.fs}`);
    resetBtn.textContent = `🔄 ${L.reset}`;

    // message only if empty or currently "pick" variants
    if (!elMsg.dataset.locked) {
      setMessage(L.pick, 'info', false);
    }
    updateMedal(); // medal text may change language
  }

  // -----------------------------
  // Voice (SpeechSynthesis)
  // -----------------------------
  let voices = [];
  function loadVoices(){
    if (!('speechSynthesis' in window)) {
      voiceToggle.checked = false;
      voiceToggle.disabled = true;
      voiceSelect.innerHTML = '<option>No speech</option>';
      voiceSelect.disabled = true;
      return;
    }

    voices = window.speechSynthesis.getVoices() || [];
    voiceSelect.innerHTML = '';
    if (!voices.length){
      voiceSelect.innerHTML = '<option>Loading voices…</option>';
      voiceSelect.disabled = true;
      return;
    }
    voiceSelect.disabled = false;

    // Sort: prefer selected language then English
    const want = currentLang();
    const sorted = voices.slice().sort((a,b)=>{
      const al = (a.lang||'').toLowerCase();
      const bl = (b.lang||'').toLowerCase();
      const aWant = want==='km' ? (al.startsWith('km')||al.includes('kh')) : al.startsWith('en');
      const bWant = want==='km' ? (bl.startsWith('km')||bl.includes('kh')) : bl.startsWith('en');
      if (aWant !== bWant) return aWant ? -1 : 1;
      // prefer local voices before "Google" sometimes sounds better; no strong rule
      return (a.name||'').localeCompare(b.name||'');
    });

    sorted.forEach(v=>{
      const opt = document.createElement('option');
      opt.value = String(voices.indexOf(v));
      opt.textContent = `${v.name} (${v.lang})`;
      voiceSelect.appendChild(opt);
    });

    // auto pick first best match
    voiceSelect.value = voiceSelect.options[0]?.value ?? '';
  }

  function speak(text){
    if (!voiceToggle.checked) return;
    if (!('speechSynthesis' in window)) return;
    window.speechSynthesis.cancel();

    const u = new SpeechSynthesisUtterance(text);
    const idx = parseInt(voiceSelect.value, 10);
    if (!Number.isNaN(idx) && voices[idx]) u.voice = voices[idx];

    // Slightly slower for Khmer for clarity
    u.rate = currentLang()==='km' ? 0.95 : 1.0;
    u.pitch = 1.0;
    u.volume = 1.0;
    window.speechSynthesis.speak(u);
  }

  // -----------------------------
  // Fullscreen (mobile-friendly)
  // -----------------------------
  function isFullscreen(){
    return !!(document.fullscreenElement || document.webkitFullscreenElement);
  }
  async function toggleFullscreen(){
    try{
      const root = document.documentElement;
      if (!isFullscreen()){
        if (root.requestFullscreen) await root.requestFullscreen();
        else if (root.webkitRequestFullscreen) await root.webkitRequestFullscreen();
      } else {
        if (document.exitFullscreen) await document.exitFullscreen();
        else if (document.webkitExitFullscreen) await document.webkitExitFullscreen();
      }
    } catch (e) {
      // ignore
    } finally {
      document.body.classList.toggle('fullscreen', isFullscreen());
      setUITexts();
    }
  }

  // Auto suggest fullscreen on mobile (no auto-enter, browsers block it)
  const isMobile = matchMedia('(max-width: 520px)').matches;

  // -----------------------------
  // Game state
  // -----------------------------
  let level = 1;
  let score = 0;      // correct total
  let streak = 0;     // consecutive correct
  let stars = 0;
  let currentAnswer = 0;

  let timerId = null;
  let timeTotal = BASE_TIME_SECONDS;
  let timeLeft = BASE_TIME_SECONDS;
  let locked = false;

  function opsForLevel(lv){
    if (lv <= 1) return ['+'];          // Level 1 only +
    if (lv === 2) return ['+','−'];     // Level 2 +/−
    return ['+','−','×'];               // Level 3+ +/−/×
  }

  function timeForLevel(lv){
    // Base is 15s, then slightly faster each level, minimum 8s
    return Math.max(8, BASE_TIME_SECONDS - (lv - 1));
  }

  function updateMedal(){
    // Based on level:
    // 1-2 bronze, 3-4 silver, 5-6 gold, 7+ diamond
    const L = t[currentLang()];
    let emoji = '🥉', name = L.medalBronze;
    if (level >= 7) { emoji='💎'; name=L.medalDiamond; }
    else if (level >= 5) { emoji='🥇'; name=L.medalGold; }
    else if (level >= 3) { emoji='🥈'; name=L.medalSilver; }
    else { emoji='🥉'; name=L.medalBronze; }

    elMedal.textContent = `${emoji} ${name}`;
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

      if (timeLeft <= 0){
        onTimeUp();
      }
    }, 1000);
  }

  function onTimeUp(){
    stopTimer();
    lockChoices(true);
    streak = 0; // streak breaks on timeout
    updateStats();

    const L = t[currentLang()];
    setMessage(`⏰ ${L.timeUp}`, 'bad', true);
    speak(L.timeUp);

    // Auto next after short delay
    setTimeout(newQuestion, 900);
  }

  function maybeLevelUp(){
    const newLevel = 1 + Math.floor(score / LEVEL_UP_EVERY);
    if (newLevel !== level){
      level = newLevel;
      updateStats();

      const L = t[currentLang()];
      setMessage(`🔥 ${L.levelUp(level)}`, 'info', true);
      speak(L.levelUp(level));

      // continue after a moment
      setTimeout(() => {
        setMessage(L.pick, 'info', false);
      }, 700);
    }
  }

  // -----------------------------
  // Question generation (answer under 20)
  // -----------------------------
  function newQuestion(){
    lockChoices(false);
    const L = t[currentLang()];
    setMessage(L.pick, 'info', false);

    const ops = opsForLevel(level);
    const op = ops[randInt(0, ops.length - 1)];
    let a=0, b=0, ans=0, symbol=op;

    // Increase number range with level but keep answer 0..19
    const maxN = Math.min(19, 8 + level * 3);

    if (op === '+'){
      a = randInt(0, maxN);
      b = randInt(0, Math.min(maxN, ANSWER_MAX - a));
      ans = a + b;
      symbol = '+';
    } else if (op === '−'){
      a = randInt(0, maxN);
      b = randInt(0, a); // non-negative result
      ans = a - b;
      symbol = '−';
    } else {
      // × (multiplication): pick an answer and factor pair
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
      // prefer less trivial pairs if possible
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
    const spread = Math.min(10, 6 + level); // more spread with level
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

          const L = t[currentLang()];
          setMessage(`🎉 ${L.correct}`, 'ok', true);
          speak(L.correct);

          // Next automatically
          setTimeout(newQuestion, 800);
        } else {
          // wrong -> reselect allowed; streak breaks
          streak = 0;
          updateStats();

          const L = t[currentLang()];
          setMessage(`❌ ${L.tryAgain}`, 'bad', false);
          speak(L.tryAgain);
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

  // -----------------------------
  // Kids mode toggle
  // -----------------------------
  function applyKidsMode(on){
    document.body.classList.toggle('kids', on);
  }

  // -----------------------------
  // Wiring
  // -----------------------------
  kidsToggle.addEventListener('change', () => applyKidsMode(kidsToggle.checked));
  langSelect.addEventListener('change', () => {
    setUITexts();
    loadVoices();
    // keep the game running; just update message language if it's not locked
    if (!elMsg.dataset.locked) setMessage(t[currentLang()].pick, 'info', false);
  });
  voiceSelect.addEventListener('change', () => {
    // test small preview if wanted:
    // speak(currentLang()==='km' ? 'សួស្តី' : 'Hello');
  });

  fsBtn.addEventListener('click', toggleFullscreen);
  resetBtn.addEventListener('click', resetGame);

  document.addEventListener('fullscreenchange', () => {
    document.body.classList.toggle('fullscreen', isFullscreen());
    setUITexts();
  });

  // Load voices (async in some browsers)
  if ('speechSynthesis' in window){
    loadVoices();
    window.speechSynthesis.onvoiceschanged = () => loadVoices();
  } else {
    voiceToggle.checked = false;
    voiceToggle.disabled = true;
    voiceSelect.innerHTML = '<option>No speech</option>';
    voiceSelect.disabled = true;
  }

  // First UI setup
  updateStats();
  setUITexts();

  // Default: if mobile, suggest fullscreen label (no auto request)
  if (isMobile) document.body.classList.add('fullscreen');

  // Start game
  resetGame();
})();
</script>
</body>
</html>
