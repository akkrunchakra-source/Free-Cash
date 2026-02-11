<html lang="hi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Free-Cash - Earn & Recharge</title>

<style>
*{box-sizing:border-box;}
body{margin:0;font-family:Arial,sans-serif;overflow-x:hidden;padding-bottom:80px}

/* Signup */
#signup{background:#000;color:#fff;padding:20px;display:flex;flex-direction:column;justify-content:center;min-height:100vh}
#signup input{width:100%;padding:14px;margin:8px 0;background:#222;border:none;border-radius:8px;color:#fff}
.signup-btn{margin-top:15px;padding:16px;background:red;border:none;border-radius:30px;color:#fff;font-size:16px;font-weight:bold}

/* Wallet */
#withdraw{display:none;background:#fff;min-height:calc(100vh - 80px)}
.header{background:#ffd700;padding:12px;text-align:center}
.balance{font-size:24px;font-weight:bold}

/* Tabs */
.tabs{display:flex;justify-content:space-around;border-bottom:1px solid #ddd}
.tab{padding:10px;font-weight:bold;cursor:pointer}
.tab.active{border-bottom:2px solid #ffd700}
.tab-content{padding:10px}
.hidden{display:none}

input,select{width:100%;padding:12px;margin:8px 0;border:1px solid #ccc;border-radius:6px;font-size:16px}

/* Plans */
.amount-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:10px;margin:10px 0}
.amount-btn{padding:14px;border:1px solid #ddd;text-align:center;border-radius:8px;cursor:pointer;background:#f8f8f8;font-weight:bold}
.amount-btn.selected{border:2px solid #2ecc71;background:#e8f5e9;position:relative}
.amount-btn.selected::after{content:"✔";position:absolute;top:5px;right:8px;color:#2ecc71;font-size:18px}

.withdraw-btn{background:#ffd700;padding:14px;text-align:center;font-weight:bold;margin:15px 10px;border-radius:8px;cursor:pointer}

/* Transaction */
.transaction-section{margin:15px 10px;background:#f9f9f9;border-radius:12px;overflow:hidden;box-shadow:0 2px 8px rgba(0,0,0,.1)}
.transaction-header{background:#333;color:#fff;padding:12px;font-weight:bold;text-align:center;cursor:pointer}
.transaction-list{max-height:300px;overflow-y:auto;display:none}
.transaction-item{padding:12px 15px;border-bottom:1px solid #eee;font-size:14px}
.transaction-amount{font-weight:bold;color:#e74c3c}

/* Live */
.live-box{margin:15px 10px;border-radius:12px;overflow:hidden}
.live-header{background:linear-gradient(90deg,#ff0080,#ff8c00,#40e0d0);color:#fff;padding:10px;font-weight:bold;text-align:center}
.live-time{font-size:12px;margin-top:4px}
.live-list{height:140px;background:#000;color:#00ff9d;overflow:hidden;position:relative}
.live-list ul{list-style:none;padding:0;margin:0;position:absolute;width:100%;animation:scrollLive 15s linear infinite}
.live-list li{padding:8px 12px;border-bottom:1px solid #222;white-space:nowrap}
@keyframes scrollLive{0%{top:100%}100%{top:-100%}}

/* Bottom Nav */
.bottom-nav{position:fixed;bottom:0;left:0;right:0;height:70px;display:flex;background:#111;border-top:1px solid #333;z-index:1000}
.nav-item{flex:1;text-align:center;color:#fff;font-weight:bold;font-size:13px;padding:10px 5px;text-decoration:none}
.nav-item.home{background:#e74c3c}
.nav-item.earn{background:#3498db}
.nav-item.watch{background:#2ecc71}
.nav-item.data{background:#9b59b6}
.nav-item.active{transform:scale(1.1)}

/* Popup */
.popup-bg{display:none;position:fixed;inset:0;background:rgba(0,0,0,.7);align-items:center;justify-content:center;z-index:10}
.popup-box{background:#000;color:#fff;padding:25px;border-radius:12px;text-align:center;max-width:320px}

/* Recharge Popup Extras */
.jio-logo{font-size:28px;font-weight:bold;color:#0a2cff}
.tick{width:80px;height:80px;border-radius:50%;border:4px solid #2ecc71;display:flex;align-items:center;justify-content:center;margin:12px auto;animation:pop .5s}
.tick::after{content:"✔";font-size:40px;color:#2ecc71}
@keyframes pop{0%{transform:scale(.3);opacity:0}100%{transform:scale(1);opacity:1}}

.popup-box button{margin-top:15px;padding:10px 20px;background:#ffd700;border:none;border-radius:20px;font-weight:bold}
</style>
</head>

<body>

<!-- Signup -->
<div id="signup">
<h2>पैसे कमाना और Free Mobile recharge Data Earn करने के लिए अपना Account Sign-up करें</h2>
<input placeholder="+91 Phone">
<input placeholder="Password">
<input placeholder="Referral Code">
<input placeholder="Verify Code">
<button class="signup-btn" onclick="showSignupPopup()">Signup - Click Here</button>
</div>

<!-- Wallet -->
<div id="withdraw">
<div class="header">
<div>Wallet Balance</div>
<div class="balance">₹180.00</div>
</div>

<div class="tabs">
<div class="tab active" onclick="openTab('paytm',this)">Add Bank Account</div>
<div class="tab" onclick="openTab('recharge',this)">Free Mobile Recharge</div>
</div>

<div id="paytm" class="tab-content">
<input value="3352585xxx05" readonly>
<div class="withdraw-btn">Withdraw Now</div>
</div>

<div id="recharge" class="tab-content hidden">
<input id="mobileNum" placeholder="Enter your mobile number">
<select id="operatorSelect">
<option>Select SIM / Operator</option>
<option>Jio</option><option>Airtel</option><option>Vi</option>
</select>

<div class="amount-grid">
<div class="amount-btn" onclick="selectPlan(this)">₹19-1GB DATA</div>
<div class="amount-btn" onclick="selectPlan(this)">₹29-2GB DATA</div>
<div class="amount-btn" onclick="selectPlan(this)">₹69-6GB DATA</div>
</div>

<div class="withdraw-btn" onclick="doRecharge()">Recharge Now</div>
</div>

<div class="live-box">
<div class="live-header">Free Mobile Recharge Successfully • LIVE
<div class="live-time" id="liveClock"></div></div>
<div class="live-list"><ul id="liveList"></ul></div>
</div>
</div>

<!-- Bottom Nav -->
<div class="bottom-nav">
<a class="nav-item home active">Home</a>
<a class="nav-item earn">Earn</a>
<a class="nav-item watch">Watch</a>
<a class="nav-item data">Data</a>
</div>

<!-- Signup Popup -->
<div id="signupPopup" class="popup-bg">
<div class="popup-box">
🎉 Your Free ₹180 Bonus Unlocked<br>
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
setInterval(()=>liveClock.innerText=new Date().toLocaleTimeString('en-IN'),1000);

function selectPlan(el){
document.querySelectorAll('.amount-btn').forEach(b=>b.classList.remove('selected'));
el.classList.add('selected');
}

function playSound(){
const c=new (AudioContext||webkitAudioContext)();
const o=c.createOscillator();o.frequency.value=900;o.connect(c.destination);o.start();
setTimeout(()=>o.stop(),150);
}

function doRecharge(){
document.getElementById("rechargeMsg").innerHTML=
"Dear Customer,<br>Your recharge of <b>Rs.19</b> is successfully.<br>1GB Data credited.<br>Valid till 12-Feb-2026";
document.getElementById("rechargePopup").style.display="flex";
playSound();
}

function closeRechargePopup(){rechargePopup.style.display="none"}
function showSignupPopup(){signupPopup.style.display="flex"}
function goToWallet(){signupPopup.style.display="none";signup.style.display="none";withdraw.style.display="block"}
function openTab(id,el){
document.querySelectorAll('.tab-content').forEach(t=>t.classList.add('hidden'));
document.getElementById(id).classList.remove('hidden');
document.querySelectorAll('.tab').forEach(t=>t.classList.remove('active'));
el.classList.add('active');
}
</script>
</body>
</html>
