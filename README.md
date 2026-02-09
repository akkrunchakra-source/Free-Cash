<!DOCTYPE html>
<html lang="hi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Free-Cash - Earn & Recharge</title>
<style>
*{box-sizing:border-box; margin:0; padding:0;}
body{font-family:Arial, sans-serif; overflow-x:hidden; padding-bottom:80px;}
.screen{min-height:calc(100vh - 80px);}

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
.tab{padding:10px; font-weight:bold;}
.tab.active{border-bottom:2px solid #ffd700;}
.tab-content{padding:10px;}
.hidden{display:none;}

input, select{width:100%; padding:10px; margin:6px 0;}
.amount-grid{display:grid; grid-template-columns:repeat(3,1fr); gap:8px;}
.amount-btn{padding:10px; border:1px solid #ddd; text-align:center; cursor:pointer;}
.amount-btn.selected{border:2px solid #ffd700; background:#fff8cc; font-weight:bold; position:relative;}
.amount-btn.selected::after{content:"✔"; position:absolute; top:4px; right:6px; color:green;}

.withdraw-btn{background:#ffd700; padding:14px; text-align:center; font-weight:bold; margin:15px 10px; border-radius:8px; cursor:pointer;}

/* Transaction History */
.transaction-section{margin:15px 10px; background:#f9f9f9; border-radius:12px; overflow:hidden; box-shadow:0 2px 8px rgba(0,0,0,0.1);}
.transaction-header{background:#333; color:white; padding:12px; font-weight:bold; text-align:center;}
.transaction-list{max-height:220px; overflow-y:auto;}
.transaction-item{padding:12px 15px; border-bottom:1px solid #eee; display:flex; justify-content:space-between; cursor:pointer;}
.transaction-item:hover{background:#f0f8ff;}
.transaction-amount{font-weight:bold;}

/* Live Box */
.live-box{margin:15px 10px; border-radius:12px; overflow:hidden;}
.live-header{background:linear-gradient(90deg,#ff0080,#ff8c00,#40e0d0); color:#fff; padding:10px; font-weight:bold; text-align:center;}
.live-indicator{color:#00ff00; font-weight:bold; animation:liveBlink 1s infinite;}
@keyframes liveBlink{0%{opacity:1;} 50%{opacity:0.3;} 100%{opacity:1;}}
.live-list{height:120px; background:#000; color:#00ff9d; overflow:hidden; position:relative;}
.live-list ul{list-style:none; padding:0; margin:0; position:absolute; width:100%; animation:scrollLive 20s linear infinite;}
.live-list li{padding:6px 10px; border-bottom:1px solid rgba(255,255,255,0.1);}
@keyframes scrollLive{0%{top:0;} 100%{top:-100%;}}

/* Popup */
.popup-bg{display:none; position:fixed; inset:0; background:rgba(0,0,0,0.7); align-items:center; justify-content:center; z-index:10;}
.popup-box{background:#000; color:#fff; padding:25px; border-radius:12px; text-align:center; max-width:320px;}
.popup-box button{margin-top:15px; padding:10px 20px; background:#ffd700; border:none; border-radius:20px; font-weight:bold;}

/* Bottom Nav */
.bottom-nav{position:fixed; bottom:0; left:0; right:0; height:70px; background:#111; display:flex; justify-content:space-around; align-items:center; border-top:1px solid #333; z-index:1000;}
.nav-item{flex:1; text-align:center; color:white; font-weight:bold; font-size:14px; padding:8px 4px; text-decoration:none;}
.nav-item:hover{transform:scale(1.05);}
.nav-item.home{background:#e74c3c;}
.nav-item.earn{background:#3498db;}
.nav-item.watch{background:#2ecc71;}
.nav-item.data{background:#9b59b6;}
.nav-item.active{transform:scale(1.1);}
</style>
</head>
<body>

<div id="signup" class="screen">
    <h2>पैसे कमाने के साथ Free Mobile recharge Data Earn करने के लिए अपना Account Sign-up करें पहला Bonus Free For New User</h2>
    <input placeholder="+91 Phone">
    <input type="password" placeholder="Password">
    <input placeholder="Referral Code">
    <input placeholder="Verify Code">
    <button class="signup-btn" onclick="showSignupPopup()">Signup - Click Here</button>
</div>

<div id="withdraw" class="screen">
    <div class="header">
        <div>Wallet Balance</div>
        <div class="balance">₹180.00</div>
    </div>

    <div class="tabs">
        <div class="tab active" onclick="openTab('paytm',this)">Paytm</div>
        <div class="tab" onclick="openTab('recharge',this)">Recharge</div>
    </div>

    <div id="paytm" class="tab-content">
        <input value="335258xxx05" readonly>
        <div class="amount-grid">
            <div class="amount-btn" onclick="selectAmount(this)">₹19</div>
            <div class="amount-btn" onclick="selectAmount(this)">₹29</div>
            <div class="amount-btn" onclick="selectAmount(this)">₹69</div>
            <div class="amount-btn" onclick="selectAmount(this)">₹199</div>
            <div class="amount-btn" onclick="selectAmount(this)">₹299</div>
            <div class="amount-btn" onclick="selectAmount(this)">₹399</div>
        </div>
        <div class="withdraw-btn" onclick="alert('Withdraw processing... (Demo)')">Withdraw Now</div>
    </div>

    <div id="recharge" class="tab-content hidden">
        <input placeholder="Mobile Number">
        <select><option>Jio</option><option>Airtel</option></select>
        <div class="withdraw-btn" onclick="performRecharge()">Recharge Now</div>
    </div>

    <!-- Transaction History -->
    <div class="transaction-section">
        <div class="transaction-header">Transaction History</div>
        <div class="transaction-list" id="transactionList"></div>
    </div>

    <!-- Live -->
    <div class="live-box">
        <div class="live-header">
            Free Mobile Recharge Successfully ● LIVE
            <div id="liveClock"></div>
        </div>
        <div class="live-list"><ul id="liveList"></ul></div>
    </div>
</div>

<div class="bottom-nav">
    <a href="#" class="nav-item nav-item home active">Home</a>
    <a href="#" class="nav-item nav-item earn">Earn Money</a>
    <a href="#" class="nav-item nav-item watch">Watch And Earn</a>
    <a href="#" class="nav-item nav-item data">Free Data Earn</a>
</div>

<!-- Popups -->
<div id="signupPopup" class="popup-bg">
    <div class="popup-box">
        Congratulations! 🎉 Your Free ₹180 Bonus Unlocked Here. Check Withdrawal Wallet<br>
        <button onclick="goWithdraw()">OK</button>
    </div>
</div>

<div id="rechargePopup" class="popup-bg">
    <div class="popup-box">
        Recharge successful! 🎉<br>
        <button onclick="document.getElementById('rechargePopup').style.display='none'">OK</button>
    </div>
</div>

<script>
// Clock
setInterval(() => {
    document.getElementById("liveClock").innerText = new Date().toLocaleTimeString();
}, 1000);

// Live list
const names = ["Rahul","Pooja","Anil","Priya"];
function addLive() {
    let li = document.createElement("li");
    li.textContent = `\( {names[Math.floor(Math.random()*names.length)]} - 9***** \){Math.floor(Math.random()*100)} / Jio Successfully Recharge`;
    document.getElementById("liveList").appendChild(li);
}
for(let i=0; i<10; i++) addLive();
setInterval(addLive, 3000);

// Functions
function showSignupPopup() {
    document.getElementById("signupPopup").style.display = "flex";
}

function goWithdraw() {
    document.getElementById("signupPopup").style.display = "none";
    document.getElementById("signup").style.display = "none";
    document.getElementById("withdraw").style.display = "block";
    // Force reflow to ensure switch
    document.body.offsetHeight;
}

function openTab(id, el) {
    document.querySelectorAll(".tab-content").forEach(t => t.classList.add("hidden"));
    document.getElementById(id).classList.remove("hidden");
    document.querySelectorAll(".tab").forEach(t => t.classList.remove("active"));
    el.classList.add("active");
}

function selectAmount(el) {
    document.querySelectorAll(".amount-btn").forEach(b => b.classList.remove("selected"));
    el.classList.add("selected");
}

function performRecharge() {
    document.getElementById("rechargePopup").style.display = "flex";
    // Add to history if you want
}

// Bottom nav active only (no page switch yet)
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
