
<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>TzuyHub Private Notification</title>
<style>
*{box-sizing:border-box}
body{
 background:#080808;color:white;
 font-family:Arial;margin:0;padding:20px;
}
.container{
 max-width:440px;margin:30px auto;
 background:#151515;padding:22px;
 border:1px solid #333;border-radius:18px;
}
h2{text-align:center;color:#a855f7}
h3{color:#c084fc}
input,button{
 width:100%;padding:13px;margin:8px 0;
 border-radius:9px;border:1px solid #444;
 background:#222;color:white;
}
button{
 background:#8b5cf6;border:0;
 font-weight:bold;cursor:pointer;
}
.notice{
 padding:13px;background:#222;
 border-left:3px solid #a855f7;
 border-radius:8px;margin:10px 0;
 overflow-wrap:anywhere;
}
.status{text-align:center;color:#aaa}
.counter{color:#c084fc}
</style>
</head>
<body>

<div class="container">
<h2>⚡ TZUYHUB</h2>
<p class="status">PRIVATE ACCOUNT SYSTEM</p>

<h3>👤 ACCOUNT</h3>
<div class="notice">
Username: <b>tuongduy</b><br>
Account: <span style="color:#22c55e">ACTIVE</span>
</div>

<h3>🔔 PRIVATE NOTIFICATION</h3>
<div class="notice">
Thông báo chưa đọc:
<b class="counter" id="counter">0</b>
</div>

<div id="notifications"></div>

<h3>📩 Gửi thông báo cho tài khoản</h3>
<input id="message" placeholder="Nhập nội dung thông báo...">
<button onclick="sendNotification()">SEND NOTIFICATION</button>

<button onclick="markRead()">MARK ALL READ</button>
<button onclick="clearHistory()" style="background:#dc2626">
DELETE HISTORY
</button>

<p class="status">TZUYHUB © 2026</p>
</div>

<script>
const KEY="tzuyhub_private_notifications";

function getData(){
 return JSON.parse(localStorage.getItem(KEY)||"[]");
}

function sendNotification(){
 const input=document.getElementById("message");
 const message=input.value.trim();

 if(!message){
  alert("Vui lòng nhập nội dung!");
  return;
 }

 const data=getData();

 data.unshift({
  message:message,
  time:new Date().toLocaleString("vi-VN"),
  read:false
 });

 localStorage.setItem(KEY,JSON.stringify(data));
 input.value="";
 render();

 alert("Đã tạo thông báo riêng!");
}

function render(){
 const data=getData();

 document.getElementById("counter").textContent=
 data.filter(x=>!x.read).length;

 document.getElementById("notifications").innerHTML=
 data.map((x,i)=>`
 <div class="notice">
 <b>🔔 ${x.read?"Đã đọc":"Thông báo mới"}</b>
 <p>${escapeHTML(x.message)}</p>
 <small>${escapeHTML(x.time)}</small>
 </div>
 `).join("")||'<p class="status">Chưa có thông báo.</p>';
}

function escapeHTML(s){
 return String(s).replace(/[&<>"']/g,c=>({
 "&":"&amp;","<":"&lt;",">":"&gt;",
 '"':"&quot;","'":"&#39;"
 }[c]));
}

function markRead(){
 const data=getData().map(x=>({...x,read:true}));
 localStorage.setItem(KEY,JSON.stringify(data));
 render();
}

function clearHistory(){
 if(confirm("Xóa tất cả thông báo?")){
  localStorage.removeItem(KEY);
  render();
 }
}

render();
</script>
</body>
</html>
