<!DOCTYPE html>  
  
<html lang="en">  
<head>  
  <meta charset="UTF-8" />  
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>  
  <title>iPhone Calculator</title>  
  <link href="https://fonts.googleapis.com/css2?family=SF+Pro+Display:wght@300;400;500&display=swap" rel="stylesheet">  
  <style>  
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }  
  
```  
body {  
  background: #1a1a1a;  
  display: flex;  
  align-items: center;  
  justify-content: center;  
  min-height: 100vh;  
  font-family: -apple-system, 'Helvetica Neue', sans-serif;  
  overflow: hidden;  
}  
  
/* iPhone Shell */  
.iphone {  
  width: 390px;  
  height: 844px;  
  background: #000;  
  border-radius: 54px;  
  position: relative;  
  box-shadow:  
    0 0 0 1px #333,  
    0 0 0 3px #1a1a1a,  
    0 0 0 4px #444,  
    0 60px 120px rgba(0,0,0,0.9),  
    inset 0 0 0 1px #222;  
  overflow: hidden;  
}  
  
/* Side buttons */  
.iphone::before {  
  content: '';  
  position: absolute;  
  left: -4px;  
  top: 160px;  
  width: 4px;  
  height: 36px;  
  background: #333;  
  border-radius: 2px 0 0 2px;  
  box-shadow: 0 52px 0 #333, 0 100px 0 #333;  
}  
.iphone::after {  
  content: '';  
  position: absolute;  
  right: -4px;  
  top: 220px;  
  width: 4px;  
  height: 80px;  
  background: #333;  
  border-radius: 0 2px 2px 0;  
}  
  
/* Dynamic Island */  
.dynamic-island {  
  position: absolute;  
  top: 14px;  
  left: 50%;  
  transform: translateX(-50%);  
  width: 120px;  
  height: 34px;  
  background: #000;  
  border-radius: 20px;  
  z-index: 10;  
}  
  
/* Screen */  
.screen {  
  width: 100%;  
  height: 100%;  
  background: #000;  
  border-radius: 54px;  
  display: flex;  
  flex-direction: column;  
  justify-content: flex-end;  
  overflow: hidden;  
}  
  
/* Status bar */  
.status-bar {  
  position: absolute;  
  top: 0;  
  left: 0;  
  right: 0;  
  height: 59px;  
  display: flex;  
  align-items: flex-end;  
  justify-content: space-between;  
  padding: 0 32px 8px;  
  z-index: 5;  
}  
  
.status-time {  
  font-size: 15px;  
  font-weight: 600;  
  color: #fff;  
  letter-spacing: -0.3px;  
}  
  
.status-icons {  
  display: flex;  
  align-items: center;  
  gap: 7px;  
}  
  
.status-icons svg {  
  fill: #fff;  
}  
  
/* Calculator UI */  
.calculator {  
  display: flex;  
  flex-direction: column;  
  padding: 0 18px 34px;  
  gap: 0;  
  flex: 1;  
  justify-content: flex-end;  
}  
  
/* Display */  
.display {  
  padding: 0 12px 12px;  
  text-align: right;  
  min-height: 100px;  
  display: flex;  
  flex-direction: column;  
  justify-content: flex-end;  
  align-items: flex-end;  
}  
  
.expression {  
  font-size: 22px;  
  color: rgba(255,255,255,0.45);  
  font-weight: 300;  
  min-height: 28px;  
  letter-spacing: -0.5px;  
  word-break: break-all;  
  max-width: 100%;  
  overflow: hidden;  
  text-overflow: ellipsis;  
  white-space: nowrap;  
}  
  
.result {  
  font-size: 88px;  
  color: #fff;  
  font-weight: 300;  
  line-height: 1;  
  letter-spacing: -4px;  
  transition: font-size 0.15s ease;  
  word-break: break-all;  
  max-width: 100%;  
}  
  
.result.shrink-2 { font-size: 66px; letter-spacing: -3px; }  
.result.shrink-3 { font-size: 50px; letter-spacing: -2px; }  
.result.shrink-4 { font-size: 38px; letter-spacing: -1px; }  
  
/* Button Grid */  
.buttons {  
  display: grid;  
  grid-template-columns: repeat(4, 1fr);  
  gap: 12px;  
}  
  
.btn {  
  aspect-ratio: 1;  
  border: none;  
  border-radius: 50%;  
  font-size: 32px;  
  font-weight: 400;  
  cursor: pointer;  
  display: flex;  
  align-items: center;  
  justify-content: center;  
  transition: filter 0.1s ease;  
  position: relative;  
  outline: none;  
  -webkit-tap-highlight-color: transparent;  
  user-select: none;  
}  
  
.btn:active {  
  filter: brightness(1.5);  
}  
  
/* Button types */  
.btn-func {  
  background: #a5a5a5;  
  color: #1c1c1e;  
  font-size: 32px;  
}  
  
.btn-op {  
  background: #ff9f0a;  
  color: #fff;  
  font-size: 36px;  
}  
  
.btn-op.active {  
  background: #fff;  
  color: #ff9f0a;  
}  
  
.btn-num {  
  background: #333333;  
  color: #fff;  
  font-size: 32px;  
}  
  
/* Zero button spans 2 columns */  
.btn-zero {  
  grid-column: span 2;  
  border-radius: 40px;  
  aspect-ratio: unset;  
  width: 100%;  
  height: auto;  
  justify-content: flex-start;  
  padding-left: 36px;  
}  
  
/* Press animation */  
.btn::after {  
  content: '';  
  position: absolute;  
  inset: 0;  
  border-radius: inherit;  
  background: rgba(255,255,255,0.18);  
  opacity: 0;  
  transition: opacity 0.08s;  
}  
  
.btn.pressed::after {  
  opacity: 1;  
}  
  
/* Equals sign */  
.btn-eq-sym {  
  font-size: 36px;  
}  
  
/* Responsive for smaller screens */  
@media (max-height: 860px) {  
  .iphone {  
    transform: scale(0.85);  
    transform-origin: center center;  
  }  
}  
  
@media (max-height: 720px) {  
  .iphone {  
    transform: scale(0.7);  
  }  
}  
```  
  
  </style>  
