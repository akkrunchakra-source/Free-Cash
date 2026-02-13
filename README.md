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
.signup-btn{padding:16px;background:red;border:none;border-radius:30px;color:#fff;font-weight:bold}

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
.transaction-header{background:#333;color:#fff;padding:12px;text-align:center;cursor:pointer}
.transaction-list{display:none;max-height:250px;overflow:auto}
.transaction-item{padding:10px;border-bottom:1px solid #eee;font-size:14px}

/* Live Recharge */
.live-box{margin:15px;border-radius:12px;overflow:hidden}
.live-header{background:linear-gradient(90deg,#ff0080,#ff8c00,#40e0d0);color:#fff;padding:10px;text-align:center}
.live-list{height:140px;background:#000;overflow:hidden}
.live-list ul{list-style:none;padding:0;margin:0;animation:scroll 6s linear infinite}
  .live-list li{
padding:8px 12px;
border-bottom:1px solid #222;
animation:colorChange 2s infinite alternate;
}

@keyframes colorChange{
0%{color:#00ff9d;}
25%{color:#ff4d4d;}
50%{color:#ffd700;}
75%{color:#40e0d0;}
100%{color:#ff00ff;}
}
@keyframes scroll{0%{transform:translateY(100%)}100%{transform:translateY(-100%)}}

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

button{padding:10px 20px;border:none;border-radius:20px;font-weight:bold}
  
  /* INSTALL SECTION */
.install-box{
text-align:center;
padding:20px;
background:#111;
margin:15px;
border-radius:12px;
}

.install-text{
font-weight:bold;
color:#fff;
font-size:16px;
margin-bottom:15px;
}

.install-btn{
padding:14px 30px;
font-size:16px;
font-weight:bold;
border:none;
border-radius:30px;
background:linear-gradient(45deg,#00ff9d,#00c3ff);
color:#000;
cursor:pointer;
animation:pulse 1.2s infinite;
}

@keyframes pulse{
0%{transform:scale(1);}
50%{transform:scale(1.08);}
100%{transform:scale(1);}
}
</style>
</head>

<body>

<!-- Signup -->
<div id="signup करें">
<h2>Free Mobile Recharge कमाने के लिए निचे Sign-up करें & </h2>
<input placeholder="+91 Mobile">
<input placeholder="Password">
<input placeholder="Enter OTP">
<input placeholder="Referral Code">
<button class="signup-btn" onclick="showSignupPopup()">Signup Click Here</button>
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
<input placeholder="Mobile Number">
<select>
<option>Select Operator</option>
<option>Jio</option><option>Airtel</option><option>Vi</option>
</select>

<div class="amount-grid">
<div class="amount-btn" onclick="selectPlan(this)">₹19 - 1GB</div>
<div class="amount-btn" onclick="selectPlan(this)">₹29 - 2GB</div>
<div class="amount-btn" onclick="selectPlan(this)">₹69 - 6GB</div>
</div>

<div class="withdraw-btn" onclick="doRecharge()">Recharge Now</div>
</div>

<!-- Transaction -->
<div id="transaction" class="tab-content hidden">
<div class="transaction-section">
<div class="transaction-header" onclick="toggleTxn()">Recharge History</div>
<div class="transaction-list" id="txnList">
<div class="transaction-item">Jio • ₹19 • Success</div>
<div class="transaction-item">Airtel • ₹29 • Success</div>
<div class="transaction-item">Vi • ₹69 • Success</div>
</div>
</div>
</div>

<!-- Live Recharge -->
<div class="live-box">
<div class="live-header">LIVE Recharge</div>
<div class="live-list">
<ul id="liveList">
<li>+91 98****4321 recharged ₹19</li>
<li>+91 87****1123 recharged ₹29</li>
<li>+91 76****9988 recharged ₹69</li>
</ul>
</div>
</div>
</div>

<!-- INSTALL BUTTON YAHAN -->
<div class="install-box">
<p class="install-text">
⚡ Apna task complete kare niche Install button par click karke  
aur wapas isi site par aaye ⚡
</p>

<a href="https://6gain.com/in/#/?rcode=Pcpb6h" target="_blank">
<button class="install-btn">INSTALL & COMPLETE TASK</button>
</a>
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
<div class="jio-logo">Jio</div>
<div class="tick"></div>
Recharge Successful 🎉<br><br>
<button onclick="closeRecharge()">OK</button>
</div>
</div>

<script>
function openTab(id,el){
document.querySelectorAll('.tab-content').forEach(t=>t.classList.add('hidden'));
document.getElementById(id).classList.remove('hidden');
document.querySelectorAll('.tab').forEach(t=>t.classList.remove('active'));
el.classList.add('active');
}

function selectPlan(el){
document.querySelectorAll('.amount-btn').forEach(b=>b.classList.remove('selected'));
el.classList.add('selected');
}

function toggleTxn(){
txnList.style.display = txnList.style.display==="block"?"none":"block";
}
  
function showSignupPopup(){signupPopup.style.display="flex"}
function goToWallet(){
signup.style.display="none";
signupPopup.style.display="none";
withdraw.style.display="block";
}

function doRecharge(){
rechargePopup.style.display="flex";
playSound();
}

function closeRecharge(){rechargePopup.style.display="none"}

function playSound(){
let c=new(AudioContext||webkitAudioContext)();
let o=c.createOscillator();
o.frequency.value=900;o.connect(c.destination);o.start();
setTimeout(()=>o.stop(),150);
}
</script>

</body>
</html>
