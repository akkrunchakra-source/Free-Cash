<html lang="hi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Free-Cash - Earn & Recharge</title>

<style>
*{box-sizing:border-box;}
body{margin:0; font-family:Arial, sans-serif; overflow-x:hidden; padding-bottom:80px;}

#signup{
    background:#000; color:#fff; padding:20px;
    display:flex; flex-direction:column; justify-content:center;
    min-height:100vh;
}
#signup input{width:100%; padding:14px; margin:8px 0; background:#222; border:none; border-radius:8px; color:#fff;}
.signup-btn{margin-top:15px; padding:16px; background:red; border:none; border-radius:30px; color:white; font-size:16px; font-weight:bold;}

#withdraw{display:none; background:#fff; min-height:calc(100vh - 80px);}

.header{background:#ffd700; padding:12px; text-align:center;}
.balance{font-size:24px; font-weight:bold;}

.tabs{display:flex; justify-content:space-around; border-bottom:1px solid #ddd;}
.tab{padding:10px; font-weight:bold; cursor:pointer;}
.tab.active{border-bottom:2px solid #ffd700;}
.tab-content{padding:10px;}
.hidden{display:none;}

input, select{width:100%; padding:12px; margin:8px 0; border:1px solid #ccc; border-radius:6px; font-size:16px;}

.amount-grid{display:grid; grid-template-columns:repeat(3,1fr); gap:10px; margin:10px 0;}
.amount-btn{padding:14px; border:1px solid #ddd; text-align:center; border-radius:8px; cursor:pointer; background:#f8f8f8; font-weight:bold;}
.amount-btn.selected{border:2px solid #2ecc71; background:#e8f5e9; position:relative;}
.amount-btn.selected::after{content:"✔"; position:absolute; top:5px; right:8px; color:#2ecc71; font-size:18px;}

.withdraw-btn{background:#ffd700; padding:14px; text-align:center; font-weight:bold; margin:15px 10px; border-radius:8px; cursor:pointer;}

/* Transaction History */
.transaction-section{margin:15px 10px; background:#f9f9f9; border-radius:12px; overflow:hidden; box-shadow:0 2px 8px rgba(0,0,0,0.1);}
.transaction-header{background:#333; color:white; padding:12px; font-weight:bold; text-align:center; cursor:pointer;}
.transaction-list{max-height:300px; overflow-y:auto; display:none;}
.transaction-item{padding:12px 15px; border-bottom:1px solid #eee; font-size:14px;}
.transaction-amount{font-weight:bold; color:#e74c3c;}

/* Live Recharge */
.live-box{margin:15px 10px; border-radius:12px; overflow:hidden;}
.live-header{background:linear-gradient(90deg,#ff0080,#ff8c00,#40e0d0); color:#fff; padding:10px; font-weight:bold; text-align:center;}
.live-indicator{color:#00ff00; font-weight:bold; animation:liveBlink 1s infinite;}
@keyframes liveBlink{0%,100%{opacity:1;} 50%{opacity:0.4;}}
.live-time{font-size:12px; margin-top:4px;}
.live-list{height:140px; background:#000; color:#00ff9d; overflow:hidden; position:relative;}
.live-list ul{list-style:none; padding:0; margin:0; position:absolute; width:100%; animation:scrollLive 15s linear infinite;}
.live-list li{padding:8px 12px; border-bottom:1px solid #222; white-space:nowrap;}

@keyframes scrollLive{0%{top:100%;} 100%{top:-100%;}}

/* Bottom Nav */
.bottom-nav{position:fixed; bottom:0; left:0; right:0; height:70px; display:flex; background:#111; border-top:1px solid #333; z-index:1000;}
.nav-item{flex:1; text-align:center; color:white; font-weight:bold; font-size:13px; padding:10px 5px; text-decoration:none;}
.nav-item:hover{transform:scale(1.05);}
.nav-item.home{background:#e74c3c;}
.nav-item.earn{background:#3498db;}
.nav-item.watch{background:#2ecc71;}
.nav-item.data{background:#9b59b6;}
.nav-item.active{transform:scale(1.1);}

/* Popup */
.popup-bg{display:none; position:fixed; inset:0; background:rgba(0,0,0,0.7); align-items:center; justify-content:center; z-index:10;}
.popup-box{background:#000; color:#fff; padding:25px; border-radius:12px; text-align:center; max-width:320px;}
.popup-box button{margin-top:15px; padding:10px 20px; background:#ffd700; border:none; border-radius:20px; font-weight:bold;}
</style>
</head>

<body>

<!-- Signup Page -->
<div id="signup">
    <h2>पैसे कमाने के साथ Free Mobile recharge Data Earn करने के लिए अपना Account Sign-up करें पहला Bonus Free For New User</h2>
    <input placeholder="+91 Phone">
    <input type="password" placeholder="Password">
    <input placeholder="Referral Code">
    <input placeholder="Verify Code">
    <button class="signup-btn" onclick="showSignupPopup()">Signup - Click Here</button>
</div>

<!-- Wallet Page -->
<div id="withdraw">
    <div class="header">
        <div>Wallet Balance</div>
        <div class="balance">₹180.00</div>
    </div>

    <div class="tabs">
        <div class="tab active" onclick="openTab('paytm', this)">Paytm</div>
        <div class="tab" onclick="openTab('recharge', this)">Recharge</div>
    </div>

    <!-- Paytm Tab -->
    <div id="paytm" class="tab-content">
        <input value="3352585xxx05" readonly style="text-align:center; font-weight:bold;">
        <div class="withdraw-btn" onclick="alert('Withdraw processing... (Demo mode)')">Withdraw Now</div>
    </div>

    <!-- Recharge Tab (Restored with mobile + select + tick) -->
    <div id="recharge" class="tab-content hidden">
        <input id="mobileNum" placeholder="Enter your mobile number">
        <select id="operatorSelect">
            <option>Select SIM / Operator</option>
            <option>Jio</option>
            <option>Airtel</option>
            <option>Vi</option>
        </select>

        <div class="amount-grid">
            <div class="amount-btn" onclick="selectPlan(this)">₹19</div>
            <div class="amount-btn" onclick="selectPlan(this)">₹29</div>
            <div class="amount-btn" onclick="selectPlan(this)">₹69</div>
            <div class="amount-btn" onclick="selectPlan(this)">₹199</div>
            <div class="amount-btn" onclick="selectPlan(this)">₹299</div>
            <div class="amount-btn" onclick="selectPlan(this)">₹399</div>
        </div>

        <div class="withdraw-btn" onclick="doRecharge()">Recharge Now</div>
    </div>

    <!-- Transaction History -->
    <div class="transaction-section">
        <div class="transaction-header" onclick="toggleHistory()">Transaction History (Click to View)</div>
        <div class="transaction-list" id="historyList"></div>
    </div>

    <!-- Live Recharge -->
    <div class="live-box">
        <div class="live-header">
            Free Mobile Recharge Successfully • LIVE
            <div class="live-time" id="liveClock"></div>
        </div>
        <div class="live-list">
            <ul id="liveList"></ul>
        </div>
    </div>
</div>

<!-- Bottom Nav -->
<div class="bottom-nav">
    <a href="#" class="nav-item nav-item home active">Home</a>
    <a href="#" class="nav-item nav-item earn">Earn Money</a>
    <a href="#" class="nav-item nav-item watch">Watch And Earn</a>
    <a href="#" class="nav-item nav-item data">Free Data Earn</a>
</div>

<!-- Signup Popup -->
<div id="signupPopup" class="popup-bg">
    <div class="popup-box">
        Congratulations! 🎉 🎉 Your Free ₹180 Bonus Unlocked Here. Check Withdrawal Wallet<br>
        <button onclick="goToWallet()">OK</button>
    </div>
</div>

<script>
// Clock
setInterval(() => {
    document.getElementById("liveClock").innerText = new Date().toLocaleTimeString('en-IN', {hour12: false});
}, 1000);

// Live Entries
const names = ["Rahul Sharma", "Priya Singh", "Amit Kumar", "Neha Patel", "Vikram Yadav", "Anjali Verma", "Rohan Gupta", "Sneha Joshi", "Sachin Mishra", "Pooja Reddy"];
const operators = ["Jio", "Airtel", "Vi"];
function addLiveEntry() {
    const name = names[Math.floor(Math.random() * names.length)];
    const op = operators[Math.floor(Math.random() * operators.length)];
    const masked = "9******" + Math.floor(10 + Math.random() * 90);
    const li = document.createElement("li");
    li.textContent = `${name} - ${masked} / ${op} Successfully Recharge`;
    document.getElementById("liveList").appendChild(li);
}
for(let i = 0; i < 12; i++) addLiveEntry();
setInterval(addLiveEntry, 4500);

// Transaction History
function loadTransactionHistory() {
    const list = document.getElementById("historyList");
    list.innerHTML = "";
    const amounts = [19, 29, 69, 199];
    for(let i = 0; i < 12; i++) {
        const amt = amounts[Math.floor(Math.random() * amounts.length)];
        const time = new Date(Date.now() - i * 3600000).toLocaleString('en-IN', {dateStyle: 'medium', timeStyle: 'short'});
        const item = document.createElement("div");
        item.className = "transaction-item";
        item.innerHTML = `<span class="transaction-amount">₹${amt} Free Data</span> - ${time} - Activated Successfully`;
        list.appendChild(item);
    }
}
function toggleHistory() {
    const list = document.getElementById("historyList");
    list.style.display = (list.style.display === "block") ? "none" : "block";
    if (list.children.length === 0) loadTransactionHistory();
}

// Tab Switch
function openTab(tabId, el) {
    document.querySelectorAll(".tab-content").forEach(t => t.classList.add("hidden"));
    document.getElementById(tabId).classList.remove("hidden");
    document.querySelectorAll(".tab").forEach(t => t.classList.remove("active"));
    el.classList.add("active");
}

// Plan Select with Tick
function selectPlan(el) {
    document.querySelectorAll(".amount-btn").forEach(btn => btn.classList.remove("selected"));
    el.classList.add("selected");
}

// Fake Recharge
function doRecharge() {
    const mobile = document.getElementById("mobileNum").value.trim();
    const operator = document.getElementById("operatorSelect").value;
    const selectedPlan = document.querySelector(".amount-btn.selected");
    
    if (!mobile || mobile.length < 10) {
        alert("Please enter valid mobile number!");
        return;
    }
    if (operator === "Select SIM / Operator") {
        alert("Please select operator!");
        return;
    }
    if (!selectedPlan) {
        alert("Please select a plan!");
        return;
    }
    
    const amount = selectedPlan.innerText;
    alert(`Recharge of ${amount} successful on \( {mobile} ( \){operator})! 🎉 (Demo)`);
    // Optional: add to history or live
}

// Signup Functions
function showSignupPopup() {
    document.getElementById("signupPopup").style.display = "flex";
}
function goToWallet() {
    document.getElementById("signupPopup").style.display = "none";
    document.getElementById("signup").style.display = "none";
    document.getElementById("withdraw").style.display = "block";
}

// Bottom Nav Active
document.querySelectorAll('.nav-item').forEach(item => {
    item.addEventListener('click', e => {
        e.preventDefault();
        document.querySelectorAll('.nav-item').forEach(i => i.classList.remove('active'));
        item.classList.add('active');
    });
});
</script>

</body>
</html>