</head>  
<body>  
  
<div class="iphone">  
  <div class="dynamic-island"></div>  
  <div class="screen">  
  
```  
<!-- Status Bar -->  
<div class="status-bar">  
  <div class="status-time" id="status-time">9:41</div>  
  <div class="status-icons">  
    <!-- Signal -->  
    <svg width="17" height="12" viewBox="0 0 17 12">  
      <rect x="0" y="6" width="3" height="6" rx="0.5"/>  
      <rect x="4.5" y="4" width="3" height="8" rx="0.5"/>  
      <rect x="9" y="2" width="3" height="10" rx="0.5"/>  
      <rect x="13.5" y="0" width="3" height="12" rx="0.5"/>  
    </svg>  
    <!-- WiFi -->  
    <svg width="16" height="12" viewBox="0 0 16 12">  
      <path d="M8 9.5a1.5 1.5 0 1 1 0 3 1.5 1.5 0 0 1 0-3z"/>  
      <path d="M8 6C6.1 6 4.4 6.8 3.2 8.1l1.4 1.4C5.5 8.6 6.7 8 8 8s2.5.6 3.4 1.5l1.4-1.4C11.6 6.8 9.9 6 8 6z" opacity=".7"/>  
      <path d="M8 2C5 2 2.3 3.3.7 5.4l1.4 1.4C3.5 5 5.6 4 8 4s4.5 1 5.9 2.8l1.4-1.4C13.7 3.3 11 2 8 2z" opacity=".4"/>  
    </svg>  
    <!-- Battery -->  
    <svg width="25" height="12" viewBox="0 0 25 12">  
      <rect x="0" y="1" width="22" height="10" rx="2.5" stroke="white" stroke-width="1" fill="none"/>  
      <rect x="23" y="3.5" width="2" height="5" rx="1" fill="white" opacity=".4"/>  
      <rect x="1.5" y="2.5" width="16" height="7" rx="1.5" fill="white"/>  
    </svg>  
  </div>  
</div>  
  
<!-- Calculator -->  
<div class="calculator">  
  <div class="display">  
    <div class="expression" id="expression"></div>  
    <div class="result" id="result">0</div>  
  </div>  
  
  <div class="buttons">  
    <!-- Row 1 -->  
    <button class="btn btn-func" data-action="clear" id="clearBtn">AC</button>  
    <button class="btn btn-func" data-action="sign">+/−</button>  
    <button class="btn btn-func" data-action="percent">%</button>  
    <button class="btn btn-op"   data-action="op" data-op="÷">÷</button>  
  
    <!-- Row 2 -->  
    <button class="btn btn-num" data-action="num" data-num="7">7</button>  
    <button class="btn btn-num" data-action="num" data-num="8">8</button>  
    <button class="btn btn-num" data-action="num" data-num="9">9</button>  
    <button class="btn btn-op"  data-action="op"  data-op="×">×</button>  
  
    <!-- Row 3 -->  
    <button class="btn btn-num" data-action="num" data-num="4">4</button>  
    <button class="btn btn-num" data-action="num" data-num="5">5</button>  
    <button class="btn btn-num" data-action="num" data-num="6">6</button>  
    <button class="btn btn-op"  data-action="op"  data-op="−">−</button>  
  
    <!-- Row 4 -->  
    <button class="btn btn-num" data-action="num" data-num="1">1</button>  
    <button class="btn btn-num" data-action="num" data-num="2">2</button>  
    <button class="btn btn-num" data-action="num" data-num="3">3</button>  
    <button class="btn btn-op"  data-action="op"  data-op="+">+</button>  
  
    <!-- Row 5 -->  
    <button class="btn btn-num btn-zero" data-action="num" data-num="0">0</button>  
    <button class="btn btn-num" data-action="decimal">.</button>  
    <button class="btn btn-op btn-eq-sym" data-action="equals">=</button>  
  </div>  
</div>  
```  
  
  </div>  
