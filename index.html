<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="UTF-8">
<title>🔑 Tzuy Key — Hạn 2 ngày</title>
<meta name="viewport" content="width=device-width, initial-scale=1">
<style>
  *{box-sizing:border-box}
  body{font-family:system-ui,sans-serif;background:#0f172a;color:#e2e8f0;margin:0;padding:20px;display:flex;justify-content:center;align-items:flex-start;min-height:100vh}
  .card{background:#1e293b;border-radius:16px;padding:28px;max-width:540px;width:100%;box-shadow:0 10px 30px #0006}
  h1{margin:0 0 10px;font-size:24px}
  h2{font-size:15px;margin-top:28px;color:#94a3b8;text-transform:uppercase;letter-spacing:1px}
  p{color:#94a3b8;line-height:1.5;margin:8px 0}
  input{width:100%;padding:12px 14px;border-radius:10px;border:1px solid #334155;background:#0f172a;color:#e2e8f0;font-size:15px;margin:8px 0}
  button,.btn{display:inline-block;width:100%;text-align:center;padding:12px;border:none;border-radius:10px;background:linear-gradient(135deg,#6366f1,#8b5cf6);color:#fff;font-weight:600;font-size:15px;cursor:pointer;text-decoration:none;margin-top:8px;transition:.2s}
  button:hover,.btn:hover{opacity:.9}
  button.ghost{background:#334155}
  .key{background:#0f172a;border:1px dashed #8b5cf6;border-radius:10px;padding:16px;font-family:monospace;font-size:16px;text-align:center;word-break:break-all;margin:12px 0;color:#a78bfa;font-weight:600}
  .ok{color:#4ade80}.err{color:#f87171}
  .hidden{display:none!important}
  .step{background:#0f172a;border-radius:10px;padding:14px;margin:12px 0;border-left:3px solid #6366f1}
  .step.done{border-left-color:#4ade80}
  .step b{color:#a78bfa}
  .badge{display:inline-block;background:#7c3aed33;color:#a78bfa;padding:4px 10px;border-radius:999px;font-size:12px;font-weight:600;border:1px solid #8b5cf655;margin:0 4px 8px 0}
  .badge.green{background:#05966933;color:#34d399;border-color:#34d39955}
  .timer{background:#0f172a;border-radius:10px;padding:12px;margin:10px 0;text-align:center;font-family:monospace;font-size:15px;color:#4ade80;font-weight:600}
  .progress{display:flex;gap:8px;margin:14px 0}
  .progress span{flex:1;height:6px;border-radius:3px;background:#334155;transition:.3s}
  .progress span.active{background:#8b5cf6}
  .progress span.done{background:#4ade80}
</style>
</head>
<body>
<div class="card">
  <h1>🔑 Tzuy Key</h1>
  <span class="badge">⏱️ Hạn: 2 ngày</span>
  <span class="badge green">🔗 Cần vượt 2 link</span>

  <div class="progress"><span id="p1"></span><span id="p2"></span></div>

  <p>Hoàn thành <b>2 link4sub</b> dưới đây để nhận key có hạn <b>2 ngày</b>.</p>

  <div id="step1">
    <div class="step"><b>Bước 1/2:</b> Vượt link4sub #1 bên dưới.</div>
    <a class="btn" id="link1Btn" href="#" target="_blank" rel="noopener">🚀 Bước 1 — Vượt link4sub #1</a>
    <div id="msg1" style="margin-top:10px"></div>
  </div>

  <div id="step2" class="hidden">
    <div class="step done">✅ <b>Bước 1 hoàn thành!</b></div>
    <div class="step"><b>Bước 2/2:</b> Vượt link4sub #2 bên dưới để nhận key.</div>
    <a class="btn" id="link2Btn" href="#" target="_blank" rel="noopener">🚀 Bước 2 — Vượt link4sub #2</a>
    <button class="ghost" onclick="resetSession()">↻ Bắt đầu lại</button>
    <div id="msg2" style="margin-top:10px"></div>
  </div>

  <div id="step3" class="hidden">
    <p class="ok">🎉 Lấy key thành công! Hạn <b>2 ngày</b>:</p>
    <div class="key" id="keyDisplay">Tzuy_XXXX</div>
    <div class="timer" id="timer">⏱️ Hạn còn lại: --</div>
    <p style="font-size:13px">📅 Hết hạn: <b id="expiresText">--</b></p>
    <button onclick="copyKey()">📋 Copy Key</button>
    <button class="ghost" onclick="resetSession()">🔄 Lấy key mới</button>
    <p style="font-size:13px;margin-top:14px">🔗 Link chia sẻ: <code id="shareUrl" style="color:#a78bfa">đang tải...</code></p>
  </div>

  <h2>🔍 Kiểm tra Key</h2>
  <input id="checkInput" placeholder="Nhập key (Tzuy_...)">
  <button onclick="checkKey()">Kiểm tra</button>
  <div id="checkResult" style="margin-top:10px"></div>
</div>

<script>
const params = new URLSearchParams(location.search);
const SK = 'tzuy_token1';
let currentKey = '';
let timerInterval = null;

window.addEventListener('DOMContentLoaded', async () => {
  await loadConfig();
  const urlToken = params.get('token');
  const saved1 = sessionStorage.getItem(SK);

  if (urlToken) {
    history.replaceState({}, '', '/get-key');
    if (!saved1) {
      sessionStorage.setItem(SK, urlToken);
      showStep(2); setProgress(1);
    } else {
      await submitBoth(saved1, urlToken);
    }
  } else {
    if (saved1) { showStep(2); setProgress(1); }
    else { showStep(1); setProgress(0); }
  }
});

async function loadConfig() {
  try {
    const r = await fetch('/api/config');
    const c = await r.json();
    document.getElementById('link1Btn').href = c.link4sub_1;
    document.getElementById('link2Btn').href = c.link4sub_2;
    document.getElementById('shareUrl').textContent = c.shareUrl;
  } catch (e) { console.error(e); }
}

function showStep(n) {
  document.getElementById('step1').classList.toggle('hidden', n !== 1);
  document.getElementById('step2').classList.toggle('hidden', n !== 2);
  document.getElementById('step3').classList.toggle('hidden', n !== 3);
}

function setProgress(done) {
  document.getElementById('p1').className = done >= 1 ? 'done' : (done === 0 ? 'active' : '');
  document.getElementById('p2').className = done >= 2 ? 'done' : (done === 1 ? 'active' : '');
}

async function submitBoth(t1, t2) {
  showStep(2);
  const msg = document.getElementById('msg2');
  msg.innerHTML = '<p>⏳ Đang xác thực 2 token...</p>';
  try {
    const r = await fetch('/api/verify', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ tokens: [t1, t2] })
    });
    const data = await r.json();
    if (!r.ok) {
      msg.innerHTML = `<p class="err">❌ ${data.error}</p>
        <button class="ghost" onclick="resetSession()">↻ Bắt đầu lại</button>`;
      return;
    }
    sessionStorage.removeItem(SK);
    currentKey = data.key;
    document.getElementById('keyDisplay').textContent = data.key;
    document.getElementById('expiresText').textContent =
      new Date(data.expiresAt).toLocaleString('vi-VN');
    showStep(3); setProgress(2);
    startCountdown(new Date(data.expiresAt).getTime());
  } catch (e) {
    msg.innerHTML = `<p class="err">❌ Lỗi: ${e.message}</p>`;
  }
}

function startCountdown(exp) {
  if (timerInterval) clearInterval(timerInterval);
  const el = document.getElementById('timer');
  const tick = () => {
    const ms = exp - Date.now();
    if (ms <= 0) {
      el.textContent = '❌ Key đã hết hạn';
      el.style.color = '#f87171';
      clearInterval(timerInterval);
      return;
    }
    el.textContent = '⏱️ Hạn còn lại: ' + fmt(ms);
  };
  tick();
  timerInterval = setInterval(tick, 1000);
}

function fmt(ms) {
  if (ms <= 0) return '0 giây';
  const s = Math.floor(ms / 1000);
  const d = Math.floor(s / 86400);
  const h = Math.floor((s % 86400) / 3600);
  const m = Math.floor((s % 3600) / 60);
  const sec = s % 60;
  const p = [];
  if (d > 0) p.push(`${d} ngày`);
  if (h > 0) p.push(`${h} giờ`);
  if (m > 0) p.push(`${m} phút`);
  if (p.length === 0 || d === 0) p.push(`${sec} giây`);
  return p.join(' ');
}

function resetSession() {
  sessionStorage.removeItem(SK);
  if (timerInterval) clearInterval(timerInterval);
  currentKey = '';
  document.getElementById('keyDisplay').textContent = 'Tzuy_XXXX';
  document.getElementById('timer').textContent = '⏱️ Hạn còn lại: --';
  document.getElementById('timer').style.color = '#4ade80';
  document.getElementById('expiresText').textContent = '--';
  document.getElementById('msg1').innerHTML = '';
  document.getElementById('msg2').innerHTML = '';
  showStep(1); setProgress(0);
  history.replaceState({}, '', '/get-key');
}

function copyKey() {
  navigator.clipboard.writeText(currentKey);
  alert('Đã copy: ' + currentKey);
}

async function checkKey() {
  const key = document.getElementById('checkInput').value.trim();
  const box = document.getElementById('checkResult');
  if (!key) { box.innerHTML = '<p class="err">Nhập key trước</p>'; return; }
  box.innerHTML = '<p>⏳ Đang kiểm tra...</p>';
  try {
    const r = await fetch('/api/check', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ key })
    });
    const d = await r.json();
    if (d.valid) {
      box.innerHTML = `
        <p class="ok">✅ ${d.reason}</p>
        <p style="font-size:13px">
          📅 Tạo: ${new Date(d.createdAt).toLocaleString('vi-VN')}<br>
          ⏰ Hết hạn: ${new Date(d.expiresAt).toLocaleString('vi-VN')}<br>
          ⏱️ Còn lại: <b class="ok">${d.remainingText}</b>
        </p>`;
    } else {
      let ex = '';
      if (d.expiresAt) ex = `<br><small>Hết hạn: ${new Date(d.expiresAt).toLocaleString('vi-VN')}</small>`;
      box.innerHTML = `<p class="err">❌ ${d.reason}${ex}</p>`;
    }
  } catch (e) {
    box.innerHTML = `<p class="err">Lỗi: ${e.message}</p>`;
  }
}
</script>
</body>
</html>
