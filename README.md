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
    background:#2b2b2b;
    border:none;
    border-radius:30px;
    color:#fff;
    font-size:16px;
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

/* AMOUNT */
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

/* BUTTON */
.withdraw-btn{
    background:#ffd700;
    padding:14px;
    text-align:center;
    font-weight:bold;
    margin-top:10px;
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
    animation:blink 1s infinite;
}
@keyframes blink{
0%{opacity:1;}
50%{opacity:0.5;}
100%{opacity:1;}
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

<!-- SIGNUP -->
<div id="signup" class="screen">
    <h2>पैसे कमाने के लिए और अधिक Free Mobile DATA Earn के लिए अपना Account Sign-Up करें!</h2>
    <input placeholder="+91 Phone">
    <input type="password" placeholder="Password">
    <input placeholder="Referral Code">
    <input placeholder="Verify Code">
    <button class="signup-btn" onclick="showSignupPopup()">Sign-up Here</button>
</div>

<!-- WALLET -->
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
            <div class="amount-btn" onclick="selectAmount(this)">₹10</div>
            <div class="amount-btn" onclick="selectAmount(this)">₹20</div>
            <div class="amount-btn" onclick="selectAmount(this)">₹50</div>
            <div class="amount-btn" onclick="selectAmount(this)">₹100</div>
            <div class="amount-btn" onclick="selectAmount(this)">₹500</div>
            <div class="amount-btn" onclick="selectAmount(this)">₹2000</div>
        </div>

        <div class="withdraw-btn">Withdraw Demo</div>
    </div>

    <div id="recharge" class="tab-content hidden">
        <input placeholder="Mobile Number">
        <select>
            <option>Jio</option>
            <option>Airtel</option>
        </select>
        <div class="withdraw-btn" onclick="showRechargeSuccess()">Recharge Now</div>
    </div>

</div>

<!-- SIGNUP BONUS POPUP -->
<div id="signupPopup" class="popup-bg">
    <div class="popup-box">
        <b>Signup Bonus ₹180 Unlocked</b><br><br>
        You can now use wallet features.<br>
        <button onclick="goWithdraw()">OK</button>
    </div>
</div>

<!-- RECHARGE SUCCESS -->
<div id="rechargePopup" class="popup-bg">
    <div class="popup-box">
        <b>Recharge Successfully Completed</b><br><br>
        Please wait few minutes.<br>
        <button onclick="backHome()">Back To Home</button>
    </div>
</div>

<script>

function setVH(){
 document.documentElement.style.setProperty('--vh', window.innerHeight + 'px');
}
setVH(); window.addEventListener('resize', setVH);

/* SIGNUP POPUP */
function showSignupPopup(){
 document.getElementById("signupPopup").style.display="flex";
}

function goWithdraw(){
 document.getElementById("signupPopup").style.display="none";
 signup.style.display="none";
 withdraw.style.display="block";
}

/* TAB */
function openTab(id,el){
 document.querySelectorAll(".tab-content")
 .forEach(t=>t.classList.add("hidden"));

 document.getElementById(id).classList.remove("hidden");

 document.querySelectorAll(".tab")
 .forEach(t=>t.classList.remove("active"));

 el.classList.add("active");
}

/* AMOUNT */
function selectAmount(el){
 document.querySelectorAll(".amount-btn")
 .forEach(btn=>btn.classList.remove("selected"));

 el.classList.add("selected");
}

/* RECHARGE */
function showRechargeSuccess(){
 document.getElementById("rechargePopup").style.display="flex";
}

function backHome(){
 document.getElementById("rechargePopup").style.display="none";
 withdraw.style.display="none";
 signup.style.display="flex";
}

</script>

</body>
</html>
