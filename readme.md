<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Simple Calculator — Dark / Light</title>
  <style>
    :root{
      /* Dark theme (defaults) */
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
    }

    /* Light theme overrides when applied to the root element (html.light-theme) */
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
    }

    *{box-sizing:border-box}
    html,body{height:100%}
    body{
      margin:0;
      font-family:Inter, Roboto, system-ui, -apple-system, "Segoe UI", Arial, sans-serif;
      background: linear-gradient(180deg,var(--bg), #071021 120%);
      color:var(--text);
      display:flex;
      align-items:center;
      justify-content:center;
      padding:24px;
      transition:background-color .25s ease, color .25s ease;
    }

    .calculator{
      width:320px;
      max-width:100%;
      background: linear-gradient(180deg,var(--panel), #07101a);
      border-radius:12px;
      box-shadow: 0 10px 30px rgba(2,6,23,0.6), inset 0 1px 0 rgba(255,255,255,0.02);
      padding:18px;
      transition:background-color .25s ease, box-shadow .25s ease;
    }

    /* top bar with title and theme toggle */
    .top{
      display:flex;
      align-items:center;
      justify-content:space-between;
      margin-bottom:8px;
    }
    .title{
      font-weight:600;
      color:var(--muted);
      font-size:0.9rem;
    }
    .theme-toggle{
      background:transparent;
      border:1px solid rgba(255,255,255,0.04);
      color:var(--text);
      padding:6px 8px;
      border-radius:8px;
      cursor:pointer;
      display:inline-flex;
      align-items:center;
      justify-content:center;
      gap:6px;
      transition:background .12s ease, color .12s ease, border-color .12s ease;
    }
    .theme-toggle .icon{font-size:1rem}
    .theme-toggle:focus{outline:2px solid rgba(0,0,0,0.08); outline-offset:2px}

    .display{
      height:72px;
      background:transparent;
      color:var(--text);
      font-size:2rem;
      display:flex;
      align-items:center;
      justify-content:flex-end;
      padding:12px;
      border-radius:8px;
      margin-bottom:12px;
      border:1px solid rgba(255,255,255,0.03);
      overflow:hidden;
      word-break:break-all;
    }

    /* buttons grid */
    .buttons{
      display:grid;
      grid-template-columns:repeat(4,1fr);
      gap:10px;
    }

    .btn{
      background:var(--btn);
      color:var(--text);
      border:0;
      padding:18px 12px;
      border-radius:10px;
      font-size:1.1rem;
      cursor:pointer;
      box-shadow: 0 4px 10px rgba(2,6,23,0.45);
      transition:transform .06s ease, background .12s ease, color .12s ease;
      user-select:none;
    }

    .btn:active{transform:translateY(2px)}
    .btn:hover{background:var(--btn-hover)}

    .span-two{grid-column:span 2}
    .operator{
      background:linear-gradient(180deg,var(--operator-start),var(--operator-end));
      color:var(--text);
    }
    .equals{
      background:linear-gradient(180deg,var(--equals-start),var(--equals-end));
      color:#002a30;
      font-weight:600;
    }

    /* small screens: slightly smaller buttons */
    @media (max-width:360px){
      .display{height:60px;font-size:1.6rem}
      .btn{padding:14px 10px;font-size:1rem}
    }
  </style>
</head>
<body>
  <main class="calculator" role="application" aria-label="Simple calculator">
    <div class="top">
      <div class="title" aria-hidden="true">Calculator</div>
      <button id="theme-toggle" class="theme-toggle" aria-pressed="false" aria-label="Toggle dark and light theme">
        <span class="icon" aria-hidden="true">☾</span>
      </button>
    </div>

    <div class="display" id="display" aria-live="polite">0</div>

    <div class="buttons" role="group" aria-label="Calculator buttons">
      <button class="btn span-two" data-action="clear" aria-label="Clear">AC</button>
      <button class="btn" data-action="delete" aria-label="Delete">DEL</button>
      <button class="btn operator" data-action="/" aria-label="Divide">÷</button>

      <button class="btn" data-action="7">7</button>
      <button class="btn" data-action="8">8</button>
      <button class="btn" data-action="9">9</button>
      <button class="btn operator" data-action="*" aria-label="Multiply">×</button>

      <button class="btn" data-action="4">4</button>
      <button class="btn" data-action="5">5</button>
      <button class="btn" data-action="6">6</button>
      <button class="btn operator" data-action="-" aria-label="Subtract">−</button>

      <button class="btn" data-action="1">1</button>
      <button class="btn" data-action="2">2</button>
      <button class="btn" data-action="3">3</button>
      <button class="btn operator" data-action="+" aria-label="Add">+</button>

      <button class="btn" data-action="0">0</button>
      <button class="btn" data-action=".">.</button>
      <button class="btn span-two equals" data-action="=" aria-label="Equals">=</button>
    </div>
  </main>

  <script>
    (function () {
      const displayEl = document.getElementById('display');
      const themeToggleBtn = document.getElementById('theme-toggle');
      const THEME_KEY = 'calculator-theme'; // 'dark' or 'light'

      // Theme handling
      function applyTheme(theme) {
        if (theme === 'light') {
          document.documentElement.classList.add('light-theme');
          themeToggleBtn.setAttribute('aria-pressed', 'true');
          themeToggleBtn.querySelector('.icon').textContent = '☀︎';
          themeToggleBtn.setAttribute('aria-label', 'Switch to dark theme');
        } else {
          document.documentElement.classList.remove('light-theme');
          themeToggleBtn.setAttribute('aria-pressed', 'false');
          themeToggleBtn.querySelector('.icon').textContent = '☾';
          themeToggleBtn.setAttribute('aria-label', 'Switch to light theme');
        }
      }

      // Initialize theme from localStorage or system preference
      const stored = localStorage.getItem(THEME_KEY);
      if (stored === 'light' || stored === 'dark') {
        applyTheme(stored);
      } else {
        const prefersLight = window.matchMedia && window.matchMedia('(prefers-color-scheme: light)').matches;
        applyTheme(prefersLight ? 'light' : 'dark');
      }

      themeToggleBtn.addEventListener('click', () => {
        const isLight = document.documentElement.classList.contains('light-theme');
        const next = isLight ? 'dark' : 'light';
        applyTheme(next);
        localStorage.setItem(THEME_KEY, next);
      });

      // Calculator logic
      let current = '';
      let previous = '';
      let operation = null;
      let resetNext = false;

      function updateDisplay() {
        displayEl.textContent = current || (previous ? previous : '0');
      }

      function clearAll() {
        current = '';
        previous = '';
        operation = null;
        resetNext = false;
        updateDisplay();
      }

      function deleteLast() {
        if (resetNext) {
          clearAll();
          return;
        }
        current = current.slice(0, -1);
        updateDisplay();
      }

      function appendNumber(num) {
        if (resetNext) {
          current = '';
          resetNext = false;
        }
        if (num === '.' && current.includes('.')) return;
        if (num === '.' && current === '') current = '0';
        // Prevent leading zeros like "00"
        if (num !== '.' && current === '0') current = num;
        else current = current + num;
        updateDisplay();
      }

      function chooseOperation(op) {
        if (current === '' && previous === '') return;
        if (previous !== '' && current !== '') {
          compute();
        } else if (current !== '') {
          previous = current;
        }
        operation = op;
        current = '';
        updateDisplay();
      }

      function compute() {
        const prev = parseFloat(previous);
        const curr = parseFloat(current);

        // If there's no explicit previous (user pressed = after single number), do nothing
        if (isNaN(prev) || isNaN(curr)) return;

        let computation = null;
        switch (operation) {
          case '+': computation = prev + curr; break;
          case '-': computation = prev - curr; break;
          case '*': computation = prev * curr; break;
          case '/':
            if (curr === 0) {
              displayEl.textContent = 'Error';
              current = '';
              previous = '';
              operation = null;
              resetNext = true;
              return;
            }
            computation = prev / curr; break;
          default: return;
        }
        computation = Number.isInteger(computation) ? computation : parseFloat(computation.toFixed(10));
        current = computation.toString();
        previous = '';
        operation = null;
        resetNext = true;
        updateDisplay();
      }

      // Button handling
      document.querySelectorAll('.btn').forEach(btn => {
        btn.addEventListener('click', () => {
          const action = btn.dataset.action;
          if (!action) return;
          if ((action >= '0' && action <= '9') || action === '.') {
            appendNumber(action);
            return;
          }
          if (['+','-','*','/'].includes(action)) {
            chooseOperation(action);
            return;
          }
          if (action === '=') {
            compute();
            return;
          }
          if (action === 'clear') {
            clearAll();
            return;
          }
          if (action === 'delete') {
            deleteLast();
            return;
          }
        });
      });

      // Keyboard support
      window.addEventListener('keydown', (e) => {
        const key = e.key;
        if ((key >= '0' && key <= '9') || key === '.') {
          appendNumber(key);
          e.preventDefault();
          return;
        }
        if (key === 'Enter' || key === '=') {
          compute();
          e.preventDefault();
          return;
        }
        if (key === 'Backspace') {
          deleteLast();
          e.preventDefault();
          return;
        }
        if (key === 'Escape') {
          clearAll();
          e.preventDefault();
          return;
        }
        if (['+','-','*','/'].includes(key)) {
          chooseOperation(key);
          e.preventDefault();
          return;
        }
      });

      // Initialize display
      clearAll();
    })();
  </script>
</body>
</html>
