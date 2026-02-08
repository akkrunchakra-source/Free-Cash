<html lang="hi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Wallet Platform</title>

<style>
*{box-sizing:border-box;}
body{
    margin:0;
    font-family:Arial, sans-serif;
    overflow:hidden;
}

.screen{ height:var(--vh); }

/* SIGNUP */
#signup{
    background:#000;
    color:#fff;
    padding:20px;
    display:flex;
    flex-direction:column;
    justify-content:center;
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

/* WALLET */
#withdraw{
    display:none;
    background:#fff;
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
    margin-top:15px;
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

.live-time{
    font-size:12px;
}

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
</style>
</head>

<body>

<div id="signup" class="screen">
    <h2>पैसे कमाने के साथ Free Mobile reacharge Data Earn करने के लिए अपना Account Sign-up‌ करें पहला Bonus Free For New User</h2>
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

<!-- POPUPS -->
<div id="signupPopup" class="popup-bg">
    <div class="popup-box">
        Congratulations! 🎉 🎉 Your Free ₹180 Bonus Unlocked Here. Check Withdrawal Wallet<br>
        <button onclick="goWithdraw()">OK</button>
    </div>
</div>

<div id="rechargePopup" class="popup-bg">
    <div class="popup-box">
      Jio: Recharge successful.

Voucher: ₹19 Data Add-on
Benefits: 1GB High Speed Data
Validity: 1 Day or till active base plan validity (whichever applicable)

Check balance on MyJio App.
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
 document.getElementById("liveClock").innerText=
 now.toLocaleTimeString();
},1000);

/* RANDOM LIVE LIST */
const names=[
"Rahul Kumar","Annu Sharma","Parul Kha","Anil Kumar",
"Rajat Dhan","Gorav Kashyap","Arun Singh",
"Pooja Sharma","Pooja Singh","Pihu Pal","Ritika Tanu"
];

const operators=["Jio","Airtel"];

function randomNumber(){
 return Math.floor(6000000000 + Math.random()*3000000000)
 .toString().replace(/(\d{4})\d{4}(\d{2})/,"$1****$2");
}

function addLive(){
 let name=names[Math.floor(Math.random()*names.length)];
 let op=operators[Math.floor(Math.random()*operators.length)];
 let li=document.createElement("li");
 li.innerText=`${name} - ${randomNumber()} / ${op} Successfully Recharge`;
 document.getElementById("liveList").appendChild(li);
}

for(let i=0;i<15;i++) addLive();
setInterval(addLive,2000);

/* FUNCTIONS */
function showSignupPopup(){
 signupPopup.style.display="flex";
}
function goWithdraw(){
 signupPopup.style.display="none";
 signup.style.display="none";
 withdraw.style.display="block";
}
function openTab(id,el){
 document.querySelectorAll(".tab-content")
 .forEach(t=>t.classList.add("hidden"));
 document.getElementById(id).classList.remove("hidden");
 document.querySelectorAll(".tab")
 .forEach(t=>t.classList.remove("active"));
 el.classList.add("active");
}
function selectAmount(el){
 document.querySelectorAll(".amount-btn")
 .forEach(btn=>btn.classList.remove("selected"));
 el.classList.add("selected");
}
function showRechargeSuccess(){
 rechargePopup.style.display="flex";
 successSound.play();
}
function backHome(){
 rechargePopup.style.display="none";
 withdraw.style.display="none";
 signup.style.display="flex";
}
</script>

</body>
</html>
