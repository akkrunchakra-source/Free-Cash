<html lang="hi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Wallet App</title>

<style>
*{box-sizing:border-box;margin:0;padding:0}
body{
font-family:Arial;
background:linear-gradient(120deg,#0f2027,#203a43,#2c5364);
color:#fff;
transition:.4s;
overflow:hidden;
}
.light{background:#f2f2f2;color:#000}

.screen{
display:none;
height:100vh;
overflow:auto;
animation:fade .4s ease;
}
.show{display:block}
@keyframes fade{from{opacity:0;transform:scale(.96)}to{opacity:1}}

.header{
margin:15px;
padding:16px;
border-radius:16px;
background:rgba(255,255,255,0.15);
backdrop-filter:blur(10px);
text-align:center;
position:relative;
}
.balance{font-size:28px;font-weight:bold}

.bell{
position:absolute;
right:15px;
top:15px;
font-size:20px;
cursor:pointer;
}

.notify-box{
position:fixed;
top:60px;
right:10px;
background:#000;
border-radius:12px;
width:220px;
display:none;
z-index:99;
}
.notify-box div{
padding:10px;
font-size:13px;
border-bottom:1px solid #333;
}

.main-btn{
margin-top:10px;
padding:14px;
background:#ffd700;
color:#000;
border-radius:30px;
text-align:center;
font-weight:bold;
}

.earn-options{margin:12px;display:flex;flex-direction:column;gap:10px}
.earn-box{
padding:14px;
border-radius:12px;
text-align:center;
font-weight:bold;
animation:blink 1.5s infinite;
}
.red{background:linear-gradient(90deg,#ff416c,#ff4b2b)}
.green{background:linear-gradient(90deg,#11998e,#38ef7d)}
@keyframes blink{50%{opacity:.7}}

.live-box{margin:12px;border-radius:14px;overflow:hidden}
.live-header{padding:10px;background:linear-gradient(90deg,#ff0080,#ff8c00,#40e0d0);text-align:center}
.live-list{height:120px;background:#000;overflow:hidden}
.live-list ul{list-style:none;animation:scroll 8s linear infinite}
.live-list li{padding:6px;font-size:13px;color:#00ff9d}
@keyframes scroll{0%{transform:translateY(100%)}100%{transform:translateY(-100%)}}

.bottom-nav{
position:fixed;
bottom:0;
left:0;
right:0;
background:#000;
display:flex;
justify-content:space-around;
padding:10px 0;
}
.bottom-nav div{font-size:12px;color:#aaa}
.bottom-nav .active{color:#ffd700}

.loader{
position:fixed;
inset:0;
background:#000;
display:none;
align-items:center;
justify-content:center;
font-size:20px;
z-index:100;
}

.toggle{
position:fixed;
top:10px;
left:10px;
background:#ffd700;
color:#000;
padding:6px 12px;
border-radius:20px;
font-size:12px;
z-index:99;
}

.avatar{
width:90px;
height:90px;
border-radius:50%;
background:#444;
margin:auto;
overflow:hidden;
}
.avatar img{width:100%;height:100%;object-fit:cover}

/* RECHARGE PLANS */
.plans{
margin-top:12px;
display:grid;
grid-template-columns:1fr 1fr;
gap:10px;
}
.plan{
padding:12px;
border-radius:12px;
background:#ffffff15;
border:2px solid transparent;
font-size:13px;
position:relative;
cursor:pointer;
}
.plan.active{
border:2px solid #00ff9d;
background:#00ff9d22;
}
.tick{
position:absolute;
top:6px;
right:8px;
display:none;
color:#00ff9d;
}
.plan.active .tick{display:block}

</style>
</head>

<body>

<div class="toggle" onclick="toggleMode()">Mode</div>
<div id="loader" class="loader">Processing...</div>

<div class="notify-box" id="notifyBox">
<div>₹19 Recharge Success</div>
<div>New Offer Available</div>
<div>Wallet Updated</div>
</div>

<!-- SIGNUP -->
<div id="signup" class="screen show">
<div style="padding:20px;margin-top:40px">
<h2>Signup kare aur ₹180 Bonus paaye</h2>
<input placeholder="+91 Phone">
<input placeholder="Password">
<input placeholder="Referral Code">
<input placeholder="Enter OTP">
<div class="main-btn" onclick="signup()">Signup</div>
</div>
</div>

<!-- HOME -->
<div id="home" class="screen">
<div class="header">
Wallet Balance
<div class="balance" id="balance">₹0</div>
<div class="bell" onclick="toggleNotify()">🔔</div>
</div>

<div style="padding:12px">
<input placeholder="Enter Mobile Number">

<select>
<option>Select SIM</option>
<option>Jio</option>
<option>Airtel</option>
<option>Vi</option>
</select>

<!-- PLANS -->
<div class="plans">

<div class="plan" onclick="selectPlan(this)">
<div class="tick">✔</div>
<b>₹19</b><br>
1GB Data<br>
Validity: 1 Day
</div>

<div class="plan" onclick="selectPlan(this)">
<div class="tick">✔</div>
<b>₹19</b><br>
Unlimited Data*<br>
Validity: 1 Hour
</div>

<div class="plan" onclick="selectPlan(this)">
<div class="tick">✔</div>
<b>₹19</b><br>
1GB + 100 SMS<br>
Validity: 1 Day
</div>

<div class="plan" onclick="selectPlan(this)">
<div class="tick">✔</div>
<b>₹19</b><br>
1.5GB Data<br>
Validity: 1 Day
</div>

</div>

<div class="main-btn" onclick="fakeLoad()">Recharge</div>
</div>

<div class="earn-options">
<div class="earn-box red">Earn Money</div>
<div class="earn-box green">Free Recharge</div>
<div class="earn-box red">Watch & Earn</div>
<div class="earn-box green">Share & Earn</div>
</div>

<div class="live-box">
<div class="live-header">Live Activity</div>
<div class="live-list"><ul id="liveList"></ul></div>
</div>
</div>

<!-- PROFILE -->
<div id="profile" class="screen">
<div style="padding:20px;text-align:center">
<div class="avatar">
<img id="avatarImg">
</div>
<input type="file" onchange="loadAvatar(event)">
<h3>Demo User</h3>
<p>Status: Active</p>
</div>
</div>

<!-- SETTINGS -->
<div id="settings" class="screen">
<div style="padding:20px">
<h2>Settings</h2>
<p>Notification: ON</p>
<p>Theme: Auto</p>
<p>Version: 1.0</p>
</div>
</div>

<!-- HISTORY -->
<div id="history" class="screen">
<div style="padding:20px">
<h2>Transactions</h2>
<p>₹19 Recharge - Success</p>
<p>₹29 Recharge - Success</p>
</div>
</div>

<div class="bottom-nav">
<div class="active" onclick="nav('home',this)">Home</div>
<div onclick="nav('history',this)">History</div>
<div onclick="nav('profile',this)">Profile</div>
<div onclick="nav('settings',this)">Settings</div>
</div>

<script>

let bal=0;

function signup(){
fakeLoad();
setTimeout(()=>{
showScreen("home");
let i=setInterval(()=>{
if(bal<180){bal++;balance.innerText="₹"+bal}
else clearInterval(i);
},20);
},1200);
}

function fakeLoad(){
loader.style.display="flex";
setTimeout(()=>loader.style.display="none",1200);
}

function showScreen(id){
document.querySelectorAll(".screen").forEach(s=>s.style.display="none");
document.getElementById(id).style.display="block";
}

function nav(id,el){
showScreen(id);
document.querySelectorAll(".bottom-nav div").forEach(d=>d.classList.remove("active"));
el.classList.add("active");
}

function toggleMode(){
document.body.classList.toggle("light");
}

function toggleNotify(){
notifyBox.style.display =
notifyBox.style.display=="block"?"none":"block";
}

function loadAvatar(e){
avatarImg.src=URL.createObjectURL(e.target.files[0]);
}

/* PLAN SELECT */
function selectPlan(el){
document.querySelectorAll(".plan").forEach(p=>p.classList.remove("active"));
el.classList.add("active");
}

/* LIVE */
const names=["Rahul","Ankit","Pooja","Neha","Rohit"];
function addLive(){
let li=document.createElement("li");
li.innerText=names[Math.floor(Math.random()*5)]+" Recharge Success";
liveList.appendChild(li);
}
for(let i=0;i<8;i++)addLive();

</script>

</body>
</html>
