<html lang="hi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Free-Cash - Earn & Recharge</title>

<style>
*{box-sizing:border-box;}
body{margin:0;font-family:Arial,sans-serif;overflow-x:hidden;padding-bottom:80px}

/* ===== Signup ===== */
#signup{background:#000;color:#fff;padding:20px;min-height:100vh}
#signup input{width:100%;padding:14px;margin:8px 0;background:#222;border:none;border-radius:8px;color:#fff}
.signup-btn{padding:16px;background:red;border:none;border-radius:30px;color:#fff;font-size:16px;font-weight:bold}

/* ===== Wallet ===== */
#withdraw{display:none}
.header{background:#ffd700;padding:12px;text-align:center}
.balance{font-size:24px;font-weight:bold}

.tabs{display:flex;justify-content:space-around;border-bottom:1px solid #ddd}
.tab{padding:10px;font-weight:bold;cursor:pointer}
.tab.active{border-bottom:2px solid #ffd700}
.tab-content{padding:10px}
.hidden{display:none}

input,select{width:100%;padding:12px;margin:8px 0;border:1px solid #ccc;border-radius:6px}

.amount-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:10px}
.amount-btn{padding:14px;border:1px solid #ddd;border-radius:8px;text-align:center;cursor:pointer}
.amount-btn.selected{border:2px solid #2ecc71;background:#e8f5e9;position:relative}
.amount-btn.selected::after{content:"✔";position:absolute;top:5px;right:8px;color:#2ecc71}

.withdraw-btn{background:#ffd700;padding:14px;text-align:center;font-weight:bold;border-radius:8px;cursor:pointer;margin-top:10px}

/* ===== Bottom Nav ===== */
.bottom-nav{position:fixed;bottom:0;left:0;right:0;height:70px;display:flex;background:#111}
.nav-item{flex:1;color:#fff;text-align:center;font-weight:bold;padding:10px}
.home{background:#e74c3c}.earn{background:#3498db}.watch{background:#2ecc71}.data{background:#9b59b6}

/* ===== Popup Base ===== */
.popup-bg{display:none;position:fixed;inset:0;background:rgba(0,0,0,.7);align-items:center;justify-content:center;z-index:999}
.popup-box{background:#000;color:#fff;padding:25px;border-radius:14px;text-align:center;max-width:320px}

/* ===== Recharge Popup ===== */
.jio-logo{
    font-size:28px;
    font-weight:bold;
    color:#0a2cff;
    margin-bottom:10px;
}
.tick{
    width:80px;height:80px;
    border-radius:50%;
    border:4px solid #2ecc71;
    display:flex;
    align-items:center;
    justify-content:center;
    margin:10px auto;
    animation:pop .6s ease;
}
.tick::after{
    content:"✔";
    font-size:40px;
    color:#2ecc71;
}
@keyframes pop{
    0%{transform:scale(.3);opacity:0}
    100%{transform:scale(1);opacity:1}
}
.popup-box button{
    margin-top:15px;
    padding:10px 25px;
    border:none;
    border-radius:20px;
    background:#ffd700;
    font-weight:bold;
}
</style>
</head>

<body>

<!-- Signup -->
<div id="signup">
<h2>Free Mobile Recharge & Earn Money</h2>
<input placeholder="+91 Phone">
<input placeholder="Password">
<button class="signup-btn" onclick="showSignupPopup()">Signup</button>
</div>

<!-- Wallet -->
<div id="withdraw">
<div class="header">
<div>Wallet Balance</div>
<div class="balance">₹180.00</div>
</div>

<div class="tabs">
<div class="tab active" onclick="openTab('paytm',this)">Add Bank</div>
<div class="tab" onclick="openTab('recharge',this)">Free Recharge</div>
</div>

<div id="paytm" class="tab-content">
<input value="3352585xxx05" readonly>
<div class="withdraw-btn">Withdraw Now</div>
</div>

<div id="recharge" class="tab-content hidden">
<input id="mobileNum" placeholder="Enter Mobile Number">
<select id="operatorSelect">
<option>Select SIM</option>
<option>Jio</option>
<option>Airtel</option>
<option>Vi</option>
</select>

<div class="amount-grid">
<div class="amount-btn" onclick="selectPlan(this)">₹19-1GB DATA</div>
<div class="amount-btn" onclick="selectPlan(this)">₹29-2GB DATA</div>
<div class="amount-btn" onclick="selectPlan(this)">₹69-6GB DATA</div>
</div>

<div class="withdraw-btn" onclick="doRecharge()">Recharge Now</div>
</div>
</div>

<!-- Bottom Nav -->
<div class="bottom-nav">
<div class="nav-item home">Home</div>
<div class="nav-item earn">Earn</div>
<div class="nav-item watch">Watch</div>
<div class="nav-item data">Free Data</div>
</div>

<!-- Signup Popup -->
<div id="signupPopup" class="popup-bg">
<div class="popup-box">
🎉 ₹180 Bonus Added Successfully
<br>
<button onclick="goToWallet()">OK</button>
</div>
</div>

<!-- Recharge Popup -->
<div id="rechargePopup" class="popup-bg">
<div class="popup-box">
<div class="jio-logo">Jio</div>
<div class="tick"></div>
<div id="rechargeMsg"></div>
<button onclick="closeRechargePopup()">OK</button>
</div>
</div>

<script>
function showSignupPopup(){
document.getElementById("signupPopup").style.display="flex"
}
function goToWallet(){
signupPopup.style.display="none"
signup.style.display="none"
withdraw.style.display="block"
}
function openTab(id,el){
document.querySelectorAll(".tab-content").forEach(t=>t.classList.add("hidden"))
document.getElementById(id).classList.remove("hidden")
document.querySelectorAll(".tab").forEach(t=>t.classList.remove("active"))
el.classList.add("active")
}
function selectPlan(el){
document.querySelectorAll(".amount-btn").forEach(b=>b.classList.remove("selected"))
el.classList.add("selected")
}

/* 🔊 Success Sound */
function playSuccessSound(){
const ctx=new (window.AudioContext||window.webkitAudioContext)()
const osc=ctx.createOscillator()
osc.type="sine"
osc.frequency.value=880
osc.connect(ctx.destination)
osc.start()
setTimeout(()=>osc.stop(),150)
}

/* Recharge */
function doRecharge(){
const mob=mobileNum.value.trim()
const op=operatorSelect.value
const plan=document.querySelector(".amount-btn.selected")
if(!mob||mob.length<10){alert("Invalid Number");return}
if(op==="Select SIM"){alert("Select Operator");return}
if(!plan){alert("Select Plan");return}

rechargeMsg.innerHTML=`
Dear Customer,<br><br>
Your recharge of <b>₹19</b> is successful.<br>
<b>1GB Data</b> credited.<br>
Valid till <b>12-Feb-2026</b>
`
rechargePopup.style.display="flex"
playSuccessSound()
}
function closeRechargePopup(){
rechargePopup.style.display="none"
}
</script>

</body>
</html>
