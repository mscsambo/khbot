<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Scientific Calculator — Dark / Light</title>
  <style>
    :root{
      --bg: #0f1724;
      --panel: #0b1220;
      --accent: #00bcd4;
      --btn: #1e293b;
      --btn-hover: #334155;
      --text: #e6eef6;
      --muted: #94a3b8;
      --operator-start: #0b3b4a;
      --operator-end: #06333a;
      --equals-start: #00bcd4;
      --equals-end: #008a98;
      --modal-bg: rgba(15, 23, 36, 0.92);
      --modal-content: #0f1724;
      --sci-btn: #0f2a36;
      --sci-hover: #1a3f4f;
    }
    .light-theme {
      --bg: #f3f7fb;
      --panel: #ffffff;
      --accent: #0b80a0;
      --btn: #eef3f7;
      --btn-hover: #e0e8ef;
      --text: #0b1220;
      --muted: #5b6b77;
      --operator-start: #e9f5f8;
      --operator-end: #d8eef3;
      --equals-start: #30a6c0;
      --equals-end: #0b80a0;
      --modal-bg: rgba(243, 247, 251, 0.92);
      --modal-content: #ffffff;
      --sci-btn: #e0f0f5;
      --sci-hover: #cce5ee;
    }
    *{box-sizing:border-box}
    html,body{height:100%; margin:0;}
    body{
      font-family: Inter, Roboto, system-ui, sans-serif;
      background: linear-gradient(180deg,var(--bg), #071021 120%);
      color:var(--text);
      display:flex;
      align-items:center;
      justify-content:center;
      padding:24px;
      transition:background-color .25s ease, color .25s ease;
    }
    .calculator{
      width:360px;  /* slightly wider for sci buttons */
      max-width:100%;
      background: linear-gradient(180deg,var(--panel), #07101a);
      border-radius:12px;
      box-shadow: 0 10px 30px rgba(2,6,23,0.6), inset 0 1px 0 rgba(255,255,255,0.02);
      padding:18px;
      transition: all .25s ease;
    }
    .top{
      display:flex;
      align-items:center;
      justify-content:space-between;
      margin-bottom:8px;
    }
    .title{font-weight:600; color:var(--muted); font-size:0.9rem;}
    .theme-toggle, .help-btn{
      background:transparent;
      border:1px solid rgba(255,255,255,0.08);
      color:var(--text);
      padding:6px 10px;
      border-radius:8px;
      cursor:pointer;
      font-size:1rem;
      transition: all .12s ease;
    }
    .theme-toggle:hover, .help-btn:hover{background: rgba(255,255,255,0.06);}
    .display{
      height:72px;
      background:transparent;
      color:var(--text);
      font-size:2.4rem;
      font-weight:400;
      display:flex;
      align-items:center;
      justify-content:flex-end;
      padding:12px;
      border-radius:8px;
      margin-bottom:14px;
      border:1px solid rgba(255,255,255,0.04);
      overflow:hidden;
      word-break:break-all;
    }
    .buttons{
      display:grid;
      grid-template-columns:repeat(5,1fr);  /* changed to 5 columns */
      gap:10px;
    }
    .btn{
      background:var(--btn);
      color:var(--text);
      border:0;
      padding:16px 10px;
      border-radius:10px;
      font-size:1.05rem;
      cursor:pointer;
      box-shadow: 0 4px 10px rgba(2,6,23,0.45);
      transition:transform .06s ease, background .12s ease;
      user-select:none;
    }
    .sci { background:var(--sci-btn); font-size:0.95rem; }
    .sci:hover { background:var(--sci-hover); }
    .btn:active{transform:translateY(2px)}
    .btn:hover{background:var(--btn-hover)}
    .span-two{grid-column:span 2}
    .operator{
      background:linear-gradient(180deg,var(--operator-start),var(--operator-end));
    }
    .equals{
      background:linear-gradient(180deg,var(--equals-start),var(--equals-end));
      color:#002a30;
      font-weight:600;
    }
    /* Help Modal styles remain the same — omitted for brevity */
    .modal { /* ... same as before ... */ }
    .modal.show { display: flex; }
    .modal-content { /* ... */ }
    /* ... rest of modal styles unchanged ... */

    @media (max-width:400px){
      .calculator { width:320px; }
      .buttons { grid-template-columns:repeat(4,1fr); }
      .sci, .span-five { display:none; } /* hide some sci on very small screens or adjust */
    }
  </style>
</head>
<body>

  <main class="calculator" role="application" aria-label="Scientific calculator">
    <div class="top">
      <div class="title">Scientific Calculator</div>
      <div>
        <button id="help-btn" class="help-btn" aria-label="Show help">?</button>
        <button id="theme-toggle" class="theme-toggle" aria-pressed="false" aria-label="Toggle theme">
          <span class="icon">☾</span>
        </button>
      </div>
    </div>

    <div class="display" id="display" aria-live="polite">0</div>

    <div class="buttons" role="group" aria-label="Calculator buttons">
      <!-- Scientific row -->
      <button class="btn sci" data-action="sin">sin</button>
      <button class="btn sci" data-action="cos">cos</button>
      <button class="btn sci" data-action="tan">tan</button>
      <button class="btn sci" data-action="log">log</button>
      <button class="btn sci" data-action="ln">ln</button>

      <!-- Standard row 1 -->
      <button class="btn span-two" data-action="clear">AC</button>
      <button class="btn" data-action="delete">DEL</button>
      <button class="btn operator" data-action="/">÷</button>
      <button class="btn sci" data-action="sqrt">√</button>

      <button class="btn" data-action="7">7</button>
      <button class="btn" data-action="8">8</button>
      <button class="btn" data-action="9">9</button>
      <button class="btn operator" data-action="*">×</button>
      <button class="btn sci" data-action="sqr">x²</button>

      <button class="btn" data-action="4">4</button>
      <button class="btn" data-action="5">5</button>
      <button class="btn" data-action="6">6</button>
      <button class="btn operator" data-action="-">−</button>
      <button class="btn sci" data-action="pow">xʸ</button>

      <button class="btn" data-action="1">1</button>
      <button class="btn" data-action="2">2</button>
      <button class="btn" data-action="3">3</button>
      <button class="btn operator" data-action="+">+</button>
      <button class="btn sci" data-action="sign">±</button>

      <button class="btn" data-action="0">0</button>
      <button class="btn" data-action=".">.</button>
      <button class="btn span-two equals" data-action="=">=</button>
    </div>
  </main>
  <script>
    (function () {
      const displayEl   = document.getElementById('display');
      const themeToggle = document.getElementById('theme-toggle');
      const helpBtn     = document.getElementById('help-btn');
      const helpModal   = document.getElementById('help-modal');
      const modalClose  = helpModal.querySelector('.modal-close');

      const THEME_KEY = 'calculator-theme';
      const MAX_SIGNIFICANT = 15;
      const MAX_DECIMALS    = 10;

      // Theme logic (unchanged)
      function applyTheme(theme) {
        const isLight = theme === 'light';
        document.documentElement.classList.toggle('light-theme', isLight);
        themeToggle.setAttribute('aria-pressed', isLight);
        themeToggle.querySelector('.icon').textContent = isLight ? '☀︎' : '☾';
      }

      let stored = localStorage.getItem(THEME_KEY) || 
        (window.matchMedia?.('(prefers-color-scheme: light)').matches ? 'light' : 'dark');
      applyTheme(stored);

      themeToggle.addEventListener('click', () => {
        const next = document.documentElement.classList.contains('light-theme') ? 'dark' : 'light';
        applyTheme(next);
        localStorage.setItem(THEME_KEY, next);
      });

      // Modal logic (unchanged)
      function showHelp() { helpModal.classList.add('show'); }
      function hideHelp() { helpModal.classList.remove('show'); }
      helpBtn.addEventListener('click', showHelp);
      modalClose.addEventListener('click', hideHelp);
      helpModal.addEventListener('click', e => { if (e.target === helpModal) hideHelp(); });
      window.addEventListener('keydown', e => {
        if (e.key === 'Escape' && helpModal.classList.contains('show')) hideHelp();
      });

      // Calculator state
      let current   = '';
      let previous  = '';
      let operation = null;
      let resetNext = false;

      function updateDisplay() {
        displayEl.textContent = current || (previous || '0');
      }

      function clearAll() {
        current = previous = '';
        operation = null;
        resetNext = false;
        updateDisplay();
      }

      function deleteLast() {
        if (resetNext) { clearAll(); return; }
        current = current.slice(0, -1);
        updateDisplay();
      }

      function appendNumber(num) {
        if (resetNext) { current = ''; resetNext = false; }
        if (num === '.' && current.includes('.')) return;
        if (num === '.' && current === '') current = '0';
        if (current === '0' && num === '0') return;

        const prospective = (current === '' && num === '.' ? '0' : current + num);
        const digitCount = prospective.replace(/[^0-9]/g, '').length;
        if (digitCount > MAX_SIGNIFICANT) return;

        if (current.includes('.') && num !== '.') {
          const dec = current.split('.')[1] || '';
          if (dec.length >= MAX_DECIMALS) return;
        }

        current = (current === '0' && num !== '.') ? num : current + num;
        updateDisplay();
      }

      function applyUnary(fn) {
        if (current === '') return;
        let val = parseFloat(current);
        if (isNaN(val)) return;

        let result = fn(val);
        if (!Number.isFinite(result)) {
          current = 'Error';
        } else {
          current = formatResult(result);
        }
        resetNext = true;
        updateDisplay();
      }

      function formatResult(num) {
        const abs = Math.abs(num);
        if (abs !== 0 && (abs >= 1e15 || abs < 1e-10)) {
          return num.toExponential(MAX_SIGNIFICANT - 1);
        }
        let str;
        if (Number.isInteger(num)) {
          str = num.toString();
        } else {
          str = parseFloat(num.toFixed(MAX_DECIMALS)).toString();
        }
        const sig = str.replace(/[^0-9]/g, '').replace(/^0+/, '').length;
        return (sig > MAX_SIGNIFICANT) ? num.toExponential(MAX_SIGNIFICANT - 1) : str;
      }

      function chooseOperation(op) {
        if (current === '' && previous === '') return;

        if (previous !== '' && current !== '') compute();

        if (current !== '') previous = current;

        operation = op;
        current = '';
        resetNext = false;
        updateDisplay();
      }

      function compute() {
        if (!operation || current === '') return;

        const prev = parseFloat(previous);
        const curr = parseFloat(current);
        if (isNaN(prev) || isNaN(curr)) return;

        let result;
        switch (operation) {
          case '+': result = prev + curr; break;
          case '-': result = prev - curr; break;
          case '*': result = prev * curr; break;
          case '/':
            if (curr === 0) { displayEl.textContent = 'Error'; clearAfterError(); return; }
            result = prev / curr; break;
          case 'pow':
            result = Math.pow(prev, curr); break;
          default: return;
        }

        current = formatResult(result);
        previous = '';
        operation = null;
        resetNext = true;
        updateDisplay();
      }

      function clearAfterError() {
        current = previous = '';
        operation = null;
        resetNext = true;
      }

      // ── New unary handlers ───────────────────────────────
      const unaryOps = {
        sin:  Math.sin,
        cos:  Math.cos,
        tan:  Math.tan,
        log:  Math.log10,
        ln:   Math.log,
        sqrt: Math.sqrt,
        sqr:  (x) => x * x,
        sign: (x) => -x
      };

      // ── Button handling ──────────────────────────────────
      document.querySelectorAll('.btn').forEach(btn => {
        btn.addEventListener('click', () => {
          const act = btn.dataset.action;
          if (!act) return;

          if ((act >= '0' && act <= '9') || act === '.') {
            appendNumber(act);
          }
          else if ('+-*/'.includes(act) || act === 'pow') {
            chooseOperation(act);
          }
          else if (act === '=') {
            compute();
          }
          else if (act === 'clear') {
            clearAll();
          }
          else if (act === 'delete') {
            deleteLast();
          }
          else if (unaryOps[act]) {
            applyUnary(unaryOps[act]);
          }
        });
      });

      // ── Keyboard support (extended) ──────────────────────
      window.addEventListener('keydown', e => {
        const k = e.key;
        if      ((k>='0'&&k<='9')||k==='.')     { appendNumber(k); e.preventDefault(); }
        else if (k==='Enter'||k==='=')          { compute(); e.preventDefault(); }
        else if (k==='Backspace')               { deleteLast(); e.preventDefault(); }
        else if (k==='Escape')                  { clearAll(); e.preventDefault(); }
        else if ('+-*/'.includes(k))            { chooseOperation(k); e.preventDefault(); }
        else if (k === '^')                     { chooseOperation('pow'); e.preventDefault(); }
        // Quick sci keys (optional)
        else if (k.toLowerCase() === 's')      { applyUnary(Math.sin);  e.preventDefault(); }
        else if (k.toLowerCase() === 'c')      { applyUnary(Math.cos);  e.preventDefault(); }
        else if (k.toLowerCase() === 't')      { applyUnary(Math.tan);  e.preventDefault(); }
      });

      clearAll();
    })();
  </script>
</body>
</html>