</div>  
  
<script>  
  // ── State ──────────────────────────────────────────────  
  let current     = '0';  
  let previous    = null;  
  let operator    = null;  
  let waitingNext = false;  
  let justEvaled  = false;  
  let expression  = '';  
  
  // ── DOM ────────────────────────────────────────────────  
  const resultEl     = document.getElementById('result');  
  const expressionEl = document.getElementById('expression');  
  const clearBtn     = document.getElementById('clearBtn');  
  
  // ── Clock ──────────────────────────────────────────────  
  function updateClock() {  
    const now = new Date();  
    let h = now.getHours(), m = now.getMinutes();  
    document.getElementById('status-time').textContent =  
      `${h}:${m.toString().padStart(2,'0')}`;  
  }  
  updateClock();  
  setInterval(updateClock, 10000);  
  
  // ── Display helpers ────────────────────────────────────  
  function formatNumber(n) {  
    if (isNaN(n) || !isFinite(n)) return n.toString();  
    const s = parseFloat(n.toPrecision(12)).toString();  
    if (s.includes('e')) return s;  
    const [int, dec] = s.split('.');  
    const formatted = parseInt(int).toLocaleString('en');  
    return dec !== undefined ? formatted + '.' + dec : formatted;  
  }  
  
  function setDisplay(val) {  
    const str = typeof val === 'number' ? formatNumber(val) : val;  
    resultEl.textContent = str;  
    // Auto-shrink for long numbers  
    const len = str.replace(/[,.]/g,'').length;  
    resultEl.className = 'result';  
    if (len > 9)  resultEl.classList.add('shrink-2');  
    if (len > 12) resultEl.classList.add('shrink-3');  
    if (len > 15) resultEl.classList.add('shrink-4');  
  }  
  
  function setExpression(val) {  
    expressionEl.textContent = val;  
  }  
  
  function updateClearLabel() {  
    clearBtn.textContent = (current !== '0' || previous !== null) ? 'C' : 'AC';  
  }  
  
  // ── Operator active highlight ──────────────────────────  
  function highlightOp(op) {  
    document.querySelectorAll('.btn-op').forEach(b => b.classList.remove('active'));  
    if (op) {  
      document.querySelectorAll('.btn-op[data-op]').forEach(b => {  
        if (b.dataset.op === op) b.classList.add('active');  
      });  
    }  
  }  
  
  // ── Core Logic ─────────────────────────────────────────  
  function calculate(a, b, op) {  
    a = parseFloat(a); b = parseFloat(b);  
    switch(op) {  
      case '+': return a + b;  
      case '−': return a - b;  
      case '×': return a * b;  
      case '÷': return b === 0 ? 'Error' : a / b;  
    }  
  }  
  
  function handleNum(n) {  
    if (waitingNext) {  
      current = n;  
      waitingNext = false;  
    } else {  
      if (justEvaled) { current = n; justEvaled = false; expression = ''; }  
      else current = current === '0' ? n : (current.length < 16 ? current + n : current);  
    }  
    setDisplay(current);  
    updateClearLabel();  
  }  
  
  function handleDecimal() {  
    if (waitingNext) { current = '0.'; waitingNext = false; setDisplay(current); return; }  
    if (!current.includes('.')) {  
      current += '.';  
      resultEl.textContent = current;  
    }  
    updateClearLabel();  
  }  
  
  function handleOp(op) {  
    if (operator && !waitingNext) {  
      const res = calculate(previous, current, operator);  
      if (res === 'Error') { setDisplay('Error'); expression = ''; operator = null; previous = null; return; }  
      previous = res;  
      setDisplay(formatNumber(res));  
      expression = formatNumber(res) + ' ' + op;  
    } else {  
      previous = parseFloat(current);  
      expression = formatNumber(parseFloat(current)) + ' ' + op;  
    }  
    operator    = op;  
    waitingNext = true;  
    justEvaled  = false;  
    setExpression(expression);  
    highlightOp(op);  
    updateClearLabel();  
  }  
  
  function handleEquals() {  
    if (!operator || previous === null) return;  
    const b   = waitingNext ? previous : parseFloat(current);  
    const res = calculate(previous, b, operator);  
    const exprStr = expression + ' ' + (waitingNext ? formatNumber(previous) : formatNumber(parseFloat(current))) + ' =';  
    setExpression(exprStr);  
    if (res === 'Error') { setDisplay('Error'); } else {  
      current = res.toString();  
      setDisplay(formatNumber(res));  
    }  
    operator    = null;  
    previous    = null;  
    waitingNext = false;  
    justEvaled  = true;  
    highlightOp(null);  
    updateClearLabel();  
  }  
  
  function handleClear() {  
    if (clearBtn.textContent === 'C') {  
      current = '0'; setDisplay('0');  
      clearBtn.textContent = 'AC';  
    } else {  
      current = '0'; previous = null; operator = null;  
      waitingNext = false; justEvaled = false; expression = '';  
      setDisplay('0'); setExpression(''); highlightOp(null);  
    }  
    updateClearLabel();  
  }  
  
  function handleSign() {  
    const n = parseFloat(current) * -1;  
    current = n.toString();  
    setDisplay(formatNumber(n));  
  }  
  
  function handlePercent() {  
    const n = parseFloat(current) / 100;  
    current = n.toString();  
    setDisplay(formatNumber(n));  
  }  
  
  // ── Events ─────────────────────────────────────────────  
  document.querySelectorAll('.btn').forEach(btn => {  
    btn.addEventListener('pointerdown', () => {  
      btn.classList.add('pressed');  
    });  
    btn.addEventListener('pointerup',   () => btn.classList.remove('pressed'));  
    btn.addEventListener('pointerleave',() => btn.classList.remove('pressed'));  
  
    btn.addEventListener('click', () => {  
      const { action, op, num } = btn.dataset;  
      switch(action) {  
        case 'num':     handleNum(num); break;  
        case 'decimal': handleDecimal(); break;  
        case 'op':      handleOp(op); break;  
        case 'equals':  handleEquals(); break;  
        case 'clear':   handleClear(); break;  
        case 'sign':    handleSign(); break;  
        case 'percent': handlePercent(); break;  
      }  
    });  
  });  
  
  // ── Keyboard support ───────────────────────────────────  
  document.addEventListener('keydown', e => {  
    if ('0123456789'.includes(e.key)) handleNum(e.key);  
    else if (e.key === '.')  handleDecimal();  
    else if (e.key === '+')  handleOp('+');  
    else if (e.key === '-')  handleOp('−');  
    else if (e.key === '*')  handleOp('×');  
    else if (e.key === '/')  { e.preventDefault(); handleOp('÷'); }  
    else if (e.key === 'Enter' || e.key === '=') handleEquals();  
    else if (e.key === 'Escape') handleClear();  
    else if (e.key === 'Backspace') {  
      if (current.length > 1) current = current.slice(0,-1);  
      else current = '0';  
      setDisplay(current); updateClearLabel();  
    }  
    else if (e.key === '%') handlePercent();  
  });  
</script>  
  
</body>  
</html>  
