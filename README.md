<html lang="hi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Wallet App</title>

<style>
*{box-sizing:border-box;margin:0;padding:0}
body{
    font-family:Arial, sans-serif;
    background:linear-gradient(120deg,#0f2027,#203a43,#2c5364);
    color:#fff;
    overflow:hidden;
}
.screen{height:100vh;display:none}
.show{display:block}

/* ---------- SIGNUP ---------- */
#signup{
    display:flex;
    flex-direction:column;
    justify-content:center;
    padding:20px;
}
#signup h2{margin-bottom:15px;font-size:18px}
#signup input{
    margin:6px 0;
    padding:14px;
    border:none;
    border-radius:10px;
    background:#ffffff22;
    color:#fff;
}
.signup-btn{
    margin-top:15px;
    padding:14px;
    border:none;
    border-radius:30px;
    background:linear-gradient(90deg,#ff416c,#ff4b2b);
    color:#fff;
    font-weight:bold;
    font-size:16px;
}

/* ---------- HEADER GLASS ---------- */
.header{
    margin:15px;
    padding:16px;
    border-radius:16px;
    backdrop-filter:blur(10px);
    background:rgba(255,255,255,0.15);
    text-align:center;
}
.balance{
    font-size:28px;
    font-weight:bold;
    margin-top:6px;
}

/* ---------- TABS ---------- */
.tabs{
    display:flex;
    justify-content:space-around;
    margin:10px;
}
.tab{
    padding:8px 14px;
    border-radius:20px;
    background:#ffffff22;
}
.tab.active{background:#ffd700;color:#000;font-weight:bold}
.tab-content{padding:10px}

/* ---------- AMOUNT GRID ---------- */
.amount-grid{
    display:grid;
    grid-template-columns:repeat(3,1fr);
    gap:8px;
}
.amount-btn{
    padding:10px;
    background:#ffffff22;
    text-align:center;
    border-radius:10px;
}
.amount-btn.selected{
    background:#ffd700;
    color:#000;
    font-weight:bold;
}

/* ---------- BUTTON ---------- */
.main-btn{
    margin-top:10px;
    padding:14px;
    background:#ffd700;
    color:#000;
    border-radius:30px;
    text-align:center;
    font-weight:bold;
}

/* ---------- EARN OPTIONS ---------- */
.earn-options{
    margin:12px;
    display:flex;
    flex-direction:column;
    gap:10px;
}
.earn-box{
    padding:14px;
    border-radius:12px;
    text-align:center;
    font-weight:bold;
    animation:blink 1.5s infinite;
}
.red{background:linear-gradient(90deg,#ff416c,#ff4b2b)}
.green{background:linear-gradient(90deg,#11998e,#38ef7d)}
@keyframes blink{
    50%{opacity:.7}
}

/* ---------- LIVE BOX ---------- */
.live-box{
    margin:12px;
    border-radius:14px;
    overflow:hidden;
}
.live-header{
    padding:10px;
    background:linear-gradient(90deg,#ff0080,#ff8c00,#40e0d0);
    text-align:center;
}
.live-indicator{
    color:#00ff00;
    animation:blink 1s infinite;
}
.live-list{
    height:120px;
    background:#000;
    overflow:hidden;
}
.live-list ul{
    list-style:none;
    animation:scroll 8s linear infinite;
}
.live-list li{
    padding:6px;
    font-size:13px;
    color:#00ff9d;
}
@keyframes scroll{
    0%{transform:translateY(100%)}
    100%{transform:translateY(-100%)}
}

/* ---------- BOTTOM NAV ---------- */
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
.bottom-nav div{
    font-size:12px;
    color:#aaa;
}
.bottom-nav .active{color:#ffd700}

/* ---------- POPUP ---------- */
.popup-bg{
    position:fixed;
    inset:0;
    background:rgba(0,0,0,.7);
    display:none;
    align-items:center;
    justify-content:center;
}
.popup-box{
    background:#111;
    padding:20px;
    border-radius:14px;
    text-align:center;
    max-width:280px;
}
.popup-box button{
    margin-top:10px;
    padding:10px 20px;
    border:none;
    border-radius:20px;
    background:#ffd700;
    font-weight:bold;
}

/* ---------- TOAST ---------- */
.toast{
    position:fixed;
    top:20px;
    left:50%;
    transform:translateX(-50%);
    background:#000;
    padding:10px 16px;
    border-radius:20px;
    display:none;
    font-size:13px;
}
</style>
</head>

<body>

<!-- SIGNUP -->
<div id="signup" class="screen show">
<h2>Signup kare aur ₹180 Bonus paaye</h2>
<input placeholder="+91 Phone">
<input placeholder="Password">
<input placeholder="Referral Code">
<button class="signup-btn" onclick="signup()">Signup</button>
</div>

<!-- WALLET -->
<div id="withdraw" class="screen">
<div class="header">
<div>Wallet Balance</div>
<div class="balance" id="balance">₹0</div>
</div>

<div class="tabs">
<div class="tab active" onclick="openTab('paytm',this)">Paytm</div>
<div class="tab" onclick="openTab('recharge',this)">Recharge</div>
</div>

<div id="paytm" class="tab-content">
<div class="amount-grid">
<div class="amount-btn" onclick="selectAmount(this)">₹19</div>
<div class="amount-btn" onclick="selectAmount(this)">₹29</div>
<div class="amount-btn" onclick="selectAmount(this)">₹69</div>
</div>
<div class="main-btn" onclick="toast('Withdrawal Requested')">Withdraw</div>
</div>

<div id="recharge" class="tab-content" style="display:none">
<input placeholder="Mobile Number">
<div class="main-btn" onclick="toast('Recharge Processing…')">Recharge</div>
</div>

<!-- EARN -->
<div class="earn-options">
<div class="earn-box red">Earn Money</div>
<div class="earn-box green">Free Mobile Recharge</div>
<div class="earn-box red">Watch & Earn</div>
<div class="earn-box green">Share & Earn</div>
</div>

<!-- LIVE -->
<div class="live-box">
<div class="live-header">Live Recharge <span class="live-indicator">●</span></div>
<div class="live-list">
<ul id="liveList"></ul>
</div>
</div>

<div class="bottom-nav">
<div class="active">Home</div>
<div>Earn</div>
<div>Wallet</div>
<div>Profile</div>
</div>
</div>

<div class="toast" id="toast"></div>

<script>
let bal=0;
function signup(){
document.getElementById("signup").style.display="none";
document.getElementById("withdraw").style.display="block";
let i=setInterval(()=>{
 if(bal<180){bal++;balance.innerText="₹"+bal}
 else clearInterval(i);
},20);
}
function openTab(id,el){
document.querySelectorAll(".tab-content").forEach(t=>t.style.display="none");
document.getElementById(id).style.display="block";
document.querySelectorAll(".tab").forEach(t=>t.classList.remove("active"));
el.classList.add("active");
}
function selectAmount(el){
document.querySelectorAll(".amount-btn").forEach(b=>b.classList.remove("selected"));
el.classList.add("selected");
}
function toast(msg){
let t=document.getElementById("toast");
t.innerText=msg;
t.style.display="block";
setTimeout(()=>t.style.display="none",2000);
}

/* LIVE DATA */
const names=["Rahul","Ankit","Pooja","Neha","Rohit"];
function addLive(){
let li=document.createElement("li");
li.innerText=names[Math.floor(Math.random()*5)]+" Recharge Successful";
liveList.appendChild(li);
}
for(let i=0;i<8;i++)addLive();
</script>

</body>
</html>
