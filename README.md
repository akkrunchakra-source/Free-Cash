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
}
.light{
background:#f2f2f2;
color:#000;
}

.screen{display:none;height:100vh;overflow:auto}
.show{display:block}

/* SIGNUP */
#signup{padding:20px;margin-top:40px}
input,select{
width:100%;
padding:14px;
margin:6px 0;
border:none;
border-radius:10px;
background:#ffffff22;
color:inherit;
}
.signup-btn{
margin-top:10px;
padding:14px;
border:none;
border-radius:30px;
background:linear-gradient(90deg,#ff416c,#ff4b2b);
color:#fff;
font-weight:bold;
}

/* HEADER */
.header{
margin:15px;
padding:16px;
border-radius:16px;
backdrop-filter:blur(10px);
background:rgba(255,255,255,0.15);
text-align:center;
}
.balance{font-size:28px;font-weight:bold}

/* BUTTON */
.main-btn{
margin-top:10px;
padding:14px;
background:#ffd700;
color:#000;
border-radius:30px;
text-align:center;
font-weight:bold;
}

/* EARN */
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

/* LIVE */
.live-box{margin:12px;border-radius:14px;overflow:hidden}
.live-header{padding:10px;background:linear-gradient(90deg,#ff0080,#ff8c00,#40e0d0);text-align:center}
.live-list{height:120px;background:#000;overflow:hidden}
.live-list ul{list-style:none;animation:scroll 8s linear infinite}
.live-list li{padding:6px;font-size:13px;color:#00ff9d}
@keyframes scroll{0%{transform:translateY(100%)}100%{transform:translateY(-100%)}}

/* NAV */
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

/* LOADER */
.loader{
position:fixed;
inset:0;
background:#000;
display:none;
align-items:center;
justify-content:center;
font-size:20px;
}

/* TOGGLE */
.toggle{
position:fixed;
top:10px;
right:10px;
background:#ffd700;
color:#000;
padding:6px 12px;
border-radius:20px;
font-size:12px;
}
</style>
</head>

<body>

<div class="toggle" onclick="toggleMode()">Mode</div>

<div id="loader" class="loader">Processing...</div>

<!-- SIGNUP -->
<div id="signup" class="screen show">
<h2>Signup kare aur ₹180 Bonus paaye</h2>
<input placeholder="+91 Phone">
<input placeholder="Password">
<input placeholder="Referral Code">
<input placeholder="Enter OTP">
<button class="signup-btn" onclick="signup()">Signup</button>
</div>

<!-- HOME -->
<div id="home" class="screen">
<div class="header">
Wallet Balance
<div class="balance" id="balance">₹0</div>
</div>

<!-- RECHARGE -->
<div style="padding:12px">
<input placeholder="Enter Mobile Number">
<select>
<option>Select SIM</option>
<option>Jio</option>
<option>Airtel</option>
<option>Vi</option>
</select>
<div class="main-btn" onclick="fakeLoad()">Recharge</div>
</div>

<!-- EARN -->
<div class="earn-options">
<div class="earn-box red">Earn Money</div>
<div class="earn-box green">Free Recharge</div>
<div class="earn-box red">Watch & Earn</div>
<div class="earn-box green">Share & Earn</div>
</div>

<!-- LIVE -->
<div class="live-box">
<div class="live-header">Live Activity</div>
<div class="live-list"><ul id="liveList"></ul></div>
</div>
</div>

<!-- PROFILE -->
<div id="profile" class="screen">
<div style="padding:20px">
<h2>Profile</h2>
<p>Name: Demo User</p>
<p>Status: Active</p>
</div>
</div>

<!-- HISTORY -->
<div id="history" class="screen">
<div style="padding:20px">
<h2>Transactions</h2>
<p>₹19 Recharge - Success</p>
<p>₹29 Recharge - Success</p>
<p>₹69 Recharge - Success</p>
</div>
</div>

<!-- NAV -->
<div class="bottom-nav">
<div class="active" onclick="nav('home',this)">Home</div>
<div onclick="nav('history',this)">History</div>
<div onclick="nav('profile',this)">Profile</div>
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
},1500);
}

function fakeLoad(){
loader.style.display="flex";
setTimeout(()=>loader.style.display="none",1500);
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

/* LIVE */
const names=["Rahul","Ankit","Pooja","Neha","Rohit"];
function addLive(){
let li=document.createElement("li");
li.innerText=names[Math.floor(Math.random()*5)]+" Activity Done";
liveList.appendChild(li);
}
for(let i=0;i<8;i++)addLive();
</script>

</body>
</html>
