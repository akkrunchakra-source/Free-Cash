initial-scale=1.0">
<title>Free-Cash - Earn & Recharge</title>

<style>
*{box-sizing:border-box;}
body{
    margin:0;
    font-family:Arial, sans-serif;
    overflow-x:hidden;
    padding-bottom:70px;       /* bottom nav के लिए space */
}

.screen{ 
    min-height: calc(100vh - 70px); 
}

/* SIGNUP */
#signup{
    background:#000;
    color:#fff;
    padding:20px;
    display:flex;
    flex-direction:column;
    justify-content:center;
    min-height:100vh;
}
#signup input{
    width:100%;
    padding:14px;
    margin:8px 0;
    background:#222;
    border:none;
    border-radius:8px;
    color:#fff;
}
.signup-btn{
    margin-top:15px;
    padding:16px;
    background:red;
    border:none;
    border-radius:30px;
    color:white;
    font-size:16px;
    font-weight:bold;
}

/* WALLET / WITHDRAW */
#withdraw{
    display:none;
    background:#fff;
    min-height: calc(100vh - 70px);
}
.header{
    background:#ffd700;
    padding:12px;
    text-align:center;
}
.balance{font-size:24px;font-weight:bold;}

.tabs{
    display:flex;
    justify-content:space-around;
    border-bottom:1px solid #ddd;
}
.tab{
    padding:10px;
    font-weight:bold;
}
.tab.active{border-bottom:2px solid #ffd700;}
.tab-content{padding:10px;}
.hidden{display:none;}

input,select{
    width:100%;
    padding:10px;
    margin:6px 0;
}

.amount-grid{
    display:grid;
    grid-template-columns:repeat(3,1fr);
    gap:8px;
}
.amount-btn{
    padding:10px;
    border:1px solid #ddd;
    text-align:center;
}
.amount-btn.selected{
    border:2px solid #ffd700;
    background:#fff8cc;
    font-weight:bold;
    position:relative;
}
.amount-btn.selected::after{
    content:"✔";
    position:absolute;
    top:4px;
    right:6px;
    color:green;
}

.withdraw-btn{
    background:#ffd700;
    padding:14px;
    text-align:center;
    font-weight:bold;
    margin-top:10px;
}

/* LIVE DEMO */
.live-box{
    margin:15px 10px;
    border-radius:12px;
    overflow:hidden;
}

.live-header{
    background:linear-gradient(90deg,#ff0080,#ff8c00,#40e0d0);
    color:#fff;
    padding:10px;
    font-weight:bold;
    text-align:center;
}

.live-time{font-size:12px;}

.live-indicator{
    color:#00ff00;
    font-weight:bold;
    animation:liveBlink 1s infinite;
}
@keyframes liveBlink{
    0%{opacity:1;text-shadow:0 0 5px #0f0;}
    50%{opacity:0.3;text-shadow:0 0 15px #0f0;}
    100%{opacity:1;text-shadow:0 0 5px #0f0;}
}

.live-list{
    height:120px;
    background:#000;
    color:#00ff9d;
    overflow:hidden;
    position:relative;
}

.live-list ul{
    list-style:none;
    padding:0;
    margin:0;
    position:absolute;
    width:100%;
    animation:scrollLive 6s linear infinite;
}

.live-list li{
    padding:6px 10px;
    border-bottom:1px solid rgba(255,255,255,0.1);
}

@keyframes scrollLive{
    0%{top:100%;}
    100%{top:-100%;}
}

/* POPUP */
.popup-bg{
    display:none;
    position:fixed;
    inset:0;
    background:rgba(0,0,0,0.7);
    align-items:center;
    justify-content:center;
    z-index:10;
}
.popup-box{
    background:#000;
    color:#fff;
    padding:25px;
    border-radius:12px;
    text-align:center;
    max-width:300px;
}
.popup-box button{
    margin-top:15px;
    padding:10px 20px;
    background:#ffd700;
    border:none;
    border-radius:20px;
    font-weight:bold;
}

/* ===== BOTTOM NAVIGATION ===== */
.bottom-nav {
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;
    height: 70px;
    background: #111;
    display: flex;
    justify-content: space-around;
    align-items: center;
    border-top: 1px solid #333;
    z-index: 1000;
    box-shadow: 0 -3px 10px rgba(0,0,0,0.5);
}

.nav-item {
    flex: 1;
    text-align: center;
    color: white;
    font-weight: bold;
    font-size: 14px;
    padding: 8px 4px;
    text-decoration: none;
    transition: all 0.2s;
}

.nav-item:hover {
    transform: scale(1.08);
}

.nav-item.home    { background: #e74c3c; } /* Red */
.nav-item.earn    { background: #3498db; } /* Blue */
.nav-item.watch   { background: #2ecc71; } /* Green */
.nav-item.data    { background: #9b59b6; } /* Purple */

.nav-item.active {
    transform: scale(1.1);
    box-shadow: 0 4px 12px rgba(255,255,255,0.2);
}
</style>
</head>

<body>

<div id="signup" class="screen">
    <h2>पैसे कमाने के साथ Free Mobile recharge Data Earn करने के लिए अपना Account Sign-up करें पहला Bonus Free For New User</h2>
    <input placeholder="+91 Phone">
    <input type="text" placeholder="Password">
    <input placeholder="Referral Code">
    <input placeholder="Verify Code">
    <button class="signup-btn" onclick="showSignupPopup()">Signup - Click Here</button>

    <!-- Earn options को signup screen पर भी दिखा सकते हो अगर चाहो, लेकिन अभी bottom nav से replace कर दिया -->
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
        <input value="335258xxx05">

        <div class="amount-grid">
            <div class="amount-btn" onclick="selectAmount(this)">₹19</div>
            <div class="amount-btn" onclick="selectAmount(this)">₹29</div>
            <div class="amount-btn" onclick="selectAmount(this)">₹69</div>
            <div class="amount-btn" onclick="selectAmount(this)">₹199</div>
            <div class="amount-btn" onclick="selectAmount(this)">₹299</div>
            <div class="amount-btn" onclick="selectAmount(this)">₹399</div>
        </div>

        <div class="withdraw-btn">Withdraw Now</div>
    </div>

    <div id="recharge" class="tab-content hidden">
        <input placeholder="Mobile Number">
        <select>
            <option>Jio</option>
            <option>Airtel</option>
        </select>
        <div class="withdraw-btn" onclick="showRechargeSuccess()">Recharge Now</div>
    </div>

    <!-- LIVE DEMO -->
    <div class="live-box">
        <div class="live-header">
            Free Mobile Recharge Successfully  
            <div class="live-indicator">● LIVE</div>
            <div class="live-time" id="liveClock"></div>
        </div>

        <div class="live-list">
            <ul id="liveList"></ul>
        </div>
    </div>

</div>

<!-- BOTTOM NAVIGATION BAR -->
<div class="bottom-nav">
    <a href="#" class="nav-item nav-item home active">Home</a>
    <a href="#" class="nav-item nav-item earn">Earn Money</a>
    <a href="#" class="nav-item nav-item watch">Watch And Earn</a>
    <a href="#" class="nav-item nav-item data">Free Data Earn</a>
</div>

<!-- POPUPS -->
<div id="signupPopup" class="popup-bg">
    <div class="popup-box">
        Congratulations! 🎉 🎉 Your Free ₹180 Bonus Unlocked Here. Check Withdrawal Wallet<br>
        <button onclick="goWithdraw()">OK</button>
    </div>
</div>

<div id="rechargePopup" class="popup-bg">
    <div class="popup-box">
      Jio: Recharge successful.<br>
      Voucher: ₹19 Data Add-on<br>
      Benefits: 1GB High Speed Data<br>
      Validity: 1 Day or till active base plan validity<br>
      Check balance on MyJio App.<br>
      Thank you for choosing Jio.<br>
        <button onclick="backHome()">Back</button>
    </div>
</div>

<audio id="successSound" src="https://actions.google.com/sounds/v1/cartoon/clang_and_wobble.ogg"></audio>

<script>
function setVH(){
 document.documentElement.style.setProperty('--vh', window.innerHeight + 'px');
}
setVH(); window.addEventListener('resize', setVH);

/* CLOCK */
setInterval(()=>{
 let now=new Date();
 document.getElementById("liveClock").innerText = now.toLocaleTimeString();
},1000);

/* RANDOM LIVE LIST */
const names = ["Rahul Kumar","Annu Sharma","Parul Kha","Anil Kumar","Rajat Dhan","Gorav Kashyap","Arun Singh","Pooja Sharma","Pooja Singh","Pihu Pal","Ritika Tanu"];
const operators = ["Jio","Airtel"];

function randomNumber(){
 return Math.floor(6000000000 + Math.random()*3000000000)
 .toString().replace(/(\d{4})\d{4}(\d{2})/,"$1****$2");
}

function addLive(){
 let name = names[Math.floor(Math.random()*names.length)];
 let op = operators[Math.floor(Math.random()*operators.length)];
 let li = document.createElement("li");
 li.innerText = `${name} - ${randomNumber()} / ${op} Successfully Recharge`;
 document.getElementById("liveList").appendChild(li);
}

for(let i=0;i<15;i++) addLive();
setInterval(addLive,2000);

/* FUNCTIONS */
function showSignupPopup(){
 document.getElementById("signupPopup").style.display="flex";
}
function goWithdraw(){
 document.getElementById("signupPopup").style.display="none";
 document.getElementById("signup").style.display="none";
 document.getElementById("withdraw").style.display="block";
}
function openTab(id,el){
 document.querySelectorAll(".tab-content").forEach(t=>t.classList.add("hidden"));
 document.getElementById(id).classList.remove("hidden");
 document.querySelectorAll(".tab").forEach(t=>t.classList.remove("active"));
 el.classList.add("active");
}
function selectAmount(el){
 document.querySelectorAll(".amount-btn").forEach(btn=>btn.classList.remove("selected"));
 el.classList.add("selected");
}
function showRechargeSuccess(){
 document.getElementById("rechargePopup").style.display="flex";
 document.getElementById("successSound").play();
}
function backHome(){
 document.getElementById("rechargePopup").style.display="none";
 document.getElementById("withdraw").style.display="none";
 document.getElementById("signup").style.display="flex";
}

/* Optional: Bottom nav click effect (active class change) */
document.querySelectorAll('.nav-item').forEach(item => {
    item.addEventListener('click', function(e) {
        e.preventDefault();
        document.querySelectorAll('.nav-item').forEach(i => i.classList.remove('active'));
        this.classList.add('active');
        // यहाँ बाद में अलग-अलग sections दिखाने का code डाल सकते हो
    });
});
</script>

</body>
</html>
<html lang="hi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Free-Cash - Earn & Recharge</title>

<style>
*{box-sizing:border-box;}
body{
    margin:0;
    font-family:Arial, sans-serif;
    overflow-x:hidden;
    padding-bottom:80px;       /* bottom nav + थोड़ा extra space */
}

.screen{ 
    min-height: calc(100vh - 80px); 
}

/* SIGNUP */
#signup{
    background:#000;
    color:#fff;
    padding:20px;
    display:flex;
    flex-direction:column;
    justify-content:center;
    min-height:100vh;
}
#signup input{
    width:100%;
    padding:14px;
    margin:8px 0;
    background:#222;
    border:none;
    border-radius:8px;
    color:#fff;
}
.signup-btn{
    margin-top:15px;
    padding:16px;
    background:red;
    border:none;
    border-radius:30px;
    color:white;
    font-size:16px;
    font-weight:bold;
}

/* WALLET / WITHDRAW */
#withdraw{
    display:none;
    background:#fff;
    min-height: calc(100vh - 80px);
}
.header{
    background:#ffd700;
    padding:12px;
    text-align:center;
}
.balance{font-size:24px;font-weight:bold;}

.tabs{
    display:flex;
    justify-content:space-around;
    border-bottom:1px solid #ddd;
}
.tab{
    padding:10px;
    font-weight:bold;
}
.tab.active{border-bottom:2px solid #ffd700;}
.tab-content{padding:10px;}
.hidden{display:none;}

input,select{
    width:100%;
    padding:10px;
    margin:6px 0;
}

.amount-grid{
    display:grid;
    grid-template-columns:repeat(3,1fr);
    gap:8px;
}
.amount-btn{
    padding:10px;
    border:1px solid #ddd;
    text-align:center;
}
.amount-btn.selected{
    border:2px solid #ffd700;
    background:#fff8cc;
    font-weight:bold;
    position:relative;
}
.amount-btn.selected::after{
    content:"✔";
    position:absolute;
    top:4px;
    right:6px;
    color:green;
}

.withdraw-btn{
    background:#ffd700;
    padding:14px;
    text-align:center;
    font-weight:bold;
    margin:15px 10px;
    border-radius:8px;
}

/* TRANSACTION HISTORY */
.transaction-section {
    margin:15px 10px;
    background:#f9f9f9;
    border-radius:12px;
    overflow:hidden;
    box-shadow:0 2px 8px rgba(0,0,0,0.1);
}

.transaction-header {
    background:#333;
    color:white;
    padding:12px;
    font-weight:bold;
    text-align:center;
}

.transaction-list {
    max-height:220px;
    overflow-y:auto;
}

.transaction-item {
    padding:12px 15px;
    border-bottom:1px solid #eee;
    display:flex;
    justify-content:space-between;
    align-items:center;
    cursor:pointer;
    transition:background 0.2s;
}

.transaction-item:hover {
    background:#f0f8ff;
}

.transaction-item:last-child {
    border-bottom:none;
}

.transaction-amount {
    font-weight:bold;
    font-size:16px;
}

.transaction-time {
    font-size:12px;
    color:#666;
}

/* LIVE DEMO */
.live-box{
    margin:15px 10px;
    border-radius:12px;
    overflow:hidden;
}

.live-header{
    background:linear-gradient(90deg,#ff0080,#ff8c00,#40e0d0);
    color:#fff;
    padding:10px;
    font-weight:bold;
    text-align:center;
}

.live-time{font-size:12px;}

.live-indicator{
    color:#00ff00;
    font-weight:bold;
    animation:liveBlink 1s infinite;
}
@keyframes liveBlink{
    0%{opacity:1;text-shadow:0 0 5px #0f0;}
    50%{opacity:0.3;text-shadow:0 0 15px #0f0;}
    100%{opacity:1;text-shadow:0 0 5px #0f0;}
}

.live-list{
    height:120px;
    background:#000;
    color:#00ff9d;
    overflow:hidden;
    position:relative;
}

.live-list ul{
    list-style:none;
    padding:0;
    margin:0;
    position:absolute;
    width:100%;
    animation:scrollLive 6s linear infinite;
}

.live-list li{
    padding:6px 10px;
    border-bottom:1px solid rgba(255,255,255,0.1);
}

@keyframes scrollLive{
    0%{top:100%;}
    100%{top:-100%;}
}

/* POPUP */
.popup-bg{
    display:none;
    position:fixed;
    inset:0;
    background:rgba(0,0,0,0.7);
    align-items:center;
    justify-content:center;
    z-index:10;
}
.popup-box{
    background:#000;
    color:#fff;
    padding:25px;
    border-radius:12px;
    text-align:center;
    max-width:320px;
}
.popup-box button{
    margin-top:15px;
    padding:10px 20px;
    background:#ffd700;
    border:none;
    border-radius:20px;
    font-weight:bold;
}

/* BOTTOM NAVIGATION */
.bottom-nav {
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;
    height: 70px;
    background: #111;
    display: flex;
    justify-content: space-around;
    align-items: center;
    border-top: 1px solid #333;
    z-index: 1000;
    box-shadow: 0 -3px 10px rgba(0,0,0,0.5);
}

.nav-item {
    flex: 1;
    text-align: center;
    color: white;
    font-weight: bold;
    font-size: 14px;
    padding: 8px 4px;
    text-decoration: none;
    transition: all 0.2s;
}

.nav-item:hover { transform: scale(1.08); }

.nav-item.home    { background: #e74c3c; }
.nav-item.earn    { background: #3498db; }
.nav-item.watch   { background: #2ecc71; }
.nav-item.data    { background: #9b59b6; }

.nav-item.active {
    transform: scale(1.1);
    box-shadow: 0 4px 12px rgba(255,255,255,0.2);
}
</style>
</head>

<body>

<div id="signup" class="screen">
    <h2>पैसे कमाने के साथ Free Mobile recharge Data Earn करने के लिए अपना Account Sign-up करें पहला Bonus Free For New User</h2>
    <input placeholder="+91 Phone">
    <input type="text" placeholder="Password">
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
        <input value="335258xxx05">

        <div class="amount-grid">
            <div class="amount-btn" onclick="selectAmount(this)">₹19</div>
            <div class="amount-btn" onclick="selectAmount(this)">₹29</div>
            <div class="amount-btn" onclick="selectAmount(this)">₹69</div>
            <div class="amount-btn" onclick="selectAmount(this)">₹199</div>
            <div class="amount-btn" onclick="selectAmount(this)">₹299</div>
            <div class="amount-btn" onclick="selectAmount(this)">₹399</div>
        </div>

        <div class="withdraw-btn" onclick="showRechargeSuccess()">Withdraw Now</div>
    </div>

    <div id="recharge" class="tab-content hidden">
        <input id="mobileNumber" placeholder="Mobile Number">
        <select id="operator">
            <option>Jio</option>
            <option>Airtel</option>
        </select>
        <div class="withdraw-btn" onclick="performRecharge()">Recharge Now</div>
    </div>

    <!-- TRANSACTION HISTORY -->
    <div class="transaction-section">
        <div class="transaction-header">Transaction History (20+ Free Data Activated)</div>
        <div class="transaction-list" id="transactionList"></div>
    </div>

    <!-- LIVE DEMO -->
    <div class="live-box">
        <div class="live-header">
            Free Mobile Recharge Successfully  
            <div class="live-indicator">● LIVE</div>
            <div class="live-time" id="liveClock"></div>
        </div>
        <div class="live-list">
            <ul id="liveList"></ul>
        </div>
    </div>
</div>

<!-- BOTTOM NAVIGATION BAR -->
<div class="bottom-nav">
    <a href="#" class="nav-item nav-item home active">Home</a>
    <a href="#" class="nav-item nav-item earn">Earn Money</a>
    <a href="#" class="nav-item nav-item watch">Watch And Earn</a>
    <a href="#" class="nav-item nav-item data">Free Data Earn</a>
</div>

<!-- POPUPS -->
<div id="signupPopup" class="popup-bg">
    <div class="popup-box">
        Congratulations! 🎉 🎉 Your Free ₹180 Bonus Unlocked Here. Check Withdrawal Wallet<br>
        <button onclick="goWithdraw()">OK</button>
    </div>
</div>

<div id="rechargeDetailPopup" class="popup-bg">
    <div class="popup-box" id="detailContent">
        <!-- डायनामिक कंटेंट यहाँ आएगा -->
        <button onclick="closeDetailPopup()">Close</button>
    </div>
</div>

<audio id="successSound" src="https://actions.google.com/sounds/v1/cartoon/clang_and_wobble.ogg"></audio>

<script>
// ------------------- UTILITIES -------------------
function setVH(){ 
    document.documentElement.style.setProperty('--vh', window.innerHeight + 'px');
}
setVH(); window.addEventListener('resize', setVH);

// CLOCK
setInterval(()=>{
    let now = new Date();
    document.getElementById("liveClock").innerText = now.toLocaleTimeString('en-IN', {hour12:true});
},1000);

// RANDOM LIVE LIST
const names = ["Rahul Kumar","Annu Sharma","Parul Kha","Anil Kumar","Rajat Dhan","Gorav Kashyap","Arun Singh","Pooja Sharma","Pooja Singh","Pihu Pal","Ritika Tanu"];
const operators = ["Jio","Airtel"];

function randomNumber(){
    return Math.floor(6000000000 + Math.random()*3000000000)
        .toString().replace(/(\d{4})\d{4}(\d{2})/,"$1****$2");
}

function addLive(){
    let name = names[Math.floor(Math.random()*names.length)];
    let op = operators[Math.floor(Math.random()*operators.length)];
    let li = document.createElement("li");
    li.innerText = `${name} - ${randomNumber()} / ${op} Successfully Recharge`;
    document.getElementById("liveList").appendChild(li);
}

for(let i=0;i<15;i++) addLive();
setInterval(addLive,2000);

// ------------------- TRANSACTION HISTORY -------------------
let transactions = [];

function generateFakeTransactions(count = 22) {
    const amounts = [19, 29, 69, 199];
    for(let i = 0; i < count; i++) {
        let amount = amounts[Math.floor(Math.random()*amounts.length)];
        let time = new Date(Date.now() - Math.random()*1000000000).toLocaleString('en-IN', {
            day:'2-digit', month:'short', hour:'2-digit', minute:'2-digit'
        });
        transactions.push({amount, time, operator: "Jio"});
    }
    renderTransactions();
}

function renderTransactions() {
    const list = document.getElementById("transactionList");
    list.innerHTML = "";
    transactions.forEach((tx, index) => {
        let div = document.createElement("div");
        div.className = "transaction-item";
        div.innerHTML = `
            <span class="transaction-amount">₹${tx.amount} Jio Data Recharge</span>
            <span class="transaction-time">${tx.time}</span>
        `;
        div.onclick = () => showTransactionDetail(tx);
        list.appendChild(div);
    });
}

function showTransactionDetail(tx) {
    const content = document.getElementById("detailContent");
    content.innerHTML = `
        <h3 style="margin:0 0 15px;">Transaction Details</h3>
        <p><b>Amount:</b> ₹${tx.amount}</p>
        <p><b>Operator:</b> ${tx.operator}</p>
        <p><b>Time:</b> ${tx.time}</p>
        <p style="color:#0f0; font-weight:bold;">Your Free Data successfully completed on ${tx.operator} 🎉</p>
        <p>Status: Success</p>
        <button onclick="closeDetailPopup()">Close</button>
    `;
    document.getElementById("rechargeDetailPopup").style.display = "flex";
}

function closeDetailPopup() {
    document.getElementById("rechargeDetailPopup").style.display = "none";
}

// ------------------- RECHARGE FUNCTION -------------------
function performRecharge() {
    const amountBtn = document.querySelector(".amount-btn.selected");
    if(!amountBtn) {
        alert("Please select amount first!");
        return;
    }
    const amount = parseInt(amountBtn.innerText.replace('₹',''));
    
    // Add to history
    let time = new Date().toLocaleString('en-IN', {
        day:'2-digit', month:'short', hour:'2-digit', minute:'2-digit'
    });
    transactions.unshift({amount, time, operator: "Jio"}); // newest first
    renderTransactions();

    // Show success popup
    document.getElementById("rechargeDetailPopup").style.display = "flex";
    document.getElementById("detailContent").innerHTML = `
        <h3>Recharge Successful! 🎉</h3>
        <p><b>₹${amount} Data Recharge</b> on Jio</p>
        <p>Your Free Data successfully completed</p>
        <p>Check MyJio App for confirmation.</p>
        <button onclick="closeDetailPopup()">OK</button>
    `;
    
    document.getElementById("successSound").play();
}

// ------------------- OTHER FUNCTIONS -------------------
function showSignupPopup(){
    document.getElementById("signupPopup").style.display="flex";
}
function goWithdraw(){
    document.getElementById("signupPopup").style.display="none";
    document.getElementById("signup").style.display="none";
    document.getElementById("withdraw").style.display="block";
}
function openTab(id,el){
    document.querySelectorAll(".tab-content").forEach(t=>t.classList.add("hidden"));
    document.getElementById(id).classList.remove("hidden");
    document.querySelectorAll(".tab").forEach(t=>t.classList.remove("active"));
    el.classList.add("active");
}
function selectAmount(el){
    document.querySelectorAll(".amount-btn").forEach(btn=>btn.classList.remove("selected"));
    el.classList.add("selected");
}
function backHome(){
    closeDetailPopup();
    document.getElementById("withdraw").style.display="none";
    document.getElementById("signup").style.display="flex";
}

// Bottom nav active
document.querySelectorAll('.nav-item').forEach(item => {
    item.addEventListener('click', function(e) {
        e.preventDefault();
        document.querySelectorAll('.nav-item').forEach(i => i.classList.remove('active'));
        this.classList.add('active');
    });
});

// Init fake history
generateFakeTransactions(22);
</script>

</body>
</html>
