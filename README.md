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
margin-top:12px;
padding:14px;
background:#ffd700;
color:#000;
border-radius:30px;
text-align:center;
font-weight:bold;
cursor:pointer;
}

/* SIGNUP LIVE TICKER */
.signup-live{
margin-top:15px;
background:#000;
border-radius:12px;
overflow:hidden;
height:32px;
display:flex;
align-items:center;
}

.signup-live span{
white-space:nowrap;
display:inline-block;
padding-left:100%;
animation:signupTicker 12s linear infinite;
color:#00ff9d;
font-size:13px;
}

@keyframes signupTicker{
0%{transform:translateX(0)}
100%{transform:translateX(-100%)}
}

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
</style>
</head>

<body>

<div class="toggle" onclick="toggleMode()">Mode</div>
<div id="loader" class="loader">Processing...</div>

<!-- SIGNUP -->
<div id="signup" class="screen show">
<div style="padding:20px;margin-top:40px">
<h2>Signup kare aur ₹180 Bonus paaye</h2>

<input placeholder="+91 Phone" style="width:100%;padding:10px;margin-top:10px">
<input placeholder="Password" style="width:100%;padding:10px;margin-top:10px">
<input placeholder="Referral Code" style="width:100%;padding:10px;margin-top:10px">
<input placeholder="Enter OTP" style="width:100%;padding:10px;margin-top:10px">

<div class="main-btn" onclick="signup()">Signup</div>

<!-- LIVE SIGNUP LINE -->
<div class="signup-live">
<span id="signupLiveText">Loading...</span>
</div>

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
<input placeholder="Enter Mobile Number" style="width:100%;padding:10px">

<select style="width:100%;padding:10px;margin-top:10px">
<option>Select SIM</option>
<option>Jio</option>
<option>Airtel</option>
<option>Vi</option>
</select>

<div class="main-btn" onclick="fakeLoad()">Recharge</div>
</div>
</div>

<div class="bottom-nav">
<div class="active" onclick="nav('home',this)">Home</div>
<div onclick="nav('signup',this)">Signup</div>
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

/* SIGNUP LIVE DATA */
const names=[
"Riya","Pooja","Anjali","Sneha","Kiran",
"Rahul","Aman","Rohit","Vikas","Ankit"
];
const sims=["Jio","Airtel","Vi"];

function updateSignupLive(){
let name=names[Math.floor(Math.random()*names.length)];
let sim=sims[Math.floor(Math.random()*sims.length)];
signupLiveText.innerText=
name+" Recharge Successfully - "+sim;
}

updateSignupLive();
setInterval(updateSignupLive,3000);
</script>

</body>
</html>
