<html lang="hi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Free-Cash - Earn & Recharge</title>

<style>
*{box-sizing:border-box}
body{margin:0;font-family:Arial,sans-serif;padding-bottom:80px}

/* Signup */
#signup{background:#000;color:#fff;padding:20px;min-height:100vh}
#signup input{width:100%;padding:14px;margin:8px 0;background:#222;border:none;border-radius:8px;color:#fff}
.signup-btn{padding:16px;background:red;border:none;border-radius:30px;color:#fff;font-weight:bold;width:100%}
.otp-btn{padding:12px;background:#ffd700;border:none;border-radius:20px;font-weight:bold;width:100%;margin-top:5px}

/* Wallet */
#withdraw{display:none}
.header{background:#ffd700;padding:12px;text-align:center}
.balance{font-size:24px;font-weight:bold}

/* Tabs */
.tabs{display:flex;border-bottom:1px solid #ddd}
.tab{flex:1;text-align:center;padding:12px;font-weight:bold;cursor:pointer}
.tab.active{border-bottom:3px solid #ffd700}
.tab-content{padding:10px}
.hidden{display:none}

input,select{width:100%;padding:12px;margin:8px 0;border-radius:6px;border:1px solid #ccc}

/* Plans */
.amount-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:10px}
.amount-btn{padding:14px;border:1px solid #ddd;border-radius:8px;text-align:center;font-weight:bold}
.amount-btn.selected{border:2px solid #2ecc71;background:#eafaf1}

/* Buttons */
.withdraw-btn{background:#ffd700;padding:14px;text-align:center;font-weight:bold;border-radius:8px;margin-top:10px}

/* Transaction */
.transaction-section{margin-top:15px;background:#f9f9f9;border-radius:12px;overflow:hidden}
.transaction-header{background:#333;color:#fff;padding:12px;text-align:center;font-weight:bold}
.transaction-list{max-height:300px;overflow:auto}
.transaction-item{
padding:10px;
border-bottom:1px solid #eee;
font-size:14px;
font-weight:bold
}

/* Live Recharge */
.live-box{margin:15px;border-radius:12px;overflow:hidden}
.live-header{background:linear-gradient(90deg,#ff0080,#ff8c00,#40e0d0);color:#fff;padding:10px;text-align:center;font-weight:bold}
.live-list{height:140px;background:#000;color:#00ff9d;overflow:hidden}
.live-list ul{list-style:none;padding:0;margin:0}
.live-list li{padding:8px 12px;border-bottom:1px solid #222}

/* Bottom Nav */
.bottom-nav{position:fixed;bottom:0;left:0;right:0;height:70px;display:flex;background:#111}
.nav-item{flex:1;text-align:center;color:#fff;padding:12px;font-weight:bold}

/* Popup */
.popup-bg{display:none;position:fixed;inset:0;background:rgba(0,0,0,.7);align-items:center;justify-content:center}
.popup-box{background:#000;color:#fff;padding:25px;border-radius:12px;text-align:center}

/* Extras */
.jio-logo{font-size:30px;color:#0a2cff;font-weight:bold}
.tick{width:80px;height:80px;border-radius:50%;border:4px solid #2ecc71;
display:flex;align-items:center;justify-content:center;margin:10px auto;animation:pop .5s}
.tick::after{content:"✔";font-size:40px;color:#2ecc71}
@keyframes pop{0%{transform:scale(.3)}100%{transform:scale(1)}}

button{cursor:pointer}
</style>
</head>

<body>

<!-- Signup -->
<div id="signup">
<h2>Free Mobile Recharge & Cash Earn</h2>

<input id="suMobile" placeholder="+91 Mobile">
<input id="suPass" placeholder="Password" type="password">
<input id="suRef" placeholder="Referral Code">

<button class="otp-btn" onclick="sendOTP()">Send OTP</button>
<input id="suOtp" placeholder="Enter OTP">

<button class="signup-btn" onclick="verifySignup()">Signup</button>
</div>

<!-- Wallet -->
<div id="withdraw">
<div class="header">
<div>Wallet Balance</div>
<div class="balance">₹180.00</div>
</div>

<div class="tabs">
<div class="tab active" onclick="openTab('bank',this)">Bank</div>
<div class="tab" onclick="openTab('recharge',this)">Recharge</div>
<div class="tab" onclick="openTab('transaction',this)">Transaction</div>
</div>

<!-- Bank -->
<div id="bank" class="tab-content">
<input value="3352585xxxx05" readonly>
<div class="withdraw-btn">Withdraw Now</div>
</div>

<!-- Recharge -->
<div id="recharge" class="tab-content hidden">
<input id="recMobile" placeholder="Mobile Number">
<select id="operator">
<option>Jio</option>
<option>Airtel</option>
<option>Vi</option>
</select>

<div class="amount-grid">
<div class="amount-btn" onclick="selectPlan(this)">₹19</div>
<div class="amount-btn" onclick="selectPlan(this)">₹29</div>
<div class="amount-btn" onclick="selectPlan(this)">₹69</div>
</div>

<div class="withdraw-btn" onclick="doRecharge()">Recharge Now</div>
</div>

<!-- Transaction -->
<div id="transaction" class="tab-content hidden">
<div class="transaction-section">
<div class="transaction-header">Recharge History</div>
<div class="transaction-list" id="txnList"></div>
</div>
</div>

<!-- Live Recharge -->
<div class="live-box">
<div class="live-header">LIVE Recharge</div>
<div class="live-list">
<ul id="liveList"></ul>
</div>
</div>
</div>

<!-- Bottom Nav -->
<div class="bottom-nav">
<div class="nav-item">Home</div>
<div class="nav-item">Earn</div>
<div class="nav-item">Watch</div>
<div class="nav-item">Data</div>
</div>

<!-- Signup Popup -->
<div id="signupPopup" class="popup-bg">
<div class="popup-box">
🎉 ₹180 Bonus Added<br><br>
<button onclick="goToWallet()">OK</button>
</div>
</div>

<!-- Recharge Popup -->
<div id="rechargePopup" class="popup-bg">
<div class="popup-box">
<div class="jio-logo" id="popOp">Jio</div>
<div class="tick"></div>
Recharge Successful 🎉<br><br>
<button onclick="closeRecharge()">OK</button>
</div>
</div>

<script>
let demoOTP = "1234";
let selectedAmount = "19";

/* OTP */
function sendOTP(){
alert("Demo OTP sent: 1234");
}
function verifySignup(){
if(suOtp.value === demoOTP){
signupPopup.style.display="flex";
}else{
alert("Invalid OTP");
}
}

/* Tabs */
function openTab(id,el){
document.querySelectorAll('.tab-content').forEach(t=>t.classList.add('hidden'));
document.getElementById(id).classList.remove('hidden');
document.querySelectorAll('.tab').forEach(t=>t.classList.remove('active'));
el.classList.add('active');
}

/* Plans */
function selectPlan(el){
document.querySelectorAll('.amount-btn').forEach(b=>b.classList.remove('selected'));
el.classList.add('selected');
selectedAmount = el.innerText.replace("₹","");
}

/* Signup */
function goToWallet(){
signup.style.display="none";
signupPopup.style.display="none";
withdraw.style.display="block";
}

/* Recharge */
function doRecharge(){
let op = operator.value;
let now = new Date();
let time = now.toLocaleTimeString('en-IN');
let date = now.toLocaleDateString('en-IN');

popOp.innerText = op;
rechargePopup.style.display="flex";
playSound();

/* Transaction add */
let txn = document.createElement("div");
txn.className="transaction-item";
txn.innerHTML = `${op} • ₹${selectedAmount} • SUCCESS<br>${date} ${time}`;
txnList.prepend(txn);

/* Live list add */
let li = document.createElement("li");
li.innerText = `+91 **** recharged ₹${selectedAmount} (${op})`;
liveList.prepend(li);
}

function closeRecharge(){rechargePopup.style.display="none"}

/* Sound */
function playSound(){
let c=new(AudioContext||webkitAudioContext)();
let o=c.createOscillator();
o.frequency.value=900;
o.connect(c.destination);
o.start();
setTimeout(()=>o.stop(),150);
}
</script>

</body>
</html>
