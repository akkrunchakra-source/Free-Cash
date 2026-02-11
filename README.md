<!DOCTYPE html>
<html lang="hi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Free-Cash - Earn & Recharge (Demo)</title>

<style>
*{box-sizing:border-box}
body{margin:0;font-family:Arial,sans-serif;padding-bottom:80px;background:#000;color:#fff}

/* Signup */
#signup{background:#000;padding:20px;min-height:100vh}
input,select{width:100%;padding:14px;margin:8px 0;background:#222;border:none;border-radius:8px;color:#fff}
.signup-btn,.otp-btn,.verify-btn{padding:16px;background:red;border:none;border-radius:30px;color:#fff;font-weight:bold;width:100%}

/* Wallet */
#withdraw{display:none}
.header{background:#ffd700;padding:12px;text-align:center;color:#000}
.balance{font-size:24px;font-weight:bold}

/* Tabs */
.tabs{display:flex;border-bottom:1px solid #444}
.tab{flex:1;text-align:center;padding:12px;font-weight:bold;cursor:pointer}
.tab.active{border-bottom:3px solid #ffd700}
.tab-content{padding:10px}
.hidden{display:none}

/* Plans */
.amount-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:10px}
.amount-btn{padding:14px;border:1px solid #444;border-radius:8px;text-align:center;font-weight:bold;background:#111}
.amount-btn.selected{border:2px solid #2ecc71;background:#1a3a2a}

/* Buttons */
.withdraw-btn{background:#ffd700;color:#000;padding:14px;text-align:center;font-weight:bold;border-radius:8px;margin-top:10px}

/* Transaction */
.transaction-section{margin-top:15px;background:#111;border-radius:12px;overflow:hidden}
.transaction-header{background:#333;padding:12px;text-align:center;cursor:pointer}

/* Live Recharge */
.live-box{margin:15px;border-radius:12px;overflow:hidden;background:#000;border:1px solid #333}
.live-header{background:linear-gradient(90deg,#ff0080,#ff8c00,#40e0d0);padding:10px;text-align:center}
.live-list{height:180px;overflow:hidden;background:#000;color:#00ff9d}
.live-list ul{list-style:none;padding:0;margin:0;animation:scroll 25s linear infinite}
.live-list li{padding:10px 12px;border-bottom:1px solid #222;font-size:14px}
@keyframes scroll{0%{transform:translateY(100%)}100%{transform:translateY(-100%)}}

/* Bottom Nav */
.bottom-nav{position:fixed;bottom:0;left:0;right:0;height:70px;display:flex;background:#111}
.nav-item{flex:1;text-align:center;padding:12px;font-weight:bold;color:#ccc}
.nav-item.active{color:#ffd700}

/* Popup */
.popup-bg{display:none;position:fixed;inset:0;background:rgba(0,0,0,.8);align-items:center;justify-content:center}
.popup-box{background:#111;padding:25px;border-radius:12px;text-align:center;width:90%;max-width:360px}

/* Extras */
.jio-logo{font-size:30px;color:#0a2cff;font-weight:bold}
.tick{width:80px;height:80px;border-radius:50%;border:4px solid #2ecc71;display:flex;align-items:center;justify-content:center;margin:15px auto}
.tick::after{content:"✔";font-size:45px;color:#2ecc71}
</style>
</head>

<body>

<!-- Signup -->
<div id="signup">
  <h2>Free Mobile Recharge & Cash Earn (Demo)</h2>
  <input id="mobileInput" placeholder="+91 Mobile Number" type="tel" maxlength="10">
  <button class="signup-btn" id="sendOtpBtn" onclick="sendOtp()">Send OTP</button>
  
  <div id="otpSection" style="display:none;">
    <input id="otpInput" placeholder="Enter 4-digit OTP" type="number" maxlength="4">
    <button class="verify-btn" onclick="verifyOtp()">Verify OTP</button>
    <p style="font-size:13px;color:#aaa;margin-top:10px;">Referral Code (optional): <input placeholder="Referral Code" style="width:60%;padding:8px;"></p>
  </div>
</div>

<!-- Wallet / Main App -->
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

  <!-- Transaction (fake static for now) -->
  <div id="transaction" class="tab-content hidden">
    <div class="transaction-section">
      <div class="transaction-header">Recharge History</div>
      <div style="padding:10px;font-size:14px;">
        Jio • ₹19 • Success • 11 Feb 2026, 09:05 AM<br>
        Airtel • ₹29 • Success • 10 Feb 2026, 11:45 PM
      </div>
    </div>
  </div>

  <!-- Live Recharge -->
  <div class="live-box">
    <div class="live-header">LIVE Recharges (Demo)</div>
    <div class="live-list">
      <ul id="liveList">
        <!-- New entries will be added here automatically -->
      </ul>
    </div>
  </div>
</div>

<!-- Bottom Nav -->
<div class="bottom-nav">
  <div class="nav-item active">Home</div>
  <div class="nav-item">Earn</div>
  <div class="nav-item">Watch</div>
  <div class="nav-item">Data</div>
</div>

<!-- Popups -->
<div id="signupPopup" class="popup-bg">
  <div class="popup-box">
    🎉 ₹180 Bonus Added!<br><br>
    <button onclick="goToWallet()" style="background:#ffd700;color:#000;padding:14px 40px;border-radius:30px;font-weight:bold;">OK</button>
  </div>
</div>

<div id="rechargePopup" class="popup-bg">
  <div class="popup-box">
    <div class="jio-logo">Jio</div>
    <div class="tick"></div>
    Recharge Successful 🎉<br><br>
    <button onclick="closeRecharge()" style="background:#2ecc71;color:#000;padding:14px 40px;border-radius:30px;font-weight:bold;">OK</button>
  </div>
</div>

<script>
// Tab switch
function openTab(id, el) {
  document.querySelectorAll('.tab-content').forEach(t => t.classList.add('hidden'));
  document.getElementById(id).classList.remove('hidden');
  document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
  el.classList.add('active');
}

// OTP flow (fake)
function sendOtp() {
  const mobile = document.getElementById('mobileInput').value.trim();
  if (mobile.length !== 10 || isNaN(mobile)) {
    alert("Please enter valid 10-digit mobile number");
    return;
  }
  document.getElementById('sendOtpBtn').style.display = 'none';
  document.getElementById('otpSection').style.display = 'block';
  alert("OTP sent! (Demo: use any 4 digits)");
}

function verifyOtp() {
  const otp = document.getElementById('otpInput').value.trim();
  if (otp.length === 4) {
    showSignupPopup();
  } else {
    alert("Enter 4-digit OTP");
  }
}

function showSignupPopup() { document.getElementById('signupPopup').style.display = 'flex'; }
function goToWallet() {
  document.getElementById('signup').style.display = 'none';
  document.getElementById('signupPopup').style.display = 'none';
  document.getElementById('withdraw').style.display = 'block';
}

// Plan selection
function selectPlan(el) {
  document.querySelectorAll('.amount-btn').forEach(b => b.classList.remove('selected'));
  el.classList.add('selected');
}

// Recharge popup
function doRecharge() {
  document.getElementById('rechargePopup').style.display = 'flex';
}
function closeRecharge() { document.getElementById('rechargePopup').style.display = 'none'; }

// Live recharge simulation
const operators = ['Jio', 'Airtel', 'Vi'];
const amounts = [10, 15, 19, 29, 49, 69, 98, 155, 199, 666];

function addLiveRecharge() {
  const now = new Date();
  const timeStr = now.toLocaleString('en-IN', {
    day: '2-digit', month: 'short', year: 'numeric',
    hour: '2-digit', minute: '2-digit', hour12: true
  }).replace(',', '');

  const randomNum = Math.floor(7000000000 + Math.random() * 3000000000);
  const masked = `+91 \( {String(randomNum).slice(0,2)}**** \){String(randomNum).slice(-4)}`;
  const op = operators[Math.floor(Math.random() * operators.length)];
  const amt = amounts[Math.floor(Math.random() * amounts.length)];

  const li = document.createElement('li');
  li.textContent = `\( {masked} recharged ₹ \){amt} ${op} • ${timeStr}`;
  
  const list = document.getElementById('liveList');
  list.appendChild(li);

  // Keep only last 12 items visible (for animation)
  if (list.children.length > 12) {
    list.removeChild(list.children[0]);
  }
}

// Add new recharge every 4-8 seconds
setInterval(addLiveRecharge, Math.random() * 4000 + 4000);

// Add 8 initial fake entries on load
for (let i = 0; i < 8; i++) {
  addLiveRecharge();
}
</script>

</body>
</html>
