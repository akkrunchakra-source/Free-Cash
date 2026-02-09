<html lang="hi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Free-Cash - Earn & Recharge</title>

<style>
*{box-sizing:border-box;}
body{margin:0; font-family:Arial, sans-serif; overflow-x:hidden; padding-bottom:80px;}

.screen{min-height:calc(100vh - 80px);}

/* Header & Balance */
.header{background:#ffd700; padding:12px; text-align:center;}
.balance{font-size:24px; font-weight:bold;}

/* Tabs */
.tabs{display:flex; justify-content:space-around; border-bottom:1px solid #ddd;}
.tab{padding:10px; font-weight:bold;}
.tab.active{border-bottom:2px solid #ffd700;}
.tab-content{padding:10px;}
.hidden{display:none;}

input, select{width:100%; padding:10px; margin:6px 0;}
.amount-grid{display:grid; grid-template-columns:repeat(3,1fr); gap:8px;}
.amount-btn{padding:12px; border:1px solid #ddd; text-align:center; cursor:pointer;}
.amount-btn.selected{border:2px solid #ffd700; background:#fff8cc; font-weight:bold; position:relative;}
.amount-btn.selected::after{content:"✔"; position:absolute; top:4px; right:6px; color:green;}

.withdraw-btn{background:#ffd700; padding:14px; text-align:center; font-weight:bold; margin:15px 10px; border-radius:8px; cursor:pointer;}

/* Transaction History */
.transaction-section{margin:15px 10px; background:#f9f9f9; border-radius:12px; overflow:hidden; box-shadow:0 2px 8px rgba(0,0,0,0.1);}
.transaction-header{background:#333; color:white; padding:12px; font-weight:bold; text-align:center; cursor:pointer;}
.transaction-list{max-height:300px; overflow-y:auto; display:none;} /* शुरू में hidden */
.transaction-item{padding:12px 15px; border-bottom:1px solid #eee; font-size:14px;}
.transaction-item:last-child{border-bottom:none;}
.transaction-amount{font-weight:bold; color:#e74c3c;}

/* Live Recharge */
.live-box{margin:15px 10px; border-radius:12px; overflow:hidden;}
.live-header{background:linear-gradient(90deg,#ff0080,#ff8c00,#40e0d0); color:#fff; padding:10px; font-weight:bold; text-align:center;}
.live-indicator{color:#00ff00; font-weight:bold; animation:liveBlink 1s infinite;}
@keyframes liveBlink{0%,100%{opacity:1;} 50%{opacity:0.4;}}
.live-time{font-size:12px; margin-top:4px;}
.live-list{height:140px; background:#000; color:#00ff9d; overflow:hidden; position:relative;}
.live-list ul{list-style:none; padding:0; margin:0; position:absolute; width:100%; animation:scrollLive 15s linear infinite;} /* faster: 15s */
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

<div class="header">
    <div>Wallet Balance</div>
    <div class="balance">₹180.00</div>
</div>

<div class="tabs">
    <div class="tab active">Paytm</div>
    <div class="tab">Recharge</div>
</div>

<div class="tab-content">
    <input value="3352585xxx05" readonly style="text-align:center; font-weight:bold;">
    
    <div class="amount-grid">
        <div class="amount-btn">₹19</div>
        <div class="amount-btn">₹29</div>
        <div class="amount-btn">₹69</div>
        <div class="amount-btn">₹199</div>
        <div class="amount-btn">₹299</div>
        <div class="amount-btn">₹399</div>
    </div>
    
    <div class="withdraw-btn">Withdraw Now</div>
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
        <div class="live-time" id="liveClock">09:01:20</div>
    </div>
    <div class="live-list">
        <ul id="liveList"></ul>
    </div>
</div>

<!-- Bottom Nav -->
<div class="bottom-nav">
    <a href="#" class="nav-item nav-item home active">Home</a>
    <a href="#" class="nav-item nav-item earn">Earn Money</a>
    <a href="#" class="nav-item nav-item watch">Watch And Earn</a>
    <a href="#" class="nav-item nav-item data">Free Data Earn</a>
</div>

<!-- Simple Popup Example (optional) -->
<div id="simplePopup" class="popup-bg">
    <div class="popup-box">
        <p id="popupText">Success!</p>
        <button onclick="document.getElementById('simplePopup').style.display='none'">OK</button>
    </div>
</div>

<script>
// Clock
setInterval(() => {
    let now = new Date();
    document.getElementById("liveClock").innerText = now.toLocaleTimeString('en-IN', {hour12: false});
}, 1000);

// Realistic Indian Names
const names = [
    "Rahul Sharma", "Priya Singh", "Amit Kumar", "Neha Patel", "Vikram Yadav", "Anjali Verma",
    "Rohan Gupta", "Sneha Joshi", "Sachin Mishra", "Pooja Reddy", "Arjun Mehta", "Kavita Nair",
    "Deepak Tiwari", "Shreya Kapoor", "Manish Pandey", "Riya Banerjee", "Ajay Thakur", "Sonali Desai"
];
const operators = ["Jio", "Airtel", "Vi"];

// Add to Live List (fixed - no code visible)
function addLiveEntry() {
    const name = names[Math.floor(Math.random() * names.length)];
    const op = operators[Math.floor(Math.random() * operators.length)];
    const masked = "9******" + Math.floor(10 + Math.random() * 90);
    const li = document.createElement("li");
    li.textContent = `${name} - ${masked} / ${op} Successfully Recharge`;
    document.getElementById("liveList").appendChild(li);
}

// Initial + continuous
for(let i = 0; i < 12; i++) addLiveEntry();
setInterval(addLiveEntry, 4500); // हर 4.5 सेकंड में नया → fast feel

// Transaction History (10+ fake entries)
function loadTransactionHistory() {
    const list = document.getElementById("historyList");
    list.innerHTML = ""; // clear if reload
    const amounts = [19, 29, 69, 199];
    for(let i = 0; i < 12; i++) { // 12 entries
        const amt = amounts[Math.floor(Math.random() * amounts.length)];
        const time = new Date(Date.now() - i * 3600000 * (Math.random() + 1)).toLocaleString('en-IN', {dateStyle: 'medium', timeStyle: 'short'});
        const item = document.createElement("div");
        item.className = "transaction-item";
        item.innerHTML = `<span class="transaction-amount">₹${amt} Free Data</span> - ${time} - Activated Successfully`;
        list.appendChild(item);
    }
}

function toggleHistory() {
    const list = document.getElementById("historyList");
    if (list.style.display === "block") {
        list.style.display = "none";
    } else {
        if (list.children.length === 0) loadTransactionHistory();
        list.style.display = "block";
    }
}

// Bottom nav active toggle (optional)
document.querySelectorAll('.nav-item').forEach(item => {
    item.addEventListener('click', (e) => {
        e.preventDefault();
        document.querySelectorAll('.nav-item').forEach(i => i.classList.remove('active'));
        item.classList.add('active');
    });
});
</script>

</body>
</html>
