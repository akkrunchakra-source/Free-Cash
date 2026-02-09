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

.screen{
display:none;
height:100vh;
overflow:auto;
animation:fade .5s ease;
}
.show{display:block}

@keyframes fade{
from{opacity:0;transform:translateY(15px)}
to{opacity:1}
}

/* BUTTON */
.main-btn{
margin-top:14px;
padding:14px;
background:#ffd700;
color:#000;
border-radius:30px;
text-align:center;
font-weight:bold;
cursor:pointer;
transition:.3s;
}
.main-btn:hover{transform:scale(1.03)}

/* SOCIAL PROOF */
.social-proof{
margin-top:15px;
display:flex;
justify-content:space-between;
font-size:13px;
opacity:.9;
}

/* LIVE LINE */
.signup-live{
margin-top:15px;
background:#000;
border-radius:12px;
overflow:hidden;
height:34px;
display:flex;
align-items:center;
}

.signup-live span{
white-space:nowrap;
display:inline-block;
padding-left:100%;
animation:ticker 14s linear infinite;
font-size:13px;
}

@keyframes ticker{
0%{transform:translateX(0)}
100%{transform:translateX(-100%)}
}

/* COLORS */
.jio{color:#00a8ff}
.airtel{color:#ff3b3b}
.vi{color:#a020f0}

/* INPUT */
input{
width:100%;
padding:11px;
margin-top:10px;
border-radius:8px;
border:none;
}

/* BOTTOM */
.bottom-nav{
position:fixed;
bottom:0;
left:0;
right:0;
background:#000;
display:flex;
justify-content:space-around;
padding:10px 0;
font-size:12px;
}

.bottom-nav div{color:#aaa}
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

</style>
</head>

<body>

<div id="loader" class="loader">Processing...</div>

<!-- SIGNUP -->
<div id="signup" class="screen show">
<div style="padding:20px;margin-top:40px">

<h2>Signup kare aur ₹180 Bonus paaye</h2>

<input placeholder="+91 Phone" id="phoneInput">
<input placeholder="Password">
<input placeholder="Referral Code">
<input placeholder="Enter OTP">

<div class="main-btn" onclick="signup()">Signup</div>

<!-- SOCIAL PROOF -->
<div class="social-proof">
<div>Users Online: <b id="onlineCount">128</b></div>
<div>Today Rewards: <b id="rewardCount">532</b></div>
</div>

<!-- LIVE -->
<div class="signup-live">
<span id="signupLiveText">Loading...</span>
</div>

</div>
</div>

<!-- HOME -->
<div id="home" class="screen">
<div style="padding:20px">
<h2>Wallet Balance</h2>
<h1 id="balance">₹0</h1>
</div>
</div>

<div class="bottom-nav">
<div class="active" onclick="nav('signup',this)">Signup</div>
<div onclick="nav('home',this)">Home</div>
</div>

<!-- SOUND -->
<audio id="signupSound">
<source src="https://actions.google.com/sounds/v1/cartoon/clang_and_wobble.ogg">
</audio>

<script>

let bal=0;

function signup(){
signupSound.play();

loader.style.display="flex";

setTimeout(()=>{
loader.style.display="none";
showScreen("home");

let i=setInterval(()=>{
if(bal<180){
bal++;
balance.innerText="₹"+bal;
}
else clearInterval(i);
},15);

},1200);
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

/* SOCIAL PROOF COUNTER */
setInterval(()=>{
onlineCount.innerText=120+Math.floor(Math.random()*20);
rewardCount.innerText=500+Math.floor(Math.random()*80);
},4000);

/* LIVE DATA */
const names=["Riya","Pooja","Anjali","Sneha","Kiran","Rahul","Aman","Rohit"];
const sims=["Jio","Airtel","Vi"];

function maskNumber(){
let num=""+Math.floor(6000000000+Math.random()*3000000000);
return num.slice(0,4)+"****"+num.slice(8);
}

function updateLive(){

let name=names[Math.floor(Math.random()*names.length)];
let sim=sims[Math.floor(Math.random()*sims.length)];
let number=maskNumber();

let colorClass=
sim=="Jio"?"jio":
sim=="Airtel"?"airtel":"vi";

signupLiveText.innerHTML=
name+" "+number+" Recharge Success - <span class='"+colorClass+"'>"+sim+"</span>";

}

updateLive();
setInterval(updateLive,3000);

</script>

</body>
</html>
