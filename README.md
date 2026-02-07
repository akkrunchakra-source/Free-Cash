<html lang="hi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>6Gain Earning Platform</title>

<style>
*{box-sizing:border-box;}
body{
    margin:0;
    font-family:Arial, sans-serif;
    overflow:hidden;
}

/* ===== DYNAMIC FULL HEIGHT ===== */
.screen{
    height:var(--vh);
}

/* ===== SIGN-UP ===== */
#signup{
    background:#000;
    color:#fff;
    padding:20px;
    display:flex;
    flex-direction:column;
    justify-content:center;
}
#signup h2{margin-bottom:15px;}
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
    background:#2b2b2b;
    border:none;
    border-radius:30px;
    color:#fff;
    font-size:16px;
}
.agree{
    margin-top:10px;
    font-size:12px;
    color:#aaa;
}
.agree span{color:red;}

/* ===== WITHDRAW ===== */
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
.notification{
    padding:6px;
    text-align:center;
    color:#ff8c00;
}

/* LIVE LIST */
.live{
    background:#f7f7f7;
    padding:6px;
    font-size:12px;
    height:60px;
    overflow:hidden;
}
.live div{
    animation:scroll 6s linear infinite;
}
@keyframes scroll{
    0%{transform:translateY(100%);}
    100%{transform:translateY(-100%);}
}

/* TABS */
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
.withdraw-btn{
    background:#ffd700;
    padding:14px;
    text-align:center;
    font-weight:bold;
    margin-top:10px;
}

/* ===== POPUP ===== */
#popup{
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
    padding:25px;
    border-radius:12px;
    text-align:center;
    animation:blink 1s infinite;
}
.popup-box b{
    color:red;
    font-size:18px;
}
.popup-box span{
    color:#00ff00;
    font-weight:bold;
}
@keyframes blink{
    0%{opacity:1;}
    50%{opacity:0.4;}
    100%{opacity:1;}
}
.ok-btn{
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

<!-- SIGNUP -->
<div id="signup" class="screen">
    <h2>पैसे And Free Reacharge Data कमाने के लिए<br>अपना Free account बनाओ!</h2>
    <input placeholder="+91 Phone">
    <input type="password" placeholder="Password डालो">
    <input placeholder="Invitation Code">
    <input placeholder="Verify Code">
    <button class="signup-btn" onclick="showCongrats()">Account Signup Click Here</button>
    <div class="agree">● मैं agree करता हूँ <span>Terms</span> & <span>Privacy</span></div>
</div>

<!-- WITHDRAW -->
<div id="withdraw" class="screen">
    <div class="header">
        <div>Withdraw</div>
        <div class="balance">₹180.00</div>
        <div>Earning cash</div>
    </div>

    <div class="notification">🔔 रोज ₹10 से ₹1000 निकाल सकते हैं Free</div>

    <div class="live"><div id="liveList"></div></div>

    <div class="tabs">
        <div class="tab active" onclick="openTab('paytm',this)">Paytm</div>
        <div class="tab" onclick="openTab('bank',this)">BANK</div>
        <div class="tab" onclick="openTab('recharge',this)">MOBILE Recharge</div>
    </div>

    <div id="paytm" class="tab-content">
        <input value="335258xxx05">
        <div class="amount-grid">
            <div class="amount-btn">₹10</div><div class="amount-btn">₹20</div><div class="amount-btn">₹50</div>
            <div class="amount-btn">₹100</div><div class="amount-btn">₹500</div><div class="amount-btn">₹2000</div>
        </div>
        <div class="withdraw-btn">पैसा निकालें</div>
    </div>

    <div id="bank" class="tab-content hidden">
        <input placeholder="Bank Account">
        <div class="withdraw-btn">पैसा निकालें</div>
    </div>

    <div id="recharge" class="tab-content hidden">
        <input placeholder="Mobile Number">
        <select><option>Jio</option><option>Airtel</option></select>
        <div class="withdraw-btn">Recharge Now</div>
    </div>
</div>

<!-- POPUP -->
<div id="popup">
    <div class="popup-box">
        <b>Congratulations ₹180 Free ADD</b><br>
        <span>Your Withdrawal Wallet Free Cash Click Here to OK</span><br>
        <button class="ok-btn" onclick="goWithdraw()">OK</button>
    </div>
</div>

<script>
// FIX HEIGHT
function setVH(){
    document.documentElement.style.setProperty('--vh', window.innerHeight + 'px');
}
setVH(); window.addEventListener('resize', setVH);

// LIVE LIST
const names=["Rahul","Aman","Neha","Pooja","Ravi","Suman","Ankit","Priya","Vikas","Kajal",
"Rohit","Simran","Deepak","Nisha","Mohit","Anjali","Sunil","Payal","Aarti","Kunal"];

setInterval(()=>{
    let n=names[Math.floor(Math.random()*names.length)];
    let a=[100,200,300,500,700][Math.floor(Math.random()*5)];
    liveList.innerHTML=`${n} ₹${a} withdrawn`;
},2000);

// FLOW
function showCongrats(){ popup.style.display="flex"; }
function goWithdraw(){
    popup.style.display="none";
    signup.style.display="none";
    withdraw.style.display="block";
}
function openTab(id,el){
    document.querySelectorAll(".tab-content").forEach(t=>t.classList.add("hidden"));
    document.getElementById(id).classList.remove("hidden");
    document.querySelectorAll(".tab").forEach(t=>t.classList.remove("active"));
    el.classList.add("active");
}
</script>

</body>
</html>
