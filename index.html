<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>Лекции в текст</title>
<style>
  :root{
    --paper:#FCFCFA;
    --ink:#1B2430;
    --ink-soft:#5B6472;
    --line:#E1DED4;
    --rec:#C1443C;
    --rec-dark:#9A322C;
    --ok:#3A7267;
    --ok-dark:#2A5750;
  }
  *{box-sizing:border-box; -webkit-tap-highlight-color:transparent;}
  html,body{
    margin:0; padding:0; height:100%;
    background:var(--paper); color:var(--ink);
    font-family:-apple-system,Roboto,"Segoe UI",Arial,sans-serif;
  }
  body{
    display:flex; flex-direction:column; height:100vh; overflow:hidden;
  }
  header{
    padding:16px 18px 10px;
    border-bottom:1px solid var(--line);
    flex-shrink:0;
  }
  h1{
    margin:0; font-size:20px; font-weight:700; letter-spacing:-0.01em;
  }
  #status{
    margin-top:4px; font-size:14px; color:var(--ink-soft); min-height:18px;
  }
  #timer{
    font-variant-numeric:tabular-nums; font-weight:600;
  }
  main{
    flex:1; overflow:hidden; padding:14px 18px; display:flex; flex-direction:column;
  }
  #transcript{
    flex:1; overflow-y:auto; -webkit-overflow-scrolling:touch;
    font-size:19px; line-height:1.55;
    padding:12px 4px; outline:none;
    white-space:pre-wrap; word-wrap:break-word;
  }
  #transcript:empty::before{
    content:"Нажмите «Записать» и говорите. Текст будет появляться здесь.";
    color:var(--ink-soft);
  }
  .interim{ color:var(--ink-soft); }
  footer{
    flex-shrink:0; padding:14px 18px 20px;
    border-top:1px solid var(--line);
    display:flex; flex-direction:column; gap:10px;
  }
  .row{ display:flex; gap:10px; }
  button{
    border:none; border-radius:12px; font-size:17px; font-weight:600;
    padding:16px 10px; cursor:pointer; flex:1;
    -webkit-user-select:none; user-select:none;
  }
  #startBtn{ background:var(--rec); color:#fff; }
  #startBtn:active{ background:var(--rec-dark); }
  #stopBtn{ background:var(--ink); color:#fff; display:none; }
  #stopBtn:active{ background:#000; }
  .secondary{ background:#fff; color:var(--ink); border:1px solid var(--line); flex:1; font-size:15px; padding:12px 8px; }
  .secondary:active{ background:var(--line); }
  #saveBtn{ color:var(--ok-dark); border-color:var(--ok); }
  .dot{
    display:inline-block; width:10px; height:10px; border-radius:50%;
    background:var(--rec); margin-right:6px; vertical-align:middle;
    animation:pulse 1.2s infinite ease-in-out;
  }
  .dot.hidden{ display:none; }
  @keyframes pulse{ 0%,100%{opacity:1;} 50%{opacity:.25;} }
</style>
</head>
<body>

<header>
  <h1>Лекции в текст</h1>
  <div id="status"><span class="dot hidden" id="dot"></span><span id="statusText">Готово к записи</span> <span id="timer"></span></div>
</header>

<main>
  <div id="transcript" contenteditable="true"></div>
</main>

<footer>
  <div class="row">
    <button id="startBtn">● Записать</button>
    <button id="stopBtn">■ Остановить</button>
  </div>
  <div class="row">
    <button class="secondary" id="saveBtn">Сохранить .txt</button>
    <button class="secondary" id="copyBtn">Копировать</button>
    <button class="secondary" id="clearBtn">Очистить</button>
  </div>
</footer>

<script>
let recognition = null;
let recognizing = false;
let finalTranscript = '';
let startTime = 0;
let timerInterval = null;

const transcriptEl = document.getElementById('transcript');
const statusText = document.getElementById('statusText');
const dot = document.getElementById('dot');
const timerEl = document.getElementById('timer');
const startBtn = document.getElementById('startBtn');
const stopBtn = document.getElementById('stopBtn');

function setStatus(text){ statusText.textContent = text; }

function initRecognition(){
  const SR = window.SpeechRecognition || window.webkitSpeechRecognition;
  if(!SR){
    setStatus('Браузер не поддерживает распознавание речи. Установите Google Chrome.');
    startBtn.disabled = true;
    return null;
  }
  const rec = new SR();
  rec.lang = 'ru-RU';
  rec.continuous = true;
  rec.interimResults = true;
  rec.maxAlternatives = 1;

  rec.onresult = function(event){
    let interim = '';
    for(let i = event.resultIndex; i < event.results.length; i++){
      const t = event.results[i][0].transcript;
      if(event.results[i].isFinal){
        finalTranscript += t + ' ';
      } else {
        interim += t;
      }
    }
    render(interim);
  };

  rec.onerror = function(event){
    if(event.error === 'not-allowed' || event.error === 'service-not-allowed'){
      setStatus('Нет доступа к микрофону. Разрешите доступ в настройках браузера.');
      stopRecording();
    } else if(event.error === 'network'){
      setStatus('Нет интернета — для распознавания речи нужна сеть.');
    }
    // 'no-speech' и подобные ошибки игнорируем, распознавание перезапустится само
  };

  rec.onend = function(){
    if(recognizing){
      try{ rec.start(); } catch(e){}
    }
  };

  return rec;
}

function render(interim){
  transcriptEl.innerHTML = escapeHtml(finalTranscript) + '<span class="interim">' + escapeHtml(interim) + '</span>';
  transcriptEl.scrollTop = transcriptEl.scrollHeight;
}

function escapeHtml(s){
  return s.replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;');
}

function startRecording(){
  if(!recognition){ recognition = initRecognition(); }
  if(!recognition) return;

  // подхватываем текст, если он уже был отредактирован вручную
  finalTranscript = transcriptEl.innerText;
  if(finalTranscript && !finalTranscript.endsWith(' ') && !finalTranscript.endsWith('\n')){
    finalTranscript += ' ';
  }

  recognizing = true;
  try{ recognition.start(); } catch(e){}

  setStatus('Идёт запись');
  dot.classList.remove('hidden');
  startBtn.style.display = 'none';
  stopBtn.style.display = 'block';

  startTime = Date.now();
  timerInterval = setInterval(updateTimer, 1000);
  updateTimer();
}

function stopRecording(){
  recognizing = false;
  if(recognition){ try{ recognition.stop(); } catch(e){} }
  setStatus('Остановлено');
  dot.classList.add('hidden');
  startBtn.style.display = 'block';
  stopBtn.style.display = 'none';
  clearInterval(timerInterval);
}

function updateTimer(){
  const diff = Math.floor((Date.now() - startTime) / 1000);
  const m = String(Math.floor(diff/60)).padStart(2,'0');
  const s = String(diff%60).padStart(2,'0');
  timerEl.textContent = m + ':' + s;
}

function saveText(){
  const text = transcriptEl.innerText.trim();
  if(!text){ setStatus('Пока нечего сохранять'); return; }
  const blob = new Blob([text], {type:'text/plain;charset=utf-8'});
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a');
  const d = new Date();
  const pad = n => String(n).padStart(2,'0');
  const fname = 'lekciya_' + d.getFullYear() + '-' + pad(d.getMonth()+1) + '-' + pad(d.getDate()) + '_' + pad(d.getHours()) + '-' + pad(d.getMinutes()) + '.txt';
  a.href = url; a.download = fname;
  document.body.appendChild(a); a.click(); document.body.removeChild(a);
  URL.revokeObjectURL(url);
  setStatus('Файл сохранён: ' + fname);
}

function copyText(){
  const text = transcriptEl.innerText;
  if(navigator.clipboard && navigator.clipboard.writeText){
    navigator.clipboard.writeText(text).then(function(){
      setStatus('Текст скопирован');
    }).catch(fallbackCopy);
  } else {
    fallbackCopy();
  }
}

function fallbackCopy(){
  const range = document.createRange();
  range.selectNodeContents(transcriptEl);
  const sel = window.getSelection();
  sel.removeAllRanges(); sel.addRange(range);
  try{ document.execCommand('copy'); setStatus('Текст скопирован'); }
  catch(e){ setStatus('Не удалось скопировать'); }
  sel.removeAllRanges();
}

function clearText(){
  if(confirm('Очистить весь текст?')){
    finalTranscript = '';
    transcriptEl.innerHTML = '';
    setStatus('Готово к записи');
  }
}

startBtn.addEventListener('click', startRecording);
stopBtn.addEventListener('click', stopRecording);
document.getElementById('saveBtn').addEventListener('click', saveText);
document.getElementById('copyBtn').addEventListener('click', copyText);
document.getElementById('clearBtn').addEventListener('click', clearText);

window.addEventListener('load', function(){
  recognition = initRecognition();
});

// не даём экрану гаснуть во время записи, если браузер это поддерживает
let wakeLock = null;
async function keepAwake(){
  try{
    if('wakeLock' in navigator){ wakeLock = await navigator.wakeLock.request('screen'); }
  } catch(e){}
}
startBtn.addEventListener('click', keepAwake);
</script>

</body>
</html>
